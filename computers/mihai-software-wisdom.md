
# System design

* **focus on contracts between modules** - Then you can have a mess in the impl.
* **ownership of the data belongs to the service writing it** - The consumer services can be eventually consistent. The reason is that its easier to have read-after-write semantic this way. The consumers will not need this anyway. Example: If many services require configuration then you can have a configuration r/w API in each service or you can have a configuration service to write config and replicate to consumer services. According to the wisdom, you should take the second option.

# Coding

* prefer toolkits (unoppionated) to frameworks (oppionated)
* best frameworks are the frameworks you developed

# Testing

* **write code first and then the tests** - if you write the test before you might need to change it as you realize that your initial API won't be good
* **tests for hard to reproduce cases**
* **prefer integration tests / bigger units** - class-level unit tests work most for leaf-code but preferably take bigger units so you catch integration problems faster and you write and maintain less tests
