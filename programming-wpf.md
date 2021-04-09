## Dependency Properties

Although our data source Nickname object made its data available via standard .NET
properties, we need something special to support data binding on the target element. Even though the TextContent property of the TextBlock element is exposed
with a standard property wrapper, in order for it to integrate with WPF services like
data binding, styling, and animation, it also needs to be a dependency property. A
dependency property provides several features not present in .NET properties,
including the ability to inherit its value from a container element, provide for objectindependent storage (providing a potentially huge memory savings), and change
tracking.

Most of the time, you won’t have to worry about dependency properties versus .NET
properties, but when you need the details, you can read about them in Chapter 18.
