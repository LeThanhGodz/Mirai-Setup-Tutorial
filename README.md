
# MIRAI SETUP FULL TUTORIAL

#### Nếu các bạn đã cài Mirai trước đó rồi thì hãy dọn dẹp tàn dư từ nó trước nhé, bằng cách dùng lệnh này:

```bash
sudo rm -rf /usr/local/go /var/www/html/* /etc/xcompile /usr/lib64/libgmp.so.10
rpm -qa | grep mysql
# Xoá hết tất cả các phiên bản MySQL hiện trên màn hình
```

Đầu tiên, các bạn cần phải tải về các package cần thiết bằng cách gõ vào Terminal các lệnh sau:

```bash
yum update -y
yum install epel-release -y
yum groupinstall "Development Tools" -y
yum install gmp-devel -y
ln -s /usr/lib64/libgmp.so.3 /usr/lib64/libgmp.so.10
yum install screen wget bzip2 gcc nano gcc-c++ electric-fence sudo git libc6-dev httpd xinetd tftpd tftp-server mysql-client mysql-server gcc glibc-static -y
```

### Cách cài MySQL trên CentOS 7

```bash
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
yum -y install mysql-community-release-el7-5.noarch.rpm
yum -y install mysql-server
systemctl start mysqld
systemctl enable mysqld
```

Sau đó cài đặt ngôn ngữ Golang (Vì Golang 1.9 trong tài liệu hướng dẫn không dùng được driver MySQL của Golang nên mình cài Go 1.13 nhé):

```bash
rm -rf /usr/local/go 
wget https://dl.google.com/go/go1.13.linux-amd64.tar.gz
sha256sum go1.13.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.13.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
source ~/.bash_profile
rm -rf go1.13.linux-amd64.tar.gz
```

Tiếp theo chúng ta sẽ tải Cross Compiler nhé :>

```bash
wget https://www.uclibc.org/downloads/binaries/0.9.30.1/cross-compiler-i586.tar.bz2
wget https://www.uclibc.org/downloads/binaries/0.9.30.1/cross-compiler-m68k.tar.bz2
wget https://www.uclibc.org/downloads/binaries/0.9.30.1/cross-compiler-mips.tar.bz2
wget https://www.uclibc.org/downloads/binaries/0.9.30.1/cross-compiler-mipsel.tar.bz2
wget https://www.uclibc.org/downloads/binaries/0.9.30.1/cross-compiler-powerpc.tar.bz2
wget https://www.uclibc.org/downloads/binaries/0.9.30.1/cross-compiler-sh4.tar.bz2
wget https://www.uclibc.org/downloads/binaries/0.9.30.1/cross-compiler-sparc.tar.bz2
wget https://www.uclibc.org/downloads/binaries/0.9.30.1/cross-compiler-armv4l.tar.bz2
wget https://www.uclibc.org/downloads/binaries/0.9.30.1/cross-compiler-armv5l.tar.bz2
wget http://distro.ibiblio.org/slitaz/sources/packages/c/cross-compiler-armv6l.tar.bz2
wget https://landley.net/aboriginal/downloads/old/binaries/1.2.6/cross-compiler-armv7l.tar.bz2
```

Giải nén Cross Compiler:
```bash
tar -jxf cross-compiler-i586.tar.bz2
tar -jxf cross-compiler-m68k.tar.bz2
tar -jxf cross-compiler-mips.tar.bz2
tar -jxf cross-compiler-mipsel.tar.bz2
tar -jxf cross-compiler-powerpc.tar.bz2
tar -jxf cross-compiler-sh4.tar.bz2
tar -jxf cross-compiler-sparc.tar.bz2
tar -jxf cross-compiler-armv4l.tar.bz2
tar -jxf cross-compiler-armv5l.tar.bz2
tar -jxf cross-compiler-armv6l.tar.bz2
tar -jxf cross-compiler-armv7l.tar.bz2
```

Xoá hết tệp thừa cho đep:
```bash
rm -rf *.tar.bz2
```

Đổi tên cho dễ nhìn và bớt dài dòng nào:

```bash
mv cross-compiler-i586 i586
mv cross-compiler-m68k m68k
mv cross-compiler-mips mips
mv cross-compiler-mipsel mipsel
mv cross-compiler-powerpc powerpc
mv cross-compiler-sh4 sh4
mv cross-compiler-sparc sparc
mv cross-compiler-armv4l armv4l
mv cross-compiler-armv5l armv5l
mv cross-compiler-armv6l armv6l
mv cross-compiler-armv7l armv7l
```

Cài các thư viện cho Golang:
```bash
go get github.com/go-sql-driver/mysql
go get github.com/mattn/go-shellwords
```
