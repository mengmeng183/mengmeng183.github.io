<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    基本shell命令使用
</h1>

这里只是列举一些常用的文件操作命令。

## cd 跳转切换目录

```
格式：cd dirname 比如在打开用户主目录盘下的 myidoc 文件夹
cd  ~/myidoc
跳转到当前目录的上一级
cd ../
```

## mkdir 新建文件夹

```
mkdir myidoc
```
mkdir -p：

创建一条完整的路径，如mkdir -p d1/d2/d3/d4，

当路径中的某个目录已经存在时，跳过该目录继续创建下一级目录。

mkdir -m：

在创建目录的同时设定权限（而不是采用umask默认值）。

如：mkdir -p -m 664 d1/d2/d3/d4。创建目录的同时设定权限为664。

## touch 创建文件

```
touch a.text
可以同时创建多个文件，也可以创建隐藏文件
touch a.tet b.html .gitignore
```

## ls 显示目录

```
ls
显示所有文件，包括隐藏文件
ls -a
显示文件详情
ls -l
```

## pwd 打印用户当前位置

```
pwd
```

## cat 显示文件内容

```
cat a.html
```

## rm 删除文件或文件夹

```
rm a.txt
rm -r myidoc
```

## cp 拷贝

```
# 将文档 file1 复制成 file2
cp file1 file2
# 将文档 file1 复制到目录 dir1 下，文件名仍为 file1.
cp file1 dir1
# 将目录 /tmp 下的文档 file1复制到现行目录下，文件名仍为 file1.
cp /tmp/file1 .
# 将目录 /tmp 下的文档 file1现行目录下，档名
为file2
cp /tmp/file1 file2
```

## mv 移动或重命名文件

```
# 将文档 file1，更改档名为 file2.
mv file1 file2
# 将文档 file1，移到目录 dir1 下，档名仍为 file1.
mv file1 dir1
```
