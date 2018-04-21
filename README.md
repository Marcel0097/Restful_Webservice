# Restful_Webservice
## Starten des Servers

Der Server ist in der Sprache `C#` geschrieben.

Um den Server unter Windows zu starten muss der komplette Projektordner in einer geeigneten IDE geöffnet werden.

Es empfiehlt sich Visual Studio (2017), da man hier lediglich die `RestSportsclub.sln` (eine Visual Studio-Projektmappe) aus dem Windows Explorer anklicken/öffnen muss.

Beim erstmaligen Öffnen wird überprüft ob das Visual Studio Plugin für `ASP.NET und Webentwicklung` installiert ist, falls nicht wird man automatisch dazu aufgefordert dies zu tun.

Nach erfolgreicher Installation des Plugins befindet sich im oberen Bereich der IDE (hier eben Visual Studio) eine Startmöglichkeit des RESTful Webservices mit der Bezeichnung `IIS Express`. Es kann jeder beliebige Browser benutzt werden, welcher nach einem Klick auf den Button geöffnet wird.

Die Startseite befindet sich auf dem Port 51270, welche eine Beschreibung der Einsatzmöglichkeiten von ASP.NET zur Verfügung stellt.

## REST-Schnittstellenspezifikation

Dies ist die Spezifikation der REST-Schnittstellen der 1.Abgabe in Automatisierung von Geschäftsprozessen (SS18)

Für alle nachfolgenden Tests und HTTP-Methoden bietet sich an das im Projekt integrierte Swagger-Plugin zu nutzen.
Es befindet sich unter http://localhost:51270/swagger/ui/index

### Schnittstellen

#### **GetAllSportsclubInfos**

Über diese Schnittstelle bekommt man alle zugehörigen Dateneinträge für einen Sportsclub zurück

##### HTTP Methode

GET

##### Pfad

http://localhost:51270/api/Sportsclub

##### Rückgabe

Die Rückgabe erfolgt in JSON Datensätzen mit den Elementen "id", "memberPrename", "memberSurname" und "category".

```json
{
   "id": 1,
   "memberPrename": "Marcel",
   "memberSurname": "Heilborn",
   "category": "Coach"
}
```

##### Response

HTTP Status Code: 200
Definition: Die Datensätze des Sportclubs wurden ausgelesen und zurürckgeliefert

#### **GetMember**

Über diese Schnittstelle bekommt man alle zugehörigen Dateneinträge zur angegebenen Id für einen Sportsclub zurück

##### HTTP Methode

GET

##### Pfad

http://localhost:51270/api/Sportsclub?id=1

##### Rückgabe

Die Rückgabe ist ein JSON Datensatz mit den Elementen "id", "memberPrename", "memberSurname" und "category", passend zur überlieferten Id

```json
{
   "id": 1,
   "memberPrename": "Marcel",
   "memberSurname": "Heilborn",
   "category": "Coach"
}
```

##### Response

HTTP Status Code: 200
Definition: Die Datensätze des Sportclubs zur passenden Id wurden ausgelesen und zurürckgeliefert

#### **PostSportsclub**

Diese Schnittstelle erstellt einen neuen Eintrag für einen Sportsclub

##### HTTP Methode

Post

##### Rückgabe

Die Rückgabe ist ein JSON Datensatz mit den Elementen "id", "memberPrename", "memberSurname" und "category"

Alle Elemente können rein theoretisch leer gelassen werden und es würde reichen "{}" mitzuschicken, damit man später mit der HTTP Put Methode weitere Einträge zu einer gegebenen Id hinzufügen kann.
Als Beispieldatensatz kann aber auch einfach folgendes verwendet werden ...

```json
{
   "id": 0,
   "memberPrename": "Marco",
   "memberSurname": "Meier",
   "category": "Reserve"
}
```

Die Id wird automatisch auf einen neuen Höchstwert gesetzt.

##### Response

HTTP Status Code: `201`.
Definition: Der Datensatz wurde angelegt.

HTTP Status Code: `500`
Defintion: Der Wert des übergebenen Parameters darf nicht NULL sein. (Dieser Fehler wird möglicherweise auch in der IDE angezeigt. Dies ist aufgrund der benutzten ASP.Net-Technologie üblich. Durch eine Ausnahmebehandlung (auf Fehlermeldung klicken und Ausnahme für RestSportsclub.ddl hinzufügen) wird dieser Fehler auch in der oben genannten Swagger-UI dargestellt).

#### **PutSportsclubInfo**

Diese Schnittstelle kann einen bereits erstellen Eintrag nachträglich verändern. Dabei wird der vorhandene Eintrag gelöscht und ein neuer Eintrag angelegt. Es muss darauf geachtet werden auch die alten Einträge zur gegebenen Id, welche man behalten möchte, mit zu übertragen

##### HTTP Methode

Put

##### Rückgabe

No Content

##### Response

HTTP Status Code: `204`.
Definition: Der Datensatz wurde angelegt.

HTTP Status Code: `404`
Definition: Der Datensatz zur zugehörigen Id wurde nicht gefunden und konnte deshalb auch nicht nachträglich verändert werden (Dieser Fehler wird möglicherweise auch in der IDE angezeigt. Siehe obige *PostSportsclub* Methode).

#### **DeleteSportsclubInfo**

Diese Schnittstelle löscht einen Eintrag für einen Sportsclub

##### HTTP Methode

Delete

##### Rückgabe

No Content

Es muss lediglich die zu löschende Id angegeben werden.

##### Response

HTTP Status Code: `204`
Definition: Der Datensatz wurde gelöscht und es wird nichts zurückgeliefert

HTTP Status Code: `404`
Definition: Der Datensatz zur zugehörigen Id wurde nicht gefunden und konnte deshalb auch nicht gelöscht werden (Dieser Fehler wird möglicherweise auch in der IDE angezeigt. Siehe obige *PostSportsclub* Methode).
