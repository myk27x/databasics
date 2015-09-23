## Databasics

Fork this repository into your own github profile.

Before closing the homework assignment issue:

- Update this README as follows:
  - [√] For each question (just after or below the question itself) include the SQL you wrote to generate the answer
  - [√] For each question (just after or below the question itself) include the *answer* to the question asked.

- Also:
  - [√] Commit the updated `store.sqlite3` database file
  - [√] Include a link to your forked repo in the comments when closing the issue.


NOTE: To run sqlite with this database: `sqlite3 store.sqlite3`

NOTE: You may want to keep a backup of the `store.sqlite3` file in case you damage the file. *OR* you can use the command `git checkout store.sqlite3` to undo any changes to the database file since the fork or your last commit.

## Explorer Mode

- [√] How many users are there?
      code: select count(first_name) from users;
      answer: 50

- [√] What are the 5 most expensive items?
      code: select title from items order by price desc limit 5;
      answer: Small Cotton Gloves
              Small Wooden Computer
              Awesome Granite Pants
              Sleek Wooden Hat
              Ergonomic Steel Car

- [√] What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
      -code: select title from items where category = "Books" order by price asc limit 1;
      -answer: Ergonomic Granite Chair
      -code: select title from items where category like "%book%" order by price asc limit 1;
      -answer: no

- [√] Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
      -code: select first_name, last_name from [users] join addresses on [users].id = user_id where street = "6439 Zetta Hills";
      -answer: Corrine|Little
      -code: select first_name, last_name, street from [addresses] join users on [addresses].user_id = users.id where first_name = "Corrine";
      -answer: Yes, 54369 Wolff Forges.

- [√] Correct Virginie Mitchell's address to "New York, NY, 10108".
      -code: update addresses set city = "New York", state = "NY", zip = "10108" where user_id in (select id from users where first_name = "Virginie");

- [√] How much would it cost to buy one of each tool?
      -code: select sum(price) from items where category = 'Tools';
      -answer: 7383
      *UNLESS* each item in a tools type category counts, then:
      -code: select sum(price) from items where category like '%tool%';
      -answer: 46477

- [√] How many total items did we sell?
      -code: select sum(quantity) from orders;
      -answer: 2125

- [√] How much was spent on books?
      -code: select sum(price * quantity) from [items] join orders on [items].id = item_id where category = "Books";
      -answer: 420566
      *UNLESS* each item in a books type category count as a book:
      -code: select sum(price * quantity) from [items] join orders on [items].id = item_id where category like "%book%";
      -answer: 1081352

- [√] Simulate buying an item by inserting a User for yourself and an Order for that User.
      -code: insert into users (first_name, last_name, email) values ('Michael', 'Reed', 'myk27x@yahoo.com');
        *added self to users*
      -code: insert into addresses (user_id, street, city, state, zip) values (51, '5186 Foxbridge Cir. N #36', 'Clearwater', 'FL', 33760);
        *added self to addresses*
      -code: insert into orders (user_id, item_id, quantity, created_at) values (51, 22, 1, '2015-09-23 00:54:27:143027');
        *added self to orders*
      *??? shouldn't there be a way to do this in one line ???*

## Adventure Mode

- [ ] What item was ordered most often? Grossed the most money?
- [ ] What user spent the most?
- [ ] What were the top 3 highest grossing categories?
