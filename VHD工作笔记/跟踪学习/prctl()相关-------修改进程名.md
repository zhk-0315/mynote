
prctl(PR_SET_NAME, "进程名"); \
关于prctl：prctl()函数详解: \
以下转载（https://www.cnblogs.com/sunyubo/archive/2010/12/10/2282086.html）\
对于多线程应用程序，如果能够给每个线程命名，那么调试起来的便利是不言而喻的。今天看LWN上的周报，看到有人正在给prctl添加给进程内其它线程命名的接口，并从中得知，给线程自身命名的接口已经存在，不由窃喜，遂写下以下验证代码：
```
#include
#include
#include
void* tmain(void *arg)
{
char name[32];
prctl(PR_SET_NAME, (unsigned long)"xx");
prctl(PR_GET_NAME, (unsigned long)name);
printf("%s/n", name);
while (1)
sleep(1);
}
int main(void)
{
pthread_t tid;
pthread_create(&tid, NULL, tmain, NULL);
pthread_join(tid, NULL);
return 0;
}
```
编译并运行：\
xiaosuo@gentux test $ gcc t_threadname.c -l pthreadxiaosuo@gentux test $ ./a.outxxs