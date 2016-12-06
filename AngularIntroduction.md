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
    selector:    'hero-list',
    templateUrl: 'hero-list.component.html',
    providers:   [ HeroService ]
})
export class HeroListComponent implements OnInit {
    /* . . . */
}
```

Der `@component` Dekorator erhält ein Konfigurationsobjekt mit folgenden Eigenschaften:
* `selector`: Der CSS-Selektor zum Einbetten der *Komponente* in eine *View*. Wenn z.B. Angular eine Eltern-*View* parsed und
das HTML enthält `<hero-list></hero-list>`, dann wird eine neue Instanz der `HeroListComponent` *Komponente* erstellt und 
die zugehörige *View* zwischen den beiden Tags eingefügt.  
* `templateUrl`: Die URL des zugehörigen HTML *Templates*, relativ zum aktuellen *Modul*. Best Practice: Jedes *Modul* befindet sich
in einem eigenen Ordner, mit Unterordnern für alle zugehörigen *Komponenten* und *Templates*.
* `providers`: Ein Array aus *Dependency Injection Providern* für alle Services, die von dieser *Komponente* benötigt werden. Somit weiß Angular,
dass der Konstruktor der *Komponente* eine Abhängigkeit zum `HeroService` benötigt.

**Merke: _Templates_, _Metadaten_ und _Komponenten_ definieren gemeinsam eine _View_.**


## Data Binding

> Deklaratives Binden von Eigenschaften/Methoden einer *Komponenten*-Klasse zu Werten/Events im HTML.

Ohne geeignetes Framework wäre der Entwickler verantwortlich, sich ändernde Datenwerte (z.B. nach einem Ajax-Request) im HTML upzudaten
bzw. auf Benutzereingaben mit zu reagieren und entsprechende JS-Methoden aufzurufen. Jeder, der eine große Anwendung mit JQuery
geschrieben hat, weiß um die Schwierigkeiten, den Code wartbar und übersichtlich geglieder zu halten.

Angular hingegen unterstützt das Konzept von *Data Binding*, um Markup in einem HTML *Template* mit Eigenschaften und Methoden einer 
*Komponenten*-Klasse zu synchronisieren. 

Insgesamt existieren 4 verschiedene Syntax-Formen für *Data Binding*, wobei jede Form eine bestimmte Richtung hat:
* Von der *Komponente* zum DOM: `{{value}}` bzw. `[property] = 'value'`
* Vom DOM zur *Komponente*: `(event) = handler()`
* Bidirektional: `[(ng-model)] = property`

![Dependencies](assets/databinding.png)

```JavaScript
<li>{{hero.name}}</li>
<hero-detail [hero]="selectedHero"></hero-detail>
<li (click)="selectHero(hero)"></li>
```

* Die `{{hero.name}}` *Interpolation* zeigt den Wert der `hero.name` Eigenschaft innerhalb eines `<li>` Tags an.
* Das `[hero]` *Property Binding* übergibt den Wert der `selectedHero` Eigenschaft der `HeroListComponent` der
`hero` Eigenschaft von der Kind-*Komponente* `HeroDetailComponent`.
* Das `(click)` *Event Binding* ruft die `selectHero` Methode auf, sobald der Benutzer auf den Namen klickt.

*Two-way Data Binding* ist eine wichtige vierte Form, die *Property* und *Event Binding* unter der Verwendung der
vordefinierten `ngModel` Direktive in einer einzigen Notation miteinerander verknüpft.

```JavaScript
<input [(ngModel)]="hero.name">
```

In obigem `Two-way Data Binding` Beispiel wird der Wert `hero.name` Eigenschaft mit dem angezeigten Wert in der
Textbox bidirektional synchronsiert, sodass 
* Änderungen der Eigenschaften den angezeigten Wert in der Textbox mitändern und
* Benutzereingaben in die Textbox denselben Wert der Eigenschaft zuweisen.

`Data Binding` spielt eine wichtige Rolle in der Kommunikation zwischen einer `Komponente` und dem zugehörigen `Template`
bzw. zwischen Eltern und Kind *Komponenten*.

![Dependencies](assets/component-databinding.png)
![Dependencies](assets/parent-child-binding.png)


## Direktiven

> Angular *Templates* sind dynamische Konstrukte - wenn Angular eine *Template* rendert, wird das DOM entsprechend den Regeln 
der innewohnenden *Direktiven* transformiert.

Eine *Direktive* ist eine Klasse mit dem `@Directive` Dekorator als *Metadaten*. Dabei werden grob 3 Formen von Direktiven 
unterschieden: *Template-Direktiven*, *Strukturelle Direktiven* und *Attribut-Direktiven*.

### Template-Direktiven

Technisch gesehen sind die bereits bekannten *Templates* lediglich Vetreter dieser speziellen *Direktiven*-Form.
Allerdings sind *Komponenten* so zentrale Bestandteile in Angular, dass es einen eigenen Dekorator gibt. 

### Strukturelle Direktiven

*Strukturelle Direktiven* ändern das Layout indem sie Elemente zum DOM hinzufügen, ersetzen oder entfernen. Sie ändern sozusagen
die DOM Struktur.

```JavaScript
<li *ngFor="let hero of heroes"></li>
<hero-detail *ngIf="selectedHero"></hero-detail>
```

* `*ngFor` fungiert wie eine for-in Schleife: Die *Direktive* erzeugt für jeden Held in der `heroes` Liste ein neues `<li>` Element.
* `*ngIf` fungiert wie ein if Statement: Die `<hero-detail>` *Komponente* wird nur dann gerendert, wenn ein Held ausgewählt wurde
(d.h. wenn `selectedHero` nicht `null` und nicht `undefinded` ist).  
* `ngSwitch` fungiert wie ein switch Statement: Es wird nur jener Teil gerendert, auf den die switch-Bedingung zutrifft.

### Attribut-Direktiven 

*Attribut-Direktiven* ändern die Erscheinungsform bzw. das Verhalten von existierenden Elementen. In einem *Template* sehen sie wie 
gewöhnliche HTML Attribute aus - deshalb der Name.

```JavaScript
<input [(ngModel)]="hero.name">
```

* `ngModel` ist ein Beispiel für eine *Attribut-Directive* und implementiert ein *Two-way Data Binding*. Es ändert das Verhalten eines
existierenden Elements (für gewöhnlich eines `<input>` Elements), indem es den angezeigten Wert ändert, sobald sich der zugewiesene
Eigenschaftswert ändert.
* Weitere Beispiele: `ngStyle` und `ngClass` zum Ändern der Erscheinungsform von HTML Elementen.


## Services

> Als *Service* bezeichnet man in Angular weitreichend jeden Wert, jede Funktion oder jedes Feature, den die Anwendung benötigt. Insbesondere
werden *Services* für die Implementierung der innewohnenden Geschäftslogik verwendet.

