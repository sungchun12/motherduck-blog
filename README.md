# MotherDuck + dbt: Better Together

## My Personal DuckDB Story
DuckDB has been charming to me ever since I wrote about it a year ago.
https://roundup.getdbt.com/p/dbt-learning-to-love-software-engineers

It gave me the glimmers of something I’ve been begging for a long time: fast should be measured in seconds, not minutes.

I kicked the tires a lot when working at dbt Labs. You see this here: https://github.com/dbt-labs/jaffle_shop_duckdb

And here:
https://www.loom.com/share/ed4a6f59957e43158837eb4ba0c5ed67

And most recently here: 
https://www.loom.com/share/e213768457094a3187663a6cff76a61d?sid=29d6d696-0581-4b50-af45-7132dfb65f80

And in all the tire kicking, it has remained true to the glimmers it gave me and so much more. It’s fast, easy, and cheap. And if it’s running on your local computer, it’s free. 

I’ve had incredibly asymmetric expectations of how much money, time, and work it takes to make data fast and easy that I think to myself, “Oh, of course you’re supposed to pay lots of dollars to run queries on millions/billions of rows per month.” This has pleasantly disrupted that inner anchoring point. I see something more charming at play. Data teams can be productive with data bigger and work faster and save more money than they could have dreamed of 5 years ago. Heck! Even a year ago. So let’s get into it.

## Why use MotherDuck + dbt?
Well, DuckDB and Motherduck’s primary use case is solving analytical problems fast. Because of its columnar design, it’s able to do just that. Even more so, the creators were smart about making integrations with adjacent data tools a first class experience. We see this with reading S3 files without copying them over and querying postgres directly without needing to extract and load it into DuckDB. And you don’t need to define schemas or tedious configurations to make it work! Motherduck enables the multiplayer experience that having a single file on your machine is too tedious to pass around and synchronize with your teammates. Motherduck runs DuckDB on your behalf AND uses your local computer if the query you’re running makes more sense to run there. You get a dynamic execution out of the box. And that’s pretty sweet.

But more than platitudes, let’s get hands-on with working code so you can taste and see for yourself!

You can follow along with this repo: https://github.com/sungchun12/jaffle_shop_duckdb/tree/blog-guide

1. Signup for a MotherDuck account! https://motherduck.com/
![signup](/images/motherduck_signup.png)

2. Sign in and your screen should look like this minus some of the stuff you’ll be building in the rest of this guide.
![signin](/images/signin.png)
