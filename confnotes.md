## Domain Driven Design Hexagonal Architecture Rails - [Github Repository](https://github.com/dwhelan/hex-ddd)
1. Embrace Complexity
   * Understanding the domain
   * Ubiquitous language
2. Know where you're going
3. Be more than just a "Rails Developer"

> Reread blog post by code climate ["7 ways to refactor fat models"](http://blog.codeclimate.com/blog/2012/10/17/7-ways-to-decompose-fat-activerecord-models/)

### Hexagonal Architectures
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

becomes:

````ruby
Post
  .joins(:comments
    .joins(Comment.joins(:author).join_sources)
    .where(

    ))

````ruby
Post.select(Post[:visitors].sum.as('visitor_total')).to_sql


* gem install arel-helpers
* scuttle.io for sql to AREL