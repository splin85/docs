# ubuntu16开发环境
## 安装ubtuntu16
## 更新ubuntu源
1. 备份原来的源  
    `cd /etc/apt; cp sources_list sources_list.bak`
    
2. 可以使用阿里源替换  
    ```
    # deb cdrom:[Ubuntu 16.04 LTS _Xenial Xerus_ - Release amd64 (20160420.1)]/ xenial main restricted
    deb-src http://archive.ubuntu.com/ubuntu xenial main restricted #Added by software-properties
    deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted multiverse universe #Added by software-properties
    deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted multiverse universe #Added by software-properties
    deb http://mirrors.aliyun.com/ubuntu/ xenial universe
    deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
    deb http://mirrors.aliyun.com/ubuntu/ xenial multiverse
    deb http://mirrors.aliyun.com/ubuntu/ xenial-updates multiverse
    deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse #Added by software-properties
    deb http://archive.canonical.com/ubuntu xenial partner
    deb-src http://archive.canonical.com/ubuntu xenial partner
    deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted multiverse universe #Added by software-properties
    deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
    deb http://mirrors.aliyun.com/ubuntu/ xenial-security multiverse
    ```
3. 更新sources源  
    `sudo apt-get update `   
    `sudo apt-get upgrade`
   
## 安装git
    sudo atp-get install git
    
## 安装并启动ssh服务
    sudo apt-get install openssh-server
  
## 安装ctags
    sudo apt-get install ctags
   
## 安装并配置vim
    sudo apt-get install vim
    cd ~ && git clone https://github.com/splin85/Vundle.vim.git ~/.vim/bundle/Vundle.vim
    获取splin的vimrc配置文件，拷贝到~/.vimrc (https://github.com/splin85/MyFirstGit.git)
    安装plugin插件 
    
    不能保存文件：E382: Cannot write, 'buftype' option is set
    : verbose set buftype
    : setlocal buftype=
   
## 路由IP配置
    1. 一网卡设置nat；
    2. 一网卡设置host-only，连接到virtualbox的虚拟网卡上；