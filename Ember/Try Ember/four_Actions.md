# Level 4: Actions
React to user events and make your application more dynamic and interesting with actions.

### 4.2 Create a New Poll 
Create and return a new Poll record from the store service.
- Add a newPoll() function to the store service. It should return the following new Poll record:
```sh
Poll.create({
  options: [
    Option.create({ votes: 0 }),
    Option.create({ votes: 0 }),
    Option.create({ votes: 0 })
  ]
})
```
- Return the store's newPoll() result as the index route's model hook.

app/services/store.js
```sh
import Ember from 'ember';
import Option from 'quiz/models/option';
import Poll from 'quiz/models/poll';

const polls = [
  Poll.create({
    id: '1',
    question: 'Which Poisonous Plant Are You?',
    options: [
      Option.create({ id: '1', value: 'Nightshade', votes: 1 }),
      Option.create({ id: '2', value: 'Hemlock', votes: 5 }),
      Option.create({ id: '3', value: 'Rhubarb', votes: 0 })
    ]
  }),

  Poll.create({
    id: '2',
    question: 'Which Is Your Favorite Woodland Wanderer Way?',
    options: [
      Option.create({ id: '4', value: 'Honesty', votes: 3 }),
      Option.create({ id: '5', value: 'Integrity', votes: 4 }),
      Option.create({ id: '6', value: 'Patience', votes: 2 })
    ]
  })
];

export default Ember.Service.extend({
  getPollById(id) {
    return this.getPolls().findBy('id', id);
  },

  getPolls() {
    return polls;
  },

  newPoll() {
    return Poll.create({
      options: [
        Option.create({ votes: 0 }),
        Option.create({ votes: 0 }),
        Option.create({ votes: 0 })
      ]
    });
  }
});
```

app/routes/index.js
```sh
import Ember from 'ember';

export default Ember.Route.extend({
  model() {
    return this.get('store').newPoll();
  },

  store: Ember.inject.service()
});
```



### 4.3 The Actions Block 250 PTS
When defining action handlers within a route, what is the property under which all of the handler functions should be defined?

actions

### 4.4 Add an Action Handler 250 PTS
To prepare for the poll creation, you'll need an action handler to capture the form submission.

- Add an actions block to the index route.
- Within the actions block, add a createPoll() action handler function that accepts one poll parameter and "saves" the given poll using the following code:
```sh
this.get('store').createPoll(poll); ```
- Finally, after the poll is saved, transition the user to the "polls.poll" route from within the createPoll action handler. Don't forget to pass along the new model.

app/routes/index.js
```sh
import Ember from 'ember';

export default Ember.Route.extend({
  actions: {
    createPoll(poll) {
      this.get('store').createPoll(poll);
      this.transitionTo('polls.poll', poll);
    }
  },

  model() {
    return this.get('store').newPoll();
  },

  store: Ember.inject.service()
});
```


### 4.5 Implement the Form
Now that a new Poll record is available, it's time to implement the new Poll functionality on the landing page.

- Update the index template to use an {{input}} helper for the Poll question. Remember, the Poll's question will be model.question in the template.
- Update the index template to use {{input}} helpers for the Option values. Remember, the Option's value will be option.value within the iterator.
- Add an action to the <form> that triggers a createPoll action, passing the Poll ( model) to the action. Remember to indicate the event type on which the action should trigger!

app/templates/index.hbs

```sh
<header class="header">
  <h2>New Poll</h2>
  <p>Use the form below to create a new poll.</p>
</header>

<main class="card card--light">
  <form class="form" {{action "createPoll" model on="submit"}}>
    <fieldset class="form-field">
      <label class="form-label">Question</label>
      {{input value=model.question class="form-input" type="text"}}
    </fieldset>

    {{#each model.options as |option|}}
      <fieldset class="form-field">
        <label class="form-label">Option</label>
        {{input value=option.value class="form-input" type="text"}}
      </fieldset>
    {{/each}}

    <button class="btn btn--primary btn--form">Submit!</button>
  </form>
</main>

<footer class="footer">
  {{#link-to "polls"}}Find a question to answer{{/link-to}}

  <p class="footer-copyright">
    <span class="footer-copyright-text">&copy; Woodland Wanderer Whatchamacallits</span>
  </p>
</footer>
```


### 4.6 Enable Voting 
Polls can now be created, but the Wilderness Wanderers still need to cast their votes.
- Add an action handler to the polls.poll route called voteForOption that accepts two parameters: a poll and an option. In it, use incrementProperty() to increase the option votes by 1.
- After the option.votes is incremented, transition the user to the polls.results route (passing the poll) to display the voting results.
- Map the voteForOption action onto the voting <button> in the polls/poll template. The action should trigger on "click" and remember to pass the Poll and Option records as arguments (order matters!).

app/routes/polls/poll.js
```sh
import Ember from 'ember';

export default Ember.Route.extend({
  actions: {
    voteForOption(poll, option) {
      option.incrementProperty('votes');
      this.transitionTo('polls.results', poll);
    }
  },

  model(params) {
    return this.get('store').getPollById(params.poll_id);
  },

  store: Ember.inject.service()
});
```

app/templates/polls/poll.hbs
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
        <ul class="list list--answer">
          {{#each model.options as |option|}}
            <li class="list-item">
              <button class="list-item-checkbox" {{action "voteForOption" model option}}>
                <b class="srt">Select</b>
              </button>
              <span>{{option.value}}</span>
            </li>
          {{/each}}
        </ul>
      </div>

      <div class="grid-box grid-box--2of5">
        <img src="assets/images/icon-flame.svg" alt="" class="icon" width="130">
      </div>
    </div>
  </div>

  <div class="grid group actions">
    <div class="grid-box grid-box--1of4">
      {{#link-to "polls.results" model class="btn btn--secondary btn--results"}}Results{{/link-to}}
    </div>
  </div>
</main>
```
