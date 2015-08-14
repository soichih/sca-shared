# isdp
ISDP multi-file download service

## TODOs

1) Currently it receives request via web and immediately start processing request. This means all simultaneously requests will be executed in parallel... instead, I need to do following.

* When a request comes, post to AMQP
* Write a separate handler that pulls request from AMQP one at a time and handle request

2) Currently doesn't handle invalid file path gracefully. Maybe I should skip missing ones and output a text file stating that files couldn't be downloaded?

3) Make sure an appropriate error message is generated (to who?) if incoming message is bogus.

4) Add a sensu check to make sure web-receiver and request handlers are running.

5) what happens if stage / publish directory can't be written? (doesn't exist, no access, not directory, disk is full)

6) add timeout mechanism for each task? also, should I async.retry?

7) what happens to error messages? 
stored in configured location (user can specify level)

8) there isn't much in the mocha test.. I need to add more unit testsing

9) what happens if amqp is down?
I am not sure if it's pooling messages to be published locally, but as soon as amqp server comes back online, it reconnects seemslessly
