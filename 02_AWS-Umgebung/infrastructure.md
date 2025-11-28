# AWS Infrastruktur Setup

Hier wird die AWS Infrastruktur dokumentiert. 

### VPC

| ID                    | Name           | Anzahl Subnetze |
| --------------------- | -------------- | --------------- |
| vpc-03e24fbf85116cba0 | 159-kulici-vpc | 2               |

### Subnetze

| ID                       | Name             | Beschreibung                          |
| ------------------------ | ---------------- | ------------------------------------- |
| subnet-0ff8f6eeae43051a6 | 159-kulici-pub2  | öffentlich zugängliches Subnetz       |
| subnet-0abccdfa3659d4edf | 159-kulici-priv1 | nicht öffentlich zugängliches Subnetz |

### Überblick

<img width=90% height=50% alt="aws_vpc_creation.png" src="https://github.com/dariokulici/m159/raw/main/02_AWS-Umgebung/media/aws_vpc_creation.png">

Es gibt zwei Routing Tabellen. Die Void Tabelle ist nicht mit dem Internet Gateway verknüpft um das Subnetz Privat zu halten. Die Public Tabelle ist mit dem Internet Gateway verknüpft. 
<br>
Das AWS Managed AD wird im privaten Subnetz deployed während die restlichen Server und Clients (eigener DC & Windows Machine) im Public Subnet deployed werden. 