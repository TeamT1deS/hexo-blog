---
title: 「Rayee@Team T1deS」Pwnable Diary \#01
author: Rayee
excerpt: Pwnable.kr  fd / collision / bof / flag / passcode
date: 2022/3/30 00:00:00
tags: 
- Rayee
- Pwnable
---

## fd  
基础题目 连接到靶机发现目录下存在flag文件 但没有读取权限  
查看fd.c代码并进行分析
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
char buf[32];
int main(int argc, char* argv[], char* envp[]){
        if(argc<2){
                printf("pass argv[1] a number\n");
                return 0;
        }
        int fd = atoi( argv[1] ) - 0x1234;//可操控点[1]
        int len = 0;
        len = read(fd, buf, 32);
        if(!strcmp("LETMEWIN\n", buf)){
                printf("good job :)\n");
                system("/bin/cat flag");
                exit(0);
        }
        printf("learn about Linux file IO\n");
        return 0;
}
```