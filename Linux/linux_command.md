## grep、egrep、fgrep
grep （global search regular expression(RE) and print out the line,全面搜索正则表达式并把行打印出来）是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。Unix的grep家族包括grep、egrep和fgrep。egrep和fgrep的命令只跟grep有很小不同。egrep是grep的扩展，支持更多的re元字符， fgrep就是fixed grep或fast grep，它们把所有的字母都看作单词，也就是说，正则表达式中的元字符表示回其自身的字面意义，不再特殊。Linux使用GNU版本的grep。它功能更强，可以通过-G、-E、-F命令行选项来使用egrep和fgrep的功能。

grep的工作方式是这样的，它在一个或多个文件中搜索字符串模板。如果模板包括空格，则必须被引用，模板后的所有字符串被看作文件名。搜索的结果被送到屏幕，不影响原文件内容。

grep可用于shell脚本，因为grep通过返回一个状态值来说明搜索的状态，如果模板搜索成功，则返回0，如果搜索不成功，则返回1，如果搜索的文件不存在，则返回2。我们利用这些返回值就可进行一些自动化的文本处理工作。

匹配模式选择:

|参数|意义|                                
|---|---|  
|-E, --extended-regexp|扩展正则表达式egrep|
|-F, --fixed-strings  | 一个换行符分隔的字符串的集合fgrep|
|-G, --basic-regexp   |基本正则|
|-P, --perl-regexp    |调用的perl正则|
|-e, --regexp=PATTERN | 后面根正则模式，默认无|
|-f, --file=FILE      | 从文件中获得匹配模式|
|-i, --ignore-case    |不区分大小写|
|-w, --word-regexp    |匹配整个单词|
|-x, --line-regexp    |匹配整行|
|-z, --null-data      |一个 0 字节的数据行，但不是空行|

杂项:

|参数|意义|                                
|---|---| 
|-s, --no-messages 	|不显示错误信息|
|-v, --invert-match 	|显示不匹配的行|
|-V, --version 		|显示版本号|
|--help 				|显示帮助信息|
|--mmap 				|use memory-mapped input if possible|

输入控制:

