# AWS Infrastruktur Setup

Hier wird die AWS Infrastruktur dokumentiert. 

---

## 1. Netzwerk

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

---

## 2. Hosts

### Security Groups

| ID  | Name      | Typ                          | Port        | Protocol | Quelle      |
| --- | --------- | ---------------------------- | ----------- | -------- | ----------- |
|     | SG-Server | RDP                          | 3389        | TCP      | 0.0.0.0     |
|     | SG-Server | LDAP                         | 389         | TCP/UDP  | 10.0.1.0/24 |
|     | SG-Server | LDAPS                        | 636         | TCP      | 10.0.1.0/24 |
|     | SG-Server | Kerberos                     | 88          | TCP/UDP  | 10.0.1.0/24 |
|     | SG-Server | SMB                          | 445         | TCP      | 10.0.1.0/24 |
|     | SG-Server | DNS                          | 53          | TCP/UDP  | 10.0.1.0/24 |
|     | SG-Server | ICMP                         | -           | ICMP     | 0.0.0.0     |
|     | SG-Server | Global Catalog               | 3268        | TCP      | 10.0.1.0/24 |
|     | SG-Server | Global Catalog SSL           | 3269        | TCP      | 10.0.1.0/24 |
|     | SG-Server | Kerberos Password Change/Set | 464         | TCP/UDP  | 10.0.1.0/24 |
|     |           |                              |             |          |             |
|     | SG-Client | RDP                          | 3389        | TCP      | 0.0.0.0     |
|     | SG-Client | Kerberos                     | 88          | TCP/UDP  | 10.0.1.0/24 |
|     | SG-Client | NetBIOS Session Service      | 139         | TCP      | 10.0.1.0/24 |
|     | SG-Client | LDAP                         | 389         | TCP      | 10.0.1.0/24 |
|     | SG-Client | DNS                          | 53          | TCP/UDP  | 10.0.1.0/24 |
|     | SG-Client | SMB                          | 445         | TCP      | 10.0.1.0/24 |
|     | SG-Client | RPC                          | 49152-65535 | TCP      | 10.0.1.0/24 |
|     | SG-Client | ICMP                         | -           | ICMP     | 10.0.1.0/24 |

### Hostnames

| Hostname | Betriebssystem | Security Group | Security Group ID |
| -------- | -------------- | -------------- | ----------------- |
| dc01     | Windows Server | SG-Server      |                   |
| client   | Windows 10     | SG-Client      |                   |
|          |                |                |                   |

*Die Security Groups werden nach der [Planung](../01_Vorbereitung/planung.md#5-aws-sicherheitsgruppen) erstellt.*

