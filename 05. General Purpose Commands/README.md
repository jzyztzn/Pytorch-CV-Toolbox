# Linux General Purpose Commands

## 统计某文件夹下文件的个数
ls -l |grep "^-"|wc -l

## 统计所有文件中包括特定字符的数量
grep -rn '"category_id": 13,' | wc -l

## 显示显卡信息（不断刷新，-1 表示一秒刷新一次）
watch -n -1 nvidia-smi

## 显示显卡信息（不断上推刷新，1000 表示一秒刷新一次）
nvidia-smi -lms 1000

## 杀进程
ps -ef | grep 'python' | awk '{print $2}' | xargs kill -9

## 转换ipython to python code
jupyter nbconvert --to script xxx.ipynb

## Ubuntu 打开pycharm
cd && cd Downloads/pycharm-2020.1.2/bin/ && sh pycharm.sh

## 多线程压缩
tar cf - xxx/ | pigz -9 -p 64 > xxx.tar.gz

## 压缩
tar -zcvf /home/xahot.tar.gz /xahot
## 解压
tar -zxvf xxx.tar.gz

## 解压中文压缩包，防止乱码
unzip -O cp936 xxx.zip

## 将一个服务器的数据同步到另一个服务器 并指定不同步某个文件夹
rsync -av -e ssh --exclude='*.out' /path/to/source/ user@hostB:/path/to/test/

## 替换 xml文件中的所有类别名称或者其他文本
find -name '*.xml' | xargs perl -pi -e 's|<name>squamous-pm</name>|<name>normal</name>|g'

## 替换所有文件的后缀
rename 's/\.jpg.xml/.xml/' ./*

## 查找包含特定字符的文件，并移动到特定文件夹
grep -rnl "<ymax>2</ymax>" | xargs mv -f -t ../Atemp/

## 大批量复制文件到特定文件夹
find res/ -name "*.jpg" | xargs -i cp {} /path/to/save

## 安装显卡驱动
sudo bash NVIDIA-Linux-x86_64-510.47.03.run  --no-opengl-files --no-x-check

## 安装CUDNN
sudo cp cuda/include/cudnn.h /usr/local/cuda-11.3/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda-11.3/lib64
sudo chmod a+r /usr/local/cuda-11.3/include/cudnn.h 
sudo chmod a+r /usr/local/cuda-11.3/lib64/libcudnn*

export PATH=$PATH:/usr/local/cuda-11.3/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.3/lib64
export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/cuda-11.3/lib64

## 修改PIP源
pip install scrapy -i http://mirrors.aliyun.com/pypi/simple mxnet-cu102mkl  --trusted-host mirrors.aliyun.com

pip install  -i http://mirrors.aliyun.com/pypi/simple  mxnet-cu102==1.6.0 --trusted-host mirrors.aliyun.com

## 新建用户并指定路径
sudo useradd  -d  /home1/xxx -m -s  /bin/bash  xxx
sudo passwd xxx

### Case 1: 创建一个带有家目录并且可以登录 bash 的用户
$ sudo useradd -m -s /bin/bash tester1
### Case 2: 指定创建用户家目录的路径
$ sudo useradd -m -d /home/xxx tester2


## 禁用python警告
import warnings
warnings.filterwarnings("ignore")


## 删除git分支
https://chinese.freecodecamp.org/news/how-to-delete-a-git-branch-both-locally-and-remotely/

git branch -d master2
git push origin --delete master1
git fetch -p

## cuda历史版本下载
https://developer.nvidia.com/cuda-toolkit-archive


## 将本地代码仓库放在162上
touch README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin http://192.168.1.162:3001/username/xxx.git
git push -u origin master