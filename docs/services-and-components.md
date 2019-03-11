# Services and Components

Components, services and dependencies:

![](images/component.png)

As every technology, Windsor has certain basic concepts that you need to understand in order to be able to properly use it. Fear not - they may have scary and complicated names and abstract definitions but they are quite simple to grasp.

作为每项技术，Windsor都有一些您需要了解的基本概念才能正确使用它。 不要害怕 - 他们可能有可怕和复杂的名字和抽象的定义，但他们很容易掌握。

## Service
## 服务

:information_source: **Service in Windsor and WCF service:** The term service is extremely overloaded and has become even more so in recent years. Services as used in this documentation are a broader term than for example WCF services.

:信息源: **Windsor 的 service 和WCF 中的 service：** service 一词过度滥用，近年来变得更加严重。 本文档中使用的 service 是一个比WCF service 更广泛的术语。


First concept that you'll see over and over in the documentation and in Windsor's API is **service**. Actual definition goes somewhat like this: "*service is an abstract contract describing some cohesive unit of functionality*".

第一个概念就是 **service**, 它在 windsor 的文档中被反复提及。 它的实际定义有点像这样: "*service 是一个  abstract contract describing ,内聚的功能单元集合*"

Now in plain language, let's imagine you enter a coffee shop you've never been to. You talk to the barista, order your coffee, pay, wait and enjoy your cup of perfect Cappuccino. Now, let's look at the interactions you went through:

现在用简单的语言，让我们想象你进入一个你从未去过的咖啡馆。 你和咖啡师聊天，点咖啡，付钱，等待，享受一杯完美的卡布奇诺咖啡。 现在，让我们来看看你经历的互动：

* specify the coffee you want
* 点一杯咖啡
* pay
* 付款
* get the coffee
* 拿到咖啡

They are the same for pretty much every coffee shop on the planet. They are the coffee shop service. Does it start making a bit more sense now? The coffee shop has clearly defined, cohesive functionality it exposes - it makes coffee. The contract is pretty abstract and high level. It doesn't concern itself with "implementation details"; what sort of coffee-machine and beans does the coffee shop have, how big it is, and what's the name of the barista, and color of her shirt. You, as a user don't care about those things, you only care about getting your cappuccino, so all the things that don't directly impact you getting your coffee do not belong as part of the service.

对于这个星球上几乎每家咖啡店来说，它们都是一样的。 他们是咖啡店服务。 它现在开始变得更有意义了吗？ 咖啡店有明确的，有凝聚力的功能，它可以制作咖啡。 合同是相当抽象和高水平的。 它并不涉及“实施细节”; 咖啡店有什么样的咖啡机和豆子，有多大，咖啡师的名字和衬衫的颜色是什么。 你作为一个用户不关心这些东西，你只关心你的卡布奇诺咖啡，所以所有不直接影响你喝咖啡的东西都不属于服务的一部分。

Hopefully you're getting a better picture of what it's all about, and what makes a good service. Now back in .NET land we might define a coffee shop as an interface (since interfaces are by definition abstract and have no implementation details you'll often find that your services will be defined as interfaces).

希望您能更好地了解它的全部内容，以及什么是一个好的 service。 现在回到.NET领域，我们可以将咖啡店定义为一个接口（因为接口按照定义是抽象的，没有实现细节，您经常会发现您的服务将被定义为接口）。

```csharp
public interface ICoffeeShop
{
   Future<Coffee> GetCoffee(CoffeeRequest request);
}
```

The actual details obviously can vary, but it has all the important aspects. The service defined by our `ICoffeeShop` is high level. It defines all the aspects required to successfully order a coffee, and yet it doesn't leak any details on who, how or where prepares the coffee.

实际细节显然可以有所不同，但它具有所有重要方面。 我们的`ICoffeeShop`定义的服务是高级的。 它定义了成功订购咖啡所需的所有方面，但它没有泄漏任何关于谁，如何或在何处准备咖啡的细节。

If coffee is not your thing, you can find examples of good contracts in many areas of your codebase. `IController` in ASP.NET MVC, which defines all the details required by ASP.NET MVC framework to successfully plug your controller into its processing pipeline, yet gives you all the flexibility you need to implement the controller, whether you're building a social networking site, or e-commerce application.

如果您不喜欢咖啡，您可以在代码库的许多方面找到合同的示例。 ASP.NET MVC中的“IController”，它定义了ASP.NET MVC框架成功将控制器插入其处理管道所需的所有细节，同时为您提供实现控制器所需的所有灵活性，无论您是在构建 社交网站或电子商务应用程序。

If that's all clear and simple now, let's move to the next important concept.

## Component

Component is related to service. Service is an abstract term and we're dealing with concrete, real world. A coffee shop as a concept won't make your coffee. For that you need an actual coffee shop that puts that concept in action. In C# terms this usually means a class implementing the service will be involved.

```csharp
public class Starbucks: ICoffeeShop
{
   public Future<Coffee> GetCoffee(CoffeeRequest request)
   {
      // some implementation
   }
}
```

So far so good. Now the important thing to remember is that, just as there can be more than one coffee shop in town, there can be multiple components, implemented by multiple classes in your application (a Starbucks, and a CofeeClub for example).

It doesn't end there! If there can be more than one Starbucks in town, there can also be more than one component backed by the same class. If you've used NHibernate, in an application accessing multiple databases, you probably had two session factories, one for each database. They are both implemented by the same class, they both expose the same service, yet they are two separate components (having different connection strings, they map different classes, or potentially one is talking to Oracle while the other to SQL Server).

It doesn't end there (still)! Who said that your local French coffee shop can only sell coffee? How about a tarte or fresh baguette to go with the coffee? Just like in real life a coffee shop can serve other purposes a single component can expose multiple services.

One more thing before we move forward. While not implicitly stated so far it's probably obvious to you by now that a component provides a service (or a few). As such all the classes in your application that do not really provide any services will not end up as components in your container. Domain model classes, DTOs are just a few examples of things you will not put in a container.

## Dependency

We're almost there. To get the full picture we need to talk about dependencies first.

A component working to fulfill its service is not living in a vacuum. Just like a coffee shop depends on services provided by utility companies (electricity), its suppliers (to get the beans, milk etc) most components will end up delegating non-essential aspects of what they're doing to others.

Now let me repeat one thing just to make sure it's obvious. Components depend on services of other components. This allows for nicely decoupled code where your coffee shop is not burdened with details of how the milk delivery guy operates.

In addition to depending on other component's services your components will also sometimes use things that are not components themselves. Things like connectionStrings, names of servers, values of timeouts and other configuration parameters are not services (as we discussed previously) yet are valid (and common) dependencies of a component.

In C# terms your component will declare what dependencies it requires usually via constructor arguments or settable properties. In some more advanced scenarios dependencies of a component may have nothing to do with the class you used as implementation (remember, the concept of a component is not the same as a class that might be used as its implementation), for example when you're applying interceptors. This is advanced stuff however so you don't have to concern yourself with it if you're just starting out.

## Putting it all together

So now lets put it all together. To effectively use a container we're dealing with small components, exposing small, well defined, abstract services, depending on services provided by other components, and on some configuration values to fulfil contracts of their services.

You will end up having many small, decoupled components, which will allow you to rapidly change and evolve your application limiting the scope of changes, but the downside of that is you'll end up having plenty small classes with multiple dependencies that someone will have to manage.

That is the job of a container.
