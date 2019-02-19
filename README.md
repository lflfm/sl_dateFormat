## JavaScript Date Format
[originaly created by Steven Levithan](http://blog.stevenlevithan.com/archives/date-time-format)

_note from lflfm:_ I created this repository since there is no official one and I intend to make a couple of small improvements that might help others so I will add them as future commits to this repo...

---

 _(directly from the [original post](http://blog.stevenlevithan.com/archives/date-time-format))_
 Here are some examples of how this script can be used:
```JavaScript
var now = new Date();

now.format("m/dd/yy");
// Returns, e.g., 6/09/07

// Can also be used as a standalone function
dateFormat(now, "dddd, mmmm dS, yyyy, h:MM:ss TT");
// Saturday, June 9th, 2007, 5:46:21 PM

// You can use one of several named masks
now.format("isoDateTime");
// 2007-06-09T17:46:21

// ...Or add your own
dateFormat.masks.hammerTime = 'HH:MM! "Can\'t touch this!"';
now.format("hammerTime");
// 17:46! Can't touch this!

// When using the standalone dateFormat function,
// you can also provide the date as a string
dateFormat("Jun 9 2007", "fullDate");
// Saturday, June 9, 2007

// Note that if you don't include the mask argument,
// dateFormat.masks.default is used
now.format();
// Sat Jun 09 2007 17:46:21

// And if you don't include the date argument,
// the current date and time is used
dateFormat();
// Sat Jun 09 2007 17:46:22

// You can also skip the date argument (as long as your mask doesn't
// contain any numbers), in which case the current date/time is used
dateFormat("longTime");
// 5:46:22 PM EST

// And finally, you can convert local time to UTC time. Either pass in
// true as an additional argument (no argument skipping allowed in this case):
dateFormat(now, "longTime", true);
now.format("longTime", true);
// Both lines return, e.g., 10:46:21 PM UTC

// ...Or add the prefix "UTC:" to your mask.
now.format("UTC:h:MM:ss TT Z");
// 10:46:21 PM UTC
```
Masks:

|Mask|Description|
|----|-----------|
|`d`|Day of the month as digits; no leading zero for single-digit days.| 
|`dd`| Day of the month as digits; leading zero for single-digit days.|
|`ddd`| Day of the week as a three-letter abbreviation.|
|`dddd`| Day of the week as its full name.|
|`m`| Month as digits; no leading zero for single-digit months.|
|`mm`| Month as digits; leading zero for single-digit months.|
|`mmm`| Month as a three-letter abbreviation.|
|`mmmm`| Month as its full name.|
|`yy`| Year as last two digits; leading zero for years less than 10.|
|`yyyy`| Year represented by four digits.|
|`h`| Hours; no leading zero for single-digit hours (12-hour clock).|
|`hh`| Hours; leading zero for single-digit hours (12-hour clock).|
|`H`| Hours; no leading zero for single-digit hours (24-hour clock).|
|`HH`| Hours; leading zero for single-digit hours (24-hour clock).|
|`M`| Minutes; no leading zero for single-digit minutes.|
|`MM`| Minutes; leading zero for single-digit minutes.|
|`s`| Seconds; no leading zero for single-digit seconds.|
|`ss`| Seconds; leading zero for single-digit seconds.|
|`l` or`L`| Milliseconds. `l` gives 3 digits. `L` gives 2 digits.|
|`t`| Lowercase, single-character time marker string: _a_ or _p_.|
|`tt`| Lowercase, two-character time marker string: _am_ or _pm_.|
|`T`| Uppercase, single-character time marker string: _A_ or _P_.|
|`TT`| Uppercase, two-character time marker string: _AM_ or _PM_.|
|`Z`| US timezone abbreviation, e.g. _EST_ or _MDT_. With non-US timezones or in the Opera browser, the GMT/UTC offset is returned, e.g. _GMT-0500_ GMT/UTC timezone offset, e.g. _-0500_ or _+0230_.|
|`S`| The date's ordinal suffix (_st_, _nd_, _rd_, or _th_). Works well with d.|
|`'…'` or `"…"`| Literal character sequence. Surrounding quotes are removed.|
|`UTC:`| Must be the first four characters of the mask. Converts the date from local time to UTC/GMT/Zulu time before applying the mask. The "UTC:" prefix is removed.|

And here are the named masks provided by default (you can easily change these or add your own):

|Name|Mask|Example|
|----|----|-------|
|`default`|`ddd mmm dd yyyy HH:MM:ss`|Sat Jun 09 2007 17:46:21|
|`shortDate`|`m/d/yy`|6/9/07|
|`mediumDate`|`mmm d, yyyy`|Jun 9, 2007|
|`longDate`|`mmmm d, yyyy`|June 9, 2007|
|`fullDate`|`dddd, mmmm d, yyyy`|Saturday, June 9, 2007|
|`shortTime`|`h:MM TT`|5:46 PM|
|`mediumTime`|`h:MM:ss TT`|5:46:21 PM|
|`longTime`|`h:MM:ss TT Z`|5:46:21 PM EST|
|`isoDate`|`yyyy-mm-dd`|2007-06-09|
|`isoTime`|`HH:MM:ss`|17:46:21|
|`isoDateTime`|`yyyy-mm-dd'T'HH:MM:ss`|2007-06-09T17:46:21|
|`isoUtcDateTime`|`UTC:yyyy-mm-dd'T'HH:MM:ss'Z'`|2007-06-09T22:46:21Z|

A couple issues:

- In the unlikely event that there is ambiguity in the meaning of your mask (e.g., `m` followed by `mm`, with no separating characters), put a pair of empty quotes between your metasequences. The quotes will be removed automatically.
- If you need to include literal quotes in your mask, the following rules apply:
    - Unpaired quotes do not need special handling.
    - To include literal quotes inside masks which contain any other quote marks of the same type, you need to enclose them with the alternative quote type (i.e., double quotes for single quotes, and vice versa). E.g., `date.format('h "o\'clock, y\'all!"')` returns `6 o'clock, y'all`. This can get a little hairy, perhaps, but I doubt people will really run into it that often. The previous example can also be written as `date.format("h") + "o'clock, y'all!"`.

---
