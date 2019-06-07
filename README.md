# Nested Hashes

## Learning Goals

- Describe how nested hashes can store complex associations of data.
- Describe the structure of a nested hash.
- Give examples of real-world situations that can require nested hashes.
- Retrieve data from a nested hash.

## Introduction


So far, we've seen hashes that store values in associated keys. In the hashes
we've built up until now, each key points to a single value. Hashes are very
useful, however, because they can be nested within each other. A key in a hash
can point to a value that is also a *collection of objects*, i.e. an array or
even another hash. This is also sometimes referred to as a multidimensional
hash.

As programmers, we strive to write code that models the real world. The programs
we write to serve a purpose––whether you're creating a simple command line game or
an app to help hospitals manage patient data, our code is designed to do a real
job, like run a game or communicate critical information.

In this lesson, we'll introduce nested, or multidimensional, hashes and explain
how they're useful in programming.

## Where Will You Find Nested Hashes?

Nested hashes are a very common way to store and operate on complex associated
data in a program. You are likely to encounter them any time you find yourself
working with a large collection of information. In particular, you will
encounter these data structures when working with data you will pull from APIs.

> API stands for "Application Programming Interface" and here refers to the way
in which organizations, companies, and governments will expose their data to the
public for use.

New York City, for example, has a robust API called NYC Open Data. Developers
can connect to this API to find information about city programs, public housing,
parks, schools, construction, health information––like this collection of
[NYC doctors who participate in project REACH][docs]––you name it.

**Note:** To view the nested hash data from the NYC Open Data API, linked to
above, in an organized and legible way in your browser, use the [Chrome JSON Viewer extension][json].

When you send a request for data to such an API, the data you get back from them
will be in the form of a nested hash that can contain information about
thousands of records.

We'll learn a lot more about APIs later on in this course. For now, just
understand that nested hashes are a very common occurrence in programming. They
are used to store complex collections of data and you will encounter them when
working with APIs, among other places.

## Nested Hashes Model Real-World Data

We can imagine so many real-world situations and environments in which we are
dealing with complicated collections of data.

Let's take, for example, a list of instructors at a school. They can
be stored in an array like this:

```ruby
instructors = ["Ian", "Johann", "Alex"]
```

What happens when we expand our data collection to include the students as well?
We could create yet another array:

```ruby
students = ["Andrew", "Howard", "Terrance", "Daniel", "Rachel", "Natalie"]
```

But both of these groups are part of a larger group, their _school_. We'd like
to group them together into a collection _that contains both_. But we want to do
this in a way that keeps a "label" describing each "sub-collection's" focus.
Otherwise, we may accidentally mix up instructors and students!

How might we convey that these two arrays are related?

## Our First Nested Hash

With a nested hash, we can store complex collections of data. In other words, we
can store data that is associated with other data via categories and
subcategories.

Both the `students` array and the `instructors` array should be associated with
the same school. So, we can create a hash, `school`, that contains keys to
denote the `instructors` and `students` categories. We can point these keys to
the arrays that contain our instructors and students respectively.

Let's take a look:

```ruby
school = {
  instructors: ["Ian", "Johann", "Alex"],
  students: ["Andrew", "Howard", "Terrance", "Daniel", "Rachel", "Natalie"]
}
```
In this example, each key in our hash points to a value that is an array.

Nested hashes allow us to further group, or associate, the data we are working
with. They help us to deal with situations in which a category or piece of data
is associated not just to one discrete value, but to a collection of values. In
such a situation, we can create a hash key that points to a value of another
hash or an array.

## A Note On Mixing our Collection Types

You may have noticed in the above example that we have a hash in which the value
of a key is an array.

Understand that arrays and hashes can store *any type of data*. In other words,
the individual index items of an array can be strings, integers, or even other
arrays and hashes. The same is true of hashes. The values that hash keys point
to may be strings, integers, and even arrays or hashes.

In fact, one of the most common nested data structures you'll see when working
with APIs, as discussed above, is an _array_ of hashes.

## Nesting an Array within a Hash

We'll be building up our own nested hash and operating on such data structures
in a number of ways over the course of the next few lessons. For now, just read
through the next example and get comfortable looking at a nested hash.

