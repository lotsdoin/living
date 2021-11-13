# Git 三剑客
## Git 最小化配置

```sh
git config --global user.name 'lotsdoin'
git config --global user.email 'lotsdoin@gmail.com'
```
git 配置的三个级别:

 `git config --local`: lcoal 只对某个仓库有效
 `git config --global`: global 对当前用户所有仓库有效
 `git config --system`: system 对系统所有登录的用户有效
 优先级关系 `system < global < local`

未跟踪，跟踪，暂存区，commit 区

```c
int main(int argc, char[] argv){
    printf("Hello, world");
}
```

## 删除未存储的变动

## 修改历史 commit 信息

```txt

commit 2907f4dad8d51a3dfbfd0a82a31989fd2cdb7e89
Author: tracer-ics2021 tracer@njuics.org
Date:   Mon Nov 8 17:49:36 2021 +0800

      compile
```
`git rebase -i 2907f4dad8d51a3dfbfd0a82a31989fd2cdb7e89` 修改保存即可。`git commit --amend` 可直接修改上最后一条 commit。
  

## 修改 git status 显示中文八进制字符编码

`git config --global core.quotepath false`

