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
<center> 
```bash
npm install -g hangman-game
```
</center>
Lets play :stuck_out_tongue_closed_eyes: :video_game: :video_game: :video_game: :video_game: :video_game: :video_game: :video_game: :video_game: 


# [2. Node Package Manager](https://www.npmjs.com/)
 > Für C# Entwickler: NPM ~ NuGet for Javacript  

* Package Verwaltung
* Erweitertes Dependencymanagement System
* Versionssicherheit bei Package Versionssprüngen. 
* Gesamte Serverumgebung mit Node möglich :mouse: (bsp.: [Trello](https://trello.com/))
 
### :rocket: Demo :rocket: ```git checkout sample_01```
<center> 
```bash
npm init
```
</center>

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

### 1. Generel
Gesamt Bild

### 1. Module Formats
Formats

### 1. Module Loaders
LoadersFormats

### 1. Module Bundlers
Bundlers

# [4. Webpack or Gulp]() :bug:todo:bug:

