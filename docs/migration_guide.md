
# Migration Guide

While we don't implement everything that jQuery provides, everything what we do implement should be compatible with jQuery.

However there are some minor differences that you should be aware about when migrating to Cash.

## Differences

### Binary CSS operators

Some CSS operators are binary, they operate on something before and after them: `>`, `~`, `+`. jQuery allows you to use them at the beginning of your selectors inside `$.fn.find`.

Cash only supports selectors the browser recognizes as valid, so you can't use `> .bar` like you sometimes can with jQuery.

```javascript
// jQuery
$('#foo').find ( '> .bar' );
$('#foo').find ( '~ .bar' );
$('#foo').find ( '+ .bar' );
// Cash
$('#foo').children ( '.bar' );
$('#foo').nextAll ( '.bar' );
$('#foo').next ( '.bar' );
```

### Negative width/height

Negative width/height get automatically converted to `0` by jQuery, both when setting them via `$.fn.width|height` and `$.fn.css`.

We discourage you from setting a negative width/height, if you want this to work like jQuery you'll have to convert negative values to `0` on your own.

```javascript
// jQuery
$('#foo').width ( myWidth );
$('#foo').css ( width, myWidth );
$('#foo').css ({ width: myWidth });
// Cash
myWidth = Math.max ( 0, parseFloat ( myWidth ) );
$('#foo').width ( myWidth );
$('#foo').css ( width, myWidth );
$('#foo').css ({ width: myWidth });
```

### Relative CSS values

jQuery supports relative CSS values.

```javascript
$('#foo').css ( 'padding-left', '+=10' );
```

This is not supported in Cash.

### Function that returns a value

In many places jQuery can accept a `function` instead of the actual value.

```javascript
$('#foo').attr ( 'bar', () => Math.random () );
```

This is not supported in Cash.

## Contributing

Did you find another difference between jQuery and Cash during your migration? Please add that to this page so that future migrations will be smoother for others.
