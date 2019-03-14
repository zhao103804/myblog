
# CentOS 7硬盘分区及挂载操作步骤

## 第一步：查看未挂载的硬盘（名称为/dev/vdb）

```
fdisk -l
```

## 第二步：创建分区

```
fdisk /dev/vdb
输入m

Command (m for help):n
 命令操作
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition
   g   create a new empty GPT partition table
   G   create an IRIX (SGI) partition table
   l   list known partition types
   m   print this menu
   n   add a new partition
   o   create a new empty DOS partition table
   p   print the partition table
   q   quit without saving changes
   s   create a new empty Sun disklabel
   t   change a partition's system id
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit
   x   extra functionality (experts only)
   
输入p
Command action
e extended
p primary partition (1-4)

输入1
Partition number (1-4): 1

回车
First cylinder (1-2610, default 1): 
Using default value 1

回车
Last cylinder, +cylinders or +size{K,M,G} (1-2610, default 2610): 
Using default value 2610

输入w

Command (m for help): w
The partition table has been altered!

```

## 第三步：格式化分区

```
mkfs.ext4 /dev/vdb1
```

## 第四步：建立挂载目录

```
mkdir /root/data
```

## 第五步：挂载分区

```
mount /dev/vdb1 /root/data
```

## 第六步：设置开机自动挂载

进入到bin目录，增加一个配置文件：

```
vi /etc/fstab
```
在vi中输入i进入INERT模式，将光标移至文件结尾处并回车，将下面的内容复制/粘贴，然后按Esc键，输入:x保存并退出

```
/dev/vdb1              /root/data                   ext4    defaults        0 0
```

## 第七步：查看挂载分区

```
查看挂载分区命令
df -TH /root/data/
或者
df -h
```


## 第八步：重启确认是否挂载成功

```
reboot
```



