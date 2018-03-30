# 中文汉字识别（in tensorflow）

**输入：已经制作好的手写中文汉字数据集**

**输出：识别的准确率**

**知识点：**

<font size="20" color="black">**tensorflow使用文件名队列+内存队列双队列的形式读入文件**

    首先，我们先创建数据流图，这个数据流图由一些流水线的阶段组成，阶段间用队列连接在一起。

    第一阶段将生成文件名，我们读取这些文件名并且把他们排到文件名队列中。

    第二阶段从文件中读取数据（使用Reader），产生样本，而且把样本放在一个样本队列中。

    根据你的设置，实际上也可以拷贝第二阶段的样本，使得他们相互独立，这样就可以从多个文件中并行读取。

    在第二阶段的最后是一个排队操作，就是入队到队列中去，在下一阶段出队。

    因为我们是要开始运行这些入队操作的线程，所以我们的训练循环会使得样本队列中的样本不断地出队。


<font size="20" color="darkblue">**主要有一下步骤：**

    1.文件名列表

    2.可配置的 文件名乱序(shuffling)

    3.可配置的 最大训练迭代数(epoch limit)

    4.文件名队列

    5.针对输入文件格式的阅读器

    6.纪录解析器

    7.可配置的预处理器

    8.样本队列

**图解：**

    ![avatar](http://wiki.jikexueyuan.com/project/tensorflow-zh/images/AnimatedFileQueues.gif)

