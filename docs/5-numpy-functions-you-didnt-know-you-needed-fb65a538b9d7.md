# 5 个你不知道自己需要的功能

> 原文：<https://blog.devgenius.io/5-numpy-functions-you-didnt-know-you-needed-fb65a538b9d7?source=collection_archive---------15----------------------->

确切地了解他们做什么，以及工作和中断的例子

![](img/9674395ec3ab0cf106c3783185e6679b.png)

NumPy(数字 Python)是一个开源的 Python 库，几乎在科学和工程的每个领域都有使用。这是在 Python 中处理数值数据的通用标准。NumPy 库包含多维数组和矩阵数据结构。它为 Python 添加了强大的数据结构，保证了使用数组和矩阵的高效计算，并且提供了一个巨大的高级数学函数库，可以对这些数组和矩阵进行操作。NumPy 代表数值 Python，它是一个开源项目。

NumPy 允许我们创建多维数组，并允许我们执行简单和复杂的操作，如索引、广播、切片、矩阵乘法。

**为什么是 NumPy？？**

NumPy 是 Python 中的一个库，它提供了处理数字数据数组的工具。它被设计为比内置的 Python 列表数据类型快得多，性能提升高达 50 倍。NumPy 中的 array 对象称为`ndarray`，它提供了许多函数，使得使用数组更加高效和方便。与分散在内存中的 Python 列表不同，NumPy 数组存储在单个连续的内存块中，允许进程更有效地访问和操作它们。

我们将看到如何更好地组织你的 NumPy 数组，并使用下面的函数计算一些有趣的运算。这些功能是

*   numpy.sort
*   numpy.argmax
*   numpy 在哪
*   numpy.count _ 非零
*   numpy.extract

让我们从导入 Numpy 作为`np`开始

`import numpy as np`

# 函数 1 — np.sort

这个函数返回一个数组的排序副本。请注意，原始数组不会改变。该函数采用以下参数。

参数:

*   arr:要排序的数组。
*   axis:我们需要沿其启动数组的轴。(可选)
*   order:该参数指定首先比较哪些字段。(可选)
*   种类:['quicksort'{default}，' mergesort '，' heap sort ']排序算法。(可选)

让我们用一些例子来理解。

示例 1

`arr1`中每个子列表的元素已经按升序排序。

示例 2

`numpy.sort`是一个可以用来对 NumPy 数组的元素进行排序的函数。`axis`参数指定了数组的哪个轴要排序。`axis`的默认值是-1，沿着最后一个轴排序。当`axis`设置为`None`时，`numpy.sort`将通过将所有子列表连接成一个一维数组来展平数组，然后按升序对结果数组进行排序。

示例 3

我们收到一个错误，指出指定的轴超出界限。我们给出了一个轴为(0，1)的二维数组。由于给定数组的第三维不存在，我们得到了错误。若要修复此错误，请确保您指定的轴在给定数组的维度范围内。

当您有一个随机无序数据的集合或数组，并且用例要求您以有组织的方式对数据进行排序时，请使用 sort()函数。

# 函数 2 — numpy.argmax

返回轴上最大值的索引。该函数采用以下参数。

参数

*   arr:输入数组
*   axis:我们需要沿其启动数组的轴。(可选)
*   out:如果提供，结果将被插入到这个数组中。(可选)
*   keepdims : bool。如果设置为真，减少的轴将作为尺寸为 1 的尺寸留在结果中。使用此选项，结果将针对阵列正确广播。(可选)

示例 1

arr2 在位置 5 具有最大值。因此，它显示 argmax 输出为 5。在最大值多次出现的情况下，返回与第一次出现相对应的索引。

示例 2

在这种情况下，`axis=0`表示应该返回每一列中的最大值。因此，`np.argmax(arr2, axis=0)`将返回一个数组，其中包含`arr2`的每一列中最大值的索引。例如，第一列中的最大值是 100，位于第一列的索引 0 处。第二列中的最大值是 15，位于第二列的索引 1 处。得到的数组将是`[0, 1, 1].`

示例 3

我们收到一个错误，指出指定的轴超出界限。我们给出了一个轴为(0，1)的二维数组。由于给定数组的第三维不存在，我们得到了错误。若要修复此错误，请确保您指定的轴在给定数组的维度范围内。

使用 np.argmax()函数获取随机变量序列最大值的索引。

# 函数 3 — numpy.where

函数 numpy.where(condition，x，y)根据条件返回从 x 或 y 中选择的元素。如果条件为真，则返回 x，如果条件为假，则返回 y

函数 numpy.where(condition)将返回当只提供条件，而没有给出 x 和 y 的值时，落在某个条件中的值的**索引位置**。

示例 1

我们检查大于 5 的值。小于 5 的值保持不变。大于 5 的值乘以 10。

示例 2

这里，函数返回满足条件的元素的索引位置，在这个例子中，它返回所有大于 14 的元素索引(行，列)。

示例 3

该错误是因为缺少第三个参数。我们必须提供所有三个参数，否则第二个和第三个参数都应该省略。

where 函数是一个非常好的函数，可以知道要分析的数据中异常值的索引，并获取这些异常值。对于条件问题，这是一个非常有用的函数，在条件问题中，满足条件的和不满足条件的需要执行不同的操作。

# 函数 4—numpy . count _ 非零

计算数组中非零值的个数。

示例 1

我们创建了一个 4 行 3 列的单位矩阵。然后我们发现给定数组中有多少非零值。

示例 2

我们可以用坐标轴来计算非零数组的个数。

示例 3

正如我们在这里看到的，提供的轴超出了界限。因此我们得到一个错误。就数组的维度而言，我们应该确保提供一个在范围内的轴。

# 函数 5 — numpy.extract

返回满足某些条件的数组元素。

Syntex : numpy.extract(condition，arr)

numpy.extract 函数有两个参数。

*   条件:一个数组，其非零或真的条目指示要提取的 arr 元素。
*   arr:与条件大小相同的输入数组。

返回:从 arr 中提取条件为真的 n array 秩为 1 的值数组。

示例 1

输出是 arr 中条件为真的值的秩为 1 的数组。

示例 2

输出是 arr 中条件为真的值的秩为 1 的数组。

示例 3

我们可以使用 and 运算符组合多个条件。

我们可以使用 Numpy extract()函数从符合条件的数组中提取特定的元素。

# 结论

我们已经了解了下面给出的这些函数和示例:-

*   numpy.sort
*   numpy.argmax
*   numpy 在哪
*   numpy.count _ 非零
*   numpy.extract

我们发现，有一些非常有用的函数可以快速、高效地用较少的代码完成特定的工作。这就是 NumPy 库的强大之处。

# 参考

这些是您的参考资料的链接:

*   Numpy 官方教程:[https://numpy.org/doc/stable/user/quickstart.html](https://jovian.ai/outlink?url=https%3A%2F%2Fnumpy.org%2Fdoc%2Fstable%2Fuser%2Fquickstart.html)
*   Numpy 线性代数官方:【https://numpy.org/doc/stable/reference/routines.linalg.html 

请随时给予反馈。希望你喜欢阅读。

可以联系我: [Linkedin](https://www.linkedin.com/in/renuverma55/)