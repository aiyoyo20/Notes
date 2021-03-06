# 1. tar
>参数说明：
>
>-c: 建立压缩档案
-x：解压
-t：查看内容
-r：向压缩归档文件末尾追加文件
-u：更新原压缩包中的文件
>
>---------------
>
>这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个。下面的参数是根据需要在压缩或解压档案时可选的。
>
>-z：有gzip属性的
-j：有bz2属性的
-Z：有compress属性的
-v：显示所有过程
-O：将文件解开到标准输出
>
>下面的参数-f是必须的
>
>-f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。
## 1.1. tar


严格来说，tar文件只是归档但并未压缩
```
tar -cvf test.tar test1.log test2.log #归档多个文件
tar -cvf test.tar test/* &emsp;[[归档test]]目录下所有文件
tar -cvf test.tar *.log &emsp;#归档所有以.log结尾的文件 
```

```
tar -xvf file.tar        //解压 tar包
```
------

## 1.2. tar.gz
```
tar -zxvf file.tar.gz     //解压tar.gz
```

```
tar -zcvf test.tar.gz file1 file2 [[打包，并以gzip]]压缩
```

## 1.3. tar.bz2
```
tar -jxvf test.tar.bz2 file1 file2 [[打包，并以bzip2]]压缩
```

```
tar -jcvf test.tar.bz2 file1 file2 [[打包，并以bzip2]]压缩
```

## 1.4. tar.Z
```
tar -xZvf file.tar.Z    //解压tar.Z
```

```
tar -cZvf file.tar.Z    //压缩tar.Z
```

## 1.5. tar.xz
```
压缩tar.xz包
先创建xxx.tar文件

tar -cvf xxx.tar xxx
再创建xxx.tar.xz文件

xz -z xxx.tar
如果要保留被压缩的文件，需要加上参数-k
```

```
解压tar.xz包
这是两层压缩，外面是xz压缩，里层是tar压缩，所以分两步实现解压。

xz -d filename.tar.xz
tar -xvf filename.tar.xz

也可以直接解压
tar -xvJf filename.tar.xz
```

# 2. zip/unzip

zip和unzip命令主要用于处理zip包。记得linux默认也是没有的，需要额外安装。

>zip
>功能说明：压缩文件。
语　　法：zip [-AcdDfFghjJKlLmoqrSTuvVwXyz$][-b <工 作目录>][-ll][-n <字 尾字符串>][-t <日 期时间>][-<压 缩效率>][压 缩文件][文件...][-i <范本样式>][-x <范本样式>]
补充说明：zip是个使用广泛的压缩程序，文件经它压缩后会另外产生具 有".zip"扩展名 的压缩文件。
参　　数：
-A   调 整可执行的自动解压缩文件。
-b<工作目录>   指 定暂时存放文件的目录。
-c   替 每个被压缩的文件加上注释。
-d   从 压缩文件内删除指定的文件。
-D   压 缩文件内不建立目录名称。
-f   此 参数的效果和指定"-u"参 数类似，但不仅更新既有文件，如果某些文件原本不存在于压缩文件内，使用本参数会一并将其加入压缩文件中。
-F   尝 试修复已损坏的压缩文件。
-g   将 文件压缩后附加在既有的压缩文件之后，而非另行建立新的压缩文件。
-h   在 线帮助。
-i<范本样式>   只 压缩符合条件的文件。
-j   只 保存文件名称及其内容，而不存放任何目录名称。
-J   删 除压缩文件前面不必要的数据。
-k   使 用MS-DOS兼容格 式的文件名称。
-l   压 缩文件时，把LF字符 置换成LF+CR字 符。
-ll   压 缩文件时，把LF+CR字 符置换成LF字符。
-L   显 示版权信息。
-m   将 文件压缩并加入压缩文件后，删除原始文件，即把文件移到压缩文件中。
-n<字尾字符串>   不 压缩具有特定字尾字符串的文件。
-o   以 压缩文件内拥有最新更改时间的文件为准，将压缩文件的更改时间设成和该文件相同。
-q   不显 示指令执行过程。
-r   递 归处理，将指定目录下的所有文件和子目录一并处理。
-S   包 含系统和隐藏文件。
-t<日期时间>   把 压缩文件的日期设成指定的日期。
-T   检 查备份文件内的每个文件是否正确无误。
-u   更 换较新的文件到压缩文件内。
-v   显 示指令执行过程或显示版本信息。
-V   保 存VMS操作系统的文 件属性。
-w   在 文件名称里假如版本编号，本参数仅在VMS操 作系统下有效。
-x<范本样式>   压 缩时排除符合条件的文件。
-X   不 保存额外的文件属性。
-y   直 接保存符号连接，而非该连接所指向的文件，本参数仅在UNIX之 类的系统下有效。
-z   替 压缩文件加上注释。
-$   保 存第一个被压缩文件所在磁盘的卷册名称。
-<压缩效率>   压 缩效率是一个介于1-9的 数值。

