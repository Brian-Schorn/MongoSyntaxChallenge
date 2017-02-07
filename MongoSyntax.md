// 1. Create a collection named orders.
db.createCollection('orders')


// 2. Insert at least 3 documents that represent an order. IMPORTANT: See section below for fields.
db.orders.insert({
... orderDate: new Date(),
... orderTotal: 42.00,
... lineItems: [
... { unitPrice: 2.00, quantity: 21, productName: 'Skittles' }]})

db.orders.insert({
... orderDate: new Date(),
... orderTotal: 20.00,
... lineItems: [
... { unitPrice: 2.00, quantity: 10, productName: 'Skittles' }]})

db.orders.insert({
... orderDate: new Date(),
... orderTotal: 50.00,
... lineItems: [
... { unitPrice: 2.00, quantity: 10, productName: 'Skittles' },
... { unitPrice: 1.00, quantity: 30, productName: 'Twinkies' }]})


// 3. Find a single order document, any order document.
db.orders.findOne()

// 4. Find all orders and make them look pretty.
db.orders.find().pretty()

// 5. Find all orders with an orderDate that is prior to 1/1/2016.
db.orders.find({ orderDate: { $lt :new ISODate("2016-01-01T00:00:00Z") }})

// 6. Find all orders with an orderDate that is after 1/1/2016.
db.orders.find({ orderDate: { $gt :new ISODate("2016-01-01T00:00:00Z") }})

// 7. Find orders with lineItems that have a quantity that is less than 50, but greater than 5. HINT: Look at $and and dot notation.
db.orders.find({ $and: [ { "lineItems.quantity": { $gt: 5}}, { "lineItems.quantity": { $lt: 50}}] }).pretty()

// 8. Update one of your line items to 42.99. HINT: Look at dot notation
//Only updates the first line item matching "Skittles", all documentation instructs to use a forEach loop to loop through an array to match more than 1 query result

db.orders.update({"lineItems.productName": "Skittles"}, { $set: {"lineItems.0.unitPrice": 42.99}} )

// 9. Remove one of your orders.
db.orders.deleteOne({orderTotal: { $gt:1}})
