#### Formatter Library
[![Build Status](https://travis-ci.org/atmajs/util-format.png?branch=master)](https://travis-ci.org/atmajs/util-format)

====

Features:

- [Date Formatter](#date-formatter)
- [Number Formatter](#number-formatter)
- [String Formatter](#string-formatter)
- [Different Languages and Cultures](#internationalization)
- MaskJS util support


### Date Formatter


Placeholder | Description
--- | ---
`yyyy` | Full **Year** Number
`yy` | Short **Year** Number
`MM` | **Month** Number in 2 digits, e.g. '03'
`#M` | **Month** Number in one or 2 digits
`Mm` | Short **Month** Name, e.g. 'Jan', 'Feb'
`MMM` | Full **Month** Name, e.g. 'January'
`dd` | **Date** Number in 2 digits
`#d` | **Date** Number in one or 2 digits
`Dd` | Short **Day** Name, e.g. 'Mo', 'Tu'
`DD` | Full **Day** Name, e.g. 'Monday'
`HH` | **Hours** Number in 2 digits, e.g. '03'
`#H` | **Hours** Number in one or 2 digits
`hh` | alias for 'HH'
`#h` | alias for '#H'
`mm` | **Minutes** in 2 digits
`#m` | **Minutes** in on or 2 digits
`ss` | **Seconds** in 2 digits
`#s` | **Seconds** in on or 2 digits

Standalone NodeJS example:
```javascript
var format = require('atma-formatter');
var str = format(new Date, "#d MMM, yyyy (hh:mm)");
//>  1 January, 2014 (09:55)
```

Mask example:
_mask_
```sass
div > 'Today - ~[format: today, "#d MMM, yyyy (hh:mm)"]'
```
_javascript model_
```javascript
{ today: new Date }
```

_Output_
```html
<div>Today - 1 January, 2014 (09:55)</div>
```

Javascript example:
```javascript
var str = mask.$utils.format(new Date, "#d MMM, yyyy (hh:mm)");
//>  1 January, 2014 (09:55)
```

### Number Formatter

Pattern: e.g. `,0.0`

Placeholder | Description
--- | ---
`,` | (optional) First char setts the integral part delimiter. Comma is used for default, which is defined by the current culture info.
`0` | Then goes the integral part of the number. More Zeros can be specified for the minimal digit output
`.` | (optional) Floating point. If omitted then the number is rounded to integer.
`0` | (optional) Fraction. When defined, the fraction part of the number is rounded to the specified zeros count

Samples:

Value | Formatter | Result
--- | --- | ---
`1234.123` | `,00000.0` | `01,234.1`
`1234.123` | `0` | `1234`
`1.5` | `00.00` | `01.50`


Standalone NodeJS example:
```javascript
var format = require('atma-formatter');
var str = format(4500.3851, ",0.00");
//>  4,500.39
```

_Mask example_
```css
div > 'Sum - ~[format: sum, ",0.00"]'
```

_Javascript model_
```javascript
{ sum: 4500.3851 }
```

_Output_
```html
<div>Sum - 4,500.39</div>
```

_Javascript example_
```javascript
var str = mask.$utils.format(4500.3851, ",0.00");
//>  4,500.39
```

### String Formatter
`{ index[,alignment][ :formatString] }`


Standalone NodeJS example:
```javascript
var format = require('atma-formatter');
var str = format(
	"Name: {0}; Born: {1:dd MMM yyyy}; Salary: ${2:,0.00}",
	'John',
	new Date(1975, 0, 1),
	17000
);
//>  Name: John; Born: 01 January 1975; Salary: $17,000.00
```


_Mask example_
```css
div > '~[format: "Name: {0}; Born: {1:dd MMM yyyy}; Salary: ${2:,0.00}", user.name, user.birth, user.salary]'
```

_Javascript model_
```javascript
{ user: { name: 'John', birth: new Date(1975, 0, 1), salary: 17000 } }
```

_Output_
```html
<div>Name: John; Born: 01 January 1975; Salary: $17,000.00</div>
```

_Javascript example_
```javascript
var str = mask.$utils.format("{0:,000}", 5.35);
//>  005
```


### Internationalization
There are already `EN` and `DE` support.

Add culture support sample:
```javascript
var formatter = require('atma-formatter');
formatter.Lang.$register('ru', {
	MONTH: ['Январь',...],
	MONTH_SHORT: ['Ян.',...],
	DAY: ['Воскресенье',...],
	DAY_SHORT: ['Bc',...],

	NUMBER: {
		// 1 000 000,00
		Delimiter: ' ',
		Point: ','
	}
});
formatter.Lang.$use('ru');
```

----
(c) MIT - Atma.js Project