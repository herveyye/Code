# 第一章

用户与之交互的程序，基于文本的称为**shell**，基于图标的称为**GUI**，它们实际上并不是操作系统的一部分

多数计算机有两种运行模式：**内核态**和**用户态**  
操作系统运行在内核态，具有对所有硬件的完全访问权，可以执行机器能够运行的任何指令  
软件的其余部分运行在用户态，只使用了机器指令中的一个子集

用户接口程序（shell或GUI）处于用户态程序中的最低层次  
操作系统运行在裸机之上，为其他所有软件提供基础的运行环境