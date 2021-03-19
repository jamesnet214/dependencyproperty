# DependencyProperty
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
[![GPLv3 license](https://img.shields.io/badge/License-GPLv3-blue.svg)](http://perso.crans.org/besson/LICENSE.html)

## DevNcore Repository
> DevNcore Git. [here.](https://github.com/devncore/devncore)

## 2. DependencyProperty
1. Class
2. Naming Rules
3. DependencyProperty.Register
4. PropertyMetadata

### 2.1. Class Structure
namespace: `System.Windows`   
assembly: `WindowsBase.dll`   
class access: `sealed`   
first version: `.net 3.0`
```csharp
namespace System.Windows
{
    public sealed class DependencyProperty
    {

    }   
}
```

### 2.2. Naming Rules



### 2.3. DependencyProperty.Register

### 2.4. PropertyMetadata

## 3. Example

### 3.1. Standard Type
#### Int Type DependencyProperty
```csharp
public class Profile : Control
{
    public int Age
    {
        get { return (int)this.GetValue(AgeProperty); }
        set { this.SetValue(AgeProperty, value); }
    }

    public static readonly DependencyProperty AgeProperty = DependencyProperty.Register(
        "Age", typeof(int), typeof(Profile), new PropertyMetadata(0));
}
```

#### Boolean Type DependencyProperty
```csharp
public class Profile : Control
{
    public bool IsUsed
    {
        get { return (bool)this.GetValue(IsUsedProperty); }
        set { this.SetValue(IsUsedProperty, value); }
    }

    public static readonly DependencyProperty IsUsedProperty = DependencyProperty.Register(
        "IsUsed", typeof(bool), typeof(Profile), new PropertyMetadata(false));
}
```

#### String Type DependencyProperty
```csharp
public class Profile : Control
{
    public string Header
    {
        get { return (string)this.GetValue(HeaderProperty); }
        set { this.SetValue(HeaderProperty, value); }
    }

    public static readonly DependencyProperty HeaderProperty = DependencyProperty.Register(
        "Header", typeof(string), typeof(Profile), new PropertyMetadata(""));
}
```

#### Object Type DependencyProperty
```csharp
public class CustomControl : Control
{
    public object Content
    {
        get { return (object)this.GetValue(ContentProperty); }
        set { this.SetValue(ContentProperty, value); }
    }

    public static readonly DependencyProperty ContentProperty = DependencyProperty.Register(
        "Content", typeof(object), typeof(Profile), new PropertyMetadata(""));
}
```
It is actually the same as the Content Property included in the ContentControl class. If you inherit ContentControl and create a control that defines ContentPresenter, use Object-type DependencyProperty.

#### Geometry Type DependencyProperty
```csharp
public class PathIcon : Control
{
    public Geometry Data
    {
        get { return (Geometry)this.GetValue(DataProperty); }
        set { this.SetValue(DataProperty, value); }
    }

    public static readonly DependencyProperty DataProperty = DependencyProperty.Register(
        "Data", typeof(Geometry), typeof(PathIcon), new PropertyMetadata(null));
}
```

#### Brush Type DependencyProperty
```csharp
public class GeometryIcon : Control
{
    public Brush Fill
    {
        get { return (Brush)this.GetValue(FillProperty); }
        set { this.SetValue(FillProperty, value); }
    }

    public static readonly DependencyProperty FillProperty = DependencyProperty.Register(
        "Fill", typeof(Brush), typeof(GeometryIcon), new PropertyMetadata(null));
}
```


#### Double Type DependencyProperty
```csharp
public class GeometryIcon : Control
{
    public double IconWidth
    {
        get { return (double)this.GetValue(IconWidthProperty); }
        set { this.SetValue(IconWidthProperty, value); }
    }

    public static readonly DependencyProperty IconWidthProperty = DependencyProperty.Register(
        "IconWidth", typeof(double), typeof(GeometryIcon), new PropertyMetadata(0));
}
```

#### ICommand
```csharp
public static readonly DependencyProperty CommandProperty = DependencyProperty.Register(
    "Command", typeof(ICommand), typeof(ControlTreeView));
```
```csharp
public ICommand Command
{
    get { return (ICommand)this.GetValue(CommandProperty); }
    set { this.SetValue(CommandProperty, value); }
}
```

### 3.2. Extender Property
```csharp
class PasswordExtender
{
    public static readonly DependencyProperty PasswordProperty =
        DependencyProperty.RegisterAttached("Password",
        typeof(string), typeof(PasswordExtender),
        new FrameworkPropertyMetadata(string.Empty, OnPasswordPropertyChanged));
}
```
```csharp
public static string GetPassword(DependencyObject dp)
{
    return (string)dp.GetValue(PasswordProperty);
}

public static void SetPassword(DependencyObject dp, string value)
{
    dp.SetValue(PasswordProperty, value);
}
```
```csharp
private static void OnPasswordPropertyChanged(DependencyObject sender,
    DependencyPropertyChangedEventArgs e)
{
}
```

### 3.3. Value Callback Changed
```csharp
public string Password
{
    get { return (string)this.GetValue(PasswordProperty); }
    set { this.SetValue(PasswordProperty, value); }
}
public static readonly DependencyProperty PasswordProperty =
    DependencyProperty.Register("Password", typeof(string), typeof(VisualPassword),
        new PropertyMetadata(string.Empty, PasswordPropertyChanged));

private static void PasswordPropertyChanged(DependencyObject d, DependencyPropertyChangedEventArgs e)
{
    
}
```

### 3.4. Binding Core Callback MVVM
```csharp
public string Password
{
    get { return (string)this.GetValue(PasswordProperty); }
    set { this.SetValue(PasswordProperty, value); }
}

public static readonly DependencyProperty PasswordProperty =
DependencyProperty.Register(
        "Password", 
        typeof(string), 
        typeof(VisualPassword),
        new FrameworkPropertyMetadata( 
                string.Empty, 
                FrameworkPropertyMetadataOptions.BindsTwoWayByDefault | FrameworkPropertyMetadataOptions.Journal,
                new PropertyChangedCallback(OnPasswordPropertyChanged),
                new CoerceValueCallback(CoercePassword),
                true, 
                UpdateSourceTrigger.LostFocus 
                ));


private static void OnPasswordPropertyChanged(DependencyObject sender, DependencyPropertyChangedEventArgs args)
{
    VisualPassword p = sender as VisualPassword;

    if (!p._password.Password.Equals(args.NewValue?.ToString()))
    {
        p._password.PasswordChanged -= p._password_PasswordChanged;
        p._password.Password = args.NewValue?.ToString();
        p._password.PasswordChanged += p._password_PasswordChanged;
    }
}
private static object CoercePassword(DependencyObject d, object value)
{
    if (value == null)
    {
        return String.Empty;
    }

    return value;
}
```
## 4. Opensource

## 99. References
> Article Tutorial 2 [here.](https://www.wpftutorial.net/DependencyProperties.html)
> Article Tutorial 2 [here.](https://sodocumentation.net/wpf/topic/2914/dependency-properties)
> 



[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
[![GPLv3 license](https://img.shields.io/badge/License-GPLv3-blue.svg)](http://perso.crans.org/besson/LICENSE.html)
[![Github all releases](https://img.shields.io/github/downloads/Naereen/StrapDown.js/total.svg)](https://GitHub.com/Naereen/StrapDown.js/releases/)
