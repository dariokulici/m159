# Entra Connect

### Domain hinzufügen

Als erstes erstelle ich eine neue Domain und füge sie dem Tenant hinzu. 

<img width=40% height=30% alt="01VerifyNewDomain.png" src="media/01VerifyNewDomain.png">

<br>

Dann erstelle ich einen neuen User mit dieser Domain. 

<img width=40% height=30% alt="02NewUser.png" src="media/02NewUser.png">

<br>

Als nächstes lasse ich den Entra Connect Client mit dem extra erstellten User laufen. 

<img width=40% height=30% alt="03EntraSync" src="media/03EntraSync.png">

<br>

Hier sieht man wie die Objekte synchronisiert werden. 

<img width=40% height=30% alt="04StuffSyncing.png" src="media/04StuffSyncing.png">


<br>
Danach konfiguriere ich SCP, sodass er Hybrid joined ist. 

<img width=40% height=30% alt="05SCPConfig.png" src="media/05SCPConfig.png">

<br>

Anbei das Bild, auf dem man erkennt, dass der Entra Sync erfolgreich war. 

<img width=40% height=30% alt="06Azureadjoined.png" src="media/06Azureadjoined.png">

<br>

[Weiter zu Aufgabe 11: Python SSO App](../07_PythonApp/pythonapp.md) 