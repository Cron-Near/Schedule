# cron_schedule
A cron expression parser, adapted for blockchain environments.

```rust
extern crate cron_schedule;
extern crate chrono;

use cron_schedule::Schedule;
use chrono::Utc;
use std::str::FromStr;

fn main() {
  //               sec  min   hour   day of month   month   day of week   year
  let expression = "0   30   9,12,15     1,15       May-Aug  Mon,Wed,Fri  2021/2";
  let schedule = Schedule::from_str(expression).unwrap();
  println!("Upcoming fire times:");
  for datetime in schedule.upcoming().take(10) {
    println!("-> {}", datetime);
  }
}

/*
Upcoming fire times:
-> 2021-06-01 09:30:00 UTC
-> 2021-06-01 12:30:00 UTC
-> 2021-06-01 15:30:00 UTC
-> 2021-06-15 09:30:00 UTC
-> 2021-06-15 12:30:00 UTC
-> 2021-06-15 15:30:00 UTC
-> 2021-08-01 09:30:00 UTC
-> 2021-08-01 12:30:00 UTC
-> 2021-08-01 15:30:00 UTC
-> 2021-08-15 09:30:00 UTC
*/
```

## Shorthand Support
This cron expression parser also supports shorthand notations for time intervals:
- `@yearly` (equivalent to `0 0 0 1 1 * *`)
- `@monthly` (equivalent to `0 0 0 1 * * *`)
- `@weekly` (equivalent to `0 0 0 * * 1 *`)
- `@daily` (equivalent to `0 0 0 * * * *`)
- `@hourly` (equivalent to `0 0 * * * * *`)

## License

MIT license ([LICENSE](LICENSE) or http://opensource.org/licenses/MIT)

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you shall be dual licensed as above, without any
additional terms or conditions.
