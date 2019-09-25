---
title: "The hard truth about testing with databases"
date: 2019-09-25T21:03:38+01:00
draft: false
toc: false
---
When your tests depend on a database, you accept (most times unintentionally) that they'll be slower, harder to maintain, and more fragile than your average unit tests.

For a start, you'll need an actual database to connect to, up and running and listening to the right port, with the correct permissions and the correct version of the schema.

You also need to make sure the state of the data is as expected _before each test_. You also need to ensure that tests are not interfering with each other because of data left behind.

Finally, you'll have to pay the price of the extra I/O for any test that hits your database. You may look at individual tests and decide they are "fast enough", but those are going to be still an order of magnitude slower than just accessing memory. 

Those issues get worse and worse as you keep adding tests.

The truth is: **you're probably using the database for far more tests than you should.**

Treat tests that hit a database like tests against an actual 3rd party system. They should care about the contract between your application and the database itself. They verify that the interactions (reading/writing your data) are correct, and nothing more.

All other tests that rely on the database should be using an in-memory replacement. 

If you're using an ORM framework that may be as simple as swapping the real database with an in-memory equivalent.

In other cases, it means introducing clear interfaces between database access and the rest of the application and using fake versions for testing.

Next time you see a test that uses a database, ask yourself: 

_Does this test relies on a particular piece of database technology, or it merely needs the ability to read/write to some storage?_

