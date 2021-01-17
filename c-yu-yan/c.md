# C语言基础

#### 基本写法

```text
#include <stdio.h>

int main(int argc, char *argv[]) {
	
	printf("this is start!");
	
	//	表示退出程序
	return 0;
}
```

#### 变量

```text
#include <stdio.h>

int x,y;
int z;
int addtwonum(){
	z=3;
	printf("this is %d \n",z);
	extern int x,y;
	x=1;
	y=2;
	return x+y;
}

int main(int argc, char *argv[]) {
	int result;
	result = addtwonum();
	printf("result : %d",result);
	return 0;
}
```

#### 常量

```text
#include <stdio.h>

#define MAX_AGE 30

const int MIN_AGE = 20;

int main(int argc, char *argv[]) {
	printf("MaxAge is %d \n",MAX_AGE);
	printf("MinAge is %d \n",MIN_AGE);
	return 0;
}
```

