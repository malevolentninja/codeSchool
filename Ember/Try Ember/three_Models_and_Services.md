
# Level 3: Models and Services
Explore services to share common features and functionality while using models to formalize your application data.

### 3.2 Create Models

Create Poll and Option models. They should both extend from Ember.Object. The model files are already provided for you.
- Import Ember into the Poll and Option models.
- Export an extended Ember.Object as your Poll and Option models.

app/models/poll.js  and app/models/option.js
```sh
import Ember from 'ember';

export default Ember.Object.extend({
});
```

### 3.3 Generate a Service
Use an Ember CLI generator to create a new service called store.
```sh
$ ember generate 
```

### 3.4 Implement the Service 250 PTS
Now that the Poll and Option models exist, implement the store service to use them. The service has already been updated to create a local, private array of Poll records.

- Import the Option and Poll models into the store service as Option and Poll, respectively.
- Create a getPolls() function in the store to return the polls array.
- Add a getPollById() function to the store that accepts an id argument. In it, use findBy() to return the Poll record which contains a matching id property value.
- Update the polls and polls/poll routes to add a new store property to each. Use Ember to inject the store service into it
- Update the polls route's model to replace the hard-coded data and instead use the store service to return its getPolls() result.
- Update the polls/poll route's model to return the store service's getPollById() result. Remember to pass the params.poll_id property to it.

app/services/store.js
```sh
import Ember from 'ember';
import Option from 'quiz/models/option';
import Poll from 'quiz/models/poll';

const polls = [
  Poll.create({
    id: '1',
    options: [
      Option.create({ id: '1', value: 'Nightshade' }),
      Option.create({ id: '2', value: 'Hemlock' }),
      Option.create({ id: '3', value: 'Rhubarb' }),
    ],
    question: 'Which Poisonous Plant Are You?'
  }),

  Poll.create({
    id: '2',
    options: [
      Option.create({ id: '4', value: 'Honesty' }),
      Option.create({ id: '5', value: 'Integrity' }),
      Option.create({ id: '6', value: 'Patience' }),
    ],
    question: 'Which Is Your Favorite Woodland Wanderer Way?'
  })
];

export default Ember.Service.extend({
  getPollById(id) {
    return this.getPolls().findBy('id', id);
  },

  getPolls() {
    return polls;
  }
});
```

app/routes/polls.js
```sh
import Ember from 'ember';

export default Ember.Route.extend({
  model() {
    return this.get('store').getPolls();
  },

  store: Ember.inject.service()
});
```

app/routes/polls/poll.js
```sh
import Ember from 'ember';

export default Ember.Route.extend({
  model(params) {
    return this.get('store').getPollById(params.poll_id);
  },

  store: Ember.inject.service()
});
```