>unzip
功 能说明：解压缩zip文 件
语　　法：unzip [-cflptuvz][-agCjLMnoqsVX][-P <密 码>][.zip文 件][文件][-d <目录>][-x <文件>] 或 unzip [-Z]
补充说明：unzip为.zip压缩文件的解压缩程序。
参　　数：
-c   将 解压缩的结果显示到屏幕上，并对字符做适当的转换。
-f   更 新现有的文件。
-l   显 示压缩文件内所包含的文件。
-p   与-c参数类似，会将解压缩的结果显示到屏幕上，但不会执行任 何的转换。
-t   检 查压缩文件是否正确。，但不解压。
-u   与-f参数类似，但是除了更新现有的文件外，也会将压缩文件中 的其他文件解压缩到目录中。
-v   执 行是时显示详细的信息。或查看压缩文件目录，但不解压。
-z   仅 显示压缩文件的备注文字。
-a   对 文本文件进行必要的字符转换。
-b   不 要对文本文件进行字符转换。
-C   压 缩文件中的文件名称区分大小写。
-j   不 处理压缩文件中原有的目录路径。
-L   将 压缩文件中的全部文件名改为小写。
-M   将 输出结果送到more程 序处理。
-n   解 压缩时不要覆盖原有的文件。
-o   不 必先询问用户，unzip执 行后覆盖原有文件。
-P<密码>   使 用zip的密码选项。
-q   执 行时不显示任何信息。
-s   将 文件名中的空白字符转换为底线字符。
-V   保 留VMS的文件版本信 息。
-X   解 压缩时同时回存文件原来的UID/GID。
[.zip文件]   指定.zip压缩文件。
[文件]   指定 要处理.zip压缩文 件中的哪些文件。
-d<目录>   指 定文件解压缩后所要存储的目录。
-x<文件>   指 定不要处理.zip压 缩文件中的哪些文件。
-Z   unzip -Z等 于执行zipinfo指 令。

## 2.1. 压缩



```
zip test.zip filename # 压缩文件
zip -r test.zip test/ # 打包test目录下的文件
zip -rj test.zip test/ # 打包test目录下文件，且压缩包不带test目录
```
压缩时如果需要对压缩包进行加密，可使用-P参数：
```
zip -r test.zip test1 test -P 66666 # 使用密码66666加密
```

## 2.2. 解压
```
unzip test.zips # 解压文件
unzip -o test.zip -d dir # 将test.zip解压到dir目录
```
## 2.3. jar包
jar包是java归档包，但同样可用unzip解压查看里面的文件：
```
unzip -o java.jar -d dir
```

# 3. gzip

>涉及参数说明：
-k 保留源文件
-d 解开压缩文件
-r 递归处理，将指定目录下的所有文件及子目录一并处理
-v 显示指令执行过程
>
>tar命令带有-z参数，并且打包成tar.gz文件时，便调用gzip进行了压缩。gzip对文本的压缩率约有60%~70%，压缩包文件常以gz为后缀。使用-k参数保留源文件：
```
gzip -k ./* [[当前目录下所有文件进行压缩，每个文件一个gz]]包
gzip -rkv ./* 递归压缩
```
解压也很简单：
```
gzip -dv test.gz 
```
# 4. bzip2

tar命令使用-j参数将文件打包为tar.bz2时，便调用了bzip2进行压缩。bzip2压缩或解压后，会将源文件删除。如果需要保留源文件，可使用-k参数:

```
bzip2 -zk test  [[压缩test]]文件
bzip2 -dk test.bz2  #解压
```

# 5. rar/unrar
rar和unrar命令并非linux发行版自带命令，需要另外安装。常见用法如下：
```
rar a test.tar test  [[将test文件压缩为test]].tar
unrar e test.rar     [[解压test]].tar
```

# 6. war
>jar
-c   创建war包
-v   显示过程信息
-f    指定归档文件名
-M  不创建条目的清单文件
-0   这个是阿拉伯数字，只打包不压缩的意思
```
jar -xvf game.war # 解压war包并存储在当前目录下
jar -cvf filename.war filename  压缩
jar -cvfM0 game.war ./      # 把当前目录下的所有文件打包成game.war
```


# 7. 压缩率比较
>压缩率一般来说：
tar.bz2>tar.gz>zip>tar
压缩率越高，压缩以及解压的时间也就越长。
总结
对文件进行压缩能够节省磁盘空间，进行网络传输时，也能节省带宽，但是需要注意的是，空间和时间是需要根据实际应用进行权衡的。

参考：
[看完这篇Linux下的解压缩你还不会吗？](https://juejin.im/post/6844903923132694536#heading-18)
[Linux：linux下解压*压缩tar.xz、等文件方法](https://www.cnblogs.com/nhdlb/p/11568991.html#_label2)