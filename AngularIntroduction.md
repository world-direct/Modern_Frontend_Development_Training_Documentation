Einstieg in Angular 2
===
> Dieser Vortrag soll einen einfachen Einstieg in die Welt von Angular 2 bieten, dem populären
Frontend-Framework von Google. Ein gutes Verständnis der Architektur und der integrierten Bausteine 
ist dabei Voraussetzung für die Entwicklung von komponentenbasierten (Web-)Anwendungen mit Angular 2.

## Vortragende
   
 **[Christian Schaiter](mailto:christian.schaiter@world-direct.at) und [Mathias Feitzinger](mailto:mfe@world-direct.at)**

## Agenda
1. Was ist Angular?
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


# [Was ist Angular](https://angular.io/)?

> Kennenlernen des populärsten (laut Google Trends) Web-Frameworks.

Speziell in der JS-Welt dreht sich die Erdkugel in den letzten Jahren sehr schnell. Für ein Unternehmen ist es deshalb wichtig, richtige und 
nachhaltige Technologie-Entscheidungen zu treffen. 

## Welche Eigenschaften muss eine moderne (Web-)Anwendung mitbringen?

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

> Angular bietet in obigen Punkten ein überzeugendes Gesamtpaket.  


## Architektur von Angular

Angular ist ein Framework für die Erstellung von Client-Applikationen in HTML und JavaScript (bzw. einer Sprache wie TypeScript, die zu JavaScript kompiliert wird).

Das Framework selbst ist modular aufgebaut:
* Kernbiblioteheken (werden immer benötigt)
* Optionale Bibliotheken (können je nach Bedarf integriert werden)

Eine Angular Applikation wird erstellt durch 
* Angularisierte HTML *Templates*,
* *Komponenten*-Klassen zum Managen dieser Templates,
* eine in *Services* gekapselte Applikationslogik 
* sowie *Module* zum Kapseln von Komponenten und Services. 

Die Applikation selbst wird durch *Bootstrapping* des *Haupt-Moduls* gestartet: Angular übernimmt fortan die Kontrolle über den Inhalt sowie Interaktion mit der
Anwendung im Browser.

Folgendes Architektur-Diagramm zeigt die 8 Hauptbausteine einer Angular 2 Anwendung:
* Module
* Komponenten
* Templates
* Metadaten
* Data Binding
* Direktiven
* Services
* Dependency Injection

![Dependencies](assets/angular-architecture.png)
Quelle: angular.io

### Module

> Angular Module kapseln Teilbereiche einer Applikationsdomäne.

Jede Angular Anwendung hat zumindest ein Angular Modul, das *Hauptmodul* oder *root module*, für gewöhnlich `AppModule` genannt.
Die meisten (größeren) Client-Applikationen haben zusätzlich zum *root module* noch viele *feature modules*: kohärente Code-Blöcke, die
Komponenten für einen speziellen Teilbereich der Anwendung kapseln. Die Teilbereiche selbst sind vielfach Abhängig von Geschäftsdomäne. 

