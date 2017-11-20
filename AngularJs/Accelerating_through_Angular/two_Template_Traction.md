# Level 2: Template Traction

Start with a few structural directives and then transform your view with pipes.

### 2.4 Looping 
Notice that our AppComponent now contains an array called races. Much like you saw in the video, modify the <li> you see in the template to use a for loop and print out each of the races.

```sh
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { BrowserModule } from '@angular/platform-browser';
import { NgModule, Component } from '@angular/core';

@Component({
  selector: 'racing-app',
  template: `
  <h1>{{heading}}</h1>
  <ul>
    <li *ngFor="let race of races">
      <h2>{{race.name}}</h2>
      <p>{{race.date}}</p>
      <p>{{race.about}}</p>
    </li>
  </ul>
  `
})

class AppComponent {
  heading = "Ultra Racing Schedule"
  races = [{
    "id": 1,
    "name": "Daytona Thunderdome",
    "date": new Date('2512-01-04T14:00:00'),
    "about": "Race through the ruins of an ancient Florida battle arena.",
    "entryFee": 3200
  }, {
    "id": 2,
    "name": "San Francisco Ruins",
    "date": new Date('2512-07-03T20:00:00'),
    "about": "Drift down the streets of a city almost sunk under the ocean.",
    "entryFee": 4700
  }, {
    "id": 3,
    "name": "New York City Skyline",
    "date": new Date('2512-07-12T21:00:00'),
    "about": "Fly between buildings in the electronic sky.",
    "entryFee": 4300
  }];

}

@NgModule({
  imports: [ BrowserModule ],
  declarations: [ AppComponent ],
  bootstrap: [ AppComponent ]
})
class AppModule {}

platformBrowserDynamic().bootstrapModule(AppModule);
```

### 2.5 Conditionals
We've added a new boolean field called isRacing to each race. 
- If isRacing is true then we've already entered this race, and if it's false we haven’t. 
- Notice in our template we have a button that will eventually allow us to enter the race, and an ```sh <h3>``` we want to display if we're already racing.
- Add a conditional directive to only display the ```sh <button> ``` if we're not racing.
-Add a conditional directive to only display the ```sh <h3>``` if we are racing.

```sh
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { BrowserModule } from '@angular/platform-browser';
import { NgModule, Component } from '@angular/core';

@Component({
  selector: 'racing-app',
  template: `<h1>{{heading}}</h1>
<ul>
  <li *ngFor="let race of races">
    <h2>{{race.name}}</h2>
    <p>{{race.date}}</p>
    <p>{{race.about}}</p>
    <button *ngIf="!race.isRacing" >Enter Race</button>
    <h3 *ngIf="race.isRacing" >Already Racing</h3>
  </li>
</ul>
  `
})
export class AppComponent {
  heading = "Ultra Racing Schedule"
  races = [{
    "id": 1,
    "name": "Daytona Thunderdome",
    "date": new Date('2512-01-04T14:00:00'),
    "about": "Race through the ruins of an ancient Florida battle arena.",
    "entryFee": 3200,
    "isRacing": false
  }, {
    "id": 2,
    "name": "San Francisco Ruins",
    "date": new Date('2512-07-03T20:00:00'),
    "about": "Drift down the streets of a city almost sunk under the ocean.",
    "entryFee": 4700,
    "isRacing": true
  }, {
    "id": 3,
    "name": "New York City Skyline",
    "date": new Date('2512-07-12T21:00:00'),
    "about": "Fly between buildings in the electronic sky.",
    "entryFee": 4300,
    "isRacing": false
  }]
}

@NgModule({
  imports: [ BrowserModule ],
  declarations: [ AppComponent ],
  bootstrap: [ AppComponent ]
})
class AppModule {}

platformBrowserDynamic().bootstrapModule(AppModule);
```


### 2.8 Pipes 
Let’s use some pipes to format our data in a better way.

- First off, notice that we've added the entryFee of each race next to the title. Use the currency pipe like you saw in the video, but instead of euros, let’s use US dollars, which have the USD code. You should end up with a $ value.
- Next, let's use the date pipe to format our date. You'll need to send in the following string as a parameter: 'MMM d, y, h:mm a'.

