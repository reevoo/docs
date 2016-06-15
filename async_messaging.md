# Asynchronous Messaging

## Purpose

We use asynchronous messaging to decouple services and deal with the requests load.

## Tools

We use [RabbitMQ](http://www.rabbitmq.com/) as a primary messaging system in all new applications and services. For services written in Ruby we use client library [Hutch](https://github.com/gocardless/hutch) to implement message producers and consumers where the pattern of [topic exchange type](https://www.rabbitmq.com/tutorials/amqp-concepts.html#exchange-topic) fits. When the other exchange type is necessary we use [Bunny](https://github.com/ruby-amqp/bunny) client library that is used internally by Hutch and allows implementation of all possible [AMQP Model patterns](https://www.rabbitmq.com/tutorials/amqp-concepts.html).

## Naming Conventions

### Topic Name

```source-service.[category ...].action``` (example: ```tracking.mark.click-through```)

For topics we use the naming convention of dot separated parts starting from left with name of a source service followed by multiple optional action category names and at the end the action name.
Names of parts are lowercased with dashes as a words separator.

Especially the topic name should not mention the consumer, just the source, otherwise we are coupling (at least in the conceptual description) when the idea of topics is to decouple.


### Queue Name

```consuming-service:topic-name``` (example: ```revieworld:tracking.mark.click-through```)

For queue names we use the the name of consuming service followed by the topic name as defined in previous step separated by colon. We do to enable multiple services to subscribe independently to the same topic.



### Hutch Consumer Setup

Message consumer is every class that include ```Hutch::Consumer``` and implement the ```process``` method. Argument of ```queue_name``` class method specify the queue name and argument of ```consume``` class method the routing key.


```Ruby
class ReviewEmailViewConsumer
  include Hutch::Consumer

  consume 'tracking.email.review-invitation.opened'
  queue_name 'revieworld:tracking.email.review-invitation.opened'

  def process(message)
    review_email = ReviewEmail.find_by_hashcode(message.body[:review_invite_hashcode]) || ReviewEmail.find(message.body[:review_email_id])
    attributes = { :viewed_at => message.body[:opened_at],
                   :submission_progress => ReviewEmail::SubmissionProgress::Clicked }
    review_email.update_attributes(attributes) if review_email.viewed_at.nil?
  end
end
```

## Open Questions

- Is it good idea to use different exchanges for different services?
- Is there any benefit to separate message consumers into rails engine?


## Resources
- [Bunny Guides](http://rubybunny.info/articles/guides.html)
- [AMQP 0-9-1 Model Explained](https://www.rabbitmq.com/tutorials/amqp-concepts.html)
- [Routing Topologies for Performance and Scalability with RabbitMQ](http://spring.io/blog/2011/04/01/routing-topologies-for-performance-and-scalability-with-rabbitmq/)
