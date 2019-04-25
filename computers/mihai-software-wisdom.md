
# System design

* **focus on elegant/well documented contracts between modules** - Then you can have a mess in the impl.
* **ownership of the data belongs to the service writing it** - The consumer services can be eventually consistent. The reason is that its easier to have read-after-write and atomicity semantic this way. The consumers will not need this anyway. Example: If many services require configuration then you can have a configuration r/w API in each service or you can have a configuration service to write config and replicate to consumer services. According to the wisdom, you should take the second option.

# Coding

* prefer toolkits (unoppionated) to frameworks (oppionated)
* best frameworks are the frameworks you developed
* one class, one idea

# Testing

* **write code first and then the tests** - if you write the test before you might need to change it as you realize that your initial API won't be good
* **focus on tests for hard to reproduce cases**
* **prefer integration tests / bigger units** - class-level unit tests work most for leaf-code but preferably take bigger units so you catch integration problems faster and you write and maintain less tests
* **assume your tests will run in parallel**

# Reviewer check-list

* Long operations, can there be parallel operations changing the same data?
* Async operation response, does the initial conditions still hold? 
* Does the code look reasonably readable?
* Atomicity, does the multi step operation handles atomicity/eventual consistency well?
* High performance code paths, double check on performance issues?
* Background jobs: Do they have record beginning and end of processing
* Background jobs: How much data do they consume?
* Database: Do you have queries with no indices?
* Database: Do you have frequent writes? Might fry the performance.
* Distributed Data Structures: Does the operation scale with increased number of nodes?
* High Availabilty: If you keep data in distributed data structures, is it possible to have an HA leak? 

