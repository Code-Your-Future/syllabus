# WEEK 16 LESSON 1 : BASIC SQL

**What we will learn today?**

* Why we need databases
* Installing Postgres
* Creating a database with SQL and storing data in it.
* Inserting data into a database using SQL.
* Retrieving data from a database using SQL.
* Escaping

## LESSON 1A: Why we need databases

So, in your previous lessons you have been taught how to store and retrieve data
using files. This is fine and works well for some data - particularly simple data -
but it can quickly cause issues when you have a *lot* of data and *complicated* data.

TEACHER STORY:

Back in 2013 I used to work for a company that ran hotel wifi for big hotel chain.
We did at least 4 big brands that you've probably heard of and a whole bunch of others.
This company had been going for a long time and used to make $8 when, back in the dark
ages, you paid $12 for a day of wifi.

The code for this system had the notion of "invoices", "wifi enrollments" and "guests" and
stored data on each of them as well as the links between them. We would store data about
these things and we would run reports on each and send them to the hotels who would
use them to bill guests.

All normal so far. Except we would sometimes send reports with invoices which didn't
have enrollments, and enrollments which didn't have guests.

Sometimes the amounts on those invoices would rack up to tens even hundreds of thousands of dollars of invoices *without* customers, and the hotel managers were rarely happy:

<!-- ![Hotel manager](grumpy-cat.jpg "Hotel manager's face") -->
<p align="center">
  <img src="grumpy-cat.jpg" display="block" width="75%"/>
</p>

This was a very, very serious problem. We were >.< this close to losing a big hotel chain as a customer - and a large part of it was because of this.

This was a problem because our system was buggy, so we had what are generally called "data integrity" issues. You've encountered bugs before on this course - data integrity issues bugs too - bugs with your data.

The difference between a bug in your code and a bug in your data, caused by a bug in your code, is that bugs in your code can always be fixed. Bugs in your data - sometimes they can never be fixed.

These lessons are about using SQL and storing and retrieving data in your code in such a way that your data is kept clean.


## LESSON 1B : What is the point of an SQL database?

We're going to teach you a new programming language. It's called SQL. Pronounced "S - Q - L" or sequel, either is fine.

Databases are simply programs that take data and stuff it in files just like you were doing in the previous lesson.

However, the way we use a database is different to the way we store things in files. In a file, you can put any random jumble of data in and get it out again. How you put it in and get it out is up to you. Your code needs to open the file, close the file, retrieve, store or modify and validate everything itself. Offloading some of that responsibility to another program means that your code can achieve all the same things but be simpler.

You interact with almost all of them using the same programming language which is called "SQL". It's been around for 31 years and is still completely dominant. Computing moves fast, but SQL doesn't change. This kind of lesson will probably still be taught in 50 years. Probably 4 out of 5 software jobs involve SQL In some way.

SQL is a different, and usually simpler kind of programming language that you use *with* a database (sometimes called an RDBMS) to:

- Store data in a way such that its structure cannot be violated.
- Retrieve data (get me all the reservations under the name "Trump") and answer questions about data ("what was the sum total of all of the invoices in february?").

An RDBMS (relational database management system) will do this by, for example:

- Data constraints (e.g. each reservation *must* have a customer)
- Data types (e.g. check in date *can only* be a date)
- Uniqueness of certain pieces of data (e.g. there is *only one* person with the driver's license ID 941413).
- Organizing how the data is retrieved and assembled (e.g. fetch me all reservations under customer "Donald Trump").
- Executes on a different process/machine, meaning that the queries can be parallelized, and work can be offloaded from the main server.


### SHOULD I USE SQL OR SHOULD I USE NOSQL?

My short answer: if in doubt, I would just use SQL. Always.

Long answer: There are two forms of NoSQL.

1) Extremely high scale -- terabytes upon terabytes of data and tens of people working just on handling the database -- the canonical example is Cassandra --- constraints are not enforced *due to extremley high loads and high levels of data*. Some companies like Netflix, Google do this. 99% of tech companies do not.

