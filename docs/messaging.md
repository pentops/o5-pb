Messaging
=========

Topology
--------

### Broadcast

![Pentops - Page 3 (3)](https://user-images.githubusercontent.com/1665328/236639414-c8e07738-b2ff-4769-91b7-ff741a267884.png)

- Zero or more Sender applications
- Exactly one 'Topic'
- Zero or more Worker applications
  - One Queue per Worker application

### Unicast

![Pentops - Page 3 (2)](https://user-images.githubusercontent.com/1665328/236639416-86a7f6db-30c9-4b21-8113-1bf6c0fdacc2.png)

- Zero or more Sender applications
- Exactly one Worker application
- Exactly one Queue

### Reply

![Pentops - Page 3 (1)](https://user-images.githubusercontent.com/1665328/236639378-bfbef3bf-e2ab-4f12-bf7e-fa5b1c856440.png)

- Exactly one Worker application
- Exactly one Input Queue
- Zero or more Sender applications
  - One Reply queue per Sender application
  
