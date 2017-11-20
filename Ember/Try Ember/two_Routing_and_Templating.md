# Level 2 Routing and Templating
Meet the Ember router and routes, and customize the presentation of your application using templates.

### 2.2 A common Template
What is the name of the outermost template that is available in all Ember applications?

Application template

### 2.3 Template Locations
Identify where the application template is located.

When using Ember CLI, the application template is located in the app/templates/application.hbs file.



### 2.4 Header and Footer

- Replace the default```sh <h2> ``` tag, including attributes, with an HTML5 ```sh <header> ``` tag.
- Inside of the new ```sh <header> ``` tag, change the text to "Wilderness Safety Quiz".
- Wrap the ```sh {{outlet}} ``` expression with a ```sh <main> ``` tag. 
         - The outlet should still be in the template when you're done
- Add the footer to the application template below the ```sh {{outlet}}``` as a ```sh<footer>``` tag with the following content:

&copy; Woodland Wanderer Whatchamacallits

index.html
```sh
<header> Wilderness Safety Quiz </header>
<main>
{{outlet}}
</main>
<footer>
  &copy; Woodland Wanderer Whatchamacallits
</footer>
```

### 2.5 Add a Poll Template

-We've created a poll template for you. Set the content of app/templates/poll.hbs to:

This is a poll.
- Add a new 'poll' mapping in app/router.js.
- Use a ```sh {{#link-to}} ``` expression in the app/templates/index.hbs template to instruct Ember to link from index to the "poll".

app/router.js
```sh
import Ember from 'ember';
import config from './config/environment';

const Router = Ember.Router.extend({
  location: config.locationType
});

Router.map(function() {
  this.route('poll');
});

export default Router;

```

app/templates/poll.hbs
```sh
This is a poll.
```

app/templates/index.hbs
```sh
{{#link-to "poll"}}Take a poll{{/link-to}}
```

### 2.7 Route Locations

Identify where routes are located:

When using Ember CLI, the routes are located under the app/routes directory.

### 2.8 Generate a Route

- Generate a route named 'polls' using Ember CLI.
```sh
quiz$ ember generate route polls
```

### 2.9 Populate the Route 250 PTS
Now that the polls route is generated, customize it to return some basic data.

- Add a model hook to the polls route.
- Return the following array of data from the polls route's model hook
```sh
[
  { id: '1', question: 'Which Poisonous Plant Are You?' },
  { id: '2', question: 'Which Is Your Favorite Woodland Wanderer Way? ' }
]
```

app/routes/polls.js

```sh
export default Ember.Route.extend({
  model() {
    return [
      { id: '1', question: 'Which Poisonous Plant Are You?' },
      { id: '2', question: 'Which Is Your Favorite Woodland Wanderer Way?' }
    ];
  }
});
```

### 2.10 Nesting Routes
Nest the poll route under the new polls route that you've just created.

- Convert the polls route into a parent route by adding a function parameter to it.
- Convert the poll route from the last level into a child route of polls. You should need only to move the definition.
- Customize the poll route's path to accept a poll_id dynamic segment.
- Add a model hook to the poll route. Remember to capture the params being sent from the router.
-  Return the following object from the poll route's model hook:
```sh
{ 
  id: params.poll_id, 
  question: 'This is poll #' + params.poll_id
}
```


app/router.js

```sh
import Ember from 'ember';
import config from './config/environment';

const Router = Ember.Router.extend({
  location: config.locationType
});

Router.map(function() {
 this.route('polls', function() {
    this.route('poll', { path: '/:poll_id' });
  });
});

export default Router;
```


app/routes/polls/poll.js
```sh
export default Ember.Route.extend({
  model(params) {
    return {
      id: params.poll_id,
      question: 'This is poll #' + params.poll_id
    };
  }
});
```

### 2.11 Nested Routes and Paths 250 PTS
With the current application route hierarchy:
```sh
Router.map(function() {
  this.route('polls', function() {
    this.route('poll', { path: '/:poll_id' });
  });
});
```
When the browser requests /polls, which route will be used?

The polls/index route

### 2.12 Nested Template Location 250 PTS
After moving the poll route underneath the polls route, into which location did the poll template file move?

app/templates/polls/poll.hbs

### 2.13 Displaying Polls

Using the route data that you've just created, display and link to the Polls in the application.

- List all of the polls on the polls template using the following HTML snippet. Use an {{#each}} iterator to loop over the Polls. Remember: model is the collection of Polls in the template.
```sh
{{outlet}}

<h4>Check out previous questions from Woodland Wanderers:</h4>

<ul>
  {{!-- {{#each}} goes here --}}
    <li>{{poll.question}}</li>
  {{!-- don't forget to close the {{#each}} --}}
</ul>
```

- Update the Poll listing to {{#link-to}} each poll. To do so, link to the "polls.poll" route and don't forget to pass it the poll to show!
- Display the Poll's question property on the polls/poll template within an <h3> element. You can replace the old "This is a poll." content from the last level.

app/templates/polls.hbs
```sh
{{outlet}}

<h4>Check out previous questions from Woodland Wanderers:</h4>

<ul>
  {{#each model as |poll|}}
    <li>{{#link-to "polls.poll" poll}}{{poll.question}}{{/link-to}}</li>
  {{/each}}
</ul>
```

app/templates/polls/poll.hbs
```sh
<h3>{{model.question}}</h3>
```
