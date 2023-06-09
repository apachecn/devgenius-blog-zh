# 畅销的科技博客 4；如何使用 Lerna 在 monorepo 中同步版本化所有包

> 原文：<https://blog.devgenius.io/salable-tech-blog-4-how-to-version-all-packages-synchronously-in-a-monorepo-using-lerna-42dad6e65140?source=collection_archive---------3----------------------->

作者康纳墨菲，开发团队畅销

![](img/eb4a27b2945445a52d99cfc27bedbce5.png)

使用 Lerna 在 monorepo 中同步版本包

在本帖中，我们将探讨如何使用 Lerna 在 monorepo 中设置包的自动版本控制。有很多方法可以用不同的技术和想法做到这一点，但主要归结为一个决定；您是希望将整个存储库作为一个整体进行版本控制，还是希望 monorepo 中的各个包相互独立地进行版本控制？

> 我们希望前者能够保持彼此同步，不管包内是否有变化。这主要是因为组织性；例如，如果一个 1.2 版不工作，我们会知道这适用于代码库的所有部分(而不是必须找出每个包中 1.2 版与什么版本相关)。)

有人担心这会变得混乱，导致产生大量不需要的版本和标签。但由于我们没有公布 monorepo 的任何部分，这在很大程度上是一个无效的问题。这是因为我们团队之外的任何人都不会看到生成的标签，并且由于 Lerna 会自动更新依赖关系，我们不需要担心手动更新版本来保持软件包同步。

## 不成功的方法

