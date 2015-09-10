Vagrant PyWebhooks
==================

Scripts to quickly spin up a single node [PyWebhooks](http://pywebhooks.io/) server
with everything you need for development using Vagrant. This includes
[RethinkDB](https://rethinkdb.com) and [Redis](https://redis.io).


To get started from a terminal:

```
$ git clone https://github.com/chadlung/vagrant-pywebhooks.git
$ cd vagrant-pywebhooks
$ vagrant box add dhoppe/ubuntu-14.04.2-amd64-nocm
$ vagrant up
```

From here, follow the instructions on my blog:
[Introducing PyWebhooks: An Easy to Use Webhooks Service (Written in Python 3)](http://www.giantflyingsaucer.com/blog/?p=5666)
