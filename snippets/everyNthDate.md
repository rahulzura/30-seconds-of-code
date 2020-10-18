---
title: everyNthDate
tags: date,intermediate
---

Returns every nth day's date in yyyy-mm-dd format within given start and end dates.

- Get date after n days using `Date.prototype.getDate()` and adding n.
- While date after n days is smaller than end date, get the date in 'yyyy-mm-dd' format using `Date.prototype.toISOString()` and push it in the nthDates array, then increment the date by n days.
- Add end date if toIncludeEnd is true and end date is equal to the last nth date.
- start and end parameters should only contain date parts and no time parts.

```js
const everyNthDate = (start, end, n, toIncludeEnd=false) => {
  const nthDates = [];
  const startDate = new Date(start);
  const endDate = new Date(end);
  
  let curr = startDate;
  curr.setDate(curr.getDate() + n);
  while (curr < endDate) {
    nthDates.push(curr.toISOString().split('T')[0]);
    curr.setDate(curr.getDate() + n);
  }

  if (toIncludeEnd && curr.getTime() === endDate.getTime()) {
    nthDates.push(curr.toISOString().split('T')[0])
  }

  return nthDates;
}
```

```js
everyNthDate('2020-10-10', '2020-10-20', 2); // ["2020-10-12", "2020-10-14", "2020-10-16", "2020-10-18"]
everyNthDate('2020-10-10', '2020-10-20', 2, true); // ["2020-10-12", "2020-10-14", "2020-10-16", "2020-10-18", "2020-10-20"]
everyNthDate('2020-10-10', '2020-12-20', 30); // ["2020-11-09", "2020-12-09"]
```
