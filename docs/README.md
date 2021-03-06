# Castle Windsor Documentation


<img align="right" src="images/windsor-logo.png">

Castle Windsor is best of breed, mature [Inversion of Control container](ioc.md) available for .NET.

Castle Windsor 是.net平台上最成熟，最好用的 [IOC容器](ioc.md).

* See [the release notes](https://github.com/castleproject/Windsor/releases/tag/v3.3)
* [Download it](https://github.com/castleproject/Windsor/releases/tag/v3.3)
* Get official builds from [NuGet](http://nuget.org/packages/Castle.Windsor): `PM> Install-Package Castle.Windsor`
* Or [get pre-release packages as they're built](https://github.com/castleproject/Home/blob/master/prerelease-packages.md)

## Show me the code already
## 展示 Castle Windsor 功能的代码

Windsor is very simple to use. Code below is not just *hello world* - that's how many big real life applications use Windsor. See the full documentation for more details on the API, features, patterns, and practices.

Windsor 使用起来非常简单。 下面的代码不仅仅是*hello world* - 这就是很多大型应用程序使用Windsor的代码。 有关API, features, patterns, and practices 的更多详细信息，请参阅完整文档。

```csharp
// application starts...
// 启动应用程序
var container = new WindsorContainer();

// adds and configures all components using WindsorInstallers from executing assembly
// 使用 WindsorInstaller 前程序集添加和配置所有的 components
container.Install(FromAssembly.This());

// instantiate and configure root component and all its dependencies and their dependencies and...
// 实例化和配置 root component 以及它的所有依赖
var king = container.Resolve<IKing>();
king.RuleTheCastle();

// clean up, application exits
// 清理，退出应用
container.Dispose();
```

So what about those [installers](installers.md)? Here's one.

什么是 [installers](installers.md)? 这里有一个例子

```csharp
// 译注: WindsorInstaller 是一个类: 一般用于集中管理当前程序集中所有注册 componet 到容器的代码.
public class RepositoriesInstaller : IWindsorInstaller
{
	public void Install(IWindsorContainer container, IConfigurationStore store)
	{
		container.Register(Classes.FromThisAssembly()
			                .Where(Component.IsInSameNamespaceAs<King>())
			                .WithService.DefaultInterfaces()
			                .LifestyleTransient());
	}
}
```

For more in-depth sample try the section below, or dive right into API documentation on the right.

有关更深入的示例，请尝试以下部分，或直接进入右侧的API文档。

## Samples and tutorials

Learn Windsor by example by completing step-by-step tutorials. See Windsor in action by exploring sample applications showcasing its capabilities:

通过完成分步教程，例子学习 windsor. 

* [Basic tutorial](basic-tutorial.md)
* [Simple ASP.NET MVC 3 application (To be Seen)](mvc-tutorial-intro.md) - built step by step from the ground up. This tutorial will help you get up to speed with Windsor quickly while keeping an eye on both the usage of the container API as well as patterns that will help you get the most out of using the container.

## Documentation

* [What's new in Windsor 3.2](whats-new-3.2.md)
* [What's new in Windsor 3.1](whats-new-3.1.md)

### Concepts

* [Inversion of Control and Inversion of Control Container](ioc.md)
* [ioc 和 ioc 容器](ioc.md)
* [Services, Components and Dependencies](services-and-components.md)
* [How components are created](how-components-are-created.md)
* [component 创建过程](how-components-are-created.md)
* [how dependencies are resolved](how-dependencies-are-resolved.md)
* [dependency 解析过程](how-dependencies-are-resolved.md)

### Using the Container

* [Using the container - how and where to call it](three-calls-pattern.md)
* [Windsor installers - this is how you tell Windsor about your components](installers.md)
* [Registration API reference](fluent-registration-api.md)
* [Using XML configuration](xml-registration-reference.md)
* [Passing arguments to the container](passing-arguments.md)
* [AOP, Proxies, and Interceptors](interceptors.md)
* [Child Containers](child-containers.md)
* [Windsor's support for debugger views and diagnostics](debugger-views.md)
* [Windsor's support for performance counters](performance-counters.md)

### Customizing the container

* [Extension Points Overview](extension-points.md)
* [Lifestyles](lifestyles.md)
* [Lifecycle](lifecycle.md)
* [Release Policy](release-policy.md)
* [ComponentModel construction contributors](componentmodel-construction-contributors.md)

### Extending the container

* [Facilities](facilities.md)

### Know another container

* [Castle Windsor for Autofac users](windsor-for-autofac-users.md)
* [Castle Windsor for StructureMap users](windsor-for-structuremap-users.md)

## Resources

* [External Resources](external-resources.md) - screencasts, podcasts, etc
* [FAQ](faq.md)
* [Roadmap](roadmap.md)