|参数|意义|                                
|---|---| 
|-m, --max-count=NUM 		|匹配的最大数|
|-b, --byte-offset 			|打印匹配行前面打印该行所在的块号码。|
|-n, --line-number 			|显示的加上匹配所在的行号|
|--line-buffered 			|刷新输出每一行|
|-H, --with-filename 		|当搜索多个文件时，显示匹配文件名前缀|
|-h, --no-filename 			|当搜索多个文件时，不显示匹配文件名前缀|
|--label=LABEL 				|print LABEL as filename for standard input|
|-o, --only-matching 		|只显示一行中匹配PATTERN 的部分|
|-q, --quiet, --silent 		|不显示任何东西|
|--binary-files=TYPE 		|假定二进制文件的TYPE 类型； TYPE 可以是binary', text', 或`without-match'|
|-a, --text 				|匹配二进制的东西|
|-I 						|不匹配二进制的东西|
|-d, --directories=ACTION 	|目录操作，读取，递归，跳过|
|-D, --devices=ACTION 		|设置对设备，FIFO,管道的操作，读取，跳过|
|-R, -r, --recursive 		|递归调用|
|--include=PATTERN 			|只查找匹配FILE_PATTERN 的文件|
|--exclude=PATTERN 			|跳过匹配FILE_PATTERN 的文件和目录|
|--exclude-from=FILE 		|跳过所有除FILE 以外的文件|
|-L, --files-without-match 	|匹配多个文件时，显示不匹配的文件名|
|-l, --files-with-matches 	|匹配多个文件时，显示匹配的文件名|
|-c, --count 				|显示匹配的行数|
|-Z, --null 				|在FILE 文件最后打印空字符|

文件控制:

|参数|意义|                                
|---|---| 
|-B, --before-context=NUM 	|打印匹配本身以及前面的几个行由NUM控制|
|-A, --after-context=NUM 	|打印匹配本身以及随后的几个行由NUM控制|
|-C, --context=NUM 			|打印匹配本身以及随后，前面的几个行由NUM控制|
|-NUM 						|和-C的用法一样的|
|--color[=WHEN],||
|--colour[=WHEN] 			|使用标志高亮匹配字串；|
|-U, --binary 				|使用标志高亮匹配字串；|
|-u, --unix-byte-offsets 	|当CR 字符不存在，报告字节偏移(MSDOS 模式)|

>‘egrep’ is the same as ‘grep -E’.  ‘fgrep’ is the same as ‘grep -F’.
Direct invocation as either ‘egrep’ or ‘fgrep’ is deprecated, but is
   Traditional ‘egrep’ did not support interval expressions and some
‘egrep’ implementations use ‘\{’ and ‘\}’ instead, so portable scripts


## head、tail
`head` 命令可用于查看文件的开头部分的内容，有一个常用的参数 -n 用于显示行数，默认为 10，即显示 10 行的内容。

命令格式：`head [参数] [文件]`

|参数|意义|
|  ----  | ----  |
|-q |隐藏文件名|
|-v |显示文件名|
|-c<数目>| 显示的字节数。|
|-n<行数>| 显示的行数。|

`tail` 命令和`head`类似，但用于查看文件的末尾部分的内容

命令格式`tail [参数] [文件] `

|参数 |  意义|
|---|---|
|-f   |	循环读取,如日志文件有更新时不断输出更新的内容|
|-q  |	不显示处理信息|
|-v		| 显示详细的处理信息|
|-c<数目>| 显示的字节数|
|-n<行数>| 显示文件的尾部 n 行内容|
|--pid=PID| 与-f合用,表示在进程ID,PID死掉之后结束|
|-q, --quiet, --silent| 从不输出给出文件名的首部|
|-s, --sleep-interval=S| 与-f合用,表示在每次反复的间隔休眠S秒|

## cat、tac
cat（英文全拼：concatenate）命令用于连接文件并打印到标准输出设备上,可输出多个文件

语法格式
`
cat [-AbeEnstTuv] [--help] [--version] fileName1 fileName2
`

|参数|意义|
|---|---|
|-b 或 --number-nonblank	|和 -n 相似，只不过对于空白行不编号。|
|-s 或 --squeeze-blank		|当遇到有连续两行以上的空白行，就代换为一行的空白行。|
|-v 或 --show-nonprinting	|使用 ^ 和 M- 符号，除了 LFD 和 TAB 之外。|
|-E 或 --show-ends  		|在每行结束处显示 $。|
|-T 或 --show-tabs			| 将 TAB 字符显示为 ^I。|
|-A, --show-all			|等价于 -vET。|
|-e						|等价于"-vE"选项；|

`tac`按行为单位反向显示文件内容，如果没有文件或文件为-则读取标准输入。
处理多个文件时，依次将每个文件反向显示，而不是将所有文件连在一起再反向显示。

|参数					|	意义|
|---|---|
|-b, --before           |  在之前而不是之后连接分隔符。|
|-r, --regex            |  将分隔符作为基础正则表达式（BRE）处理。|
|-s, --separator=STRING |  使用STRING作为分隔符代替默认的换行符。|
|--help                 |  显示帮助信息并退出。|
|--version              |  显示版本信息并退出。|

## less、more
less 可以随意浏览文件，支持翻页和搜索，支持向上翻页和向下翻页。

|参数| 意义|
|---|---|
|-b |<缓冲区大小> 设置缓冲区的大小|
|-e |当文件显示结束后，自动离开|
|-f |强迫打开特殊文件，例如外围设备代号、目录和二进制文件|
|-g |只标志最后搜索的关键词|
|-i |忽略搜索时的大小写|
|-m |显示类似more命令的百分比|
|-N |显示每行的行号|
|-o |<文件名> 将less 输出的内容在指定文件中保存起来|
|-Q |不使用警告音|
|-s |显示连续空行为一行|
|-S |行过长时间将超出部分舍弃|
|-x |<数字> 将"tab"键显示为规定的数字空格|

进入文件浏览页面后可以进一步操作的键

|参数| 意义|
|---|---|
|/字符串|向下搜索"字符串"的功能|
|?字符串|向上搜索"字符串"的功能|
|n|重复前一个搜索（与 / 或 ? 有关）|
|N|反向重复前一个搜索（与 / 或 ? 有关）|
|b| 向上翻一页|
|d |向后翻半页|
|h| 显示帮助界面|
|Q |退出less 命令|
|u |向前滚动半页|
|y| 向前滚动一行|
|空格键| 滚动一页|
|回车键 |滚动一行|
|[pagedown]| 向下翻动一页|
|[pageup]| 向上翻动一页|

浏览多个文件:`less log1.log log2.log`

说明：

输入 `：n`后，切换到 log2.log

输入 `：p` 后，切换到log1.log

more 命令类似 cat ，不过会以一页一页的形式显示，更方便使用者逐页阅读

语法：`more [-dlfpcsu] [-num] [+/pattern] [+linenum] [fileNames..]`

|参数|意义|
|---|---|
|-num|一次显示的行数|
|-d 		|提示使用者，在画面下方显示 [Press space to continue, 'q' to quit.] ，如果使用者按错键，则会显示 [Press 'h' for instructions.] 而不是 '哔' 声|
|-l 		|取消遇见特殊字元 ^L（送纸字元）时会暂停的功能|
|-f 		|计算行数时，以实际上的行数，而非自动换行过后的行数（有些单行字数太长的会被扩展为两行或两行以上）|
|-p 		|不以卷动的方式显示每一页，而是先清除萤幕后再显示内容|
|-c 		|跟 -p 相似，不同的是先显示内容再清除其他旧资料|
|-s 		|当遇到有连续两行以上的空白行，就代换为一行的空白行|
|-u 		|不显示下引号 （根据环境变数 TERM 指定的 terminal 而有所不同）|

+/pattern 在每个文档显示前搜寻该字串（pattern），然后从该字串之后开始显示

+linenum 从第 num 行开始显示

fileNames 欲显示内容的文档，可为复数个数

|常用操作命令|意义|
|---|---|
|Enter  |向下n行，需要定义。默认为1行|
|Ctrl+F |向下滚动一屏|
|空格键  |向下滚动一屏|
|Ctrl+B |返回上一屏|
|=     |输出当前行的行号|
|：f   |输出文件名和当前行的行号|
|V     |调用配置的编辑器|
|!命令 |调用Shell，并执行命令|
|q     |退出more|

## find

`find` 语法:`find   path   -option   [   -print ]   [ -exec   -ok   command ]   {} \;`

path 为查找的起始目录，如果 path 是空字串则使用目前路径，path 后的部分为expression，如果 expression 是空字串则使用 -print 为预设 expression。

|参数|意义|
|---|---|
|-amin<分钟>|查找在指定时间曾被存取过的文件或目录，单位以分钟计算；|
|-anewer<参考文件或目录>|查找其存取时间较指定文件或目录的存取时间更接近现在的文件或目录；|
|-atime<24小时数>|查找在指定时间曾被存取过的文件或目录，单位以24小时计算；|
|-cmin<分钟>|查找在指定时间之时被更改过的文件或目录；|
|-cnewer<参考文件或目录>|查找其更改时间较指定文件或目录的更改时间更接近现在的文件或目录；|
|-ctime<24小时数>|查找在指定时间之时被更改的文件或目录，单位以24小时计算；|
|-daystart|从本日开始计算时间；|
|-depth|从指定目录下最深层的子目录开始查找；|
|-empty|寻找文件大小为0 Byte的文件，或目录下没有任何子目录或文件的空目录；|
|-exec<执行指令>|假设find指令的回传值为True，就执行该指令；|
|-false|将find指令的回传值皆设为False；|
|-fls<列表文件>|此参数的效果和指定“-ls”参数类似，但会把结果保存为指定的列表文件；|
|-follow|排除符号连接；|
|-fprint<列表文件>|此参数的效果和指定“-print”参数类似，但会把结果保存成指定的列表文件；|
|-fprint0<列表文件>|此参数的效果和指定“-print0”参数类似，但会把结果保存成指定的列表文件；|
|-fprintf<列表文件><输出格式>|此参数的效果和指定“-printf”参数类似，但会把结果保存成指定的列表文件；|
|-fstype<文件系统类型>|只寻找该文件系统类型下的文件或目录；|
|-gid<群组识别码>|查找符合指定之群组识别码的文件或目录；|
|-group<群组名称>|查找符合指定之群组名称的文件或目录；|
|-help或--help|在线帮助；|
|-ilname<范本样式>|此参数的效果和指定“-lname”参数类似，但忽略字符大小写的差别；|
|-iname<范本样式>|此参数的效果和指定“-name”参数类似，但忽略字符大小写的差别；|
|-inum<inode编号>|查找符合指定的inode编号的文件或目录；|
|-ipath<范本样式>|此参数的效果和指定“-path”参数类似，但忽略字符大小写的差别；|
|-iregex<范本样式>|此参数的效果和指定“-regexe”参数类似，但忽略字符大小写的差别；|
|-links<连接数目>|查找符合指定的硬连接数目的文件或目录；|
|-lname<范本样式>|指定字符串作为寻找符号连接的范本样式；|
|-ls|假设find指令的回传值为Ture，就将文件或目录名称列出到标准输出；|
|-maxdepth<目录层级>|设置最大目录层级；|
|-mindepth<目录层级>|设置最小目录层级；|
|-mmin<分钟>|查找在指定时间曾被更改过的文件或目录，单位以分钟计算；|
|-mount|此参数的效果和指定“-xdev”相同；|
|-mtime<24小时数>|查找在指定时间曾被更改过的文件或目录，单位以24小时计算；|
|-name<范本样式>|指定字符串作为寻找文件或目录的范本样式；|
|-newer<参考文件或目录>|查找其更改时间较指定文件或目录的更改时间更接近现在的文件或目录；|
|-nogroup|找出不属于本地主机群组识别码的文件或目录；|
|-noleaf|不去考虑目录至少需拥有两个硬连接存在；|
|-nouser|找出不属于本地主机用户识别码的文件或目录；|
|-ok<执行指令>|此参数的效果和指定“-exec”类似，但在执行指令之前会先询问用户，若回答“y”或“Y”，则放弃执行命令；|
|-path<范本样式>|指定字符串作为寻找目录的范本样式；|
|-perm<权限数值>|查找符合指定的权限数值的文件或目录；|
|-print|假设find指令的回传值为Ture，就将文件或目录名称列出到标准输出。格式为每列一个名称，每个名称前皆有“./”字符串；|
|-print0|假设find指令的回传值为Ture，就将文件或目录名称列出到标准输出。格式为全部的名称皆在同一行；|
|-printf<输出格式>|假设find指令的回传值为Ture，就将文件或目录名称列出到标准输出。格式可以自行指定；|
|-prune|不寻找字符串作为寻找文件或目录的范本样式;|
|-regex<范本样式>|指定字符串作为寻找文件或目录的范本样式；|
|-size<文件大小>|查找符合指定的文件大小的文件；|
|-true|将find指令的回传值皆设为True；|
|-type<文件类型>|只寻找符合指定的文件类型的文件；|
|-uid<用户识别码>|查找符合指定的用户识别码的文件或目录；|
|-used<日数>|查找文件或目录被更改之后在指定时间曾被存取过的文件或目录，单位以日计算；|
|-user<拥有者名称>|查找符和指定的拥有者名称的文件或目录；|
|-version或——version|显示版本信息；|
|-xdev|将范围局限在先行的文件系统中；|
|-xtype<文件类型>|此参数的效果和指定“-type”参数类似，差别在于它针对符号连接检查。|

类型参数列表：

|参数|意义|
|---|---|
|f| 普通文件|
|l| 符号连接|
|d| 目录|
|c| 字符设备|
|b| 块设备|
|s| 套接字|
|p| Fifo|

你可以使用 ( ) 将运算式分隔，并使用下列运算。
```
exp1 -and exp2
! expr
-not expr
exp1 -or/-o exp2
exp1, exp2
```
例子：

在/home目录下查找以.txt结尾的文件名：`find /home -name "*.txt"`

查找上周新增的图片：`find ~ \( -iname '*jpeg' -o -iname '*jpg' \) -type f -mtime -7`

借助-exec选项与其他命令结合使用；

删除 mac 下自动生成的文件：`find ./ -name '__MACOSX' -depth -exec rm -rf {} \;`

查找 /var/log 目录中更改时间在 7 日以前的普通文件，并在删除之前询问它们：`find /var/log -type f -mtime +7 -ok rm {} \;`

## slocate/locate + updatedb
在manjaro中并没有自带locate这个命令，需要自行安装`sudo pacman -Sy mlocate`,初次使用需要`updatedb`建立初始库

`locate`命令用于查找符合条件的文档，他会去保存文档和目录名称的数据库内，查找合乎范本样式条件的文档或目录。一般情况我们只需要输入 locate your_file_name 即可查找指定文件。

与find 不同，find 是去硬盘找，locate 只在 /var/lib/slocate 资料库中找。
locate 的速度比 find 快，它并不是真的查找，而是查数据库，一般文件数据库在 /var/lib/slocate/slocate.db 中，所以 locate 的查找并不是实时的，而是以数据库的更新为准，一般是系统自己维护，也可以手工升级数据库 ，

命令为：`updatedb`,可能需要权限，以及更新需要较长的时间

语法`locate [-d ][--help][--version][范本样式...]`

后面才了解到manjaro有`slocate`这个命令，功能和`locate`差不多，且共用库，

|参数|意义|
|---|---|
|-b, --basename  | 仅匹配路径名的基本名称|
|-c, --count     | 只输出找到的数量|
|-d, --database DBPATH | 使用DBPATH指定的数据库，而不是默认数据库 /var/lib/mlocate/mlocate.db|
|-e, --existing  | 仅打印当前现有文件的条目|
|-1 | 如果 是 1．则启动安全模式。在安全模式下，使用者不会看到权限无法看到 的档案。这会始速度减慢，因为 locate 必须至实际的档案系统中取得档案的  权限资料。|
|-0, --null            | 在输出上带有NUL的单独条目|
|-S, --statistics      | 不搜索条目，打印有关每个数据库的统计信息|
|-q                    | 安静模式，不会显示任何错误讯息。|
|-P, --nofollow, -H    | 检查文件存在时不要遵循尾随的符号链接|
|-l, --limit, -n LIMIT | 将输出（或计数）限制为LIMIT个条目|
|-n                    | 至多显示 n个输出。|
|-m, --mmap            | 被忽略，为了向后兼容|
|-r, --regexp REGEXP   | 使用基本正则表达式|
|    --regex           | 使用扩展正则表达式|
|-q, --quiet           | 安静模式，不会显示任何错误讯息|
|-s, --stdio           | 被忽略，为了向后兼容|
|-o                    | 指定资料库存的名称。|
|-h, --help            | 显示帮助|
|-i, --ignore-case     | 忽略大小写|
|-V, --version         | 显示版本信息|

不同的locate有对应的updatedb

>updatedb - update a database for mlocate
部分参数

|参数|意义|
|---|---|
|-U、 --database-root PATH|仅存储扫描以生成的数据库路径为根的文件系统子树的结果。默认情况下，会扫描整个文件系统。|
|-o、 --output FILE|将数据库写入文件，而不是使用默认数据库。|

## touch、mkdir
`touch`命令用于修改文件或者目录的时间属性，包括存取时间和更改时间。若文件不存在，系统会建立一个新的文件。

|参数|意义|
|---|---|
|-a |改变档案的读取时间记录。
|-m |改变档案的修改时间记录。
|-c |假如目的档案不存在，不会建立新的档案。与 --no-create 的效果一样。|
|-f |不使用，是为了与其他 unix 系统的相容性而保留。|
|-r |使用参考档的时间记录，与 --file 的效果一样。|
|-d |设定时间与日期，可以使用各种不同的格式。|
|-t |设定档案的时间记录，格式与 date 指令相同。|
|--no-create |不会建立新档案。|
|--help		 |列出指令格式。|
|--version 	|	列出版本讯息。|


`mkdir`:英文全拼,make directory,命令用于创建目录

|参数|意义|
|---|---|
|-m, --mode=MODE 	|创建目录并且设定权限|
|-p, --parents  	|创建多级目录时确保没一级目录都会创建 与-m参数使用时，作用在最后一级目录|
|-v, --verbose 		|为每个创建的目录打印一条消息|
|--help 			|显示帮助之后退出|


## rm 、rmdir
`rm`:（英文全拼:remove）命令用于删除一个文件或者目录。

|参数|意义|
|---|---|
|-d|直接把欲删除的目录的硬连接数据删除成0，删除该目录；|
|-f|强制删除文件或目录；|
|-i|删除已有文件或目录之前先询问用户；|
|-r或-R|递归处理，将指定目录下的所有文件与子目录一并处理；|
|--preserve-root|不对根目录进行递归操作；|
|-v|显示指令的详细执行过程。|

文件一旦通过`rm`命令删除，则无法恢复，所以必须格外小心地使用该命令。

`rmdir`:（英文全拼:remove directory）命令删除空的目录。

语法: `rmdir [-p] dirName`

dirName：要删除的空目录列表。当删除多个空目录时，目录名之间使用空格隔开。

|参数|意义|
|-p 或 --parents|删除指定目录后，若该目录的上层目录已变成空目录，则将其一并删除；|
|--ignore-fail-on-non-empty|此选项使rmdir命令忽略由于删除非空目录时导致的错误信息；|
|-v或-verboes|显示命令的详细执行过程；|
|--help|显示命令的帮助信息；|
|--version|显示命令的版本信息。|

`rmdir -p www/Test`：在工作目录下的 www 目录中，删除名为 Test 的子目录。若 Test 删除后，www 目录成为空目录，则 www 亦予删除。


## pwd
`pwd`：（英文全拼：print work directory） 命令用于显示工作目录。

执行 pwd 指令可立刻得知您目前所在的工作目录的绝对路径名称。

|参数|意义|
|---|---|
|-L, --logical |打印环境变量"$PWD"的值，可能为符号链接。|
|-P, --physical |（默认值）打印当前工作目录的物理位置。|
|--help |显示帮助信息并退出。|
|--version |显示版本信息并退出。|

## ls
`ls`（英文全拼：list files）命令用于显示指定工作目录下之内容（列出目前工作目录所含之文件及子目录)。

语法:
```
ls [选项] [文件名...]
   [-1abcdfgiklmnopqrstuxABCDFGLNQRSUX] [-w cols] [-T cols] [-I pattern] [--full-time]
   [--format={long,verbose,commas,across,vertical,single-col‐umn}]
   [--sort={none,time,size,extension}] [--time={atime,access,use,ctime,status}]
   [--color[={none,auto,always}]] [--help] [--version] [--]
