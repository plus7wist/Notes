# 使用 makefile

最近觉得累，又抛弃了存代码的行为，不过还是想写写题解的。恩……此处不表这个。

撸题的时候建个叫做 cpp 的文件夹，里面搞个 makefile：

```make
data.out: data.in main
	@time -f "time used: %E" ./main < data.in > data.out
	@more data.out
main: main.cpp
	@g++ main.cpp -o main -std=c++11
```

每次就可以光 make 了。
