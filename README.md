simple-AMQ
===========

Getting Started
---------------
>###Start and Stop AMQ
> ./bin/activemq start
> ./bin/activemq stop

>### starting AMQ with a config file
> `./bin/activemq start xbean:./conf/activemq-stomp.xml`
> `./bin/activemq console`

>## Example 1  : Queue
>### Sync consumer
>### CD to the project directory to run the code
>* mvn compile exec:java
>* TextMessage message = session.createTextMessage();

>## Example 2: Queue
>### Prefetch 1 and asyn listner
>###job-consumer and job-producer , random processing time set. Test with two consumers.
' destination = session.createQueue("JOBQ.Work");
'

## Example 3 : Topics
>### Open two windows for event-subscriber and one window for event-publisher
>* destination = session.createTopic("EVENTS.QUOTES");
>* Message message = session.createMessage();
>### For durable : set client id and also create durablesubscriber
>### DurableTopics have limitions : either use queues or virtual destinations i.e. 
>### http://activemq.apache.org/virtual-destinations.html

## Example 4 : Topics Message Selection
>### Selecting Messages also known as content-based-routing - sql92 syntax
>### event-publisher and selective-event-consumer that selects only with symbol goog
>* selector = System.getProperty("QuoteSel", "symbol = 'GOOG'");
>* AAPL: $ (881.46906)
>* GOOG: $ (534.5367)
>* MSFT: $ (232.24496)
>* mvn compile exec:java -DquoteSel="symbol='MSFT' AND price >= 800"


## Example 5 : Request Response
jms-requestor and jms-responder
request.setJMSReplyTo(responseQ); #response Queue property added.
responder = session.createProducer(null); # created anonymous producer to send message to any destination.

## Example 6 :  Schedule Message Delivery : Update activemq.xml set schedulerSupport=true in broker tag.
message-scheduling
        TextMessage message = session.createTextMessage("Wake Up!");
        message.setLongProperty(ScheduledMessage.AMQ_SCHEDULED_DELAY, delay);
        message.setLongProperty(ScheduledMessage.AMQ_SCHEDULED_PERIOD, period);
        message.setIntProperty(ScheduledMessage.AMQ_SCHEDULED_REPEAT, repeat);
Supports CRON scheduling, one can browser scheduled messages and also remove them.

Example 7
advisory-generator and advisory-consumer
MJUST for dynamic network brokers
http://activemq.apache.org/advisory-message.html

Example 8 : Embeded Broker
Update POM file in this case.

Example 9: Connection Pooling
Pooling of Connections
Pooling of Sessions
Pooling of MessageProducer

Example 10: Virtual Destinations
By default, whenever a topic is created with a name matching the pattern VirtualTopic.<TopicName>, we gain access to the feature known as Virtual Destinations. These Virtual Destinations allow us to send a message to a topic but create consumers that have all the benefits of queue consumers, namely, those of load balancing and message persistence. Our queue consumers just need to use their own naming convention to access the Virtual Destination functionality. Each consumer that we 
want to create must be named using the pattern Consumer.<Name>.VirtualTopic.<TopicName>.
http://activemq.apache.org/virtual-destinations.html


Example 11: Failover
