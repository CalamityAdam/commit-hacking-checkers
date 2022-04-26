# CHECKERS
[example](https://github.com/CalamityAdam?tab=overview&from=2017-12-01&to=2017-12-31)

Currently supporting all non-leap years. (modify this yourself to figure out a leap year.)

## The Logic

We'll start by adding commits for every other day in a month. Starting from the 1st of the month we will add commits for the 1st, 3rd, 5th, etc.. We'll call this an "odd number month". If we start adding commits on the 2nd, 4th, 6th, etc. we'll call this an "even number month".

If we start with January as an odd number month, the last day of the month (the 31st) will have commits. This means the next month, February, should be an even number month so that Jan 31st will have commits, Feb 1st will not, and Feb 2nd will, and so on.

Following this pattern, January will be an odd number month, february will be an even number month, and since the last day of February is the 28th, and the 28th will have commits, March will also be an even number month. The 1st of march should not have commits, but the 2nd should, and so on.

months with 31 days - 01 03 05 07 08 10 12

months with 30 days - 04 06 09 11

months with 28 days - 02

the formula should be as follows:

| month | type | end day |
| -- | -- | -- |
| 01 | odd | 31 |
| 02 | even | 28 |
| 03 | even | 31 |
| 04 | odd | 30 |
| 05 | odd | 31 |
| 06 | even | 30 |
| 07 | even | 31 |
| 08 | odd | 31 |
| 09 | even | 30 |
| 10 | even | 31 |
| 11 | odd | 30 |
| 12 | odd | 31 |

odd numbers, 30 days:

04 11

odd numbers, 31 days:

01 05 08 12

even numbers, 30 or 31 days:

03 06 07 09 10

even numbers, 28 days:

02


## The Script
(for non leap years)

replace `2017` with the year of your choice (if choosing a leap year, double check that the odd/even stuff is still correct)
```bash odds
for i in 1 2 3 4 5 6 7 8 9 10;
  for m in 04 11; # odd numbers, 30 days
    for d in 01 03 05 07 09 11 13 15 17 19 21 23 25 27 29;
      git commit -m 2017-$m-$d --date="2017-$m-$d 04:56:12" --allow-empty;
    end; git push;
  end;
  for m in 01 05 08 12; # odd numbers, 31 days
    for d in 01 03 05 07 09 11 13 15 17 19 21 23 25 27 29 31;
      git commit -m 2017-$m-$d --date="2017-$m-$d 04:56:12" --allow-empty;
    end; git push;
  end;
  for m in 03 06 07 09 10; # even numbers
    for d in 02 04 06 08 10 12 14 16 18 20 22 24 26 28 30;
      git commit -m 2017-$m-$d --date="2017-$m-$d 04:56:12" --allow-empty;
    end; git push;
  end;
  for m in 02; # february
    for d in 02 04 06 08 10 12 14 16 18 20 22 24 26 28;
      git commit -m 2017-$m-$d --date="2017-$m-$d 04:56:12" --allow-empty;
    end; git push;
  end;
end;
```
