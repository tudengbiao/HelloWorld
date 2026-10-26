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


