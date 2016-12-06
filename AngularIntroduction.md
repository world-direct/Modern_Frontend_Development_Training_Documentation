Einstieg in Angular 2
===
> Dieser Vortrag soll einen einfachen Einstieg in die Welt von Angular 2 bieten, dem populären
Frontend-Framework von Google. Ein gutes Verständnis der Architektur und der integrierten Bausteine 
ist dabei Voraussetzung für die Entwicklung von komponentenbasierten (Web-)Anwendungen mit Angular 2.

## Vortragende
   
 **[Christian Schaiter](mailto:christian.schaiter@world-direct.at) und [Mathias Feitzinger](mailto:mfe@world-direct.at)**

## Agenda
1. Was ist Angular 2?
1. Architektur Übersicht
    * Module
    * komponentenbasierten
    * Templates
    * Metadaten
    * Data Binding
    * Direktiven
    * Services
    * Dependency Injection
1. Start der Beispielapplikation


# [Was ist Angular 2](https://angular.io/)

> Kennenlernen des populärsten (laut Google Trends) Web-Frameworks.

Speziell in der JS-Welt dreht sich die Erdkugel in den letzten Jahren sehr schnell. Für ein Unternehmen ist es deshalb wichtig, richtige und 
nachhaltige Technologie-Entscheidungen zu treffen. 

## Welche Eigenschaften soll eine (Web-)Anwendung haben

* Moderne und wartbare Client-Anwendungen zu schreiben (z.B. für den Browser), stellt für viele Entwicklerteams eine große Herausforderung dar.
Der konventionelle Ansatz mit JQuery resultiert oftmals in einer engen Kopplung aus View-Code (HTML) und Logik (JavaScript), wodurch bereits das
Umbenennen eines CSS-Klassennamens die Applikation brechen kann, sollte dieser Klassenname als JQuery-Selektor verwendet werden und nicht überall im JS-Code
ebenfalls umbenannt werden. Diese Art der Programmierung resultiert im Allgemeinen zu sehr fragilem Code (aka "Spaghetti Code").

* Mit dem Aufkommen des MVVM (Model-View-ViewModel) Patterns wurde eine klare Trennung zwischen View und Logik erreicht, was in einer
deutlichen Verbesserung der Code-Wartbartkeit resultiert. Dieses Pattern wurde bereits erfolgreich in Desktop-Anwendungsframeworks wie
WPF (Windows Presentation Foundation) eingesetzt und erprobt. Diese Prinzipien sollen nun ebenfalls in Web-Anwendungen zum Einsatz kommen.  

* Komponentenbasierte Systeme haben den Vorteil, dass die komplette Applikationslogik in kleine modulare Komponenten gekapselt wird - jede
Komponente kümmert sich nur um einen winzigen Teilaspekt der Anwendung. Sollte es in diesem Teil einen Fehler geben, muss nur ein in sich
gekapselter Bereich für die Fehlersuche betrachtet werden - eine ungemein wertvolle Eigenschaft für die Wartbarkeit der Anwendung im Allgemeinen.

* Eine große und aktive Community bedeutet stetige Weiterentwicklung, Hilfe bei Problemen, Entwicklung von neuen Plugins, etc. Deshalb ist es
wichtig, auf Technologien zu setzen, die (1) von einem oder mehrerer großen IT-Playern getragen werden (Stichwort: Zukunftssicherheit) und (2) die
eine große Akzeptanz in der Entwickler-Community haben (Stichwort: Hilfestellung, Plugins).

* Weitere Fragen, die nicht außen vor gelassen werden sollten: 
    * Finde ich leicht Entwickler, die Know-How in den verwendeten Technologien haben?
    * Gibt es ausreichend qualitativ hochwertige Literatur, um sich ggf. das Know-How schnell aneignen zu können?
    * Wird das Framework auch in Zukunft gewartet, gibt es eine Roadmap?
    * Wie sieht die Tool-Unterstützung aus (z.B. Integration in IDEs)? 

All diese Eigenschaften sollten bei der Auswahl eines Frameworks mitberücksichtigt werden. 

> Angular 2 bietet in obigen Punkten ein überzeugendes Gesamtpaket.  


## Architektur von Angular 2 

Angular 2 ist ein Framework für die Erstellung von Client-Applikationen in HTML und JavaScript (bzw. einer Sprache wie TypeScript, die zu JavaScript kompiliert wird).

Das Framework selbst ist modular aufgebaut, mit einigen Kernbiblioteheken und einigen optionalen.