当涉及到 monorepo 的版本控制时，我们的第一个想法是利用我们用于开源包的同一个包，这就是语义发布。这是一个很棒的包，可以为你处理所有的发布和标记工作。但不幸的是，正如[在他们的知识库上的这个长期运行的开放 GitHub 问题](https://github.com/semantic-release/semantic-release/issues/193)中所记录的，他们不支持 monorepos。

现在，多年来已经有一些尝试将语义发布与其他技术如 Lerna 结合起来，甚至将 monorepo 支持添加到包中，如[这个](https://www.npmjs.com/package/semantic-release-monorepo)和[这个](https://github.com/atlassian/lerna-semantic-release)。但是，唉，这些尝试似乎没有经受住时间的考验，不再得到支持，或者没有跟上主包本身的步伐。

这排除了在我们的 monorepo 中使用语义释放。但是环顾结合语义发布和 Lerna 的尝试，确实让我思考；我们可以只使用 Lerna 吗？

## 我们的版本控制解决方案

我们已经利用了 Lerna！

最后，经过一番研究，发现 Lerna 为我们提供了完美的工具。它可以在 CI 环境中运行，使用常规提交自动检测版本，基于提交生成变更日志，使版本彼此同步，等等。我们必须在 Lerna 之外做的唯一一件事就是通过一个脚本修改根[package.json]的版本号(我们将在本文后面讨论)。

Lerna 可以通过包含["]来提升根版本。]在配置文件的[packages]选项中，但是这样做在我们的 CI 环境中引起了许多问题，内存分配被超过，所以我们把它分离到它自己的脚本中以提高可靠性。

从 Lerna 开始，你需要[将它安装到你的项目](https://www.npmjs.com/package/lerna)中，然后在你的 monorepo 的根目录下创建一个【lerna.json】文件，我们的看起来像下面的 json，但是请根据你的需要定制它。

```
{
  "version": "1.0.3",
  "packages": ["packages/*", "repositories/*"],
  "npmClient": "yarn",
  "command": {
    "version": {
      "message": "chore(release): publish %s [skip ci]",
      "conventionalCommits": true,
      "changelogPreset": "conventionalcommits",
      "allowBranch": ["main"]
    }
  }
}
```

创建了这个根配置文件后，我们需要将 Lerna 命令添加到 CI 配置文件中。我们在可扩展的 monorepo 上使用 Bitbucket 管道，因此如果您没有使用它，您可能需要定制下面的代码，以便在您自己的 CI 环境中工作。

正如上面的配置文件提到的，我们在[main]分支上运行 Lerna 命令。更具体地说，在并入[主]分支时。我们[主]分支的管道运行安装命令、jest 和 cypress 测试、构建应用程序、用数据播种数据库，然后如果所有这些都成功的话，最后对 monorepo 进行版本化。

为了简洁起见，我省略了所有其他步骤，但是它看起来像这样；

```
pipelines:
 branches:
   main:
     # ...Other steps mentioned above

      - step:
       name: Versioning
        caches:
         - node
        script:
         - npx lerna version --conventional-commits --yes --force-publish='*' --no-push --no-git-tag-versionAs you can see we run our [npx lerna version] command with a few flags, so let’s quickly run over what each of those means.
```

[--conventi on-commits]这告诉 Lerna 在计算下一个要碰撞的版本时，根据自上一个版本以来的提交消息，使用传统的提交规范。

[- -yes]该标志向通常显示的任何用户提示传递“yes”。

[- -force-publish="*"]这个标志意味着发布配置文件中定义的所有包，不管自上一版本以来该包是否有变化。这个标志是我们如何在版本之间保持所有包同步的。

[- -no-push]这个标志告诉 Lerna 不要推送到远程目的地，这是默认行为。这样做的原因是我们仍然需要更新根[package.json]文件，正如前面提到的，我们将在一个独立的脚本中完成这项工作，我们还将处理推送到远程的操作。

[- -no-git-tag-version]这个标志防止 Lerna 用新版本标记它创建的提交。通常你会想要这种行为，但因为我们仍然需要修改根版本，我们想推迟标记，直到完成。我们将在根版本脚本中创建我们自己的 git 标签。

## 根[package.json]脚本

为了更新根[package.json]文件，我们在 CI 环境中运行一个脚本，执行[npx lerna version … ]命令，该脚本将从[lerna.json]文件中获取新版本，然后用它更新根[package.json]版本。然后，它提交所有的更改，为该版本创建一个新的 git 标记，最后将该提交和新创建的 git 标记推送到远程目的地。

```
const fs = require('fs');
const {execSync} = require('child_process');

const root = '..';
const packageJsonName = 'package.json';
const {version} = require(`${root}/lerna.json`);

let pName;

const updateVersion = (file, version, json) => {
  json.version = version;

  return fs.writeFileSync(file, JSON.stringify(json, null, 2).concat('\n'), {encoding: 'utf8', flag: 'w'});
};

if (fs.existsSync(packageJsonName)) {
  pName = require(`${root}/${packageJsonName}`);
  updateVersion(packageJsonName, version, pName);
}

execSync(`git add .`, (stdout, stderr) => {
  if (stdout) {
    console.log(stdout);
  }

  if (stderr) {
    console.error(stderr);
    process.exit(1);
  }
});

execSync(`git commit -m "chore(release): publish v${version} [skip ci]"`, (stdout, stderr) => {
  if (stdout) {
    console.log(stdout);
  }

  if (stderr) {
    console.error(stderr);
    process.exit(1);
  }
});

execSync(`git tag v${version}`, (stdout, stderr) => {
  if (stdout) {
    console.log(stdout);
  }

  if (stderr) {
    console.error(stderr);
    process.exit(1);
  }
});

execSync(`git push --atomic origin main v${version}`, (stdout, stderr) => {
  if (stdout) {
    console.log(stdout);
  }

  if (stderr) {
    console.error(stderr);
    process.exit(1);
  }
});
```

我们剩下要做的唯一一件事就是修改我们的 Bitbucket 管道来添加脚本。

```
pipelines:
  branches:
    main:
      # ...Other steps mentioned above

      - step:
          name: Versioning
          caches:
            - node
          script:
            - npx lerna version --conventional-commits --yes --force-publish="*" --no-push --no-git-tag-version
            - node ./scripts/versionRootPackage.js
```

随着我们的 pipelines 配置的更新，我们的 monorepo 已经设置好了，并准备好在新代码合并到[main]分支时进行版本控制。当合并发生时，该管道将运行，并且(假设版本化之前的所有步骤都成功)版本化步骤将运行。Lerna 将为我们自动计算下一个版本，并提交所有版本。

## 结论

在本文中，我们介绍了如何使用 Lerna 和 Bitbucket 管道在 monorepo 中处理和设置版本控制，以确保整个 monorepo 中的所有[package.json]文件保持同步。

[获得可销售的](http://www.salable.app)

我们的脚本基于 GitHub 评论中的[脚本。](https://github.com/lerna/lerna/issues/1996#issuecomment-622106404)