```

参数及意义
```
-C     # 多列输出，纵向排序。
-F     # 每个目录名加 "/" 后缀，每个 FIFO 名加 "|" 后缀， 每个可运行名加“ * ”后缀。
-R     # 递归列出遇到的子目录。
-a     # 列出所有文件，包括以 "." 开头的隐含文件。
-c     # 使用“状态改变时间”代替“文件修改时间”为依据来排序（使用“-t”选项时）或列出（使用“-l”选项时）。
-d     # 将目录名像其它文件一样列出，而不是列出它们的内容。
-i     # 输出文件前先输出文件系列号（即 i 节点号: i-node number）。 -l  列出（以单列格式）文件模式
       # （file mode），文件的链接数，所有者名，组名，文件大小（以字节为单位），时间信息，及文件名。
       # 缺省时，时间信息显示最近修改时间；可以以选项“-c”和“-u”选择显示其它两种时间信息。对于设备文件，
       # 原先显示文件大小的区域通常显示的是主要和次要的信号（majorand minor device numbers）。
-q     # 将文件名中的非打印字符输出为问号。（对于到终端的输出这是缺省的。）
-r     # 逆序排列。
-t     # 按时间信息排序。
-u     # 使用最近访问时间代替最近修改时间为依据来排序（使用“-t”选项时）或列出（使用“-l”选项时）。
-1     # 单列输出。
-1, --format=single-column  # 一行输出一个文件（单列输出）。如标准输出不是到终端，此选项就是缺省选项。
-a, --all # 列出目录中所有文件，包括以“.”开头的文件。
-b, --escape # 把文件名中不可输出的字符用反斜杠加字符编号(就像在 C 语言里一样)的形式列出。
-c, --time=ctime, --time=status
      # 按文件状态改变时间（i节点中的ctime）排序并输出目录内
      # 容。如采用长格式输出（选项“-l”），使用文件的状态改
      # 变时间取代文件修改时间。【译注：所谓文件状态改变（i节
      # 点中以ctime标志），既包括文件被修改，又包括文件属性（ 如所有者、组、链接数等等）的变化】
