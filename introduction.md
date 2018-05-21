### 简介

SciPy是基于Python的Numpy扩展构建的数学算法和便利函数的集合。它通过向用户提供用于操作和可视化数据的高级命令和类，为交互式Python会话增加了强大的功能。通过SciPy，交互式Python会话成为与MATLAB，IDL，Octave，R-Lab和SciLab等系统相媲美的数据处理和系统原型开发环境。

将SciPy基于Python的额外好处是，这也使得强大的编程语言可用于开发复杂的程序和专用应用程序。使用SciPy的科学应用程序受益于世界各地开发人员在众多软件领域的附加模块的开发。从并行编程到Web和数据库子例程和类的所有内容都已经提供给Python程序员。除了SciPy中的数学库之外，所有这些功能都可用。

本教程将使SciPy的首次使用者了解其一些最重要的功能。它假定用户已经安装了SciPy包。也假设了一些通用的Python工具，比如可以通过Python发行版的教程来获得。有关进一步的介绍性帮助，用户将被引导至Numpy文档。

为了简洁和方便，我们经常会假设主包（numpy，scipy和matplotlib）已经被导入为：

```python
import numpy as np
import matplotlib as mpl
import matplotlib.pyplot as plt

```

这些是我们的社区在公共邮件列表讨论后通过的重要惯例。您将看到NumPy和SciPy源代码和文档中使用的这些约定。虽然我们显然不要求您在自己的代码中遵循这些约定，但强烈建议您这么做。


#### Scipy的组织结构
--
SciPy被组织成覆盖不同科学计算领域的子包。这些总结在下表中：

子包	        
cluster -->  聚类算法
constants	 -->   物理和数学常数
fftpack	 -->   快速傅立叶变换例程
integrate	 -->   积分和常微分方程求解器
interpolate -->	插值和平滑样条
io	  -->        输入和输出
linalg  -->  	线性代数
ndimage	-->   N维图像处理
odr	      -->   正交距离回归
optimize	-->   优化和查找程序
signal	   -->   信号处理
sparse	   -->   稀疏矩阵和相关例程
spatial	-->   空间数据结构和算法
special	-->   特殊功能
stats	   -->   统计分布和功能

Scipy子包需要单独导入，例如：

```
from scipy import linalg,optimize

```

由于它们无处不在，这些子包中的一些功能也可以在scipy名称空间中使用，以便于在交互式会话和程序中使用它们。另外，还有许多基本的阵列功能numpy都可以在scipy软件包的顶层获得。在分别查看子包之前，我们先看看其中一些常用功能。

#### 查找文档
--
SciPy和NumPy在https://docs.scipy.org/上提供了HTML和PDF格式的文档版本，涵盖了几乎所有可用的功能。但是，这些文档仍在进行中，有些部分可能不完整或不完整。由于我们是一个志愿者组织，并依靠社区实现增长，因此欢迎并积极鼓励您的参与 - 从提供反馈到改进文档和代码。

Python的文档字符串在SciPy中用于在线文档。有两种方法可以阅读并获得帮助。一个是 模块help中的Python命令pydoc。在没有参数的情况下输入此命令（即）会启动一个交互式帮助会话，该会话允许搜索所有Python可用的关键字和模块。其次，以对象作为参数运行命令 help（obj）将显示对象的调用签名和文档字符串。>>> help

pydoc方法help很复杂，但使用寻呼机来显示文本。有时这可能会干扰您正在运行交互式会话的终端。在命令下也可以使用numpy / scipy特定的帮助系统numpy.info。传递给help命令的对象的签名和文档字符串将打印到标准输出（或作为第三个参数传递的可写入对象）。第二个关键字参数numpy.info定义了打印行的最大宽度。如果一个模块被作为参数传递，help那么将打印在该模块中定义的函数和类的列表。例如：

```python
>>> np.info(optimize.fmin)
 fmin(func, x0, args=(), xtol=0.0001, ftol=0.0001, maxiter=None, maxfun=None,
      full_output=0, disp=1, retall=0, callback=None)

Minimize a function using the downhill simplex algorithm.

Parameters
----------
func : callable func(x,*args)
    The objective function to be minimized.
x0 : ndarray
    Initial guess.
args : tuple
    Extra arguments passed to func, i.e. ``f(x,*args)``.
callback : callable
    Called after each iteration, as callback(xk), where xk is the
    current parameter vector.

Returns
-------
xopt : ndarray
    Parameter that minimizes function.
fopt : float
    Value of function at minimum: ``fopt = func(xopt)``.
iter : int
    Number of iterations performed.
funcalls : int
    Number of function calls made.
warnflag : int
    1 : Maximum number of function evaluations made.
    2 : Maximum number of iterations reached.
allvecs : list
    Solution at each iteration.

Other parameters
----------------
xtol : float
    Relative error in xopt acceptable for convergence.
ftol : number
    Relative error in func(xopt) acceptable for convergence.
maxiter : int
    Maximum number of iterations to perform.
maxfun : number
    Maximum number of function evaluations to make.
full_output : bool
    Set to True if fopt and warnflag outputs are desired.
disp : bool
    Set to True to print convergence messages.
retall : bool
    Set to True to return list of solutions at each iteration.

Notes
-----
Uses a Nelder-Mead simplex algorithm to find the minimum of function of
one or more variables.
```
另一个有用的命令是source。当用Python编写的函数作为参数时，它会打印出该函数的源代码列表。这可以帮助您了解算法或了解某个函数在其参数中所做的工作。另外不要忘记dir 可以用来查看模块或包的命名空间的Python命令。

另外在jupyter notebook中还可以使用例如optimize.fmin？和optimize.fmin？？分别获取函数的说明以及函数的源码。
