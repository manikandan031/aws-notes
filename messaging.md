**Messaging**

[back](index.md)

**SQS**
* Queues are used for asynchronous processing and decouple applications. It helps in scaling and handle sudden bursts.
* **SQS - Queue Model**
    * Single receiver receives and processes messages
    * Messages are not pushed to receivers. Receiver _polls_ for messages, process it and _deletes_ it.
    * Messages are retained in the queue for 4 days (default) and maximum of 14 days.
    * Standard or FIFO
    * 256kb per message
    * _Atleast once delivery_
    * Producers send messages using the SDK sendMessage API
    * Consumers 
        * can be any service or AWS Lambda
        * Can receive upto 10 messages at a time
        * We can scale consumers horizontally to increase throughput. The consumers _ASG_ can be based on an Cloudwatch Alarm which is triggered based on the _(Queue length / Number of instances)_ Cloudwatch metric.
        * After a message is polled by a consumer it is _invisible_ to the other consumers till the message _visibility timeout_ (default 30 seconds, max 12 Hrs). After the timeout if the consumer did not delete the message it will appear and will be polled by other consumers. Consumer can call ChangeMessageVisibility api to increase the timeout
    * Cross account access is possible via sqs access policies
    * Dead Letter Queue - We can set a max times that a message can go back to the queue. After _MaximumReceives_ threshold is crossed the message is moved to DLQ.
    * SQS - Request-Response systems - use correlation_id and a reply_to header in the request. SQS Temporary Queue Client can be used to implement this pattern.
    * Delay Queues - use delivery delay setting to set a wait time (0-15 minutes) after which only the message is visible to consumer.
    * FIFO Queues - guarantees order of messages.  Exactly send once messages. Messages are processed in the same order by consumer. Name should end .fifo
* **SNS - Pub/Sub Model**
    * Used to send push notifications to several subscribers. 
    * Support for sms, email, http endpoint, sqs, mobile notifications(direct publish)
    * A lot AWS services can automatically send notifications to SNS
    * SNS + SQS Fanout pattern -> message is sent to 1 SNS and multiple queues subscribe to that SNS topic.
    * Message filtering can be used to set up a json filter policy to filter out messages that go to SQS topic
* **Kinesis - Streaming model**
    * Collect, process and analyse real time streaming data
    * Example - application logs, website click streams, Not Telemetry data
    * Kinesis Data Streams - capture, process and store data streams
    * Kinesis Data FireHose - load data streams into AWS data stores
    * Kinesis Data Analytics - analyse data streams with SQL or Apache Flink
    * Kinesis Video streams - capture, process and store video streams
    * **Kinesis data streams**
        * Stores data stream in shards. 
        * Each record has a partition key and a data blob (upto 1MB).
        * Throughput - 1MB/sec or 1000 messages per second per shard incoming and 2MB/Sec outgoing. So increase number of shards for higher throughput.
        * Consumers of kinesis data streams can be apps / lambda / firehose / analytics
    * **Kinesis Data firehose**
        * Store data into target destinations
        * Can read data from kinesis data streams / cloud watch / aws iot
        * Reads records (upto 1MB), can call a lambda to process / transform it and then writes to destination in batches.
        * Destinations can be 
            * AWS— >S3, AWS Redshift, AWS Elastic Search
            * Other - New Relic, Data dog, Splunk etc
            * Custom Http Endpoint
    * **Kinesis Data analytics**
        * Sql statements to process streams of data for real Time analytics
        * Real time dashboards / metrics
    * **Amazon MQ**
        * To get managed apache active mq in service.
        * Doesn’t scale as much but it is compatible to standard protocols.
        * High availability is maintained using a standby queue in another AZ with EFS for storage.

[back](index.md)