In this example, we have a hash, `school`, which stores some data about
us. This data is broken down into the categories of `:instructors`, `:students`
and `:classes`, thanks to our nested hash.

```ruby
school = {
  instructors: ["Ian", "Johann", "Alex"],
  students: ["Andrew", "Howard", "Terrance", "Daniel", "Rachel", "Natalie"],
  classes: ["Software Engineering", "Data Science"]
}
```

In the above example, each key points to an array of strings. We may not know
how to work with nested hashes just yet, but we *do* know how to work with
one-dimensional hashes and arrays.

The `school` hash has a key of `:instructors`. The value of that key is an array
of instructors. In order to access that array, we can use the `[]` method we've
been using all along to grab the values of a particular hash key.

```ruby
instructors = school[:instructors]
 # => ["Ian", "Johann", "Alex"]
```

Here, we set a variable, `instructors`, equal to the return value of calling
`school[:instructors]`, which is simply the array of instructors.

Now, to operate on that collection of instructors, we can simply operate on our
`instructors` array.

What if I wanted to grab *just the first name* in the instructor's array? We use
the same methods for accessing array index items that we've been using all
along:

```ruby
instructors[0]
#  => "Ian"
```

We could, alternatively, use more than one set of brackets to find our answer:

```ruby
school[:instructors][0]
#  => "Ian"
```

## Nesting a Hash within a Hash

Imagine we're putting together information on various TV show characters, each
including information about a particular TV show character. An individual hash
for each character might look something like this:

```ruby
homer = {name: "Homer Simpson", occupation: "Nuclear Safety Inspector", hobbies: ["Watching TV", "Eating donuts"]}
jon = {name: "Jon Snow", occupation: "King in the North", hobbies: ["Fighting white walkers", "Knowing nothing"]}
fred = {name: "Mr. Rogers", occupation: "Neighbor", hobbies: ["Making children feel loved and appreciated", "Singing songs"]}
```

While each hash is about a different character, they are _all_ part of a larger
collection. We _could_ put them in an array:

```ruby
[
  {name: "Homer Simpson", occupation: "Nuclear Safety Inspector", hobbies: ["Watching TV", "Eating donuts"]},
  {name: "Jon Snow", occupation: "King in the North", hobbies: ["Fighting white walkers", "Knowing nothing"]},
  {name: "Mr. Rogers", occupation: "Neighbor", hobbies: ["Making children feel loved and appreciated", "Singing songs"]}
]
```

This seems weird though. There isn't a particular order we need to maintain.
Having everything in an array makes it more difficult to find a particular hash,
since you will need to know the exact index of that hash to access it. It makes
more sense to contain these hashes within another hash.

```ruby
tv_show_characters = {
  "Homer Simpson" => {name: "Homer Simpson", occupation: "Nuclear Safety Inspector", hobbies: ["Watching TV", "Eating donuts"]},
  "Jon Snow" => {name: "Jon Snow", occupation: "King in the North", hobbies: ["Fighting white walkers", "Knowing nothing"]},
  "Mr. Rogers" => {name: "Mr. Rogers", occupation: "Neighbor", hobbies: ["Making children feel loved and appreciated", "Singing songs"]}
}
```

Here we've used character names as keys to make it more convenient to access
our hashes even though this data is already stored in the hashes themselves.
With this hash, we can directly look up a particular character's information
just by using their name:

```ruby
tv_show_characters["Homer Simpson"]
#=> {name: "Homer Simpson", occupation: "Nuclear Safety Inspector", hobbies: ["Watching TV", "Eating donuts"]}

tv_show_characters["Jon Snow"][:occupation]
#=> "King in the North"

tv_show_characters["Mr. Rogers"][:hobbies][1]
#=> "Singing songs"
```

Notice that when accessing nested data, we can use bracket notation multiple
times to go deeper into the data. We can even mix hash keys and array indexes,
as with `tv_show_characters["Mr. Rogers"][:hobbies][1]`.

## Conclusion

Nested hashes can get pretty complicated. Read through the example in this
lesson again before moving on. It's okay if you don't understand everything;
just try to get comfortable reading through the above nested hash.

[docs]: https://data.cityofnewyork.us/resource/7btz-mnc8.json
[json]: https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh?hl=en-US
