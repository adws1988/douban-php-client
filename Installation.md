## douban-php-client 安装 ##
1，安装DOM。请检查PHP是否支持DOM，若不支持，需重新编译PHP，configure参数参考如下：
```
./configure --prefix=/usr/local/php  --with-zlib-dir 
--with-bz2  --with-libxml-dir=/usr/local/libxml2 
--with-gd=/usr/local/gd2 --with-freetype-dir 
--with-jpeg-dir --with-png-dir --enable-mbstring  
--with-config-file-path=/etc --with-iconv --disable-ipv6 
--enable-static --enable-maintainer-zts --enable-zend-multibyte 
--enable-inline-optimization --enable-zend-multibyte 
--enable-sockets --enable-soap --with-curl=/usr/local/curl 
--enable-pcntl  --with-mcrypt=/usr/local/libmcrypt  
--with-xmlrpc  --enable-pcntl
```

2，安装HTTP扩展库。请确认PHP的扩展库HTTP是否已经安装。使用PEAR安装HTTP库方法请参考[pear manual](http://pear.php.net/manual/)；也可以先下载HTTP库[HTTP package](http://pecl.php.net/packages.php?catpid=11&catname=HTTP)，然后通过phpize安装：
```
$ cd extname
$ phpize
$ ./configure
$ make
$ make install
```

上述过程执行完毕之后，还需要修改php.ini（请先确认正确的php.ini路径）。在extension\_dir一项加上http.so的路径；同时在extension一项加上http.so。

如在作者机子上，对应项内容为：
```
; Directory in which the loadable extensions (modules) reside.
extension_dir = "/usr/local/php/lib/php/extensions/no-debug-zts-20060613/"
....
; ... or under UNIX:
;
extension=http.so
```

3，安装Zend Gdata。下载[Zend Gdata](http://framework.zend.com/download/gdata)并解压缩，并把Zend Gdata的library路径添加到php.ini的include\_path项中，注意各项path之间以":"隔开。

4，安装douban-php-client。从Downloads下载tgz包并解压；或者从Source获取源码。修改php.ini中的include\_path，添加douban-php-client的library路径。

如在作者机子上，include\_path项内容为：
```
; UNIX: "/path1:/path2"
include_path = ".:/home/flyingww/douban-php-client/library:/home/flyingww/ZendGdata-1.5.2/library/"
```