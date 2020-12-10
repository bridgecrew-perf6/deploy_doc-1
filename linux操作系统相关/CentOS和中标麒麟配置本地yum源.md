## CentOS6和中标麒麟6配置本地yum源

1. 上传镜像文件至服务器上

   ```sh 
       su -
       mkdir /root/iso1
       mount -o loop -t iso9660 CentOS-6.6-x86_64-bin-DVD1.iso /root/iso1
       mkdir /root/iso2
       mount -o loop -t iso9660 CentOS-6.6-x86_64-bin-DVD2.iso /root/iso2
       cp -r /root/iso1 /root/iso
       cp -r /root/iso2/Packages/*.rpm /root/iso/Packages/
       cat /root/iso[12]/Packages/TRANS.TBL |sort >/root/iso/Packages/TRANS.TBL
   ```

2. 配置本地yum源

```
    su -
    cd /etc/yum.repos.d/
    mkdir bak
    mv *.repo bak/
    vi centos.repo 
        [centos-source]
        name=CentOS $releasever - $basearch - Source
        baseurl=file:///root/iso
        enabled=1
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
    yum clean all
    yum list
```

## CentOS7和中标麒麟7配置本地yum源

1. 挂载光盘或者上传镜像至服务器上

   ```
   su -
   mkdir /root/iso
   mount -o loop -t iso9660 CentOS-7-x86_64-DVD-2003.iso /root/iso
   ```

   或者挂载光盘

   ```
   su -
   mkdir /root/iso
   mount /dev/cdrom /root/iso
   ```

2. 配置本地yum源

   ```
   su -
   cd /etc/yum.repos.d/
   mkdir bak
   mv *.repo bak/
   vi cd.repo 
       [cd-source]
       name=CentOS $releasever - $basearch - Source
       baseurl=file:///root/iso
       enabled=1
       gpgcheck=0
   yum clean all
   ```

## CentOS8配置本地yum源

1. 挂载光盘或者上传镜像至服务器上

   ```
   su -
   mkdir /root/iso
   mount -o loop -t iso9660 CentOS-7-x86_64-DVD-2003.iso /root/iso
   ```

   或者挂载光盘

   ```
   su -
   mkdir /root/iso
   mount /dev/cdrom /root/iso
   ```

2. 配置本地yum源

   ```
   su -
   cd /etc/yum.repos.d
   mkdir bak
   mv *.repo bak
   vi centos.repo
       [base]
       name=Base
       baseurl=file:///root/iso/BaseOS
       gpgcheck=0
       enabled=1
       [AppStream]
       name=AppStream
       gpgcheck=0
       enabled=1
       baseurl=file:///root/iso/AppStream
   dnf clean all
   dnf makecache
   ```