2) For beginner programmers - Mongo --- constraints (among other features) are not there *to simplify things for beginners*. This means it will be quicker to build your project but you face a higher risk of data integrity issues
once you do and shifting from mongo to an SQL database once you're deep into a project is tricky.


#### EXERCISE 1B: INSTALLING POSTGRES ON YOUR LAPTOP AND CREATING YOUR FIRST DATABASE

The RDBMS we are going to teach you is called "postgresql" (pronounced postgres-q-l) or
"postgres". It's one of the most popular free, open source databases and if you end
up becoming web developers it's highly likely that you will be using it. We will be
using version 11 although for straightforward databases you will probably not notice
much of a difference for anything over version 9.

### FOR MAC OS USERS:

1. Go to https://postgresapp.com
2. Go to the Downloads tab
3. Download the latest version
4. Open the downloaded file
5. Drag the app to Applications folder
6. Got to the Applications folder
7. Open Postgres
8. Click the Open button in the popup
9. Click the Initialize button
10. Run the following in the terminal:

>> psql -d template1

You should see:

```
postgres=#
```

To quit, run "\q".


### FOR MAC OS USERS:

To set up on Linux you need to do the following:

>> sudo apt-get install postgresql

>> whoami
gareth

Replace gareth with whatever your username is, e.g.:

>> sudo -u postgres createuser gareth --superuser --no-password -d

If you run this command

>> psql -d template1

You should have a command prompt like follows:

```
postgres=#
```

To quit, run "\q"



## LESSON 1C: CREATING A TABLE

The first thing we want to store is customers, since without customers, you don't have a hotel.

First, open a file in any text editor and put the following in a file called 'hotel.sql':

```sql
drop database if exists mydb;

create database mydb;

\connect mydb;

create table customers (
    title varchar,
    firstname varchar,
    surname varchar
);

insert into customers (title, firstname, surname) values ('Mr', 'Donald', 'Trump');
```

What we have here:

* Dropping a database - if a database named `mydb` already exists, this removes it so that we can make a new one with that name.
* Creating a database - this creates a new database that for you to use.
* Connecting to a database - this tells Postgres to work with our new databse.
* Creating a table - this creates the *structure* which you can use to put data in. The items are *columns*.
* Insert into - puts data *into* that structure.
* 'title varchar' - this means we're creating a column with the name 'title' which holds a 'variable number of characters'. This is pretty much the same thing as a string in javascript.

Now, in the command prompt run the following:

```
$ psql -f hotel.sql
```

Now the file has been loaded with one table containing one row of data. Open the Postgres command line with the new databse like this:

```
$ psql -d mydb
```

Then read the rows of data out like this:

```sql
select * from customers;
```

This should display:

```
postgres=# select * from customers;
 title | firstname | surname 
-------+-----------+---------
 Mr    | Donald    | Trump
(1 row)
```


#### EXERCISE 1C: Create tables and insert data

1. Amend hotel.sql to create the database again and add yourselves as *second* customer using INSERT - so you're now staying in a hotel with Donald Trump. Run `select * from customers;` and ensure that you see yourself both as guests.

2. Change hotel.sql again to store email addresses from yourself and Donald (donald.trump@whitehouse.gov) and have them displayed on screen. Select everything again, and ensure you are both guests.

3. Change hotel.sql again. Add the CYF mentor "Colm OConner" as your third customer. His email address is "colm.oconner.github@gmail.com".

## LESSON 1D: Data types and directives

Add this at the end of `hotel.sql`:

```sql
create table invoices (
    id                  integer,
    total               decimal,
    invoice_date_time   timestamp not null,
    paid                boolean default false
);

insert into invoices (id, total, invoice_date_time, paid) values (123, 3444.50, '2017-01-01', true);

insert into invoices (id, total, invoice_date_time) values (124, 3445.50, '2017-01-02');
```

Run the file, open the Postgres command box, and enter this:

```sql
select * from invoices;
```

What we have here:

* An 'integer', a 'decimal', a 'timestamp' and a 'boolean'. These are all analogous to data types which you have learned about in javascript.

