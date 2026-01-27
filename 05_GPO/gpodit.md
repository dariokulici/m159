# GPO & DIT

### Passwort Richtlinie

Die Passwort Richtlinie wird nach den Anforderungen entsprechend angepasst. 

<img width=60% height=50% alt="01passwordpolicy.png" src="media/01passwordpolicy.png">

<br>

### Netzlaufwerke verteilen

Das Konzept sagt ja aus, es soll alles in Organisation Units geordnet sein und keine Gruppen mehr. Das heisst es müssen zwei OUs erstellt werden. Der Pool Drive wird als GPO auf Domänen Eben erstellt, damit sie für alle gillt. 

<br>

Daher erstelle ich als erstes die Pool Drive GPO. 

<img width=60% height=50% alt="01passwordpolicy.png" src="media/02PoolGPO.png">

<br>

Dann bewege ich die User in die entsprechenden OUs und erfasse die entsprechenden Netzlaufwerke der Abteilungen.  

<img width=60% height=50% alt="03MoveUsersToOU.png" src="media/03MoveUsersToOU.png">

<br>

<img width=60% height=50% alt="04RestDrives.png" src="media/04RestDrives.png">

<br>

Im folgenden Bild bin ich mit Martin Meer eingeloggt, der Mitglied bei Intern ist und die GPO hat die Laufwerke Pool und Intern erstellt. 

<img width=60% height=50% alt="05GPOWorks.png" src="media/05GPOWorks.png">

<br>

### Desktop Shortcut

Damit das Desktop Shortcut auf Domänen Ebene sein kann aber trotzdem nur für die Gruppe Intern angewendet muss dies beim Security Filtering geändert werden. 

<img width=60% height=50% alt="06CreateSHortcutGPO.png" src="media/06CreateSHortcutGPO.png">

<br>

<img width=60% height=50% alt="07Delegation.png" src="media/07Delegation.png">

<br>

Auf dem nächsten Bild sieht man die Funktionalität. Bei mir klappte es erst nach dem kompletten Logout des Users und nicht einfach mit gpupdate. 

<img width=60% height=50% alt="08ShortcutWorks.png" src="media/08ShortcutWorks.png">

<br>

### Fazit

Somit waren das 3 von 6 Aufgaben, die mit GPOs zu tun hatten. 