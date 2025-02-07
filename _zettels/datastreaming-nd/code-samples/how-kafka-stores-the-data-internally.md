---
date: 2024-08-26
layout: zettel
category: show
tags:
  - data-streaming
title: Exploration on how kafka stores data internally
---
Exploration of how data is stored in partitions internally

## Topic Storage

First, let's create a topic

`kafka-topics --create --topic kafka-arch --partitions 1 --replication-factor 1 --zookeeper localhost:2181`

### <a name="dir"></a>Inspecting the Directory Structure

Now that the topic is successfully created, let's see how Kafka stored it on disk.

`ls -alh /var/lib/kafka/data | grep kafka-arch`

What does the output look like?

What kind of data is kept inside of the directory?

`ls -alh /var/lib/kafka/data/kafka-arch*`

If you try to open the file ending in `.log` is there anything in it?

### Produce Data

Now that we have this topic, let's produce some data into it.

`kafka-console-producer --topic "kafka-arch" --broker-list localhost:9092`

Produce 5-10 messages.

Once you're done, hit Ctrl+C to exit.

Repeat the steps from [Inspecting the Directory Structure](#dir) and see how the results have
changed.


## Topics and Partitions

Now that you've seen what a topic with a single partition looks like, let's see what happens if we
modify the number of partitions

`kafka-topics --alter --topic kafka-arch --partitions 3 --zookeeper localhost:2181`

Try repeating the steps from [the previous section](#dir). How many folders do you see now?

Try modifying the number of partitions a few more times to see how Kafka modifies the data on disk.

