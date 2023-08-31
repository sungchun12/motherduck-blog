# MotherDuck + dbt: Better Together

## My Personal DuckDB Story
DuckDB has been charming to me ever since I wrote [about it a year ago](https://roundup.getdbt.com/p/dbt-learning-to-love-software-engineers).

It gave me the glimmers of something I’ve been begging for a long time: fast should be measured in seconds, not minutes.

[I kicked the tires a lot when working at dbt Labs](https://github.com/dbt-labs/jaffle_shop_duckdb).

- [And here](https://www.loom.com/share/ed4a6f59957e43158837eb4ba0c5ed67)


- [And most recently here](https://www.loom.com/share/e213768457094a3187663a6cff76a61d?sid=29d6d696-0581-4b50-af45-7132dfb65f80)

And in all the tire kicking, it has remained true to the glimmers it gave me and so much more. It’s fast, easy, and cheap. And if it’s running on your local computer, it’s free. 

I’ve had incredibly asymmetric expectations of how much money, time, and work it takes to make data fast and easy that I think to myself, “Oh, of course you’re supposed to pay lots of dollars to run queries on millions/billions of rows per month.” This has pleasantly disrupted that inner anchoring point. I see something more charming at play. Data teams can be productive with data bigger and work faster and save more money than they could have dreamed of 5 years ago. Heck! Even a year ago. So let’s get into it.

## Why use MotherDuck + dbt?
Well, DuckDB and Motherduck’s primary use case is solving analytical problems fast. Because of its columnar design, it’s able to do just that. Even more so, the creators were smart about making integrations with adjacent data tools a first class experience. We see this with reading S3 files without copying them over and querying postgres directly without needing to extract and load it into DuckDB. And you don’t need to define schemas or tedious configurations to make it work! Motherduck enables the multiplayer experience that having a single file on your machine is too tedious to pass around and synchronize with your teammates. Motherduck runs DuckDB on your behalf AND uses your local computer if the query you’re running makes more sense to run there. You get dynamic execution out of the box. And that’s pretty sweet.

But more than platitudes, let’s get hands-on with working code so you can taste and see for yourself!

## Get Started

You can follow along with this repo: https://github.com/sungchun12/jaffle_shop_duckdb/tree/blog-guide

1. Signup for a MotherDuck account! https://motherduck.com/
![signup](/images/motherduck_signup.png)

2. Sign in and your screen should look like this minus some of the stuff you’ll be building in the rest of this guide.
![signin](/images/signin.png)

3. Click on the settings in the upper right hand corner and copy your Service Token to the clipboard.
![signin](/images/service_token.png)

4. Clone the repo and change directories into it.

```bash
git clone -b blog-guide https://github.com/sungchun12/jaffle_shop_duckdb.git
cd jaffle_shop_duckdb
```

5. Follow the detailed instructions to setup your free AWS account and use S3: https://docs.aws.amazon.com/AmazonS3/latest/userguide/GetStartedWithS3.html

> Note: Feel free to skip this step if you already have an AWS account with S3 setup!

6. Take the csv files stored in the git repo here and upload them into S3: https://github.com/sungchun12/jaffle_shop_duckdb/tree/blog-guide/seeds
![signin](/images/seeds.png)
![signin](/images/s3_seeds.png)

7. Copy the AWS S3 access keys to authenticate your dbt project for later: https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html 

## Configure Your dbt project
> Note: Huge thanks to Josh Wills for creating the dbt-duckdb adapter and it works great with both DuckDB and MotherDuck: https://github.com/jwills/dbt-duckdb. This demo only works with DuckDB version 0.8.1: https://motherduck.com/docs/intro

1. Adjust your `profiles.yml` for the naming conventions that make sense to you. Specifically, focus on schema. 

```yaml
jaffle_shop:

  target: dev
  outputs:
    dev:
      type: duckdb
      schema: dev_sung
      path: 'md:jaffle_shop'
      threads: 16
      extensions: 
        - httpfs
      settings:
        s3_region: us-west-1
        s3_access_key_id: "{{ env_var('S3_ACCESS_KEY_ID') }}"
        s3_secret_access_key: "{{ env_var('S3_SECRET_ACCESS_KEY') }}"

    prod:
      type: duckdb
      schema: prod_sung
      path: 'md:jaffle_shop'
      threads: 16
      extensions: 
        - httpfs
      settings:
        s3_region: us-west-1
        s3_access_key_id: "{{ env_var('S3_ACCESS_KEY_ID') }}"
        s3_secret_access_key: "{{ env_var('S3_SECRET_ACCESS_KEY') }}"
```

2. Export your motherduck and S3 credentials to the terminal session, so your dbt project can authenticate to both

```shell
# all examples are fake
export motherduck_token=<your motherduck token> # aouiweh98229g193g1rb9u1
export S3_ACCESS_KEY_ID=<your access key id> # haoiwehfpoiahpwohf
export S3_SECRET_ACCESS_KEY=<your secret access key> # jiaowhefa998333
```

3. Create a python virtual environment and install the packages to run this dbt project

```shell
python3 -m venv venv
source venv/bin/activate
python3 -m pip install --upgrade pip
python3 -m pip install -r requirements.txt
```

4. Run `dbt debug` to verify dbt can connect to motherduck and S3

```shell
dbt debug
```

5. Run `dbt build` to run and test the project!

```shell
dbt build
```

6. Now, you should see everything ran with green font everywhere and you should see this in the UI! Including the S3 data you built a dbt model on top of!

![signin](/images/green_logs.png)
![signin](/images/motherduck_success.png)



That’s it! Ruffle up those feathers and start quacking and slapping those juicy SQL queries together to solve your analytics problems faster and cheaper than ever before!

## Conclusion

We’re at a really cool place where all I had to give you was a couple instructions to get you up and running with MotherDuck. I really hope the data industry gets to a place where we brag about the things we do NOT have to do vs. pride ourselves on complexity for its own sake. What matters is that we solve problems and spend time, money, and energy doing it where it’s actually worth it to solve those problems. I’m excited to see you all build MotherDuck guides far superior to mine. That’s why this is so fun. We get to sharpen each other!
