# M159 - Planung

---

## 1. Übersicht Umgebung

Diese Umgebung umfasst:

- **1x Windows Server (DC)** auf AWS EC2  
- **1x Windows Server (Client)** auf AWS EC2 (da AWS keine Windows Clients anbietet)  
- **1x Windows Server (Admin Center)** auf AWS EC2 zur Verwaltung der AWS Managed AD  
- **AWS Managed AD** mit Trust zur On-Premises(EC2) AD  
- **Entra Connect** zur Synchronisation mit Entra ID sowie Entra AD  
- **Lokale AD-Domain** (zu Beginn), später **öffentliche Domain als UPN**  

---
## 2. Ressourcen

| Feld                                                                                                                                                                                                                                                                                                                    | Wert                  |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| Active Directory Second-Level-Domäne                                                                                                                                                                                                                                                                                    | kulici.ch             |
| Geplante öffentliche Domain (UPN)                                                                                                                                                                                                                                                                                       | kulici.ch             |
| Azure Education Account Passwort                                                                                                                                                                                                                                                                                        | sdf3432lk4nsdfäö$3244 |

---


## 4. AWS VPC Setup

**Hinweis:**  
Alle Instanzen liegen in einem öffentlichen Subnetz und sind über RDP (Port 3389) von außen erreichbar.  
Alle weiteren Ports sind nur innerhalb des VPCs offen.  

| Komponente                      | VPC-ID | CIDR        | Name             |
| ------------------------------- | ------ | ----------- | ---------------- |
| VPC                             |        | 10.0.0.0/16 | 159-kulici-vpc   |
| M159-subnet-private1-us-east-1a |        | 10.0.1.0/24 | 159-kulici-priv1 |
| M159-subnet-public2-us-east-1a  |        | 10.0.2.0/24 | 159-kulici-pub2  |


---

## 5. AWS Sicherheitsgruppen

### Sicherheitsgruppe für Domain Controller

| Regeltyp                     | Port(e)                 | Quelle      |
| ---------------------------- | ----------------------- | ----------- |
| RDP                          | 3389  (TCP)             | 0.0.0.0     |
| LDAP                         | 389 (TCP/UDP)           | 10.0.1.0/24 |
| LDAPS                        | 636 (TCP)               | 10.0.1.0/24 |
| Kerberos                     | 88 (TCP/UDP)            | 10.0.1.0/24 |
| SMB                          | 445  (TCP)              | 10.0.1.0/24 |
| DNS                          | 53 (TCP/UDP)            | 10.0.1.0/24 |
| RPC                          | 135, 49152-65535  (TCP) | 10.0.1.0/24 |
| ICMP                         | Alle                    | 0.0.0.0     |
| Global Catalog               | 3268 (TCP)              | 10.0.1.0/24 |
| Global Catalog SSL           | 3269 (TCP)              | 10.0.1.0/24 |
| Kerberos Password Change/Set | 464 (TCP/UDP)           | 10.0.1.0/24 |

### Sicherheitsgruppe für Clients

| Regeltyp | Port(e)     | Beschreibung                             | Quelle      |
| -------- | ----------- | ---------------------------------------- | ----------- |
| RDP      | 3389        | Remote Desktop                           | 0.0.0.0     |
| TCP      | 88          | Kerberos Authentication                  | 10.0.1.0/24 |
| TCP      | 135         | RPC Endpoint Mapper                      | 10.0.1.0/24 |
| TCP      | 139         | NetBIOS Session Service                  | 10.0.1.0/24 |
| TCP      | 389         | LDAP                                     | 10.0.1.0/24 |
| UDP      | 53          | DNS                                      | 10.0.1.0/24 |
| TCP      | 445         | SMB/CIFS (Dateifreigabe, AD-Operationen) | 10.0.1.0/24 |
| TCP      | 49152-65535 | RPC Ephemeral Ports                      | 10.0.1.0/24 |
| ICMP     | Alle        | Ping etc.                                | 0.0.0.0     |

