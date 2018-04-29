# Ruby Object Relations: Has-Many Through

## Introduction

We've seen how objects can be related to one another directly, when one object contains a reference to another. This is the "has many"/"belongs to" association, and is a direct relationship.

However, in the real-world, different entities can be connected to one another _indirectly_ as well as directly. For example:

* A company that offers a network of doctors to their employees _through_ the company's insurance program.
* A user on a popular media sharing site can have many "likes", that occur _through_ the pictures they post.
* A Lyft driver that you are connected to _through_ the rides you've taken.

These are just a few examples of the kind of indirect relationships that we may need to model in our programs.

In this lesson, we'll build out just such a relationship using waiters, customers, and meals. A customer can has many meals, and a customer can have many waiters through those meals. Similarly, a waiter has many meals, and has many customers through meals. We'll dig into that in just a minute, but let's start with the stuff we already know.

## Our Domain Model

Domain models often mimic real life. They don't always have to, but in this case, our model is going to be something that we all know pretty well. Let's start by building out the `Customer` and `Waiter` classes.

```ruby
class Customer
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end
end
```

As you can see, our `Customer` has a name and an age. Their name and age are set upon initialization, and because we created an attribute accessor for both, the customer is able to change their name or age. If we wanted to limit this ability to read only, we would create an attibute reader instead.

```ruby
class Waiter
  attr_accessor :name, :yrs_experience

  def initialize(name, yrs_experience)
    @name = name
    @yrs_experience = yrs_experience
  end
end
```

Our `Waiter` has a name and an attribute tracking their years of experience. We could instantiate a waiter with anything we wanted to, but it might be fun to do some math later and see if our customers tip experienced waiters better.

## The "has many through" Relationship

If you're a customer at a restaurant, each time you go, you have a different meal. Even if you order the same exact thing, it's a different instance of that meal. So it goes without saying that a customer can have many meals.

It's a safe bet to assume that unless you only eat at one very small restaurant, you'll have many different waiters as well. Not all at once of course, because you only have one waiter per meal. So it could be said that your relationship with the waiter is through your meal. The same could be said of the waiter's relationship with each customer.

That's the essence of the `has many through` relationship.

## How Does That Work in Code?

Great question! The way we're going to implement this relationship is by setting up our `Meal` class as a join between our `Waiter` and our `Customer`. And because we're obeying the `single source of truth`, we're going to tell the `Meal` class to know all the details of each meal. That means not only the total cost and the tip, but who the customer and waiter were for each meal.

## Conclusion: The Advantages of the "has many through" relationship

Why associate artists to genre objects _through_ songs? By associating songs to genres, we are not only reflecting the real world situation that our program is meant to model, but we are also creating clean and re-usable code. Without the song/genre association, you'll find that you have to add a given song to an artist's list of songs and then separately add a genre to that artist.

With our "through association", as long as we have properly associated a song to a given genre and that same song to a given artist, our connection between an artist and his or her genres will automatically follow.

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/ruby-objects-has-many-through-readme' title='Ruby Object Relations: Has-Many Through'>Ruby Object Relations: Has-Many Through</a> on Learn.co and start learning to code for free.</p>

<p class='util--hide'>View <a href='https://learn.co/lessons/ruby-objects-has-many-through-readme'>Has Many Objects Through</a> on Learn.co and start learning to code for free.</p>
