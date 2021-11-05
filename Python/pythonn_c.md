算法题：
一个长字符串，去除重复字符串，且保持字典序最小


linux 题：
查找一个目录下的的某个类型的文件
find file_addr -name "*.type"

一个文件中的内容是有规律的，比如以时间等等，现在想要获取其中某个时间段内的 http 状态码为200的次数
按照时间段取内容并输出为新文本：
sed -n '/2021-04-05 02:27:25/,/2021-04-09 05:05:58/p' obsidian.log > ob.txt
统计：
grep -c count_word ob.txt 
通过管道连接起来即可:
sed -n '/2021-04-05 02:27:25/,/2021-04-09 05:05:58/p' obsidian.log | grep -c app