-d, --directory
      # 将目录名像其它文件一样列出，而不是列出它们的内容。
-f    # 不排序目录内容；按它们在磁盘上存储的顺序列出。同时启 动“ -a ”选项，如果在“ -f ”之前存在“ -l”、
      # “ - -color ”或“ -s ”，则禁止它们。
-g    # 忽略，为兼容UNIX用。
-i, --inode
      # 在每个文件左边打印  i  节点号（也叫文件序列号和索引号:  file  serial  number and index num‐
      # ber）。i节点号在每个特定的文件系统中是唯一的。
-k, --kilobytes
      # 如列出文件大小，则以千字节KB为单位。
-l, --format=long, --format=verbose
      # 输出的信息从左到右依次包括文件名、文件类型、权限、硬链接数、所有者名、组名、大小（byte）
      # 、及时间信息（如未指明是其它时间即指修改时间）。对于6个月以上的文件或超出未来
      # 1小时的文件，时间信息中的时分将被年代取代。
      # 每个目录列出前，有一行“总块数”显示目录下全部文件所占的磁盘空间。块默认是1024字节；
      # 如果设置了 POSIXLY_CORRECT 的环境变量，除非用“-k”选项，则默认块大小是 512 字节。
      # 每一个硬链接都计入总块数（因此可能重复计数），这无 疑是个缺点。

