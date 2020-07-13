provider "aws" {
region = "ap-south-1"
profile = "payal24"
}
resource "aws_vpc" "payalvpc1" {
cidr_block = "192.168.0.0/16"
instance_tenancy = "default"
tags = {
Name = "payalvpc1"
}
}
resource "aws_subnet" "payalvpc1_subnet-1a" {
vpc_id = "${aws_vpc.payalvpc1.id}"
cidr_block = "192.168.0.0/24"
availability_zone = "ap-south-1a"
map_public_ip_on_launch = true
}
resource "aws_subnet" "payalvpc1_subnet-1b" {
vpc_id = "${aws_vpc.payalvpc1.id}"
cidr_block = "192.168.1.0/24"
availability_zone = "ap-south-1b"
}
resource "aws_internet_gateway" "payalvpc1_internet_gateway" {
vpc_id = "${aws_vpc.payalvpc1.id}"
tags = {
Name = "payalvpc1_internet_gateway"
}
}
resource "aws_route_table" "payalvpc1_route_table" {
vpc_id = "${aws_vpc.payalvpc1.id}"
route {
cidr_block = "0.0.0.0/0"
gateway_id = "${aws_internet_gateway.payalvpc1_internet_gateway.id}"
}
tags = {
Name = "payalvpc1_route_table"
}
}
resource "aws_route_table_association" "a" {
subnet_id = aws_subnet.payalvpc1_subnet-1a.id
route_table_id = "${aws_route_table.payalvpc1_route_table.id}"
}
resource "aws_security_group" "payalweb" {
name = "payalweb"
description = "Allow ssh http and icmp"
vpc_id = "${aws_vpc.payalvpc1.id}"
ingress {
description = "http"
from_port = 80
to_port = 80
protocol = "tcp"
cidr_blocks = ["0.0.0.0/0"]
}
ingress {
description = "ssh"
from_port = 22
to_port = 22
protocol = "tcp"
cidr_blocks = ["0.0.0.0/0"]
}
ingress {
description = "ICMP-IPv4"
from_port = 0
to_port = 0
protocol = "-1"
cidr_blocks = ["0.0.0.0/0"]
}
egress {
from_port = 0
to_port = 0
protocol = "-1"
cidr_blocks = ["0.0.0.0/0"]
}
tags = {
Name = "payalweb"
}
}
resource "aws_security_group" "payalsql" {
name = "payalsql"
description = "Allow sql"
vpc_id = "${aws_vpc.payalvpc1.id}"
ingress {
description = "MYSQL"
security_groups=[ "${aws_security_group.payalweb.id}" ]
from_port = 3306
to_port = 3306
protocol = "tcp"
}
egress {
from_port = 0
to_port = 0
protocol = "-1"
cidr_blocks = ["0.0.0.0/0"]
}
tags = {
Name = "payalsql"
}
}
resource "aws_security_group" "payalbastion" {
name = "payalbastion"
description = "Allow ssh for bastion"
vpc_id = "${aws_vpc.payalvpc1.id}"
ingress {
description = "ssh"
from_port = 22
to_port = 22
protocol = "tcp"
cidr_blocks = ["0.0.0.0/0"]
}
egress {
from_port = 0
to_port = 0
protocol = "-1"
cidr_blocks = ["0.0.0.0/0"]
}
tags = {
Name = "payalbastion"
}
}
resource "aws_security_group" "payalsqlallow" {
name = "payalsqlallow"
description = "ssh allow to the payalsql"
vpc_id = "${aws_vpc.payalvpc1.id}"
ingress {
description = "ssh"
security_groups=[ "${aws_security_group.payalbastion.id}" ]
from_port = 22
to_port = 22
protocol = "tcp"
}
egress {
from_port = 0
to_port = 0
protocol = "-1"
cidr_blocks = ["0.0.0.0/0"]
}
tags = {
Name = "payalsqlallow"
}
}
resource "aws_instance" "payalwordpress" {
ami = "ami-03831ab5ff3dd2f03"
instance_type = "t2.micro"
key_name = "payal286"
availability_zone = "ap-south-1a"
subnet_id = "${aws_subnet.payalvpc1_subnet-1a.id}"
security_groups = [ "${aws_security_group.payalweb.id}" ]
user_data = <<-EOF
#! /bin/bash
sudo yum install dnf install php-mysqlnd php-fpm httpd tar curl php-json -y
systemctl start httpd
systemctl enable httpd
curl https://wordpress.org/latest.tar.gz --output wordpress.tar.gz
tar xf wordpress.tar.gz
cp -r wordpress /var/www/html
chown -R apache:apache /var/www/html/wordpress
chcon -t httpd_sys_rw_content_t /var/www/html/wordpress -R
EOF
tags = {
Name = "payalwordpress"
}
}
resource "aws_instance" "payalsqlsecure" {
ami = "ami-03831ab5ff3dd2f03"
instance_type = "t2.micro"
key_name = "payal286"
availability_zone = "ap-south-1b"
subnet_id = "${aws_subnet.payalvpc1_subnet-1b.id}"
security_groups = [ "${aws_security_group.payalsql.id}" ,
"${aws_security_group.payalsqlallow.id}"]
user_data = <<-EOF
#! /bin/bash
sudo yum install @payalsql -y
systemctl start payalsqld
systemctl enable payalsqld
EOF
tags = {
Name = "payalsqlsecure"
}
}
resource "aws_instance" "payalbastion" {
ami = "ami-03831ab5ff3dd2f03"
instance_type = "t2.micro"
key_name = "payal286"
availability_zone = "ap-south-1a"
subnet_id = "${aws_subnet.payalvpc1_subnet-1a.id}"
security_groups = [ "${aws_security_group.payalbastion.id}" ]
tags = {
Name = "payalbastion"
}
}
resource "aws_eip" "payalvpc1_eip" {
vpc = true
}
resource "aws_nat_gateway" "payalvpc1_nat_gateway" {
allocation_id = "${aws_eip.payalvpc1_eip.id}"
subnet_id = "${aws_subnet.payalvpc1_subnet-1b.id}"
tags = {
Name = "payalvpc1_nat_gateway"
}
}
resource "aws_route_table" "payalvpc1_route_table2" {
vpc_id = "${aws_vpc.payalvpc1.id}"
route {
cidr_block = "0.0.0.0/0"
nat_gateway_id = "${aws_nat_gateway.payalvpc1_nat_gateway.id}"
}
}
