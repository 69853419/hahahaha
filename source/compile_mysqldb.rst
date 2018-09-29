.. sphinx_demo documentation master file, created by
   sphinx-quickstart on Wed Sep 26 11:14:17 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


在Mac上编译MySQLdb for python2.x
=======================================

1、从http://ftp.ntu.edu.tw/pub/MySQL/Downloads/下载:

    | Connector-C/mysql-connector-c-6.1.10-macos10.12-x86_64.dmg
    | MySQL-8.0/mysql-8.0.11-macos10.13-x86_64.dmg
    | 并安装

2、随便搜一个MySQL-python-1.2.5的tar包，解压

  | 打开site.cfg，编辑mysql_config = /usr/local/\ *mysql/bin/*\ mysql_config（斜体部分根据mysql_config实际位置更改）
  | 执行$sudo python setup.py clean
  | 执行$sudo python setup.py build，
  | 如果报_mysql.c:44:10: fatal error: 'my_config.h' file not found，
  | 执行$ sudo python setup.py build_ext -I\ */usr/local/mysql-connector-c-6.1.10-macos10.12-x86_64*\ /include（斜体部分根据mysql-connector-c实际位置更改）

  
  执行$sudo python setup.py install

3、最后，如果import MySQLdb报如下错：

  | >>> import MySQLdb
  | Traceback (most recent call last):
  |   File "<stdin>", line 1, in <module>
  |   File "build/bdist.macosx-10.13-x86_64/egg/MySQLdb/__init__.py", line 19, in <module>
  |   File "build/bdist.macosx-10.13-x86_64/egg/_mysql.py", line 7, in <module>
  |   File "build/bdist.macosx-10.13-x86_64/egg/_mysql.py", line 6, in __bootstrap__

  | ImportError: dlopen(/Users/smzdm/Library/Caches/Python-Eggs/MySQL_python-1.2.5-py2.7-macosx-10.13-x86_64.egg-tmp/_mysql.so, 2): Library not loaded: 
  | @rpath/libmysqlclient.21.dylib
  |   Referenced from: /Users/smzdm/Library/Caches/Python-Eggs/MySQL_python-1.2.5-py2.7-macosx-10.13-x86_64.egg-tmp/_mysql.so
  |   Reason: image not found

  | export DYLD_LIBRARY_PATH=/usr/local\ */mysql-8.0.11-macos10.13-x86_64*\ /lib（根据实际mysql安装位置修改）
  | 或者根据错误提示，对dylib文件创建软链接
