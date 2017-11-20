# Level 5: Service Fuel Injection
Learn how to create your own services and then how to use the HTTP library to call out to the internet.


### 5.2 Injector
We tell our dependency injector what it can create and send by registering a 
 provider with it.


### 5.3 Moving to a Service
It's time to move our mocks into services for our racing schedule app. We've gone ahead and started creating a race.service.ts file for you. Please note that this is a RaceService class, not RacingDataService class like in the slides. We need your help hooking it all up.

 - First, in the race.service.ts file, import the @Injectable decorator and use it properly with our RaceService class.
 - Great! Now, in the main.ts, import our RaceService and let our module know about it.
 - Good job! Now, in the races.component.ts, import the service and create the constructor that will allow it to be injected.
 - Lastly, finish implementing our ngOnInit() to call our new service and fetch our races using the getRaces() method.

app/race.service.ts
```sh
import { RACES } from './mocks';
import { Injectable } from '@angular/core';

@Injectable()
export class RaceService {
  getRaces() {
    return RACES;
  }
}
app/main.ts

import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { AppComponent } from './app.component';
import { RacesComponent } from './races.component';
import { RaceService } from './race.service';

@NgModule({
  imports: [ BrowserModule, FormsModule ],
  declarations: [ AppComponent ],
  providers: [ RaceService ],
  bootstrap: [ AppComponent ]
})
class AppModule {}

platformBrowserDynamic().bootstrapModule(AppModule);
app/races.component.ts

import { Component } from '@angular/core';
import { Race } from './race';
import { RaceService } from './race.service';

@Component({
  selector: 'my-races',
  templateUrl: 'app/races.component.html',
  styleUrls:['app/races.component.css']
})
export class RacesComponent {
  heading = "Ultra Racing Schedule"
  cash = 10000;
  races: Race[];

  constructor(private raceService: RaceService) { }

  ngOnInit() {
    this.races = this.raceService.getRaces();
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

### 5.5 Over the Internet
We've gone ahead and created a races.json file for you — check it out. Let's import and use http to fetch our data.

- Inside our main.ts, go ahead and import the HttpModule and add it to the imports section of the NgModule decorator.

-  Now inside our race.service.ts we've already added the libraries you need, but we could use your help adding a constructor() to inject the Http service.
-  Now let's implement the getRaces() method to get our app/races.json file, and return the racesData array. We should use the map() method to map the response into a JSON object and then return the array of race data within it.

FYI, calling .data won’t work — you'll need to look inside our json file to find where our array is located.
- Inside the races.component.ts it's time to finish implementing the ngOnInit() method of races.component.ts to take the array of races emitted by getRaces() and save it as this.races.

app/main.ts
```sh
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { AppComponent } from './app.component';
import { RacesComponent } from './races.component';
import { RaceService } from './race.service';
import { HttpModule } from '@angular/http';

@NgModule({
  imports: [ BrowserModule, FormsModule, HttpModule ],
  declarations: [ AppComponent, RacesComponent ],
  providers: [ RaceService ],
  bootstrap: [ AppComponent ]
})
class AppModule {}

platformBrowserDynamic().bootstrapModule(AppModule);
app/race.service.ts

import { RACES } from './mocks';
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';
import { Race } from './race';
import 'rxjs/add/operator/map';

@Injectable()
export class RaceService {

  constructor(private http: Http) { }

  getRaces() {
    return this.http.get('app/races.json')
    .map(response => <Race[]>response.json().racesData);
  }
}
```

app/races.component.ts
```sh
import { Component } from '@angular/core';
import { Race } from './race';
import { RaceService } from './race.service';

@Component({
  selector: 'my-races',
  templateUrl: 'app/races.component.html',
  styleUrls:['app/races.component.css']
})
export class RacesComponent {
  heading = "Ultra Racing Schedule"
  cash = 10000;
  races: Race[];

  constructor(private raceService: RaceService) { }

  ngOnInit() {
    this.raceService.getRaces()
        .subscribe(data => this.races = data);
  }

  totalCost() {
    let sum = 0;
    if (this.races) {
      for (let race of this.races) {
        if (race.isRacing) sum += race.entryFee;
      }
    }
    return sum;
  }

  castDate(date) {
    return new Date(date);
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

app/races.json
```sh 
{
  "racesData": [
    {
      "id": 1,
      "name": "Daytona Thunderdome",
      "date": "2512-01-04T14:00:00",
      "about": "Race through the ruins of an ancient Florida battle arena.",
      "entryFee": 3200,
      "isRacing": false,
      "image": "/images/daytona_thunderdome.jpg",
      "imageDescription": "Race track with laser lanes"
    }, {
      "id": 2,
      "name": "San Francisco Ruins",
      "date": "2512-07-03T20:00:00",
      "about": "Drift down the streets of a city almost sunk under the ocean.",
      "entryFee": 4700,
      "isRacing": false,
      "image": "/images/san_francisco_ruins.jpg",
      "imageDescription": "Golden Gate Bridge with lasers"
    }, {
      "id": 3,
      "name": "New York City Skyline",
      "date": "2512-07-12T21:00:00",
      "about": "Fly between buildings in the electronic sky.",
      "entryFee": 4300,
      "isRacing": true,
      "image": "/images/new_york_city_skyline.jpg",
      "imageDescription": "Bridge overlooking New York City"
    }
  ]
} 
```
