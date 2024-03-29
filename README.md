
# The challenge:

We want to get a simple shopping cart. For this, we need to build a NodeJs application that allows us to
* Ask for available products.
* Add or delete products to and from the cart.
* Check at all times the available stock.
* **Extra:** It's good to know what the best products to buy are, or maybe the best sold products in the store.

## What you have to code

* A NodeJs application with all endpoints to solve our exercise.
* Postman collection file.
* Extra: We will be so happy if you can make the solution oriented to a microservices architecture.

## Skills we are going to assert:

**General coding skills:**

* How readable your code is
* How you structure your code

**Modeling skills:**

* Which model you create to solve the problem

**Problem solving skills:**

* How you solve logical problems
* How you use the tools the language provides
* How well you know the best practices of the language
* Which patterns you put in practice
* Which best practices you use
* Basic git skills, how you organize the changes.


**Skills we are NOT going to assert:**

* Page load performance optimization
* Extra features we did not ask for our application

## How to start with the exercise

To start with the exercise you need to run this command to build the Docker containers

    ./up.sh
If you want to load some example products you can use our seeders:

    ./seeders.sh

---------------------------------------------------------------------------------------

# Solution:

## Proposal

To solve the described challenge, I am going to use a MongoDb database with two collections and a set of API endpoints built in Node.js.
The main idea is to have a CRUD of Products, and the ability of add and delete those to Orders. In addition, the API have to be able to obtain the "best seller" products.
The collections and API endpoints are described in the following sections. 

## Collection description

### Product:

This collections stores product information, below collection attributes are described.
* title: Product title.
* description: Product description.
* price: Product price.
* stock: Available quantity of a product.

### Order:

This collections stores order information, below collection attributes are described.
* creationDate: Order creation date.
* closedDate: Order checkout date.
* status: Represents the actual status of a order, it can be 'open' or 'closed'.
* total: Total order amount.
* items [ {product, quantity} ]: Array of products in a order and the corresponding quantity of each one.

## API endpoint description

What follows are a list and description of the API endpoints developed for this project.

### Products

#### GET  /products
Get all products.

#### GET  /products/:id
Get a product specified by id.

#### POST  /products
Create a product with parameters: `title`, `description`, `price`, `stock`.

#### DELETE  /products/:id
Delete a product specified by id.

#### PATCH  /products/bestSeller
Get a list of 'Best Sellers' products. It just counts products in 'Closed' orders.

### Orders

#### GET  /orders
Get all orders.

#### GET  /orders/:id
Get a order specified by id.

#### POST  /orders
Create a new order.

#### DELETE  /orders/:id
Delete a order specified by id.

#### POST  /orders/:id/products
Add product specified in body request with `id` and `quantity` to order given by id.

#### DELETE  /orders/:id/products/:idProduct
Delete product specified in body request with `id` to order given by id.

#### GET  /orders/:id/checkout
Checkout a order specified by id, it calculates order total and change state to 'Closed'.




