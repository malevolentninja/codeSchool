
# Level 5: Properties and Components 
Bring everything together for cleanliness and reuse with Ember’s computed properties and components.


### 5.2 Features of Computed Properties 
Computed properties provide the following:

- A property value computed from a function call
- Automatic invalidation when dependent properties change

### 5.3 Count the Votes
With voting in place, it's time to count the votes and determine a winner.
- Add an optionVotes property to the Poll model. It should return an array of votes from each option record. Use the Ember.computed.mapBy() macro or create your own to create an array of option votes values
- Add a votes property to the Poll model. This should be the total number (summation) of the optionVotes values. Hint: Use the Ember.computed.sum() macro.

app/models/poll.js
```sh
import Ember from 'ember';

export default Ember.Object.extend({
  optionVotes: Ember.computed.mapBy('options', 'votes'),
  votes: Ember.computed.sum('optionVotes')
});
```


### 5.5 Action Handlers
Select the objects below that are capable of capturing and handling actions.

Routes 
Components

### 5.6 Generating a Component 
Generate a new component named "option-tally" using an Ember CLI generator.

quiz$ ember generate component option-tally


### 5.7 Implement the Option Tally 
With an option-tally component available, use it to calculate the option percentage for the results page.

- Create a percentage computed property on the option-tally component. This property will use optionVotes and pollVotes attributes, so ensure that you identify them as dependent properties for the computed function.
- Create a percentage computed property on the option-tally component. This property will use optionVotes and pollVotes attributes, so ensure that you identify them as dependent properties for the computed function.

app/components/option-tally.js
```sh
import Ember from 'ember';

export default Ember.Component.extend({
  percentage: Ember.computed('optionVotes', 'pollVotes', function() {
    return Math.round(this.get('optionVotes') * 100 / this.get('pollVotes'));
  })
});
```


### 5.8 Use the Component 
With the option-tally component in place, use it in the results.
- Fill out the option-tally component template by displaying the option vote count and percentage. The template should render something like:
```sh
3 votes (33%)
```
Where 3 is the component's optionVotes, and 33 is the percentage computed property.
- Use the option-tally component in the polls.results template to replace the vote count and percentage placeholders.

Remember to pass the optionVotes and pollVotes properties to the component.

app/templates/components/option-tally.hbs
```sh
{{optionVotes}} votes ({{percentage}}%)
```

app/components/option-tally.js
```sh
import Ember from 'ember';

export default Ember.Component.extend({
  percentage: Ember.computed('optionVotes', 'pollVotes', function() {
    return this.get('optionVotes') * 100 / this.get('pollVotes');
  })
});
```

app/templates/polls/results.hbs
```sh
<header class="header">
  <h2>Welcome, Woodland Wanderers!</h2>
  <p>Now that you've completed your training, here's a quick quiz to test your skills.</p>
</header>

<main class="card card--light">
  <h3 class="border">{{model.question}}</h3>
  <div class="border">
    <div class="grid group">

      <div class="card-content grid-box grid-box--3of5">
        <ul class="list list--answer list--answer--flush">
          {{#each model.options as |option|}}
            <li class="list-item">
              <span>{{option.value}}</span>
            </li>
          {{/each}}
        </ul>
      </div>

      <div class="grid-box grid-box--2of5">
        {{#each model.options as |option|}}
          <div class='progress'>
            <p class='progress-info'>{{option-tally optionVotes=option.votes pollVotes=model.votes}}</p>
          </div>
        {{/each}}
      </div>
    </div>
  </div>

  <div class="grid group actions">
    <div class="grid-box grid-box--1of4">
      {{#link-to "polls.poll" model class="btn btn--primary btn--back"}}Back{{/link-to}}
    </div>
  </div>
</main>
```