* For "paid" which is either yes (`true`) or no (`false`) - we have a default of no (`false`)- it's saying that if you insert data and don't specify 'paid' as a column when you INSERT data, it will assume you meant 'no'.

* For 'invoice_date_time' you must store the data in the form of a combination of date and time. It has a 'not null' constraint which means that you *have* to give a timestamp when you insert data, it will refuse to let you insert an invoice without specifying invoice_date_time and refuse to let you explicitly give your invoice_date_time as null.

<!-- ![postman-get-1](postman-get-1.png) -->
<p align="center">
  <img src="perfect-date.png" display="block" width="85%"/>
</p>

For the sake of simplicity we will be using the `YYYY-MM-DD` date format.


Further reading on Postgres types  [here](https://www.postgresql.org/docs/current/datatype.html).


#### EXERCISE 1D : Data types and directives

In your "hotel.sql" create a reservations table with columns for customer ID, room ID, check in date, check out date and price per night and insert a bunch of example data - maybe you and 10 friends or celebrities.

The hotel manager has told you:

- Customers *do* have to give a check in date, but they don't have to give a check out date.
- Reservations need a customer ID and a room ID
- Reservations have a check in date, a check out date and a price per night.

## LESSON 1E : SELECT

Currently we've just put data in to a table and gotten *all* of it out. What about if we only want *specific* data?

For this we will introduce a SQL key word called 'WHERE'.

Lets go back to the invoices table and add a bunch of data.
Replace the previous insert statements for invoices with the following ones:

```sql
insert into invoices (id, total, invoice_date_time, paid) values (123, 143.50, '2017-01-01', true);

insert into invoices (id, total, invoice_date_time) values (124, 250.50, '2017-01-02');

insert into invoices (id, total, invoice_date_time) values (150, 431.50, '2017-01-03');

insert into invoices (id, total, invoice_date_time, paid) values (155, 300.50, '2017-01-04', true);

insert into invoices (id, total, invoice_date_time, paid) values (156, 284.35, '2017-01-04', true);
```

So, if you do a regular query you just get all of the data:

```sql
select * from invoices;
```

But you can filter the data through logical expressions like:

```sql
select * from invoices where id = 123;
```

or:
```sql
select * from invoices where invoice_date_time < '2017-01-03';
```

#### EXERCISE 1F : SELECT

Write SQL for the following:

1. Which invoices were paid?

2. Which invoices were for under 300 pounds?

3. Which invoices paid on 3rd January 2017 or after?


## LESSON 1G : Primary Keys

Ok, now we're going to introduce a problem. Let's say a secretary types in a bunch of invoice IDs and values:

```sql
insert into invoices (id, total, invoice_date_time, paid) values (323, 143.50, '2017-01-01', true);

insert into invoices (id, total, invoice_date_time) values (323, 250.50, '2017-01-02');
```

QUESTION FOR CLASS : What is the problem here? [ A business calls up and says they need to pay invoice 323 ]

We solve this problem with something called a "primary key" - what this does is make it so the database will refuse to accept a value that is already in the database, it will not accept duplicates. We can define a primary key for the `id` adding `primary key` after the type for `id` as follows:

```sql
create table invoices (
    id                  integer primary key,
    total               decimal,
    invoice_date_time   timestamp not null,
    paid                boolean default false
);

insert into invoices (id, total, invoice_date_time, paid) values (323, 143.50, '2017-01-01', true);
```

Update your hotel.sql file to have the invoices table defined as above.

Try entering an invoice with ID 323 now, what do you get?

```sql
mydb=# insert into invoices (id, total, invoice_date_time) values (323, 250.50, '2017-01-02');
ERROR:  duplicate key value violates unique constraint "invoices_pkey"
DETAIL:  Key (id)=(323) already exists.
```

Now, picking primary keys is a tricky problem. You need to make sure that you pick some kind of identifier which you know will always be *unique*.


QUESTIONS FOR CLASS:

* Is first name a good candidate for a primary key?
* Is first name and surname together a good candidate for a primary key?
* Is a driver's license ID a good candidate for a primary key? [ if and only if everybody is from the same country ]
* Is a passport ID a good candidate for a primary key? [ if and only if everybody is from europe ]
* Is just coming up with an arbitrary number that is unique a good candidate for a primary key?

## LESSON 1H: AUTOINCREMENTING PRIMARY KEYS

We still have a problem here. Joe the office manager who is entering invoices doesn't really want to keep coming up with random numbers every time he enters an invoice. Why not just get the database to give us an ID?

We can do that with a magic feature called serial numbers. You don't specify the ID and the database will just give your row a new ID. What ID will it give it? The ID of the last row plus one.

```sql
create table invoices (
    id                  serial primary key,
    total               decimal,
    invoice_date_time   timestamp not null,
    paid                boolean default false
);

insert into invoices (total, invoice_date_time, paid) values (143.50, '2017-01-01', true);

insert into invoices (total, invoice_date_time) values (250.50, '2017-01-02');
```

#### EXERCISE 1H : PRIMARY KEYS

1. Update yout hotel.sql file to account for the serial ids on the `invoices` table. Meaning, remove the id from the insert, because they should be automatically added now.

2. Recreate customer table with a primary key. Bear in mind that you don't have a driver's license or passport ID. Update all the insert statements for `customers` to not specify the id.


## LESSON 1I : FOREIGN KEYS

Now, as we've seen two tables that have an intrinsic relationship to one another. Every invoice has a reservation ID.


```sql
create table invoices (
    id                  serial primary key,
    reservation_id      integer,
    total               decimal,
    invoice_date_time   timestamp not null,
    paid                boolean default false
);

create table reservations (
    id                    serial primary key,
    customer_id           integer,
    room_id               integer,
    check_in_date         timestamp not null,
    check_out_date        timestamp,
    room_price_per_night  decimal
);

insert into reservations (customer_id, room_id, check_in_date, check_out_date, room_price_per_night) values (123, 55, '2017-01-01', '2017-01-02', 100);

insert into reservations (customer_id, room_id, check_in_date, check_out_date, room_price_per_night) values (124, 55, '2017-01-03', '2017-01-05', 100);

insert into invoices (reservation_id, total, invoice_date_time, paid) values (123, 100, '2017-01-03', true);

insert into invoices (reservation_id, total, invoice_date_time, paid) values (124, 50, '2017-01-06', false);

insert into invoices (reservation_id, total, invoice_date_time) values (124, 50, '2017-01-06');
```

Point out that the reservation ID corresponds with the ID on the reservations table.

```sql
insert into invoices (reservation_id, total, invoice_date_time) values (125, 50, '2017-01-06');
```

QUESTION FOR CLASS: What's the problem with the last statement?

A: Invoice isn't going to get paid because we don't know who it's for.

To fix this problem we place an additional restriction on the data
- you can only add IDs that *exist* to columns referencing other tables
- and you really need to specify the `reservation_id` when you are inserting on the invoices.


```sql

create table reservations (
    id                    serial primary key,
    customer_id           integer,
    room_id               integer,
    check_in_date         timestamp not null,
    check_out_date        timestamp,
    room_price_per_night  decimal
);

create table invoices (
    id                              serial primary key,
    reservation_id                  integer not null,
    total                           decimal,
    invoice_date_time               timestamp not null,
    paid                            boolean default false,
    foreign key(reservation_id)     references reservations(id)
);

```

Now, if you try to add invoices without a `reservation_id` that really references a reservation entry on the reservations table you'll get this:

```sql
mydb=# insert into invoices (reservation_id, total, invoice_date_time) values (125, 50, '2017-01-06');
ERROR:  insert or update on table "invoices" violates foreign key constraint "invoices_reservation_id_fkey"
DETAIL:  Key (reservation_id)=(125) is not present in table "reservations".
```

Or, if you try to add an invoice without specifying the `reservation_id` at all:

```sql
mydb=# insert into invoices (total, invoice_date_time) values (50, '2017-01-06');
ERROR:  null value in column "reservation_id" violates not-null constraint
DETAIL:  Failing row contains (5, null, 50, 2017-01-06 00:00:00, f).
```

Note that:

- 'foreign key(reservation_id)' means that we're putting a foreign key relationship on the *reservation_id* column.
- 'references reservations(id)' means that it's referring to the 'id' column in the reservations table.
- reservation_id is a column on invoices. It is a number, like 3 - referring to the 'id' of a row in reservations.
- reservation_id can *not* be null because it must *always* reference an existing row.

Remember:

- If you removed "foreign key(reservation_id) references reservations(id)" it will let you insert invalid data without giving you an error - you won't be able to create an invoice with a reservation_id of 9435454 without a corresponding reservation with id 9435454 in the reservations table.

- We WANT errors like this, which is why we put the foreign key there.

#### EXERCISE 1I : Foreign keys

1. Change the `hotel.sql` file to respect the `foreign keys` and `not null` constraints on the invoice insert statements.

2. Change the file to add foreign key relationship for reservations table and customers table; update the insert statements accordingly; and add more data for those tables.


## LESSON 1J : Updating data

Let's say that we made a mistake with one of the invoices created above.

First get the ID of an invoice entered earlier:

```sql
select * from invoices where invoice_date_time = '2017-01-03';
```

If you want to change this invoice to be £300, you need to use 'UPDATE'.

```sql
update invoices set total = 300.0 where id = 1;
```

#### EXERCISE 1J : Updating data

1. Run SQL from lesson 1C where Colm's surname was entered as OConner. His name is actually O'Connor. Fix it using 'UPDATE'.

# HOMEWORK


### Homework part 1: Setting up the environment for next class

You have already worked with back end servers using Express. This is just another yet another one that we will be connecting to a database.

In order for us to interact with the server, we are going to use [Postman](https://www.getpostman.com/), which will accurately mimic API calls made from react. In the last three lessons you're going to make react do to this back end what postman is going to do today.


**Task** Fork and then clone the [repo](https://github.com/CodeYourFuture/cyf-hotel-db), and follow the instructions to set up and environment.

**Task** Install chrome extention for [Postman](https://chrome.google.com/webstore/detail/tabbed-postman-rest-clien/coohjcphdfgbiolnekdpbcijmhambjff?hl=en-GB).

<!-- ![postman-get-1](client-postman-server.jpg) -->
<p align="center">
  <img src="client-postman-server.jpg" display="block" width="60%"/>
</p>



<!-- ![postman-get-1](postman-get-1.png) -->
<p align="center">
  <img src="postman-get-1.png" display="block" width="85%"/>
</p>

Run "npm start" and use postman to GET from `http://localhost:8080/api/customers` and email a screenshot
to ams.pedro@gmail.com and crdoconnor@gmail.com.

If you have any issues (and you might), please contact one of us or the mentors for help.

### Homework part 2: Add tables and data to the hotel database

Using what you have learned in today's lesson, extend database/schema.sql in the cyf-hotel-db repo you
just set up.

It currently contains a customers table with one customer in it:

    CREATE TABLE IF NOT EXISTS customers (
      ID INTEGER PRIMARY KEY AUTOINCREMENT,
      title TEXT(16),
      first_name TEXT(64) NOT NULL,
      surname TEXT (64) NOT NULL,
      email TEXT (64)
    );


    INSERT INTO customers (
      title, first_name, surname, email
    ) VALUES (
      'Mr',
      'John',
      'Dove',
      'john.doe@domain.com'
    );


Extend it so that it has a structure like so (each line is a foreign key):

<!-- ![postman-get-1](postman-get-1.png) -->
<p align="center">
  <img src="hotel-er-diagram.png" display="block" width="85%"/>
</p>

As well as creating the database tables that create that structure, add insert statements for
5-10 rows of example data for each table as well.

Email your amended schema.sql to to ams.pedro@gmail.com and crdoconnor@gmail.com.
