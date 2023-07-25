# C-p55---2-
C语言学习笔记 p55 自定义数据类型-结构体(2)
#include<stdio.h>
int main()
struct S3
{
    double d;
    char c;
    int i;
};
{
    struct S3 s3;
    printf("%d\n",sizeof(struct S3));
    return 0;
}//输出为16，注：这里要计算偏移量。double偏移量0-7、char c在8的位置上没有问题，到int时，偏移量为9不是4的倍数，中间浪费3个内存空间，在偏移量为12的内存空间进行

struct S4
{
    char c1;
    struct S3 s3;//存放结构体时，前面一个类型要浪费结构体中占内存最大的变量的字节，这里要浪费7个字节才能等于s3的最大类型double(8),然后在放16个字节
    double d;//这里偏移量为24，可以整除8，所以直接放
};//答案输出为32


//在设计结构体的时候，我们既要满足对齐，又要节省空间，要做到让占用空间小的成员尽量集中在一起

//修改默认对齐数
#pragma pack(4)//设置默认对齐数为4
struct S
{
    char c1;//1
    //原来是浪费7个字节，现在修改默认对齐数，浪费3个字节
    double d;//8
    
}；
#pragma pack()
//取消设置的默认对齐数

int main()
{
    struct S s;
    printf("%d\n",sizeof(s));
    return 0;
}

#include<stddef.h>
struct S
{
    char c;
    int i;//偏移量为4
    double d;//偏移量为8
};
int main()
{
    //offsetof();计算结构体成员的偏移量，offsetof是宏不是函数
    printf("%d\n",offsetof(struct S,c));
    printf("%d\n",offsetof(struct S,i));
    printf("%d\n",offsetof(struct S,d));
    return 0;
}
