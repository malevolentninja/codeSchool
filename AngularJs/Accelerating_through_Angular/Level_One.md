# Level 1: Angular Ignition
Get an introduction to Angular and create your first module and component with a template.

### 1.5 Our First Component 
Let’s build out a racing schedule app. It will be similar to what we built in the video, but a little different.

In the index.html file, create a custom HTML element called racing-app between the body tags, with the inner content of Loading...
-  In the index.html file, create a custom HTML element called racing-app between the body tags, with the inner content of Loading...
- Next, to make our module aware of the component, let's add the AppComponent to the declarations array inside our @NgModule decorator.
- Let's add a new property to our @NgModule decorator called bootstrap and set it as an array. 
      - Inside this array, let's add a reference to AppComponent to tell Angular to render it when the module is bootstrapped.

```sh
import { NgModule, Component } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
@Component({
  selector: 'racing-app',
  template: '<h1>{{ heading }}</h1>'

})

class AppComponent {
  heading = "Ultra Racing Schedule"
}

@NgModule({
  imports: [ BrowserModule ],
  declarations: [AppComponent],
   bootstrap: [ AppComponent ],
})
class AppModule {}

platformBrowserDynamic()
.bootstrapModule(AppModule);
```

index.html
```sh
<!DOCTYPE html>
<html>
  <head>
    <title>Racing App</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="styles.css">

    <!-- 1. Load libraries -->
     <!-- Polyfill(s) for older browsers -->
    <script src="https://unpkg.com/core-js/client/shim.min.js"></script>

    <script src="https://unpkg.com/zone.js@0.6.25?main=browser"></script>
    <script src="https://unpkg.com/reflect-metadata@0.1.8"></script>
    <script src="https://unpkg.com/systemjs@0.19.39/dist/system.src.js"></script>

    <!-- 2. Configure SystemJS -->
    <script src="systemjs.config.js"></script>

    <script>
      System.import('app/main').catch(function(err){ console.error(err);  });
    </script>
  </head>

  <!-- 3. Display the application -->
  <body>
    <racing-app> Loading... </racing-app>
  </body>
</html>
```


### 1.6 Making It Dynamic
We've added a new component property called race inside our class. Fill in the empty template elements using this race property. The name should be in the <h2>, the date in the first <p> tag, and the about in the last <p> tag. Don't forget to click the "Check My Work" button when you think you have it right.

main.ts
```sh
import { NgModule, Component } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

@Component({
  selector: 'racing-app',
  template: `
    <h1>{{ heading }}</h1>
    <h2>{{race.name}}</h2>
    <p>{{race.date}}</p>
    <p>{{race.about}}</p>
  `
})
class AppComponent {
  heading = "Ultra Racing Schedule"
  race = {
    "id": 1,
    "name": "Daytona Thunderdome",
    "date": new Date('2512-01-04T14:00:00'),
    "about": "Race through the ruins of an ancient Florida battle arena.",
    "entryFee": 3200
  }
}

@NgModule({
  imports: [ BrowserModule ],
  declarations: [ AppComponent ],
  bootstrap: [ AppComponent ]
})
class AppModule {}

platformBrowserDynamic()
.bootstrapModule(AppModule);
```sh
