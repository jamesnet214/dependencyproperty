# DependencyProperty
### Our
Contributors [Here.](https://devncore.org/aboutus/contributors)   
### DevNcore
GitHub Organization [Here.](https://github.com/devncore)   
Official Website [Here.](https://devncore.org)   
### License Policy
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
[![GPLv3 license](https://img.shields.io/badge/License-GPLv3-blue.svg)](http://perso.crans.org/besson/LICENSE.html)

## _What is the DependencyProperty?_
**DependencyProperty**는 DependencyObject에서 파생되는 클래스의 속성이며, 단순히 백업 필드를 사용하여 값을 저장하는 것이 아니라 DependencyObject에서 일부 도우미 메서드를 사용한다는 점에서 특별합니다.   

가장 좋은 점은 데이터 바인딩을위한 모든 배관이 내장되어 있다는 것입니다. 무언가를 바인딩하면 변경 될 때 알림을 보냅니다.

여러분이 MVVM 패턴을 더욱 더 적극적으로 활용하기 위해서는 `DependencyProperty`가 필연적으로 필요합니다.
## 1. Orverview
이 문서는 DependencyProperty 속성에 관련된 연구 기술 논문입니다. WPF는 이 의존 프로퍼티를 통해 강력한 Binding, 프로퍼티 상속 구조를 지니고 있기 때문에 기술의 범위와 깊이에 있어 다소 높은 난이도를 필요로 합니다.
#### 1.1. Class Version 
The first target version of DependencyProperty is based on .NET Frmaeowrk `3.0`
| Target Name    | Version                                                                                  |
|:---------------|:-----------------------------------------------------------------------------------------|
| .NET           | 5.0                                                                                      |
| .NET Core      | 3.0, 3.1                                                                                 |
| .NET Framework | 3.0, 3.5, 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2, 4.8              |

#### _So .NET Framework 2.0 doesn't allow us to use DependencyProperty?_   
> That's right. WPF starts at 3.0. :smile:

#### 1.2. Class Information
| Assembly             | Namespace                   | Class Access        | Base Class      |
|:---------------------|:----------------------------|:--------------------|:----------------|
| WindowsBase.dll      | System.Windows              | `sealed`            | `Object`        |

#### 1.3. Class Structure
DependencyPropery 클래스의 Access 권한은 `sealed`이므로 직접 상속받을 수 없습니다.

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

## 2. Declaration
DependencyProperty 선언 구조를 응용하여 필요로 하는 속성 `Type`을 만들 수 있습니다.
#### 2.1. Example of dependency-properties by type

#### Int type
Register `Int` Type Dependency Property
```csharp
public static readonly DependencyProperty AgeProperty = DependencyProperty.Register(
    "Age", typeof(int), typeof(<class>), new PropertyMetadata(0));
```
```csharp
public int Age
{
    get { return (int)this.GetValue(AgeProperty); }
    set { this.SetValue(AgeProperty, value); }
}
```

#### Boolean Type
```csharp
public static readonly DependencyProperty IsUsedProperty = DependencyProperty.Register(
    "IsUsed", typeof(bool), typeof(<class>), new PropertyMetadata(false));
```
```csharp
public bool IsUsed 
{ 
    get { return (bool)this.GetValue(IsUsedProperty); }
    set { this.SetValue(IsUsedProperty, value); }
}
```

#### String Type
```csharp
public static readonly DependencyProperty PlaceHolderProperty = DependencyProperty.Register(
    "Header", typeof(string), typeof(<class>), new PropertyMetadata(""));
```
```csharp
public string PlaceHolder
{
    get { return (string)this.GetValue(PlaceHolderProperty); }
    set { this.SetValue(PlaceHolderProperty, value); }
}
```

#### Object Type
```csharp
public static readonly DependencyProperty ContentProperty = DependencyProperty.Register(
    "Content", typeof(object), typeof(<class>), new PropertyMetadata(""));
```
```csharp
public object Content
{
    get { return (object)this.GetValue(ContentProperty); }
    set { this.SetValue(ContentProperty, value); }
}
```
It is actually the same as the Content Property included in the ContentControl class. If you inherit ContentControl and create a control that defines ContentPresenter, use Object-type DependencyProperty.

#### Geometry Type
```csharp
public static readonly DependencyProperty DataProperty = DependencyProperty.Register(
    "Data", typeof(Geometry), typeof(<침ㄴㄴ>), new PropertyMetadata(null));
```
```csharp
public Geometry Data
{
    get { return (Geometry)this.GetValue(DataProperty); }
    set { this.SetValue(DataProperty, value); }
}
```

#### Brush Type
```csharp
public static readonly DependencyProperty FillProperty = DependencyProperty.Register(
    "Fill", typeof(Brush), typeof(<class>), new PropertyMetadata(null));
```
```csharp
public Brush Fill
{
    get { return (Brush)this.GetValue(FillProperty); }
    set { this.SetValue(FillProperty, value); }
}
```


#### Double Type
```csharp
public static readonly DependencyProperty IconWidthProperty = DependencyProperty.Register(
    "IconWidth", typeof(double), typeof(<class>), new PropertyMetadata(0));
```
```csharp
public double IconWidth
{
    get { return (double)this.GetValue(IconWidthProperty); }
    set { this.SetValue(IconWidthProperty, value); }
}
```

#### ICommand
```csharp
public static readonly DependencyProperty SelectionCommandProperty = DependencyProperty.Register(
    "SelectionCommand", typeof(ICommand), typeof(<class>));
```
```csharp
public ICommand SelectionCommand
{
    get { return (ICommand)this.GetValue(SelectionCommandProperty); }
    set { this.SetValue(SelectionCommandProperty, value); }
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
### 99.1 Community Docs
#### WPF Tutorial
> DependencyProperties [here.](https://www.wpftutorial.net/DependencyProperties.html)   
#### So Documentation
> Dependency-Properties [here.](https://sodocumentation.net/wpf/topic/2914/dependency-properties)   
#### Microsoft Docs
> DependencyProperty Class [Here.](https://docs.microsoft.com/ko-kr/dotnet/api/system.windows.dependencyproperty?view=netframework-4.8)   

