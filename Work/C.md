# C language programming

## 通过设置环境变量来添加系统 include, 链接库 的路径
可以通过`echo | gcc -v -x c -E -` 来显示 gcc 详细查看 include，链接库信息。
通过`export -p`显示环境变量如果有目录需要添加可以用`:`不同目录即可。

```bash
# C in macOS
export C_INCLUDE_PATH=path/you/want/add:another/path
# C in Linux
export C_INCLUDE_PATH=path/you/want/add:$C_INCLUDE_PATH
# C++ in macOS
export CPLUS_INCLUDE_PATH=path/you/want/add:another/path
# C++ in Linux
export CPLUS_INCLUDE_PATH=path/you/want/add:$C_INCLUDE_PATH
# 动态链接库搜索路径 in macOS
export LD_LIBRARY_PATH=path/you/want/add:another/path
# 动态链接库搜索路径 in Linux
export LD_LIBRARY_PATH=path/you/want/add:$LD_LIBRARY_PATH
# 静态链接库搜索路径 in macOS
export LIBRARY_PATH=path/you/want/add:another/path
# 静态链接库搜索路径 in Linux
export LIBRARY_PATH=path/you/want/add:$LIBRARY_PATH

```

## 重复定义

```c
#ifndef __CPP // if not define
#define __CPP
#endif
```

## ln -s source link

最好都是用的绝对路径，macOS 上用相对路径生成软连接都没成功。
```bash
# 生成 openssl (密码库)文件软链接
ln -s usr/local/Cellar/openssl@1.1/1.1.1l_1/include/ /usr/local/include/openssl
ln -s ln -s /usr/local/Cellar/openssl@1.1/1.1.1l_1/lib/libcrypto.1.1.dylib  /usr/local/lib/libcrypto.dylib
ln -s /usr/local/Cellar/openssl@1.1/1.1.1l_1/lib/libssl.1.1.dylib  /usr/local/lib/libssl.dylib
```
## 编译

`gcc -E source_code.c` 编译停止在预阶段，`gcc -S source_code.c` 编译停在汇编阶段，`gcc -c source_code.c` 链接阶段
`objdump -d`查看二文件反汇编
编译遇到好的办法是`阅读命令的日志`,`gcc --verbose source_code.c`

## 宏定义与展开

宏展开：通过复制/粘贴改编代码的形态
因为 aa 与 bb 都是空，所以相等
```c
#include <stdio.h>
int main(){
#define aa == bb
printf("Yes");
#else
printf("No");
#endif
return 0;
}
```
知乎问题：如搞垮一个 OJ ？

```c
#define A 'aaaaaaaaaa'
#define TEN(A) A A A A A A A A A A 
#deinfe B TEN(A)
#deinfe C TEN(A)
#deinfe D TEN(A)
#deinfe E TEN(A)
#deinfe F TEN(A)
#deinfe G TEN(A)
int main(){puts(G);}
```