---

## 6. Active Directory Umgebung

### On-Premises Active Directory (AWS EC2)

| Feld                                  | Wert          |
| ------------------------------------- | ------------- |
| Active Directory Third-Level-Domäne-1 | ad.kulici.ch  |
| Domänenadministrator                  | Administrator |
| Kennwort Domänenadministrator         |               |
| Kennwort-Demote (Herunterstufen)      |               |

### Azure AD (Entra ID)

| Feld                         | Wert |
| ---------------------------- | ---- |
| Entra AD Tenant Name         |      |
| Azure Administrator (UPN)    |      |
| Kennwort Azure Administrator |      |
| Entra Connect Server (Name)  |      |

### AWS Managed AD

| Feld                                  | Wert                 |
| ------------------------------------- | -------------------- |
| Active Directory Third-Level-Domäne-2 | ad.kulici.ch         |
| Trust-Typ                             | Tree-Root Trust      |
| AWS Managed Admin User                | admin_kul            |
| AWS Managed Admin Passwort            | BzahcK1Vh!2my*KQcgn5 |
| IP-Adresse                            |                      |
| DNS-Server 1                          |                      |
| DNS-Server 2                          |                      |
| Trust Passwort                        |                      |
| Subnetz 1                             |                      |
| Subnetz 2                             |                      |

---

## 7. EC2-Instanzen

| Komponente                                       | FQDN                     | Elastic IP         | Private IP (CIDR) | Subnetz                         | DNS-Server 1 | DNS-Server 2 | Lokaler Admin | Kennwort |
| ------------------------------------------------ | ------------------------ | ------------------ | ----------------- | ------------------------------- | ------------ | ------------ | ------------- | -------- |
| IaaS/OnPrem AD DC                                | z.b. dc.ec2.tbz.m159     |                    | z.b.  10.0.129.10 | M159-subnet-private1-us-east-1a |              |              | Administrator |          |
| Windows Server (Client)                          | z.b. client.ec2.tbz.m159 | z.b. 44.198.134.36 | z.b.  10.0.129.20 | M159-subnet-public1-us-east-1a  |              |              | Administrator |          |
| Managed AWS EC2 DC                               |                          |                    |                   |                                 |              |              |               |          |
| Windows Server Admin Center (Managed AWS EC2 DC) |                          |                    |                   |                                 |              |              |               |          |

---

## 8. Abteilungen & Benutzer

Definieren Sie je einen Benutzer dieser 3 Abteilungen 

| Abteilung | Name der Abteilung | Benutzername | Vorname | Nachname | Kennwort | Bereiche |
| --------- | ------------------ | ------------ | ------- | -------- | -------- | -------- |
| 1         | Sekretariat        |              |         |          |          | intern   |
| 2         | Buchhaltung        |              |         |          |          | intern   |
| 3         | GL                 |              |         |          |          | intern   |
| 4         | Promoter           |              |         |          |          | extern   |

## 09. Python-App-Registration (Entra-ID)

| Name                    | Wert |
| ----------------------- | ---- |
| Directory (tenant) ID   |      |
| Application (client) ID |      |
| Client Secret ID        |      |



## 10. Hinweise

- Beginnen Sie mit der lokalen Domain-Umgebung und konfigurieren Sie **später den UPN-Suffix** mit der öffentlichen Domain.  
- Achten Sie auf **richtige Portfreigaben** in den AWS Sicherheitsgruppen, insbesondere für RDP, SMB und AD-Dienste.  
- Dokumentieren Sie alle IP-Adressen, Benutzernamen und Kennwörter konsequent in dieser Vorlage.
- Diese Vorlage wurde für das Schuljahr 2025/26 komplett neu erstellt. Falls Ihnen etwas fehlt, ist die Lehrperson dankbar, wenn Sie ihr dies mitteilen.