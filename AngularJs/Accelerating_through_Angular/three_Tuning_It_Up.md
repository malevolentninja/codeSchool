
# Level 3: Tuning It Up

### 3.3 Refactoring Classes
We've gone ahead and split out your components for you, much like we did in the video. However, there are a few more pieces of code we need you to write.

- Both our app.component.ts and our races.component.ts are missing the export keyword to allow their classes to be imported. Could you add them where they’re needed?
- Great! Now, inside our app.component.ts we need to display the RacesComponent by using the selector set in the races.component.ts. Add the tag right under the heading in the AppComponent.
- Lastly, we need to tell our AppModule that we’re using the RacesComponent in the template. Add code within main.ts to do this.

app/main.ts
```sh
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { RacesComponent } from './races.component';

@NgModule({
  imports: [ BrowserModule ],
  declarations: [ AppComponent, RacesComponent ],
  bootstrap: [ AppComponent ]
})
class AppModule {}

platformBrowserDynamic().bootstrapModule(A


app/app.component.ts

import { Component } from '@angular/core';

@Component({
  selector: 'racing-app',
  template: `
    <h1>{{heading}}</h1>
    <my-races></my-races>
  `
})

export class AppComponent {
  heading = "Ultra Racing Schedule"
}
```

app/races.component.ts
```sh
import { Component } from '@angular/core';

@Component({
  selector: 'my-races',
  template: `
    <h2>Cash left to enter races: {{cashLeft() | currency:'USD':true}} </h2>
    <ul>
      <li *ngFor="let race of races">
        <h2>{{race.name}} {{race.entryFee | currency:'USD':true}}</h2>
        <p>{{race.date | date:'MMM d, y, h:MM a'}}</p>
        <p>{{race.about}}</p>
        <button *ngIf="!race.isRacing">Enter Race</button>
        <h3 *ngIf="race.isRacing">Already Racing</h3>
      </li>
    </ul>
    <h2>Total cost: {{totalCost() | currency:'USD':true}}</h2>
})
export class RacesComponent {
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

  cashLeft() {
    return this.cash - this.totalCost();
  }

}
```

### 3.5 Adding HTML and CSS

Let’s separate out HTML and CSS files for our RacesComponent.

- As you can see, we moved the HTML of the racing app into a races.component.html file. Let's include it in the component metadata.
- Great! We also created races.component.css and added a few styles there. Let's go ahead and include that as well.

app/races.component.ts
```sh
import { Component } from '@angular/core';

@Component({
  selector: 'my-races',
  templateUrl: 'app/races.component.html',
  styleUrls:['app/races.component.css']
})
export class RacesComponent {
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

  cashLeft() {
    return this.cash - this.totalCost();
  }

}
```

### 3.7 Data Organization

In Angular, with TypeScript, it’s best to specify a class for our data, as well as class property types in a model .


### 3.8 Modeling and Mocking

It's time to create a model and a mock file, like we did in the video.

- We've already started creating a race.ts file and listed its properties, which will contain our model. Please help us finish it by adding property types. FYI, the date should be of type Date, and isRacing should be of type boolean.
- We've moved the data into our mocks.ts file. We need you to help export the data using a constant called RACES, which is cast as an array containing objects of type Race.
- Lastly, we need to set the races in our RacesComponent equal to the RACES mock. You know, inside the ngOnInit().

app/race.ts
```sh
export class Race {
  id: number;
  name: string;
  date: Date;
  about: string;
  entryFee: number;
  isRacing: boolean;
}
```

app/mocks.ts
```sh
export const RACES: Race[] = [{
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
```

app/races.component.ts
```sh
import { Component } from '@angular/core';
import { Race } from './race';
import { RACES } from './mocks';

@Component({
  selector: 'my-races',
  templateUrl: 'app/races.component.html',
  styleUrls:['app/races.component.css']
})
export class RacesComponent {
  heading = "Ultra Racing Schedule"
  cash = 10000;
  races: Race[];
  ngOnInit() {
    this.races = RACES;
  }

  totalCost() {
    let sum = 0;
    for (let race of this.races) {
      if (race.isRacing) sum += race.entryFee;
    }
    return sum;
  }

  cashLeft() {
    return this.cash - this.totalCost();
  }

}
```

app/races.component.html
```sh
<h2>Cash left to enter races: {{cashLeft() | currency:'USD':true}} </h2>
<ul>
  <li *ngFor="let race of races">
    <h2>{{race.name}} {{race.entryFee | currency:'USD':true}}</h2>
    <p>{{race.date | date:'MMM d, y, h:MM a'}}</p>
    <p>{{race.about}}</p>
    <button *ngIf="!race.isRacing">Enter Race</button>
    <h3 *ngIf="race.isRacing">Already Racing</h3>
  </li>
</ul>
<h2>Total cost: {{totalCost() | currency:'USD':true}}</h2>
```

app/races.component.css
```sh
h2 {
  color: green;
}
p {
  font-size: small;
}
``
