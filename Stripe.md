# Stripe 

The Stripe payment feature consists of the following:

- [Stripe]() API to support a payment functionality
- The frontend will use Stripe Elements to integrate the Stripe UI

##  Request flow

1) The client will initiate a Payment Intent request to the Ocean Premium (OP) API

2) The OP API will contact the Strip API, to generate a _Payment Intent_, and returns a `client_secret` to the client

3) The client uses the given `client_secret` returned by the Ocean Premium API 

![3989691234-1*1380x8iqFlXB8-e_R7KXVw.png](https://bitbucket.org/repo/r8KBn74/images/665762307-3989691234-1*1380x8iqFlXB8-e_R7KXVw.png)