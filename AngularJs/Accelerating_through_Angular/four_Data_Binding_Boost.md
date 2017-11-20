# Level 4: Data Binding Boost

### 4.2 Binding to What?
Property binding allows us to bind component properties to:

DOM element properties

### 4.3 Template Property Binding
We've gone ahead and applied new HTML and CSS to our app to make it prettier. We also have two new fields in our model and mocks: image and imageDescription.

- Use property binding to display our race images in the <img> tag we’ve added.
- Use property binding to add an alt attribute to each of our images that contains the value of our imageDescription.
- Use class binding to optionally add the racing css class to our ```sh <li>``` if we are racing in this race.

app/races.component.html
```sh
<main class="container" role="main">
<h2>Cash left to enter races: <span>{{cashLeft() | currency:'USD':true}}</span> </h2>
<ul>
  <li class="card" *ngFor="let race of races" [class.racing]="race.isRacing"  >
    <div class="panel-body">
      <div class="photo">
        <img [src]="race.image" [alt]="race.imageDescription">
      </div>
      <table class="race-info">
        <tr>
          <td>
            <h3>{{race.name}}</h3>
            <p class="date">{{race.date | date:'MMM d, y, h:MM a'}}</p>
            <p class="description">{{race.about}}</p>
          </td>
          <td>
            <p class="price">{{race.entryFee | currency:'USD':true}}</p>
          </td>
          <td>
            <button class="button" *ngIf="!race.isRacing">Enter Race</button>
            <div *ngIf="race.isRacing">
              <p class="status">Racing</p>
              <button class="button-cancel">Cancel Race</button>
            </div>
          </td>
        </tr>
      </table>
    </div>
  </li>
</ul>
<div class="price-total">
  <h3>Total cost:</h3>
  <p>{{totalCost() | currency:'USD':true}}</p>
</div>
</main>
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

app/mocks.ts
```sh
import { Race } from './race';

export const RACES: Race[] = [{
  "id": 1,
  "name": "Daytona Thunderdome",
  "date": new Date('2512-01-04T14:00:00'),
  "about": "Race through the ruins of an ancient Florida battle arena.",
  "entryFee": 3200,
  "isRacing": false,
  "image": "/images/daytona_thunderdome.jpg",
  "imageDescription": "Race track with laser lanes"
}, {
  "id": 2,
  "name": "San Francisco Ruins",
  "date": new Date('2512-07-03T20:00:00'),
  "about": "Drift down the streets of a city almost sunk under the ocean.",
  "entryFee": 4700,
  "isRacing": true,
  "image": "/images/san_francisco_ruins.jpg",
  "imageDescription": "Golden Gate Bridge with lasers"
}, {
  "id": 3,
  "name": "New York City Skyline",
  "date": new Date('2512-07-12T21:00:00'),
  "about": "Fly between buildings in the electronic sky.",
  "entryFee": 4300,
  "isRacing": true,
  "image": "/images/new_york_city_skyline.jpg",
  "imageDescription": "Bridge overlooking New York City"
}]; 
```


### 4.5  Racing
Time to implement the "Enter Race" button and "Cancel Race" link.

- First (because it's a little easier), let’s listen for the click event on the "Cancel Race" link and tell it to call the cancelRace() method. (Don’t forget to send the current race in.)
- Now let's implement the cancelRace() method in our component. It’ll simply need to set the race's isRacing to false.
- Next, let's implement the "Enter Race" button by listening for a click and then calling the enterRace() method.
- Here's where things get a little tricky. First, take a look at the cashLeft() method we wrote for you in races.component.ts. This returns how much cash we have left to enter races.

Define an enterRace() method that checks to see if cashLeft() is greater than the race entryFee. If it is, then enter us in the race by setting isRacing to true, otherwise pop up a JavaScript alert() that says "You don't have enough cash".

app/races.component.html
```sh
<main class="container" role="main">
<h2>Cash left to enter races: <span>{{cashLeft() | currency:'USD':true}}</span> </h2>
<ul>
  <li class="card" *ngFor="let race of races" [class.racing]="race.isRacing" >
    <div class="panel-body">
      <div class="photo">
        <img [src]="race.image" [alt]="race.imageDescription">
      </div>
      <table class="race-info">
        <tr>
          <td>
            <h3>{{race.name}}</h3>
            <p class="date">{{race.date | date:'MMM d, y, h:MM a'}}</p>
            <p class="description">{{race.about}}</p>
          </td>
          <td>
            <p class="price">{{race.entryFee | currency:'USD':true}}</p>
          </td>
          <td>
            <button class="button" *ngIf="!race.isRacing" (click)="enterRace(race)" >Enter Race</button>
            <div *ngIf="race.isRacing">
              <p class="status">Racing</p>
              <button class="button-cancel"  (click)="cancelRace(race)" >Cancel Race</button>
            </div>
          </td>
        </tr>
      </table>
    </div>
  </li>
</ul>
<div class="price-total">
  <h3>Total cost:</h3>
  <p>{{totalCost() | currency:'USD':true}}</p>
</div>
</main>
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
  enterRace(race) {
if (this.cashLeft() > race.entryFee) {
race.isRacing = true;
} else {
alert("You don't have enough cash");
}
}

cancelRace(race) {
race.isRacing = false;
}
}
```sh

### 4.6 Sending Event Data 
Which of the following is the proper syntax for listening for a keypress and sending in the event?
```sh
<input type="text"(keydown)="call($event)">
```

### 4.8 Input Binding
Let’s add the ability for us to manually increase the cash we can spend on races.

In our races.component.html, we’ve added an input field. Use two-way binding to bind this to the cash component property.

Once you complete the challenge, feel free to play with it in the Preview window.

app/races.component.html
```sh
<main class="container" role="main">
<h2>Money for racing: <input type="text" class="cash" [(ngModel)]="cash"></h2>
<h2>Cash left to enter races: <span>{{cashLeft() | currency:'USD':true}}</span> </h2>
<ul>
  <li class="card" *ngFor="let race of races" [class.racing]="race.isRacing" >
    <div class="panel-body">
      <div class="photo">
        <img [src]="race.image" [alt]="race.imageDescription">
      </div>
      <table class="race-info">
        <tr>
          <td>
            <h3>{{race.name}}</h3>
            <p class="date">{{race.date | date:'MMM d, y, h:MM a'}}</p>
            <p class="description">{{race.about}}</p>
          </td>
          <td>
            <p class="price">{{race.entryFee | currency:'USD':true}}</p>
          </td>
          <td>
            <button class="button" *ngIf="!race.isRacing" (click)="enterRace(race)">Enter Race</button>
            <div *ngIf="race.isRacing">
              <p class="status">Racing</p>
              <button class="button-cancel" (click)="cancelRace(race)">Cancel Race</button>
            </div>
          </td>
        </tr>
      </table>
    </div>
  </li>
</ul>
<div class="price-total">
  <h3>Total cost:</h3>
  <p>{{totalCost() | currency:'USD':true}}</p>
</div>
</main>
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

  enterRace(race) {
    if (this.cashLeft() > race.entryFee) {
      race.isRacing = true;
    } else {
      alert("You don't have enough cash");
    }
  }

  cancelRace(race) {
    race.isRacing = false;
  }

}
```


### 4.9 ngModel
This symbol [()] is sometimes called?

Banana in a box
