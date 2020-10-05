## **Shell_Note**

1 重复，统计

```shell
pip3 install tesserocr pillow

#去除重复行
sort file |uniq
#查找非重复行	
sort file |uniq -u
#查找重复行
sort file |uniq -d
统计
sort file | uniq -c

find -not -empty -type f -printf "%s\n" | sort -rn |uniq -d | xargs -I{} -n1 find -type f -size {}c -print0 | xargs -0 md5sum | sort | uniq -w32 --all-repeated=separate | cut -b 36- >result.txt

2. ubuntu sudo apt-get install xxx 报错
E: The package needs to be reinstalled, but I can't find an archive for it [duplicate]
A:sudo rm /var/lib/apt/lists/* -vf
  sudo apt-get update
The program 'java' can be found in the following packages:

```

2 Shell中的${}、##和%%使用范例:

```shell
假设定义了一个变量为：
file=/dir1/dir2/dir3/my.file.txt
可以用${ }分别替换得到不同的值：
${file#*/}：删掉第一个 / 及其左边的字符串：dir1/dir2/dir3/my.file.txt
${file##*/}：删掉最后一个 /  及其左边的字符串：my.file.txt
${file#*.}：删掉第一个 .  及其左边的字符串：file.txt
${file##*.}：删掉最后一个 .  及其左边的字符串：txt
${file%/*}：删掉最后一个  /  及其右边的字符串：/dir1/dir2/dir3
${file%%/*}：删掉第一个 /  及其右边的字符串：(空值)
${file%.*}：删掉最后一个  .  及其右边的字符串：/dir1/dir2/dir3/my.file
${file%%.*}：删掉第一个  .   及其右边的字符串：/dir1/dir2/dir3/my
记忆的方法为：
# 是 去掉左边（键盘上#在 $ 的左边）
%是去掉右边（键盘上% 在$ 的右边）
单一符号是最小匹配；两个符号是最大匹配
${file:0:5}：提取最左边的 5 个字节：/dir1
${file:5:5}：提取第 5 个字节右边的连续5个字节：/dir2
也可以对变量值里的字符串作替换：
${file/dir/path}：将第一个dir 替换为path：/path1/dir2/dir3/my.file.txt
${file//dir/path}：将全部dir 替换为 path：/path1/path2/path3/my.file.txt
```

3 打印一个文件从第 i 行开始到第 j 行结束的所有行

```shell
sed -n'2,5p' inputfile  # 打印第2行到第5行
line=`sed -n ''$i','$j'p' ${json_tmpfile_path}`
```

