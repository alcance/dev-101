# Introducción
---
[Link](https://gist.github.com/alcance/77127a545ed563e8c86c04b1eca6ebc8)
![Image](http://via.placeholder.com/350x150)


```js
import Ember from 'ember';
import moment from 'moment';

export default Ember.Component.extend({

  init(){
    this._super(...arguments);
    console.log(`${this.get('day')}`);
    isActive: true;
  },

  day: Ember.computed('dayPassed', function(){
    return moment().day(`${this.get('dayPassed')}`).format('MM/DD/YYYY');
  }),

  actions: {
    toggleState(){
      this.toggleProperty('isActive');
    },
    submit() {
      const startDate = this.get('day') + ' ' + this.get('start');
      const endDate = this.get('day') + ' ' + this.get('end');
      const dayDate = moment(this.get('day')).day();
      const selectedDate = {
        day: this.get('dayPassed').toLowerCase(),
        start: moment(startDate).utc().format(),
        end: moment(endDate).utc().format()
      };
      this.get('onAdd')(selectedDate);
    }
  }
});
```