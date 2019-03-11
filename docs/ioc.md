# Inversion of Control
# IOC

Inversion of Control is a principle used by frameworks as a way to allow developers to extend the framework or create applications using it. The basic idea is that the framework is aware of the programmer's objects and makes invocations on them.

ioc 是一种原则被框架用于允许开发人员扩展框架 / 创建应用程序。  基本思想是框架知道程序员的对象并对它们进行调用。

This is the opposite of using an API, where the developer's code makes the invocations to the API code. Hence, frameworks invert the control: it is not the developer code that is in charge, instead the framework makes the calls based on some stimulus.

这与使用API相反, 其由开发人员的代码对API代码进行调用。因此，框架反转了控制: 不由开发人员的代码负责，而是由框架基于某些触发来调用。

You have probably been in situations where you have developed under the light of this principle, even though you were not aware of it.

你可能在已经基于这一原则开发，即使没有明确意识到它。

## Inversion of Control Container
## IOC 容器

An Inversion of Control Container uses the principle stated above to (in a nutshell) manage classes. That is, their creation, destruction, lifetime, configuration, and dependencies. This way classes do not need to obtain and configure the classes they depend on. This dramatically reduces coupling in a system and, as a consequence, simplifies reuse and testability.

ioc 容器使用上述原则来管理类。也就是说它负责 creation, destruction, lifetime, configuration, and dependencies.这样，类不需要获取和配置它们所依赖的类。这大大减少了系统中的耦合，因此简化了重用和可测试性。

There is some confusion created by people that think that 'Inversion of Control' is a synonym for 'Inversion of Control Container'. As stated, Inversion of control is a broader principle.

人们认为“ioc”是“ioc container”的同义词，造成了一些混乱。 如上所述，ioc是一个比 ioc container 更广泛的原则。

Often people think that it is all about "injection", and broadcast that this is the primary purpose of IoC containers. In fact, "injection" is a consequence, a means to decouple, not the primary purpose.

通常人们认为这完全是关于“injection”，并且传播说这是IoC容器的主要目的。 事实上，“injection”是一种结果，一种解耦的手段，而不是主要目的。

## External resources
## 外部资源

* [Blog post by Stefano Mazzocchi (Jan 22, 2004)](http://www.betaversion.org/~stefano/linotype/news/38/)
* [bliki article by Martin Fowler, which totally misses the point](http://www.martinfowler.com/articles/injection.html)
