# 说明

这只是一个练习git相关命令使用的例子。

```bash
[root@2-0002 HelloWorld]# ls
AUTHORS  ChangeLog  CODE_OF_CONDUCT.md  configure.ac  CONTRIBUTING.md  LICENSE  main.c  Makefile.am  NEWS  README  README.md  utils.c  utils.h

[root@2-0002 HelloWorld]# autoreconf -ivf
configure.ac:2: installing './install-sh'
configure.ac:2: installing './missing'
Makefile.am: installing './INSTALL'
Makefile.am: installing './COPYING' using GNU General Public License v3 file
Makefile.am:     Consider adding the COPYING file to the version control system
Makefile.am:     for your code, to avoid questions about which license your project uses
Makefile.am: installing './depcomp'

[root@2-0002 HelloWorld]# ls
aclocal.m4  AUTHORS  autom4te.cache  ChangeLog  CODE_OF_CONDUCT.md  configure  configure.ac  CONTRIBUTING.md  COPYING  depcomp  INSTALL  install-sh  LICENSE  main.c  Makefile.am  Makefile.in  missing  NEWS  README  README.md  utils.c  utils.h
```

# GitHub 的 Actions 报错

CI 在 configure 步骤失败了，报错信息是 Permission denied，退出码为 126。这是一个非常典型的问题，通常不涉及代码错误，而是文件执行权限的问题。

## 🎯 错误原因
configure 脚本没有可执行权限
exit code 126 在 Linux 中明确表示“命令找到了，但没有执行权限”。
当你把在 Windows（或权限控制不严的环境）下生成的 configure 脚本提交到仓库时，Git 可能只记录了文件内容，而没有记录它的“可执行”属性。
因此，当 GitHub Actions 的 Ubuntu 环境尝试运行 ./configure 时，系统会拒绝执行。

## 🛠️ 解决方案
在仓库中直接修改文件权限（推荐）

在本地终端（Git Bash）中，进入项目根目录。

执行以下命令，为 configure 文件添加可执行权限：

```bash
git update-index --chmod=+x configure
```
这个命令会更新 Git 索引，将 configure 文件标记为可执行文件。

提交并推送这个改动：

```bash
git commit -m "fix: make configure script executable"
git push
```
推送后，GitHub 仓库中的 configure 文件就会带上可执行权限，后续 CI 流程中的 ./configure 步骤就能正常运行了。
