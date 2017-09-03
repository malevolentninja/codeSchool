# CoffeeScript Level Three Conditionals & Operators


### 3.1 conditionals

```sh
alert('High Caffeine Level')
```

Make sure the alert function is called only if caffeineLevel > 5.

```sh
alert 'High Caffeine Level' if caffeineLevel > 5
```

#### Live javaScript

```sh
if (caffeineLevel > 5) {
  alert('High Caffeine Level');
}
```


### 3.2 conditionals Part II

```sh
caffeineLevel > 5 ? alert('Too High') : alert('OK');
```
CoffeeScript does not support ternary operators. Change the code to use if/then/else.

```sh
if caffeineLevel > 5 then alert 'Too High' else alert 'OK'
```

#### Live javaScript

```sh
if (caffeineLevel > 5) {
  alert('Too High');
} else {
  alert('OK');
}
```


### 3.3 conditionals part III

```sh
# if(!coffeeReady){
#   alert('Please wait 5 more minutes.')
# }
```

Rewrite the javascript below to use an unless conditional.

```sh
alert 'Please wait 5 more minutes.' unless coffeeRead
```
#### Live javaScript

```sh
if (!coffeeRead) {
  alert('Please wait 5 more minutes.');
}
```

### 3.4 chained comparisons

```sh
if lowLevel < newLevel && newLevel < highLevel
  alert 'ok'
else
  alert 'abnormal caffeine level'
```

Rewrite the if to use CoffeeScript's chained comparisons syntax.

```sh
if lowLevel < newLevel < highLevel
    alert 'ok'
else
    alert 'abnormal caffeine level'
```

#### Live javaScript

```sh
if ((lowLevel < newLevel && newLevel < highLevel)) {
  alert('ok');
} else {
  alert('abnormal caffeine level');
}
```

### 3.5 Switch/case

```sh
# if (newLevel === 1) {
#   message = 'Out of bed yet?';
# } else if (newLevel === 2) {
#   message = 'Good morning!';
# } else {
#   message = 'You should stop while you can';
# }
```

Given the JavaScript code, rewrite it in CoffeeScript using a switch/when expression.

```sh
message = switch newLevel
    when 1 then 'Out of bed yet?'
    when 2 then 'Good morning!'
    else 'You should stop while you can'
```
#### Live javaScript

```sh
var message;
message = (function() {
  switch (newLevel) {
    case 1:
      return 'Out of bed yet?';
    case 2:
      return 'Good morning!';
    default:
      return 'You should stop while you can';
  }
})();
```

### 3.6 Existential operator

```sh
# if (typeof newLevel !== "undefined" && newLevel !== null){
#   checkLevel(newLevel);
# } else {
#   resetLevel();
# }
```

Make use of CoffeeScript's existential operator (the ?) to rewrite the JavaScript code below using CoffeeScript.

```sh
if newLevel? then checkLevel newLevel else resetLevel()
```

#### Live javaScript

```sh
if (typeof newLevel !== "undefined" && newLevel !== null) {
  checkLevel(newLevel);
} else {
  resetLevel();
}
```

### 3.7 existential operator - part II

Use the existential operator (the ?) to make sure the checkLevel and resetLevel functions are defined before calling them.

```sh
if level?
    checkLevel(level) unless checkLevel?
else
    resetLevel() unless resetLevel?
```

#### Live javaScript

```sh
if (typeof level !== "undefined" && level !== null) {
  if (typeof checkLevel === "undefined" || checkLevel === null) {
    checkLevel(level);
  }
} else {
  if (typeof resetLevel === "undefined" || resetLevel === null) {
    resetLevel();
  }
}
```

