# Install MyRocks


Reference: [MyRocks Home Page](http://myrocks.io/docs/getting-started/)



## Getting Started

### Prerequisites

```bash
$ sudo apt-get update
$ sudo apt-get install g++ cmake libbz2-dev libaio-dev bison \
  zlib1g-dev libsnappy-dev libgflags-dev libreadline6-dev libncurses5-dev \
  libssl-dev liblz4-dev libboost-dev gdb git
```

### Set up Git Repository

```bash
$ git clone https://github.com/facebook/mysql-5.6.git
$ cd mysql-5.6
$ git submodule init
$ git submodule update
$ cmake . -DCMAKE_BUILD_TYPE=RelWithDebInfo -DWITH_SSL=system \
  -DWITH_ZLIB=bundled -DMYSQL_MAINTAINER_MODE=0 -DENABLED_LOCAL_INFILE=1 \
  -DENABLE_DTRACE=0 -DCMAKE_CXX_FLAGS="-march=native"
$ make -j8
$ sudo make install
```

- 만일 문제가 생긴다면 [아래](https://github.com/Csoyee/documents/blob/master/KVStore/install_myrocks.md#error-handling)에 정리된 error handling 부분을 확인하자.



### MySQL Path
```bash
$ sudo vim /etc/profile
```
- 맨 아랫줄에 아래 내용 추가

```bash
export PATH=$PATH:/usr/local/mysql/bin:/usr/local/mysql/scripts
```


### Initialize and Start

- 우선 내가 사용한 my.cnf 는 다음과 같다.
```bash
[mysqld]
user=mysql
rocksdb
default-storage-engine=rocksdb
skip-innodb
default-tmp-storage-engine=MyISAM
datadir=/home/csoyee/RocksDB/datadir/   # 본인에 맞게 바꾸기

log-bin
binlog-format=ROW
```

**Initialize :**

```bash
$ mysql_install_db --defaults-file=/path/to/my.cnf --basedir=/usr/local/mysql/ 
```

- 만일 LZ4F 에러가 난다면 버전 문제이기 때문에 버전 문제 해결하기 위해 [본 링크](https://github.com/hermanlee/mysql-5.6/commit/8fd1e1dc40ffca01ec5bd1143e1fc6e57810f847) 따라하고 mysql 다시 

**Start :**
```bash
$ mysqld_safe --defaults-file=my.cnf --basedir=/usr/lock/mysql
```

**Shutdown :**
```bash
$ mysqladmin -u root shutdown
```

### Error Handling

#### ZSTD Not found
- [해당 레포](https://github.com/facebook/zstd) 에서 ZSTD 라이브러리 설치

#### LZ4F Not found
- [해당 레포](https://github.com/lz4/lz4) 에서 LZ4 라이브러리 설치
