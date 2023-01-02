# Deploy-a-apache-kafka-server-and-create-a-topic
Kafka is a distributed event streaming platform that lets you read, write, store, and process events (also called records or messages in the documentation) across many machines.

#### Install Java version 8
`sudo apt-get install openjdk-8-jdk`

![Install java](https://user-images.githubusercontent.com/49678841/210263353-82d5df02-7627-4f06-a7ab-2c3044f881fa.png)


#### Create a Directory and Download kafka using this link https://dlcdn.apache.org/kafka/3.3.1/kafka_2.13-3.3.1.tgz
![crate dir and download kafka](https://user-images.githubusercontent.com/49678841/210262798-09474851-6d54-4988-8858-2be8e60f84ab.png)

#### unzip the downloads
`$ tar -xzf kafka_2.13-3.3.1.tgz`

`$ cd kafka_2.13-3.3.1`

#### Start the Kafka environment
Apache Kafka can be started using ZooKeeper or KRaft. In our case we would be using zookeeper

```
# Start the ZooKeeper service
$ bin/zookeeper-server-start.sh config/zookeeper.properties

```
![Start Kafka broker service](https://user-images.githubusercontent.com/49678841/210264728-4171bc9f-0256-4632-abca-95acf42b27eb.png)

Open another terminal and navigate to the download directory and run this command below

```
# Start the Kafka broker service
$ bin/kafka-server-start.sh config/server.properties
```

![Start Kafka broker service](https://user-images.githubusercontent.com/49678841/210265166-ec7f3f6b-5695-44c2-875a-36eb38b4df3d.png)

#### Create a topic to store your event
Kafka is a distributed event streaming platform that lets you read, write, store, and process [events](https://kafka.apache.org/documentation/#messages) also called records or messages in the documentation across many machines.

Example events are payment transactions, geolocation updates from mobile phones, shipping orders, sensor measurements from IoT devices or medical equipment, and much more. These events are organized and stored in [topics](https://kafka.apache.org/documentation/#intro_concepts_and_terms). Very simplified, a topic is similar to a folder in a filesystem, and the events are the files in that folder.

So before you can write your first events, you must create a topic. Open another terminal session, navigate to the download directory and run:

`$ bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092`

![created a  topic event](https://user-images.githubusercontent.com/49678841/210268736-9c2a461f-0b94-4021-8f25-355b80bbc711.png)

#### Write some events into the topic

A Kafka client communicates with the Kafka brokers via the network for writing (or reading) events. Once received, the brokers will store the events in a durable and fault-tolerant manner for as long as you need—even forever.

Run the console producer client to write a few events into your topic. By default, each line you enter will result in a separate event being written to the topic.

```
$ bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
This is my first event
This is my second event

```
You can stop the producer client with `Ctrl-C` at any time.

![wrote my first event](https://user-images.githubusercontent.com/49678841/210269026-29a23841-3ca1-4c96-bf72-cb1477176352.PNG)

#### Read the events

Open another terminal session and run the console consumer client to read the events you just created:

```
$ bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
This is my first event
This is my second event

```
![Read the event](https://user-images.githubusercontent.com/49678841/210269297-97fecdab-8f30-435f-94fb-4e413d47a718.PNG)

Because events are durably stored in Kafka, they can be read as many times and by as many consumers as you want. You can easily verify this by opening yet another terminal session and re-running the previous command again.

