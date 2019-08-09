# Nested Hashes

## Learning Goals

- Describe how nested `Hash`es can store complex associations of data.
- Describe the structure of a nested `Hash`.
- Give examples of real-world situations that can require nested `Hash`es.
- Retrieve data from a nested `Hash`.

## Preface

In order to finish the final challenges of this module, you'll need to be able
to build complex nested data structures and write methods to access their data.
This might be a good place to ***slow down*** and make sure you're
experimenting on your own and are following everything we say. Don't rush to
the final challenge, build your understanding patiently through these next few
lessons. It'll pay off!

## Introduction

So far, we've seen `Hash`es that store values in associated keys. But here's a
simple but powerful truth: `Hash` keys can point to `Hash`es, and those
`Hash`es keys can point to other `Hash`es and so on. This can lead to
staggeringly complex data structures whose data we access by "just adding more
`[]`s. Astoundingly, `Array`s can be full of `Hash`es or a `Hash` can point to
an `Array` that's full of `Hash`es. The possibilities are astounding.

Collections of collections are called "nested" or "multidimensional data
structures. It might be more honest to call them "complex" but Rubyists tend to
say "nested" so we'll do the same.

In this lesson, we'll introduce nested, or multidimensional, `Hash`es and
explain how they're useful in programming.

## Where Will You Find Nested Hashes?

Nested `Hash`es are a very common way to receive, store, and share information.
If you want to integrate with Twitter or Soundcloud, you'll need to be able to
work with the nested `Hash`es they return. If your business partner wants to
send data to you, they'll likely want to do it in the form of a nested `Hash`.

New York City, for example, shares information to developers through a special
web site called NYC Open Data. Developers can connect to it to find out
information about weather, sanitation routes, and whether or not parking
enforcement has been suspended on account of snow.

We'll learn a lot more about working with third-party data later on in this
course. For now, trust that nested `Hash`es are a very common "raw material" we
use in our programs.

## Nested Hashes Model Real-World Data

We can imagine so many real-world situations and environments in which we are
dealing with complicated collections of data.

Let's take, for example, a list of instructors at a school. They can
be stored in an `Array` like this:

```ruby
instructors = ["Ian", "Johann", "Alex"]
```

What happens when we expand our data collection to include the students as well?
We could create yet another `Array`:

```ruby
students = ["Andrew", "Howard", "Terrance", "Daniel", "Rachel", "Natalie"]
```

But both of these groups are part of a larger group, their _school_. We'd like
to group them together into a collection _that contains both_. But we want to
do this in a way that keeps a "label" describing each "sub-collection's" focus.
Hmm, meaningful label, pointing to data...sounds like a job for a `Hash`!

## Our First Nested Hash

With a nested `Hash`, we can store complex collections of data. In other words,
we can store data that is associated to other data via categories and
subcategories.

Both the `students` `Array` and the `instructors` `Array` should be associated to
the same school. So, we can create a `Hash`, `school`, that contains keys to
denote the `instructors` and `students` categories. We can point these keys to
the `Array`s that contain our instructors and students respectively.

Let's take a look:

```ruby
school = {
  instructors: ["Ian", "Johann", "Alex"],
  dev_team: ["Andrew", "Howard", "Terrance", "Daniel", "Rachel", "Natalie"],
  school_name: "Flatiron School: Downtown NYC"
}
```
In this example, each key in our `Hash` points to a value that is an `Array`.

Nested `Hash`es allow us to further group, or associate, the data we are working
with. They help us to deal with situations in which a category or piece of data
is associated not just to one discrete value, but to a collection of values. In
such a situation, we can create a `Hash` key that points to a value of another
`Hash` or an `Array`.

Also, let's add a `:school_name` key for a human-friendly display name of the
school.

## A Note On Mixing our Collection Types

Keep in mind that we can mix what keys point to. In the example above, two keys
point to `Array`s and one key points to a `String`.

## Retrieve Data From a Nested `Hash`.

Let's use our nested structure.

What if we wanted to grab *just the first name* in the instructor's `Array`?

First, we access the instructors `Array` with

```ruby
school[:instructors]
```

To get the first instructor's name we ask that `Array` for it's `0`th element:

```ruby
school[:instructors][0]
```

## Nesting a Hash within a Hash

Imagine we're putting together information on various TV show characters, each
including information about a particular TV show character. An individual `Hash`
for each character might look something like this:

```ruby
homer = {name: "Homer Simpson", occupation: "Nuclear Safety Inspector", hobbies: ["Watching TV", "Eating donuts"]}
jon = {name: "Jon Snow", occupation: "King in the North", hobbies: ["Fighting white walkers", "Knowing nothing"]}
fred = {name: "Mr. Rogers", occupation: "Neighbor", hobbies: ["Making children feel loved and appreciated", "Singing songs"]}
```

While each `Hash` is about a different TV personality, they are _all_ part of a
larger collection. We _could_ put them in an `Array`:

```ruby
tv_personalities = [
  {name: "Homer Simpson", occupation: "Nuclear Safety Inspector", hobbies: ["Watching TV", "Eating donuts"]},
  {name: "Jon Snow", occupation: "King in the North", hobbies: ["Fighting white walkers", "Knowing nothing"]},
  {name: "Mr. Rogers", occupation: "Neighbor", hobbies: ["Making children feel loved and appreciated", "Singing songs"]}
]
```

Or, we could make this a `Hash` of `Hash`es:

```ruby
tv_personalities = {
  :homer => {name: "Homer Simpson", occupation: "Nuclear Safety Inspector", hobbies: ["Watching TV", "Eating donuts"]},
  :jon => {name: "Jon Snow", occupation: "King in the North", hobbies: ["Fighting white walkers", "Knowing nothing"]},
  :nice_fred => {name: "Mr. Rogers", occupation: "Neighbor", hobbies: ["Making children feel loved and appreciated", "Singing songs"]}
}
```

Here we've used character names as keys to make it more convenient to access
our `Hash`es even though this data is already stored in the `Hash`es themselves.
With this `Hash`, we can directly look up a particular character's information
just by using their name:

```ruby
tv_personalities[:homer]
#=> {name: "Homer Simpson", occupation: "Nuclear Safety Inspector", hobbies: ["Watching TV", "Eating donuts"]}

tv_personalities[:jon][:occupation]
#=> "King in the North"

tv_personalities[:nice_fred][:hobbies][1]
#=> "Singing songs"
```

Notice that when accessing nested data, we can use bracket notation multiple
times to go deeper into the data. We can even mix `Hash` keys and `Array` indexes,
as with `tv_personalities[:nice_fred][:hobbies][1]`.

## Conclusion

Nested `Hash`es can get pretty complicated. Read through the example in this
lesson again before moving on.

In many programming challenges the first step is **understanding how the data
you need to work with is structured**. Try building your own nested structres
and test them out with Ruby.

[docs]: https://data.cityofnewyork.us/resource/7btz-mnc8.json
[json]: https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh?hl=en-US
