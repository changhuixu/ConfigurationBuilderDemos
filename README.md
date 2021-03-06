# `ConfigurationBuilder` Demos

<a href='https://ko-fi.com/changhuixu' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://cdn.ko-fi.com/cdn/kofi3.png?v=2' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>

![Binding an array](./array-binding-configuration.png)

## Binding a JSON Array to an Array Object

Recently, when I set a JSON array in the `appsettings.json` files in an ASP.NET Core project, the result of the final configuration data surprised me. After some googling, I found that there are already many Stack Overflow questions ([1](https://stackoverflow.com/questions/51614792/how-to-override-an-asp-net-core-configuration-array-setting-reducing-length-of-t), [2](https://stackoverflow.com/questions/49136954/how-can-i-override-an-array-based-setting-from-appsettings-json-in-an-environmen), [3](https://stackoverflow.com/questions/37657320/how-to-override-asp-net-core-configuration-array-settings-using-environment-vari), [4](https://stackoverflow.com/questions/52755027/override-array-settings-in-appsettings-json-with-those-in-appsettings-production), and [5](https://stackoverflow.com/questions/45819524/removing-inherited-asp-net-core-appsettings)) and GitHub issues ([1](https://github.com/dotnet/runtime/issues/36569), [2](https://github.com/dotnet/runtime/issues/36384), [3](https://github.com/aspnet/Configuration/issues/836), [4](https://github.com/aspnet/Configuration/issues/694), [5](https://github.com/aspnet/Configuration/issues/727), and [6](https://github.com/aspnet/Configuration/issues/773)) discussing this interesting behavior of configuration inheritance for arrays. I think it is worth writing a short article to describe the "problem" so that you won't stumble on the same stone.

ASP.NET Core uses configuration providers to read configuration key-value pairs from a variety of sources. If there are some key-value pairs with the same keys, then a configuration provider that is added later will override previous key settings. You can read more about configuration in ASP.NET Core in [its official documentation](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/), which has covered tons of use cases in detail.

We usually put some generic configuration data in the `appsettings.json` file, and put environment-specific configurations in the `appsettings.{Environment}.json` file and/or in the environment variables. In this way, the system can override the settings based on the runtime environment when the application starts. For example, a connection string set in the `appsettings.json` file will be used for the development environment if its value is not set in the `appsettings.Development.json` file. On the other hand, if a connection string is set in the `appsettings.Production.json` file, then the value in the `appsettings.json` file will be overridden and the value in the `appsettings.Production.json` file will be used in the production environment.

I also traced back and found this behavior was first proposed in [this GitHub issue](https://github.com/aspnet/Configuration/issues/115#issuecomment-95433424).

## License

Feel free to use the code in this repository as it is under MIT license.

<a href='https://ko-fi.com/changhuixu' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://cdn.ko-fi.com/cdn/kofi3.png?v=2' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>
