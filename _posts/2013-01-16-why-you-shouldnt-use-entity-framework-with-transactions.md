---
layout: post
title:  "Why you shouldn't use Entity Framework with Transactions"
date:   2013-01-16 18:49:00
categories: Work DotNet
---

## EntityFramework

This is a .net ORM Mapper Framework from Microsoft to help you talking with your Database in an object oriented manner. [Wikipedia][1]

## Database Transaction

A database transaction, by definition, must be atomic, consistent, isolated and durable. Database practitioners often refer to these properties of database transactions using the acronym [ACID][2]. Transactions in a database environment have two main purposes:

  1. To provide reliable units of work that allow correct recovery from failures and keep a database consistent even in cases of system failure, when execution stops (completely or partially) and many operations upon a database remain uncompleted, with unclear status.
  2. To provide isolation between programs accessing a database concurrently. If this isolation is not provided, the program’s outcome are possibly erroneous. [Wikipedia][3]

## .NET Transactions

A .NET Transaction can be used in different ways by different frameworks to support transactions. The .NET Transaction itself is not connected with the database by any means. [MSDN][4]

## .NET Transactions and the EntityFramework

If you are using the Entity Framework during an opened TransactionScope, EntityFramework will open a new Transaction right with the next command that will be sent to the Database ([CRUD][5] Operation).

Consider this code block:

```
using (var transaction = new System.Transactions.TransactionScope())
{
    // DBC = Database Command

    // create the database context
    var database = new DatabaseContext();

    // search for the user with id #1
    // DBC: BEGIN TRANSACTION
    // DBC: select * from [User] where Id = 1
    var userA = database.Users.Find(1);
    // DBC: select * from [User] where Id = 2
    var userB = database.Users.Find(2);
    userA.Name = "Admin";

    // DBC: update User set Name = "Admin" where Id = 1
    database.SaveChanges();

    userB.Age = 28;
    // DBC: update User set Age = 28 where Id = 2
    database.SaveChanges();

    // DBC: COMMIT TRANSACTION
    transaction.Complete();
}
```

The `database.SaveChanges()` call sends your changes to the database and executes them but they are not really persisted because you are in the database transaction scope. `transaction.Complete()` actually finishes the database transaction and your data is saved.

That behavior is actually cool and very useful, right?

**NO. Absolutely not. full stop.**

## Why not using .NET Transactions along with EntityFramework

The default isolation mode is [`read committed`][6] and fits perfectly to 99% of your needs, eg. reading data. When you want to save the changes you made to the database (Create, Update, Delete), EntityFramework is smart enough to create a transaction without your notice behind the scenes to wrap the changes. You can be sure that everything will be saved or every change will be discarded ([Atomicity][7]).

By using transactions in EntityFramework, you change that behavior and force every [CRUD][5] operation during a transaction scope to be executed in [`serializable`][8] isolation mode which is the highest and most blocking type. No process will be able to access the tables you have touched (even reading from it) during your transaction. That can lead to [Deadlocks][9] pretty fast and you want to avoid them at all costs!

That’s how the code looks like without the explicit usage of transactions:

```
// DBC = Database Command

// create the database context
var database = new DatabaseContext();

// search for the user with id #1
// DBC: select * from [User] where Id = 1
var userA = database.Users.Find(1);
// DBC: select * from [User] where Id = 2
var userB = database.Users.Find(2);
userA.Name = "Admin";
userB.Age = 28;

// DBC: BEGIN TRANSACTION
// DBC: update User set Name = "Admin" where Id = 1
// DBC: update User set Age = 28 where Id = 2
// DBC: COMMIT TRANSACTION
database.SaveChanges();
```

**_Rule of Thumb: Save only once per task and don’t use transactions._**

Edit: One thread should have access to one instance of DbContext which works best in web applications where every request acts as one thread. In windows applications every command or task should have one DbContext which is not shared. If you share the DbContext between threads you might run into issues like having reads sneaked into a foreign transaction.

   [1]: https://en.wikipedia.org/wiki/Entity_framework
   [2]: https://en.wikipedia.org/wiki/ACID
   [3]: https://en.wikipedia.org/wiki/Database_transaction
   [4]: http://msdn.microsoft.com/en-us/library/system.transactions.transaction.aspx
   [5]: https://en.wikipedia.org/wiki/Create,_read,_update_and_delete
   [6]: https://en.wikipedia.org/wiki/Isolation_%28database_systems%29#Read_committed
   [7]: https://en.wikipedia.org/wiki/Atomicity_(database_systems)#Atomicity_(database_systems)
   [8]: https://en.wikipedia.org/wiki/Isolation_(database_systems)#Serializable
   [9]: https://en.wikipedia.org/wiki/Deadlock
