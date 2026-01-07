# Wissen aneignen

In diesem Dokument werden wichtige Begriffe und Zusammenhänge erklärt, um das Verständnis zu verbessern. 

---

### Active Directory - Was ist das?

Active Directory ist enthält verschiedene Services, die auf Windows Server laufen und **Berechtigungen** und den **Zugang** zu **Ressourcen im Netzwerk** verwalten. Daten werden in Form von Objekten gespeichert. Diese Objekte sind einzelne Elemente wie Gruppen, Benutzer oder Applikationen. Die Kategorisierung der Objekte erfolgt über Attribute und Namen welche Informationen zum Benutzer bspw. SSH Keys oder Passwörter enthalten. 

<br>

### Domain Controller - ist das nicht das Gleiche?

Der Hauptservice von Active Directory ist die Verwaltung von Domänen. Grundsätzlich wird auf einem Windows Server Active Directory installiert. Das AD enthält die Daten und diese können via Domain Controller verwaltet werden. Bspw. um ein Passwort für einen Benutzer zurückzusetzen. Wenn sich ein Benutzer mit seinem Konto anmelden möchte sendet er eine Anfrage an den Domain Controller und dieser prüft die Authentizität des Benutzers. Wenn man von einem Domain Controller spricht ist ein Windows Server gemeint, auf dem die Active Directory Services installiert sind. 

<br>

### Mehrere Domain Controller - Wie geht denn das?

Es können mehrere Domain Controller verwendet werden um eine High Availability und Load Balancing sicherzustellen. Durch die Redundanz hat man auch eine bessere Fault Tolerance. Wenn ein DC bspw. wegen Hardware Problemen aussteigt können die anderen DCs übernehmen. Auf jedem DC wird eine lokale Kopie des Active Directory's gespeichert, die bei Änderungen synchronisiert wird. Gewisse Anfragen werden an den Primary Domain Controller Emulator (PDC) weitergeleitet. Beispielsweise eine Überprüfung einer Passwort Änderung. Der PDC-Emulator wird befragt ob das Passwort letztens geändert wurde und dieser würde dann gegebenfalls mit ja antworten und das aktuelle Passwort mitgeben. Zudem werden wichtige Aufgaben wie die Zeitsynchronisation vom PDC-Emulator übernommen. 

<br>

### Wichtige Protokolle

Viele sind als Repetition nochmals beschrieben. 

| **Protokolle**         | **Port**  | **Ausgeschrieben**                             | **Kommunikation** | **Hauptnutzen**                                                                             | **Beispiel**                                                                       |
| ---------------------- | --------- | ---------------------------------------------- | ----------------- | ------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **LDAP / LDAPS**       | 389 / 636 | Lightweight Directory Access Protocol (Secure) | TCP               | Zugriffsprotokoll für Abfragen und Änderungen, Authentifizierung von Userdaten.             | Login an einem domain-joined PC.                                                   |
| **Kerberos**           | 88        | Kerberos                                       | TCP / UDP         | Standard-Authentifizierungsprotokoll in AD, Ticket-basiertes System (TGT/ST).               | Erhalt eines Tickets nach dem Login für "Single Sign-On".                          |
| **RPC**                | 135       | Remote Procedure Call                          | TCP               | "Telefonbuch" für Dienste; weist dynamische Ports für Client-Server-Kommunikation zu.       | Client fragt beim Server an, welcher Port für die AD-Replikation offen ist.        |
| **Global Catalog**     | 3268      | Global Catalog                                 | TCP               | Suche nach Objekten im gesamten Forest (multidomain-fähig), ohne den Domainnamen zu kennen. | Suche nach einer E-Mail-Adresse eines Users in einer anderen Sub-Domain.           |
| **Global Catalog SSL** | 3269      | Global Catalog (Secure)                        | TCP               | Verschlüsselte Suche nach Objekten über den gesamten Forest hinweg.                         | Sichere Abfrage von Attributen aus dem Forest über eine verschlüsselte Verbindung. |
| **Kerberos Password**  | 464       | Kerberos Password Change / Set                 | TCP / UDP         | Ermöglicht User das Ändern oder Zurücksetzen ihres Passworts über Kerberos.                 | User drückt `Strg+Alt+Entf` und ändert sein Domänenpasswort.                       |
| **RDP**                | 3389      | Remote Desktop Protocol                        | TCP / UDP         | Fernsteuerung von grafischen Oberflächen auf anderen Windows-Rechnern.                      | Admin schaltet sich per Fernwartung auf einen Server auf.                          |
| **SMB**                | 445       | Server Message Block                           | TCP               | Dateizugriff, Druckerfreigabe und Kommunikation zwischen Prozessen (Named Pipes).           | Zugriff auf ein Netzlaufwerk oder Kopieren einer Datei auf den Server.             |
| **DNS**                | 53        | Domain Name System                             | UDP / TCP         | Namensauflösung (Hostname zu IP) und Lokalisierung von Domain Controllern (SRV Records).    | Eingabe von `google.com` oder Suche nach dem DC im Netzwerk.                       |
| **ICMP**               | -         | Internet Control Message Protocol              | ICMP              | Pingen von Geräten, Erreichbarkeit prüfen, Fehlerdiagnose im Netzwerk.                      | Test mit `ping 8.8.8.8`, ob die Internetverbindung steht.                          |

