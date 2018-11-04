# 2、准备阶段

## 1、安装、配置MySQL Embedded开发环境

创建一个MySQL嵌入式服务器的开发、运行环境，我们需要libmysqld函数库、MySQl头文件、运行时依赖的相关文件。

#### Ubuntu 14.04 /16.04/18.04、Debian8下执行以下命令安装：

首先更新软件源

```bash
sudo apt update
sudo apt upgrade -y
```

安装开发工具包

```bash
sudo apt install build-essential
```

安装libmysqld

```bash
sudo apt install libmysqld-dev
```

Ubuntu18.04默认安装的是5.7.23版、16.04（需要测试）、14.04默认安装 5.5.61版

Debian8默认安装的是5.5.60版

安装完成后会安装以下文件（以Ubuntu 16.04为例）：

```bash
/usr/lib/x86_64-linux-gnu/libmysqld.a
/usr/lib/x86_64-linux-gnu/libmysqlservices.a
/usr/share/doc/libmysqld-dev/NEWS.Debian.gz
/usr/share/doc/libmysqld-dev/changelog.Debian.gz
/usr/share/doc/libmysqld-dev/copyright
```

#### Debian9不支持原版MySQL Embedded，您可以用安装MariaDB的libmariadbd-dev来代替：

首先更新软件源

```bash
sudo apt update
sudo apt upgrade -y
```

安装开发工具包

```bash
sudo apt install build-essential
```

安装libmariadbd

```bash
sudo apt install libmariadbd-dev
```

#### Centos7：

首先更新软件源

```bash
yum update
```

安装开发工具包

```bash
yum groupinstall "Development Tools"
```

下载安装MySQL RPM软件源

```bash
wget https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm
rpm -ivh ./mysql80-community-release-el7-1.noarch.rpm
```

编辑文件，激活5.7.23版本的MySQL软件源

```bash
vim /etc/yum.repos.d/mysql-community.repo
```

安装libmysqld

```bash
yum install mysql-community-embedded-devel.x86_64
```

Centos7默认安装5.7.23版本

#### 编译安装：

FreeBSD以及其他系统需要编译安装，以下安装步骤以5.7.23为例：

## 2、启动你的第一个MySQL应用

这时候你应该准备好了MySQL Embedded开发环境了，我们启动一个简单的应用来测试一下我们的应用能否在开发环境中正常运行。

首先创建一个新的文件夹go\_for\_mysql，同时创建一个子目录data。创建并编辑文件main.cpp：

{% code-tabs %}
{% code-tabs-item title="main.cpp" %}
```cpp
#include <stdio.h>
#include <stdlib.h>
#include <stdarg.h>
#include "mysql.h"

MYSQL *mysql;
static char *server_options[] = \
       { "mysql_test", "--defaults-file=my.cnf", NULL };
int num_elements = (sizeof(server_options) / sizeof(char *)) - 1;

int main(void)
{
    mysql_library_init(num_elements, server_options, NULL);
    mysql = mysql_init(NULL);
    mysql_options(mysql, MYSQL_OPT_USE_EMBEDDED_CONNECTION, NULL);

    mysql_real_connect(mysql, NULL,NULL,NULL,NULL, 0,NULL,0);

    printf("Hola, MySQL Embedded is ready!\n");
    mysql_close(mysql);
    mysql_library_end();

    return 0;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

创建并编辑my.cnf：

{% code-tabs %}
{% code-tabs-item title="my.cnf" %}
```bash
[server]
sql_mode=TRADITIONAL
[embedded]
datadir=./data
```
{% endcode-tabs-item %}
{% endcode-tabs %}

编译、运行程序

```bash
g++ -g main.cpp -o go_for_mysql `mysql_config --include –libmysqld-libs` go_for_mysql
./go_for_mysql
```

一切顺利的话，输出应该是：

```bash
Ubuntu 18.04:
mysql_embedded: Unknown error 1146
Hola, MySQL Embedded is ready!

Ubuntu 16.04:
mysql_embedded: Unknown error 1146
Hola, MySQL Embedded is ready!

Ubuntu 14.04:
无法正常运行

Debian8:
无法正常运行
```

可以忽略MySQL给出的第一条输出 “mysql\_embedded: Unknown error 1146”

## 这一节，你学到了：

1. 如何安装、配置MySQL Embedded开发环境
2. 如何启动你的第一个MySQL Embedded应用