# 列出的权限类似于以符号表示（文件）模式的规范。但是 ls
      # 在每套权限的第三个字符中结合了多位（ multiple bits ） 的信息，如下： s 如果设置了  setuid
      # 位或 setgid   位，而且也设置了相应的可执行位。 S 如果设置了 setuid 位或 setgid
      # 位，但是没有设置相应的可执行位。 t 如果设置了  sticky  位，而且也设置了相应的可执行位。  T
      # 如果设置了 sticky 位，但是没有设置相应的可执行位。              x
      # 如果仅仅设置了可执行位而非以上四种情况。 - 其它情况（即可执行位未设置）。
-m, --format=commas
      # 水平列出文件，每行尽可能多，相互用逗号和一个空格分隔。
-n, --numeric-uid-gid
      # 列出数字化的 UID 和 GID 而不是用户名和组名。
-o    #  以长格式列出目录内容，但是不显示组信息。等于使用“         --format=long          --no-group
      # ”选项。提供此选项是为了与其它版本的 ls 兼容。
-p    #  在每个文件名后附上一个字符以说明该文件的类型。类似“ -F ”选项但是不 标示可执行文件。
-q, --hide-control-chars
      # 用问号代替文件名中非打印的字符。这是缺省选项。
-r, --reverse
      # 逆序排列目录内容。
