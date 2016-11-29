Termin 1
===
> Ökosystem für die moderne Frontend-Entwicklung auf Basis von Web-Technologien

#### Vortragende
   
 **Christian Schaiter und Mathias Feitzinger**


## [Agenda]()
* Node Package Manager (npm): Das Package Management System für node.js
    * Wie werden alle weiteren notwendigen Tools/Frameworks/Bibliotheken geladen und eingebunden
* Module Loaders und Module Bundlers
    * Unterschiede zwischen AMD und CommonJS
    * SystemJS vs. Webpack: State-of-the-Art Module-Loaders 
* TaskRunner:  
    * Automatisierte Frontend-Builds (ähnlich zu Ant in Java) am Beispiel von Gulp
    * Integration in TFS-Builds 
* Entwicklung mit Typescript
    * Best Practices von TypeScript  für Angular 2 (Annotationen, Klassen, Interfaces, Imports, Module, etc.)
    * Verwenden von JS-Fremdbibliotheken mit Hilfe von Declaration-Files
    * Visual Studio Code
    * Kurzeinführung in den neuen Code-Editor von MS

# [1. Node.js](https://nodejs.org/en/)
> Javascript für Server


* Javascript direkt am Rechner ausführen. 
* [Node.js](https://nodejs.org/en/) läuft als Dienst am Computer (Mac, Windows, Linux etc..)

### :rocket: Demo :rocket:  
```bash
npm install -g hangman-game
```
Lets play :stuck_out_tongue_closed_eyes: :video_game: :video_game: :video_game: :video_game: :video_game: :video_game: :video_game: :video_game: 


# [2. Node Package Manager](https://www.npmjs.com/)
 > Für C# Entwickler: NPM ~ NuGet for Javacript  

* Package Verwaltung
* Erweitertes Dependencymanagement System
* Versionssicherheit bei Package Versionssprüngen. 
* Gesamte Serverumgebung mit Node möglich :mouse: (bsp.: [Trello](https://trello.com/))
 
### :rocket: Demo :rocket: ```git checkout sample_01```

* NPM Packet anlegen: ```npm init```
* Development Http Server mit LiveReload: ```npm install -g live-server``` and execute ```live-server```

**index.html**
```html
<!DOCTYPE html>
<html lang="en">
    <head>
    </head>
    <body>
    <h1>May the force is with you</h1>
    <span>Your are </span><span id='name'>???</span>
    <script src="./main.js" type="text/javascript"></script>
    </body>
</html>
```

**main.js**
```JavaScript
'use strict';

function forceMe(){
var nameSpan = document.getElementById('name');
nameSpan.innerHTML = "Franz";
}

forceMe();
```

### NPM Packet einbinden (einfachste Art)
* Abhaengigkeit zu [NPM Packet](https://www.npmjs.com/package/random-lastname) herstellen ```npm install --save random-lastname```
* In main.js verwenden:
```JavaScript
var randomLastname = require("random-lastname");
```
**:boom:ERROR:boom: :scream::scream::scream:**
* :exclamation: Browser versteht kein AMD oder CommonJS ohne Hilfe
* npm-run installieren um executables direkt zu starten ```npm install -g npm-run```
* [browserify](http://browserify.org/) ```npm install browserify --save-dev```
* [watchify](https://www.npmjs.com/package/watchify) fur Autoreload ```watchify main.js -o static/bundle.js```

Da wir nun ein NPM Package verwenden muessen wir die Html sowie das Javascript erweitern:

**index.html**
```html
<!DOCTYPE html>
<html lang="en">
    <head>
    </head>
    <body>
    <h1>May the force is with you</h1>
    <span>Your are </span><span id='name'>???</span>
<button onclick="forceMe()">Force me!!</button>
    <script  src="bundle.js" type="text/javascript"></script>  
    </body>
</html>
```

**main.js**
```JavaScript
'use strict';

var randomLastname = require("random-lastname");

function forceMe(){
var nameSpan = document.getElementById('name');
nameSpan.innerHTML = randomLastname() + " " +randomLastname();
}

forceMe();
window.forceMe = forceMe;
```


##### Wichtige Befehle:
* Packet installieren ```npm install <PACKAGE_NAME>```
* Packet installieren und in package.json verweis ablegen ```npm install <PACKAGE_NAME> --save```
* Packet für Entwicklungsumgebung installieren ```npm install <PACKAGE_NAME> --dev-save ```
* Packet "global" installieren 
```npm install <PACKAGE_NAME> --global```
* Alle Packete für aktuelles Projekt installieren
```npm update```

### Semantic versioning (semver) <sup>[Image Sources](http://bytearcher.com/goodies/semantic-versioning-cheatsheet/)</sup>
![alt text](http://bytearcher.com/articles/semver-explained-why-theres-a-caret-in-my-package-json/promopics/1-table-semver-plain.png "Logo Title Text 1")
![alt text](http://bytearcher.com/goodies/semantic-versioning-cheatsheet/wheelbarrel-with-tilde-caret-white-bg-w1000.jpg "Logo Title Text 1")

:bug: Lock down dependency versions :bug:

# [3. JavaScript Modules]() :bug:todo:bug:
> Use Modules to organize your JavaScript Codes
Module: Calculator, Logger und DomWriter und eine Main 
Zeichnung der Abhaengigkeiten

### 1. Generel
Plain Javascript

### 1. Module Formats and Loaders
Bsp als AMD mit RequireJs
Bsp als CommonJS mit SystemJS

### 1. ES15 bzw TypeScript
Gleiches Beispiel mit Typescript nur mit tsc

### 1. Module Bundlers
browserify mit CommonJS

# [4. Webpack]() :bug:todo:bug:
