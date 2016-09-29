---
layout: post
title:  "Log-based single-processing SOA"
published: true
---
## TL/DR
In a nutshell, every incoming request/message is stuck unto a request queue, while a single message processor continuously dequeues, processes, and commits each request in a log and publishes any relevant events(messages) for any other interested services, all in a transcation.

## Self healing
If the service goes down for any reason at all, on re-start, every request in the transaction commit log will get replayed in-order, rebuilding the internal state of the service before switching to catch-up with messages that may have been missed while down and then begin listening for new requests.

## Idempotence
It is important to note that a message should not be processed more than once. This can cause data inconsistencies in the state of the domain model. If there is no guarantee that the incoming messages will not arrive more than once, then idempotence within the LBSP service will need to be implemented.

## Read Model
An eventually consistent read (view) model projection of the state of the world can be built by a separate dedicated service that listens for relevant events published by one or more other services. It may be neccessary to also apply the LBSP technique described above to make self-healing possible. However, the underlying storage can be anything (in-memory, SQL DB, Document DB, Elastic Search etc) depending on your needs. This is not too different from the techniques used in CQRS.
