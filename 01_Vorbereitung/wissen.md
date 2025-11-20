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