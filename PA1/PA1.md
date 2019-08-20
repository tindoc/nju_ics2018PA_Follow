# 实验记录

1. SSH 图形界面连接

    其中，[这个方法](https://blog.csdn.net/weixin_42232749/article/details/81624156) 里面的 3.2连接ssh图形用户界面 中的命令 `export DISPORT=localhost:10.0` 可能无效，改成 `export DISPORT=127.0.0.0:20022` 可以，原理不明

    > 其他注意事项：显示图形界面的主机使用的是带有图形界面的Linux

2. 计算机能自动执行出于一个约定：当执行完一条指令之后, 就继续执行下一条指令。（“存储程序”的思想）*Program Counter,PC 程序计数器（在 x86 中又叫 EIP）* 的作用是让计算机知道执行到了哪一条指令，从此**计算机只做一件事**

    ``` c
    while (1) {
      从EIP指示的存储器位置取出指令;
      执行指令;
      更新EIP;
    }
    ```

3. 一个最简单的真实计算机需要满足一下条件

    - 结构上, *Turing Machine,TRM 图灵机* 有存储器, 有PC, 有寄存器, 有加法器
    - 工作方式上, TRM不断地重复以下过程: 从PC指示的存储器位置取出指令, 执行指令, 然后更新PC

4. 在线图灵机演示/模拟

    [中文](http://blog.sciencenet.cn/blog-506146-492176.html)

    [英文](https://turingmachinesimulator.com/)

5. `getopt()` 函数，[参考](https://www.cnblogs.com/qingergege/p/5914218.html)，更详细的参考 `man 3 getopt`

    原型：`int getopt(int argc,char * const argv[ ],const char * optstring);` (#include <unistd,h>)

    附带几个变量：optarg, optind, opterr, optopt

    参数 optstring 的解析：

    `a:b:cd::e` 中的 : 表示参数（一个表示一定带参数，可以连写 `-a123`，可以分写 `-a 123` ，两个表示可选参数，必须连写 `-d123`）

    如果 optstring 以 '+' 开头，非 optstring 中的字符马上停止函数调用；如果以 '-' 开头，非 optstring 中的字符函数返回1，

6. 



# 问题解答

1. 初始虚拟机

    "Hello world" Program

    Simulated x86 hardware

    NEMU

    GNU/Linux

    Docker

    Windows

    Computer hardware

2. 计算机的状态模型

    TRM也有状态的概念。指令表征了TRM的状态，另外包括了一个起始状态（不知道接受状态和拒绝状态算不算指令状态，还是另外独立的状态）。执行指令是一个状态的改变，执行程序是多个状态的改变。

3. 需要多费口舌吗？

    main.c

4. reg_test()是如何测试你的实现的?

    先为结构体 cpu 的 gpr 联合体数组赋值，即为八个32位寄存器依次赋值，再测试对应的16位寄存器和8位寄存器的值是否正确。**是否可以看出是小端，因为 union 的存储方式是相同的起始地址，小的存在上方。**

5. 究竟要执行多久？

    不知道

6. 温故而知新

    不知道 opcode_table 是什么类型。opcode_entry ?????

7. 谁来指示程序的结束？

    应该是程序停止的指令。如果在 main 函数的返回之前调用程序停止的指令，应该就可以在 main 函数返回之前结束程序。

8. 

