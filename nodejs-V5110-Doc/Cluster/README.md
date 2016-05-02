# Table of Contents

 - [Cluster](#cluster)
  - [How It Works](#how-it-works)
  - [Class: Worker](#class-worker)
    - [Event: 'disconnect'](#event-disconnect)
    - [Event: 'error'](#event-error)
    - [Event: 'exit'](#event-exit)
    - [Event: 'listening'](#event-listening)
    - [Event: 'message'](#event-message)
    - [Event: 'online'](#event-online)
    - [worker.disconnect()](#workerdisconnect)
    - [worker.exitedAfterDisconnect](#workerexitedafterdisconnect)
    - [worker.id](#workerid)
    - [worker.isConnected()](#workerisconnected)
    - [worker.isDead()](#workerisdead)
    - [worker.kill([signal='SIGTERM'])](#workerkillsignalsigterm)
    - [worker.process](#workerprocess)
    - [worker.send(message[, sendHandle][, callback])](#workersendmessage-sendhandle-callback)
    - [worker.suicide](#workersuicide)
  - [Event: 'disconnect'](#event-disconnect-1)
  - [Event: 'exit'](#event-exit-1)
  - [Event: 'fork'](#event-fork)
  - [Event: 'listening'](#event-listening-1)
  - [Event: 'message'](#event-message-1)
  - [Event: 'online'](#event-online-1)
  - [Event: 'setup'](#event-setup)
  - [cluster.disconnect([callback])](#clusterdisconnectcallback)
  - [cluster.fork([env])](#clusterforkenv)
  - [cluster.isMaster](#clusterismaster)
  - [cluster.isWorker](#clusterisworker)
  - [cluster.schedulingPolicy](#clusterschedulingpolicy)
  - [cluster.settings](#clustersettings)
  - [cluster.setupMaster([settings])](#clustersetupmastersettings)
  - [cluster.worker](#clusterworker)
  - [cluster.workers](#clusterworkers)


# Cluster
# How It Works
# Class: Worker
### Event: 'disconnect'
### Event: 'error'
### Event: 'exit'
### Event: 'listening'
### Event: 'message'
### Event: 'online'
### worker.disconnect()
### worker.exitedAfterDisconnect
### worker.id
### worker.isConnected()
### worker.isDead()
### worker.kill([signal='SIGTERM'])
### worker.process
### worker.send(message[, sendHandle][, callback])
### worker.suicide
# Event: 'disconnect'
# Event: 'exit'
# Event: 'fork'
# Event: 'listening'
# Event: 'message'
# Event: 'online'
# Event: 'setup'
# cluster.disconnect([callback])
# cluster.fork([env])
# cluster.isMaster
# cluster.isWorker
# cluster.schedulingPolicy
# cluster.settings
# cluster.setupMaster([settings])
# cluster.worker
# cluster.workers