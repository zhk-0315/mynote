- 屏蔽原因：socket网络编程中，在一端断连情况下，存在另一端发送内容是会造成进程产生SIGPIPE信号而导致进程结束，这是我们所不愿看到的。
- 屏蔽方法
  1. signal(SIGPIPE , SIG_SIG)------SIG_IGN的缺省方式为忽略。
  2. signal(SIGPIPE , handler)---------handler为自定义函数指针，可以自行设置信号处理方式。