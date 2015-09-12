# react-native-timer-mixin

Fork of
[react-timer-mixin](https://github.com/reactjs/react-timer-mixin) to add
integration with the react-native `InteractionManager`.

Using bare setTimeout, setInterval, setImmediate, requestAnimationFrame
and InteractionManager.runAfterInteractions calls is very dangerous
because if you forget to cancel the request before the component is
unmounted, you risk the callback throwing an exception. In the case of
InteractionManager.createInteractionHandle you also want to be sure that
the handle is cleaned up if for whatever reason the component is
unmounted before that has a chance to occur.

If you include TimerMixin, then you can replace your calls to
`setTimeout(fn, 500)` with `this.setTimeout(fn, 500)` (just prepend
`this.`) and everything will be properly cleaned up for you.

## Installation

Install the module directly from npm:

```
npm install react-native-timer-mixin
```

## Example

```js
var React = require('react');
var TimerMixin = require('react-timer-mixin');

var Component = React.createClass({
  mixins: [TimerMixin],
  componentDidMount() {
    this.setTimeout(() => {
      console.log('I do not leak!');
    }, 500);
    this.runAfterInteractions(() => {
      console.log('I also do not leak, unless you want me to ;)');
    });
  }
});
```

## TODO

- [ ] Mock out InteractionManager and add tests.
