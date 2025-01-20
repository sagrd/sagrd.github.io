---
date: 2024-08-27
layout: zettel
category: show
tags:
  - data-streaming
title: synchronous and asynchronous  data producers in kafka
---
- Synchronous producers 
	- block producer program execution until the kafka broker has confirmed the receipt
	- Broker is supposed to respond to the producer that it had successfully received the data
	- these type of producers are rare in kafka world but have their place
		- example: credit card transaction and the application should require successful message delivery
			- if the message is not delivered we can roll back the transaction
- Asynchronous producers:
	- Producer program continuously sends message and does not wait for kafka broker confirmation
	- Eventually the broker sends confirmation that these messages are received
	- How does it know the messages are successfully delivered or not?
		- kafka client offers callback when message are delivered or an error occurs
		- the application will be given a chance to take some rectifying action.
	- `producer.flush()` can be use to specify asynchronous production