-s, --size
      # 在每个文件名左侧输出该文件的大小，以    1024   字节的块为单位。如果设置了   POSIXLY_CORRECT
      # 的环境变量，除非用“ -k ”选项，块大小是 512 字节。
-t, --sort=time
      # 按文件最近修改时间（ i 节点中的 mtime ）而不是按文件名字典序排序，新文件 靠前。
-u, --time=atime, --time=access, --time=use
      # 类似选项“    -t    ”，但是用文件最近访问时间（    i     节点中的     atime     ）取代文件修
      # 改时间。如果使用长格式列出，打印的时间是最近访问时间。
-w, --width cols
       # 假定屏幕宽度是      cols      （      cols     以实际数字取代）列。如未用此选项，缺省值是这
       # 样获得的：如可能先尝试取自终端驱动，否则尝试取自环境变量          COLUMNS          （如果设
       # 置了的话），都不行则取 80 。

-x, --format=across, --format=horizontal
       # 多列输出，横向排序。

-A, --almost-all
       # 显示除 "." 和 ".." 外的所有文件。

-B, --ignore-backups
       # 不输出以“ ~ ”结尾的备份文件，除非已经在命令行中给出。

-C, --format=vertical
       # 多列输出，纵向排序。当标准输出是终端时这是缺省项。使用命令名 dir 和 d 时， 则总是缺省的。