Ein Angular Modul (egal ob *root* oder *feature module*) ist eine Klasse mit dem `NgModule` [Dekorator](https://www.typescriptlang.org/docs/handbook/decorators.html).

```JavaScript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

@NgModule({
  imports:      [ BrowserModule ],
  providers:    [ Logger ],
  declarations: [ AppComponent ],
  exports:      [ AppComponent ],
  bootstrap:    [ AppComponent ]
})

export class AppModule { }
```

Das Konfigurationsobjekt für den `@NgModule` Dekorator hat folgende Eigenschaften:
* `declarations`: Die *View-Klassen*, die zum Modul gehören. Angular unterscheidet dabei 3 View-Klassen: Komponenten, Direktiven und Pipes.
* `exports`: Die Submenge von `declarations`, die in Templates von anderen Modulen verwendet werden dürfen.
* `imports`: Eine Liste von anderen Modulen, dessen exportierte Klassen von Templates in diesem Modul benötigt werden.
* `providers`: Erzeuger von Services, welche dieses Modul zur globalen Sammlung von Services beitägt. Diese sind in allen Teilen der Applikation zugänglich. 
* `bootstrap`: Die Haupt-View der Applikation (*root component*), welche alle anderen Views der App beinhaltet. Nur das *root module* sollte die `bootstrap` Eigenschaft setzen.


#### Angular Module vs JavaScript Module

> **Achtung:** Angular Module (d.h. eine Klasse mit dem `@NgModule` Dekorator) haben nichts mit den in [Teil 1](Ecosystem.md) 
vorgestellten JavaScript Modulen zu tun. Dies sind komplett unterschiedliche Konzepte und dürfen nicht miteinander vermischt 
werden.

Angular besteht aus einer Sammlung von JavaScript Modulen - oftmals als *library modules* bezeichnet. Angular Bibliotheken beginnen mit dem `@angular` prefix 
und werden wie gewohnt über NPM installiert und einzelne Klassen werden mit dem `import` Statement importiert.

Z.B. kann man den `Component` Dekorator aus der `@angular/core` Bibliothek importieren. Es können auch Angular Module aus Angular Bibliotheken mittels JS `import` Statements
import werden.

```JavaScript
import { Component } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
```


## Komponenten

> Angular Komponenten steuern einen kleinen Teil des Screens, sogenannte *Views*.

Die Applikationslogik einer Komponente - d.h. alles, was notwendig ist, um die zugehörige *View* zu steuern, wird einer einfachen
TypeScript Klasse definiert. Diese Klasse interagiert mit der *View* über die öffentliche API, bestehend aus Eigenschaften und
Methoden.

Beispiel:
* Die folgende `HeroListComponent` Komponente eine `heroes` Eigenschaft, welche ein Array aus *Hero* Instanzen zurückgibt, die wiederum selbst vom `HeroService` gelesen werden. 
* Des Weiteren bietet `HeroListComponent` eine `selectHero()` Methode an, welche die `selectedHero` Eigenschaft setzt, sobald der Benutzer einen Helden aus der obigen Liste anklickt. 
 
 ```JavaScript
export class HeroListComponent implements OnInit {
    heroes: Hero[];
    selectedHero: Hero;

    constructor(private service: HeroService) { }

    public ngOnInit() {
        this.heroes = this.service.getHeroes();
    }

    public selectHero(hero: Hero) { 
        this.selectedHero = hero; 
    }
}
 ```
Angular erzeugt, updated und zerstört Komponenten, je nachdem ob sie zur Anzeige einer aktuellen *View* benötigt werden. Mit Hilfe 
von *Livecycle Hooks* kann die Applikation kann in den Livecycle einer Komponente eingreifen, sie z.B. über die obige `ngOnInit()` Methode.  


### Templates

> Die *View* einer Komponente wird durch en zugehöriges *Template* definiert. Ein Template ist eine mit "angularisierte" Form von HTML,
mit der Angular feststell, wie die Komponente gerendert werden soll.

```html
<h2>Hero List</h2>
<p><i>Pick a hero from the list</i></p>
<ul>
    <li *ngFor="let hero of heroes" (click)="selectHero(hero)">
        {{hero.name}}
    </li>
</ul>
<hero-detail *ngIf="selectedHero" [hero]="selectedHero"></hero-detail>
```

Obiges *Template* verwendet neben gewöhnlichen HTML Tags wie `<h2>` oder `<ul>` auch auf den ersten Blick ungewöhnliche Konstrukte,
wie z.B. `*ngFor`, `{{hero.name}}`, `(click)`, `[hero]` oder `<hero-detail>` - dies ist die Angular *Template* Syntax.

In der letzten Zeile des *Templates* repräsentiert das `<hero-detail>` Tag eine weitere eigene *Komponente*, die `HeroDetailComponent`.

Die `HeroDetailComponent` ist eine *komplett andere* *Komponente* als `HeroListComponent`, in dessen *View* sie eingebettet wurde. Somit
ist `HeroDetailComponent` eine Kind von `HeroListComponent`. An diesem Beispiel erkennt man sehr schön den hierarchischen kompnentenbasierten
Aufbau von Angular Applikationen.

Im Grunde wird das Standard-Set an HTML Tags durch eigene Tags (wie z.B. `<hero-detail>`) erweitert, die wie jedes andere HTML Tag
an verschiedenen Stellen im HTML Code Verwendung finden können. D.h. *Komponenten* sind hochgradig wiederverwertbare Konstrukte.


## Metadaten

> Durch *Metadaten* weiß Angular, welche Aufgabe eine TypeScript Klasse erfüllt (z.B. dass eine Klasse eine *Komponente* oder ein *Modul* ist).

Das Code-Beispiel von `HeroListComponent` war nur eine gewöhnliche TypeScript Klasse, es gab kein Indiz für Angular, dass diese Klasse eine
*Komponente* darstellen soll. Wir müsssen Angular explizit mitteilen, dass es sich bei der Klasse um eine Angular Komponente handelt:
Dies wird mit dem `@Component` Dekorator realisiert.

```JavaScript
@Component({
    moduleId: module.id,
    selector:    'hero-list',
    templateUrl: 'hero-list.component.html',
    providers:  [ HeroService ]
})
export class HeroListComponent implements OnInit {
    /* . . . */
}
```