```sh
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { BrowserModule } from '@angular/platform-browser';
import { NgModule, Component } from '@angular/core';

@Component({
  selector: 'racing-app',
  template: `
<h1>{{heading}}</h1>
<ul>
  <li *ngFor="let race of races">
    <h2>{{race.name}} {{race.entryFee | currency:'USD':true }}</h2>
    <p>{{race.date | date:'MMM d, y, h:mm a'}}</p>
    <p>{{race.about}}</p>
    <button *ngIf="!race.isRacing">Enter Race</button>
    <h3 *ngIf="race.isRacing">Already Racing</h3>
  </li>
</ul>
  `
})
export class AppComponent {
  heading = "Ultra Racing Schedule"
  races = [{
    "id": 1,
    "name": "Daytona Thunderdome",
    "date": new Date('2512-01-04T14:00:00'),
    "about": "Race through the ruins of an ancient Florida battle arena.",
    "entryFee": 3200,
    "isRacing": false
  }, {
    "id": 2,
    "name": "San Francisco Ruins",
    "date": new Date('2512-07-03T20:00:00'),
    "about": "Drift down the streets of a city almost sunk under the ocean.",
    "entryFee": 4700,
    "isRacing": true
  }, {
    "id": 3,
    "name": "New York City Skyline",
    "date": new Date('2512-07-12T21:00:00'),
    "about": "Fly between buildings in the electronic sky.",
    "entryFee": 4300,
    "isRacing": false
  }];
}

@NgModule({
  imports: [ BrowserModule ],
  declarations: [ AppComponent ],
  bootstrap: [ AppComponent ]
})
class AppModule {}

platformBrowserDynamic().bootstrapModule(AppModule);
```

### 2.9 Methods
Let's do some math to display the total amount we've spent entering races, and then how much cash we have left to enter new races.

- At the bottom of our template we've added a place to display our total cost. Our total cost will be calculated by summing up the entryFee properties of ONLY the races we are racing in ( isRacing is true). Write a method named totalCost() in our AppComponent that returns this value.

- Using the method we created in the first task, display the totalCost() value in the h2 element from the template that has the Total cost: label prepopulated for us.

- It looks like the output of our code needs to be formatted as currency. Pipe the output to the currency pipe to display the value as US dollars like entryFee.

main.ts
```sh
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { BrowserModule } from '@angular/platform-browser';
import { NgModule, Component } from '@angular/core';

@Component({
  selector: 'racing-app',
  template: `
  <h1>{{heading}}</h1>
  <ul>
    <li *ngFor="let race of races">
      <h2>{{race.name}} {{race.entryFee | currency:'USD':true}}</h2>
      <p>{{race.date | date:'MMM d, y, h:MM a'}}</p>
      <p>{{race.about}}</p>
      <button *ngIf="!race.isRacing">Enter Race</button>
      <h3 *ngIf="race.isRacing">Already Racing</h3>
    </li>
  </ul>
  <h2>Total cost:{{totalCost() | currency:'USD':true}}</h2>
  `
})
export class AppComponent {
  heading = "Ultra Racing Schedule"
  cash = 10000;
  races = [{
    "id": 1,
    "name": "Daytona Thunderdome",
    "date": new Date('2512-01-04T14:00:00'),
    "about": "Race through the ruins of an ancient Florida battle arena.",
    "entryFee": 3200,
    "isRacing": false
  }, {
    "id": 2,
    "name": "San Francisco Ruins",
    "date": new Date('2512-07-03T20:00:00'),
    "about": "Drift down the streets of a city almost sunk under the ocean.",
    "entryFee": 4700,
    "isRacing": true
  }, {
    "id": 3,
    "name": "New York City Skyline",
    "date": new Date('2512-07-12T21:00:00'),
    "about": "Fly between buildings in the electronic sky.",
    "entryFee": 4300,
    "isRacing": true
  }];
   totalCost() {
    let sum = 0;
    for (let race of this.races) {
      if (race.isRacing) sum += race.entryFee;
    }
    return sum;
  }
}

@NgModule({
  imports: [ BrowserModule ],
  declarations: [ AppComponent ],
  bootstrap: [ AppComponent ]
})
class AppModule {}

platformBrowserDynamic().bootstrapModule(AppModule);
```
