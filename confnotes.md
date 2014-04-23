## Domain Driven Design Hexagonal Architecture Rails - [Github Repository](https://github.com/dwhelan/hex-ddd)
1. Embrace Complexity
   * Understanding the domain
   * Ubiquitous language
2. Know where you're going
3. Be more than just a "Rails Developer"

> Reread blog post by code climate ["7 ways to refactor fat models"](http://blog.codeclimate.com/blog/2012/10/17/7-ways-to-decompose-fat-activerecord-models/)

## Hexagonal Architectures
* Core App
* Adapters
* DB/API/Message Queue
1. Form Object
  * Works well for multiple model attributes
2. Request Object
  * Virtus gem
3. Service Object
    * Basically breaks everything on a model out to a class? OrderService, CustomerService, BillingService, etc.

 
## Too Big to fail
> Need to go over slides but the talk had really interesting ways to deal with failing actions in an app that has multiple processes/steps for an action.
* broken_record gem
* ultra_marathon


## Advanced AREL - When ActiveRecord Just Isn't Enough
> Cameron Dutro @camertron

````ruby
Posts.joins(:comments).joins(:comments => :author).where()
````

becomes:

````ruby
Post
  .joins(:comments
    .joins(Comment.joins(:author).join_sources)
    .where(

    ))

Post.select(Post[:visitors].sum.as('visitor_total')).to_sql
````

* gem install arel-helpers
* scuttle.io for sql to AREL

## Refactoring to Component based Rails
* Hashtag #cbra

[Next Big Thing](https://github.com/shageman/the_next_big_thing)

````ruby
gem 'component_name', path: "../components/comp_name"

````

### SOLID
* Single Responsibility Principle
  1. SRP - WHere?
    1. Method - Yes
    2. Class - Yes
    3. Namespace - You should!
    4. Application - You should!
    5. Component - Now you can!
* Compenents over SOAs
  1. 1 repo
  2. 1 test suite
  3. 1 deployment
  4. no additional versioning constraints
  5. easier refactorings between parts
* Teasing out app component
  0. Got tests?
  1. find a vertical that makes sense on its own
  2. namespace controllers, views and models 
  3. hunt down other dependencies
  4. move all namespaced code into an engine
* Extracting functional component
  1. find functional component
  2. create gem
  3. move all files into gem and namespace
  4. move the other stuff the gem needs
  5. require the gem from your app
  6. add shims/ports/adapters to make the app happy
  