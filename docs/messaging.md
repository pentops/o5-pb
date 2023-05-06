Messaging
=========

Topology
--------

### Broadcast

- Zero or more Sender applications
- Exactly one 'Topic'
- Zero or more Worker applications
  - One Queue per Worker application

### Unicast

- Zero or more Sender applications
- Exactly one Worker application
- Exactly one Queue

### Reply

- Exactly one Worker application
- Exactly one Input Queue
- Zero or more Sender applications
  - One Reply queue per Sender application
