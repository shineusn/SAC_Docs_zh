两种数据形式
============

SAC 文件格式有两种形式：二进制型和字符型\ [1]_。字符型与二进制型是完全等价的，
只是字符型是给人看的，二进制型是给机器读写的。从 C 程序的角度来看，两者的区别
在于，写文件时前者使用 ``fprintf`` 后者使用 ``fwrite``\ 。

二进制型的 SAC 数据，占用更小的磁盘空间，读写速度更快，因而是最常用的 SAC
格式形式。当文件出现问题时，字符型数据便于查看文件内容。

通常，字符型的SAC文件以 ``ASC``\ [2]_\ 结尾， 二进制型的 SAC 文件以后缀 ``SAC``
结尾。但是，SAC 在读取文件时是不判断文件后缀的，所以文件后缀是什么并不重要，
在某些情况下，会以 ``BHE``\ 、\ ``BHN``\ 、\ ``BHZ`` 这样的后缀结尾。在下面的
示例中，很多 SAC 文件甚至没有后缀。

两种形式的互相转换
------------------

你是否想要一个字符型的 SAC 文件，用编辑器打开好好看看 SAC 数据究竟长什么样？
SAC 自带的命令可以实现两种形式的转换\ [3]_。

.. code:: bash

    SAC> fg seis
    SAC> w seis             # 先生成一个二进制型 SAC 数据，以做测试

将二进制型转换成字符型：

.. code:: bash

    SAC> r seis             # 读二进制型文件
    SAC> w alpha seis.a     # 以字符型写入

将字符型转换成二进制型：

.. code:: bash

    SAC> r alpha seis.a     # 读字符型文件
    SAC> w sac seis.b       # 以二进制型写入，可以省略sac，写成w seis.b

试试用你最喜欢的文本编辑器打开字符型的 ``seis.a`` 吧，其内容如下：

.. code:: bash

   0.01000000      -1.569280       1.520640      -12345.00      -12345.00
     9.459999       19.45000      -41.43000       10.46400      -12345.00
    -12345.00      -12345.00      -12345.00      -12345.00      -12345.00
    -12345.00      -12345.00      -12345.00      -12345.00      -12345.00
    -12345.00      -12345.00      -12345.00      -12345.00      -12345.00
    -12345.00      -12345.00      -12345.00      -12345.00      -12345.00
    -12345.00       48.00000      -120.0000      -12345.00      -12345.00
     48.00000      -125.0000      -12345.00       15.00000      -12345.00
    -12345.00      -12345.00      -12345.00      -12345.00      -12345.00
    -12345.00      -12345.00      -12345.00      -12345.00      -12345.00
     373.0627       88.14721       271.8528       3.357465      -12345.00
    -12345.00    -0.09854718       0.000000       0.000000      -12345.00
    -12345.00      -12345.00      -12345.00      -12345.00      -12345.00
    -12345.00      -12345.00      -12345.00      -12345.00      -12345.00
         1981        88        10        38        14
            0         6         0         0      1000
       -12345    -12345    -12345    -12345    -12345
            1        50         9    -12345    -12345
       -12345    -12345        42    -12345    -12345
       -12345    -12345    -12345    -12345    -12345
       -12345    -12345    -12345    -12345    -12345
            1         1         1         1         0
    CDV      K8108838
    -12345  -12345  -12345
    -12345  -12345  -12345
    -12345  -12345  -12345
    -12345  -12345  -12345
    -12345  -12345  -12345
    -12345  -12345  -12345
    -12345  -12345  -12345
    -0.09728001    -0.09728001    -0.09856002    -0.09856002    -0.09728001
    -0.09600000    -0.09472002    -0.09344001    -0.09344001    -0.09344001
    -0.09344001    -0.09344001    -0.09472002    -0.09472002    -0.09344001
    ......

第1–30行是头段区，31之后的行是数据区。目前你可能还看不懂头段区的
这些数字或者字符代表什么。没关系，在下一节会详细介绍 SAC 头段区，记得
一定要一边看下一节的内容，一边对照着这个例子，好好琢磨每一个头段的含义。

.. [1] 原为 alphanumeric，译为文数字。
.. [2] ASCII 的简写。
.. [3] 也可以使用 SAC 的 ``convert`` 命令进行转换，不过此命令即将被淘汰，因而
   这里不会介绍。
