# Green Grocer

## Learning Goals

- Access and iterate over hashes
- Translate data from arrays to hashes
- Translate data from hashes to other hashes
- Count repeat items in a hash
- Perform calculations based on hash data

## Introduction

Over the last several lessons, we've explored nested data structures and how
they can model complex real-world situations. Now we're going to take everything
we've learned and use it to program a grocery store checkout process.

Think for moment about what it's like to shop at a grocery store. As you walk
through the store, you put the items you want to buy into your cart. Your cart,
then, becomes a _collection_ of grocery items. Every one of those grocery items
has specific attributes: for example, its price and whether or not it's on
clearance. You can also have multiples of the same item in your cart, and
chances are they will be all mixed together in no particular order or structure.

When you pay for all your items at the checkout, however, you expect to get a
receipt that lists all of the items you bought, how many of each item you
bought, any coupons or discounts applied and the total cost of all the items in
your cart.

So, along the way, someone has to have figured out how to take all those grocery
items you put in your cart, plus all their attributes, and represent them in
data that can then be manipulated and calculated. With our newly-gained
knowledge of nested data structures, we can figure out the same.

In this lab, your task is to write a set of methods to handle the different
pieces of the checkout process. This might seem complicated, but, whether you
know it or not, you've been collecting all of the pieces you need over the
course of this lesson cycle, and we're here to help you through each step of
putting them together.

## Instructions

Ultimately, we want to implement a method called `checkout` that will calculate
the total cost of a cart of items, applying discounts and coupons as necessary.

This `checkout` method will rely on three other methods: `consolidate_cart`,
`apply_coupons`, and `apply_clearance`.

Let's begin with the first of the necessary methods: `consolidate_cart`.

### Write the `consolidate_cart` Method

As we start shaping our methods, we should keep in mind the strategy we
encountered earlier of getting insights from our nested data structures. Step
one of that process is to understand the nested data structures we're working
with.

Take a moment to think about our cart of items. The cart starts as an array
of individual items, right? We want to translate it into a hash that includes
the counts for each item with the `consolidate_cart` method.

For instance, if the method is given the array below:

```ruby
[
  {"AVOCADO" => {:price => 3.00, :clearance => true }},
  {"AVOCADO" => {:price => 3.00, :clearance => true }},
  {"KALE"    => {:price => 3.00, :clearance => false}}
]
```

then the method should return the hash below:

```ruby
{
  "AVOCADO" => {:price => 3.00, :clearance => true, :count => 2},
  "KALE"    => {:price => 3.00, :clearance => false, :count => 1}
}
```

After you write this method, you can test it out in IRB with the provided
example to see how it works in action.

### Write the `apply_coupons` Method

Now we need to write an `apply_coupons` method that takes in a cart and an
_Array_ of  coupons, applying the coupons _if_ appropriate.

If the method is given a cart that looks like this:

```ruby
{
  "AVOCADO" => {:price => 3.00, :clearance => true, :count => 3},
  "KALE"    => {:price => 3.00, :clearance => false, :count => 1}
}
```

and an Array with a single coupon for avocados that looks like this:

```ruby
[{:item => "AVOCADO", :num => 2, :cost => 5.00}]
```

then `apply_coupons` should return the following hash:

```ruby
{
  "AVOCADO" => {:price => 3.00, :clearance => true, :count => 1},
  "KALE"    => {:price => 3.00, :clearance => false, :count => 1},
  "AVOCADO W/COUPON" => {:price => 2.50, :clearance => true, :count => 2},
}
```

In this case, we have a 2 for $5.00 coupon, but 3 avocados counted in the
consolidated cart. Since the coupon only applies to 2 avocados, the cart
shows there is one remaining avocado at $3.00 and a count of _2_ discounted
avocados.

As we want to be consistent in the way our data is structured,
each item in the consolidated cart should include the price of _one_ of that
item. Even though the coupon states $5.00, since there are 2 avocados, the
price is listed as $2.50.

### Write the `apply_clearance` Method

This method should discount the price of every item on clearance by twenty
percent.

For instance, if the `apply_clearance` method was given this cart:

```ruby
{
  "PEANUT BUTTER" => {:price => 3.00, :clearance => true,  :count => 2},
  "KALE"         => {:price => 3.00, :clearance => false, :count => 3}
  "SOY MILK"     => {:price => 4.50, :clearance => true,  :count => 1}
}
```

it should return a cart with clearance applied to peanut butter and soy milk:

```ruby
{
  "PEANUT BUTTER" => {:price => 2.40, :clearance => true,  :count => 2},
  "KALE"         => {:price => 3.00, :clearance => false, :count => 3}
  "SOY MILK"     => {:price => 3.60, :clearance => true,  :count => 1}
}
```

**Hint**: you may find the Float class' built in [round][round] method to be
helpful here to make sure your values align.

### Write the `checkout` Method

Create a `checkout` method that calculates the total cost of the consolidated
cart. Just like a customer arriving at a register with mixed up cart, this
method is given an array of unsorted items. In addition to an array of items,
`checkout` is also given an array of _coupons_.

The `checkout` method will need to utilize all the previous methods we've
written. It consolidates the cart, applies coupons, and applies discounts. Then,
it totals the cost of the entire cart, accounting for each item and their
prices, and returns this value.

When writing this method, make sure to address each step in the proper order:

- Consolidate the cart array into a hash

- Apply coupon discounts if the proper number of items are present

- Apply 20% discount if items are on clearance

In addition to coupons and clearance, our grocer store offers a deal for
customers buying lots of items: if, after all coupons and discounts, the cart's
total is over $100, the customer gets an additional 10% off. Apply this
discount when appropriate.

## Conclusion

Utilizing arrays and hashes is key when working with a lot of data. With our
knowledge of iteration and data manipulation, we can do all sorts of things with
this data. We can build methods that access that data and modify only what we
want. We can extract additional information, as we did here calculating a total.
We can take data that isn't helpful to us and restructure it to be _exactly_
what we need.

## Resources

- [round][round]

[round]: https://ruby-doc.org/core-2.1.2/Float.html#method-i-round

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/green_grocer'>Green Grocer</a> on Learn.co and start learning to code for free.</p>