-D, --dired
       # 当采用长格式（“-l”选项）输出时，在主要输出后，额外打印一行：  //DIRED//  BEG1 END1 BEG2
       # END2 ...

# BEGn 和 ENDn 是无符号整数，记录每个文件名的起始、结束位置在输出中的位置（
#        字节偏移量）。这使得          Emacs          易于找到文件名，即使文件名包含空格或换行等非正
#        常字符也无需特异的搜索。
#
# 如果目录是递归列出的（“ -R ”选项），每个子目录后列出类似一行：
       # //SUBDIRED//  BEG1 END1 ...  【译注：我测试了 TurboLinux4.0 和 RedHat6.1 ，发现它们都是在 “
       # //DIRED//     BEG1...     ”之后列出“     //SUBDIRED//     BEG1     ...      ”，也即只有一个
       # 而不是在每个子目录后都有。而且“ //SUBDIRED// BEG1 ... ”列出的是各个子目 录名的偏移。】

-F, --classify, --file-type
       # 在每个文件名后附上一个字符以说明该文件的类型。“  * ”表示普通的可执行文件； “ / ”表示目录；“
       # @ ”表示符号链接；“ | ”表示FIFOs；“ = ”表示套接字 (sockets) ；什么也没有则表示普通文件。

-G, --no-group
       # 以长格式列目录时不显示组信息。

