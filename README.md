# IP v4 中国城市地址库

整理 [IPIP.net](https://www.ipip.net) 和 [QQ IP 数据库纯真版](http://www.cz88.net/down/76250/) 为符合[中华人民共和国行政区划代码](http://www.mca.gov.cn/article/sj/tjbz/a/)的国家与地区、省或直辖市、地级市或省管县级市地址。

[![Latest Stable Version](https://poser.pugx.org/larryli/ipv4/v/stable)](https://packagist.org/packages/larryli/ipv4)
[![Total Downloads](https://poser.pugx.org/larryli/ipv4/downloads)](https://packagist.org/packages/larryli/ipv4)
[![Latest Unstable Version](https://poser.pugx.org/larryli/ipv4/v/unstable)](https://packagist.org/packages/larryli/ipv4)
[![License](https://poser.pugx.org/larryli/ipv4/license)](https://packagist.org/packages/larryli/ipv4)
[![Build Status](https://travis-ci.org/larryli/ipv4.svg?branch=master)](https://travis-ci.org/larryli/ipv4)

## 目标

在 IPIP.net 库的基础上去掉 IDC/ISP 数据补上纯真 IP 库的数据，然后生成下列四个库：

* ```mini```：**迷你库**用于快速识别中华人民共和国境内 IP（不含台澎金马、香港、澳门）；
* ```china```: **国内城市库**用于定位中华人民共和国第一级和第二级行政区划（含部分省管第三级行政区划），即俗称的城市定位（含台湾、香港、澳门，作为第一级行政区划）；
* ```world```: **国家库**用于定位国家与地区（含台湾、香港、澳门地区）；
* ```full```: **完整库**是国内城市库与国家地区库的合集（台湾、香港、澳门作为中华人民共和国第一级行政区划）；

## 通过 composer 安装

```shell
composer require larryli/ipv4
```

## 使用

```php
$monipdb = new \larryli\ipv4\MonipdbQuery(__DIR__ . '/17monipdb.dat');
if (!$monipdb->exists()) {
    $monipdb->init();
}
$qqwry = new \larryli\ipv4\QqwryQuery(__DIR__ . '/qqwry.dat');
if (!$qqwry->exists()) {
    $qqwry->init();
}
$your_query = new \larryli\ipv4\FullQuery(new YourDatabase());
if (!$your_query->exists()) {
    $your_query->setProviders([$monipdb, $qqwry]);
    $your_query->init();
}
$your_query->find(ip2long('127.0.0.1'));

class YourDatabase extends \larryli\ipv4\Database
{
    ...
}
```

可以选用 ```larryli/ipv4-medoo``` 的 ```\larryli\ipv4\medoo\Database```。

## 相关包

* 控制台命令 [larryli/ipv4-console](https://github.com/larryli/ipv4-console)
* Medoo 数据库支持 [larryli/ipv4-medoo](https://github.com/larryli/ipv4-medoo)
* Yii2 组件 [larryli/ipv4-yii2](https://github.com/larryli/ipv4-yii2)
* Yii2 示例 [larryli/ipv4-yii2-sample](https://github.com/larryli/ipv4-yii2-sample)
