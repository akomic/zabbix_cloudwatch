#Zabbix CloudWatch and ELB

Zabbix template for CloudWatch and AWS EC2 Elastic Load Balancer monitoring.

CloudWatch part comes with some default items including AutoScaling and RDS

It's low-level discovering AWS EC2 ELB instances and assigning items/triggers to each.


## Install
This is installed on the host you are running the zabbix agent on and that you would like to acccess AWS, usually it's agent running on the machine as zabbix server.

```
$ git clone https://github.com/akomic/zabbix_cloudwatch
$ cd zabbix_cloudwatch
$ cp zabbix-cloudwatch.py /etc/zabbix/externalscripts/zabbix-cloudwatch.py && chmod 755 /etc/zabbix/externalscripts/zabbix-cloudwatch.py
$ cp cloudwatch.conf /etc/zabbix/zabbix_agentd.conf.d

```
Make sure this line is present in zabbix agent configuration file

```
Include=/etc/zabbix/zabbix_agentd.conf.d/
```

## AWS Configuration

With IAM create user and attach AmazonEC2ReadOnlyAccess and CloudWatchReadOnlyAccess.
Memorize user key and secret, you'll need it later.

## Script configuration

Edit zabbix-cloudwatch.py and add previously acquired key/secret to the aws_key and aws_secret variables.

## Zabbix Configuration

* Import template into zabbix in Template section of web gui
* Add the template to the host
* Add {$MYACCOUNT} macro to the host with value "zabbix"

This code is built on
https://github.com/lorieri/zabbix/blob/master/chef/cookbooks/zabbix-aws/templates/default/cloudwatch/zabbix-cloudwatch.py.erb