-I, --ignorepattern
       # 除非在命令行中给定，不要列出匹配shell文件名匹配式（pattern ，不是指一般
       # 表达式）的文件。在shell中，文件名以"."起始的不与在文件名匹配式(pattern)
       # 开头的通配符匹配。

-L, --dereference
       # 列出符号链接指向的文件的信息，而不是符号链接本身。

-N, --literal
       # 不要用引号引起文件名。

-Q, --quote-name
       # 用双引号引起文件名，非打印字符以 C 语言的方法表示。

-R, --recursive
       # 递归列出全部目录的内容。

-S, --sort=size
       # 按文件大小而不是字典序排序目录内容，大文件靠前。

-T, --tabsize cols
       # 假定每个制表符宽度是 cols 。缺省为 8。为求效率， ls 可能在输出中使用制表符。  若 cols 为
       0，则不使用制表符。

-U, --sort=none
       # 不排序目录内容；按它们在磁盘上存储的顺序列出。（选项“-U”和“-f”的不
       # 同是前者不启动或禁止相关的选项。）这在列很大的目录时特别有用，因为不加排序
       # 能显著地加快速度。

-X, --sort=extension
       # 按文件扩展名（由最后的 "." 之后的字符组成）的字典序排序。没有扩展名的先列 出。

--color[=when]
       # 指定是否使用颜色区别文件类别。环境变量  LS_COLORS  指定使用的颜色。如何设置 这个变量见 dir‐
       # colors(1) 。 when 可以被省略，或是以下几项之一：
none # 不使用颜色，这是缺省项。
       # auto 仅当标准输出是终端时使用。 always 总是使用颜色。指定 --color 而且省略 when  时就等同于
       # --color=always 。

--full-time
       # 列出完整的时间，而不是使用标准的缩写。格式如同          date(1)          的缺省格式；此格式
       # 是不能改变的，但是你可以用 cut(1) 取出其中的日期字串并将结果送至命令 “ date -d ”。

# 输出的时间包括秒是非常有用的。（ Unix 文件系统储存文件的时间信息精确到秒，
       # 因此这个选项已经给出了系统所知的全部信息。）例如，当你有一个         Makefile          文件
       # 不能恰当地生成文件时，这个选项会提供帮助。
```
