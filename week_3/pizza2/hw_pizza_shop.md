# Homework: Pizza Shop

## Today

Today we created a program that tracks pizza orders. We created a Ruby class (`PizzaOrder`) and a database table (pizza\_orders) which is able to persist objects of this type. Currently, our database table is structured as follows...

| first_name | last_name | topping         | quantity |
|------------|-----------|-----------------|----------|
| Luke       | Skywalker | Pepperoni       | 2        |
| Leia       | Organa    | Ham & Pineapple | 1        |

Our table stores a combination of pizza and customer details. This isn't ideal for a number of reasons. If a single customer makes many orders then their details appear in our database many times. Firstly, this is not efficient. It would be much nicer if we could create a customer once and then attribute many orders too them. This would also help to protect us against typos as we would only have to submit a new customer once.

## Tomorrow

Tomorrow we are going to refactor our program. We will add another class, `Customer`, which will also have the full set of CRUD actions. This class will be responsible for the customer details, while `PizzaOrders` will be responsible for the pizza order that is being processed.

We will also extract some of the database connection code into a new class, `SqlRunner`.

Once completed, our tables should be structured as follows...

### customers

| id | first_name | last_name |
|----|------------|-----------|
| 1  | Luke       | Skywalker |
| 2  | Leia       | Organa    |

### pizza_orders

| id | topping         | quantity | customer_id |
|----|-----------------|----------|-------------|
| 1  | Pepperoni       | 2        | 1           |
| 2  | Ham & Pineapple | 1        | 2           |
| 3  | Meat Feast      | 1        | 1           |

## Task

Your task this evening is to read over the completed end\_code for tomorrow's lesson, understand it as much as possible, and answer the following questions.

1) What is the relationship between customers and pizza\_orders?

one to many

2) At what point is the id of a `PizzaOrder` created?

When SqlRunner executes the prepared SQL statement to save the Pizza Order into the database, the database creates a unique id for the order.

3) At what point do we assign a value to the `@id` instance variables of our objects?

When SqlRunner returns the result of the save query, the PizzaOrder class's save function extracts the id value from the array of hashes and assigns it to the instance variable @id. The same thing happens when a Customer is saved to the database, but using the Customer class's save function.

4) Name 2 things that the `Customer`'s `@id` property is used for.

1: searching the database to find all the customer's pizza orders, in the Customer class's pizza_orders function.

2: deleting a customer found by their id, using the Customer class delete function

5) Why might it be important to check if `options['id']` is `nil` in our `initialize` method before assigning `@id` the value of `options[‘id’].to_i?`

Because if you try to convert nil to an integer there will be an error and the program will stop running.

6) What are the responsibilities of `SqlRunner`?

SqlRunner connects to the database, executes preprepared SQL queries, closes the database and returns the results of the queries.

7) How does `SqlRunner` improve the quality of our code?

If any changes need to be made to the database connection, they can all be made in one place. Also this is more likely to prevent mistakes, eg by ensuring the database is always closed again after use.
