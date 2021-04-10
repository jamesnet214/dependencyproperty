# DependencyProperty
### About us
Contributors [Here.](https://devncore.org/aboutus/contributors)

### DevNcore
GitHub Organization [Here.](https://github.com/devncore)   
Official Website [Here.](https://devncore.org) 

### License Policy
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
[![GPLv3 license](https://img.shields.io/badge/License-GPLv3-blue.svg)](http://perso.crans.org/besson/LICENSE.html)

<br />  

## _What is the DependencyProperty?_
The __DependencyProperty__ class is one of the most important design bases hidden deep in the .Net Framework WPF.

This class is protected by sealed from the .Net Framework.
This property differs from the one-dimensional general property in that it not only stores field values, but also takes advantage of the various functions provided within the class.
Most importantly, there is a full foundation for data binding. You can also send notifications whenever you bind something.  

The MVVM development methodology already has a limited set of DependencyProperty provided by the .Net Framework, so this technology is essential to more aggressive use of Binding.


## Overview
DependencyProperty is one of the key design elements of the WPF. This involves a combination of concepts and logical structures rather than a single function, requiring in-depth research and a somewhat higher degree of difficulty in the scope and depth of the technology.

#### Class Version 
The first target version of DependencyProperty is based on .NET Framework `3.0`

| Target Name    | Version                                                                                  |
|:---------------|:-----------------------------------------------------------------------------------------|
| .NET           | 5.0                                                                                      |
| .NET Core      | 3.0, 3.1                                                                                 |
| .NET Framework | 3.0, 3.5, 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2, 4.8              |

##### _So, .NET Framework 2.0 doesn't allow us to use DependencyProperty?_   
> That's right. WPF starts at 3.0. :smile:

#### Class Information
| Assembly             | Namespace                   | Class Access        | Base Class      |
|:---------------------|:----------------------------|:--------------------|:----------------|
| WindowsBase.dll      | System.Windows              | `sealed`            | `Object`        |

#### 1.3. Class Structure
Access rights in the DependencyProperty class is `sealed` and have a structure that cannot be inherited directly from the custom class.

```csharp
namespace System.Windows
{
    public sealed class DependencyProperty
    {

    }   
}
```
## Understanding DependencyProperty
- [Using Property](#using-property)

### Using Property
DependencyProperty 속성은 기본적으로 일반 속성처럼 사용이 가능하기 때문에 `get`과 `set`을 자유롭게 사용할 수 있습니다.
```csharp
Button btn = new Button();
btn.Content = "James";
btn.Width = 100;
btn.Height = 50;

double width = btn.Width;
double height = btn.Height;
string Content = btn.Content.ToString();
```
Xaml 디자인 영역에서의 사용도 크게 다르지 않습니다.
```xaml
<Button Content="Elena" Width="100" Height="50"/>
```


## Did You Know That?
- [x] DependencyProperty 속성은 일반적인 속성처럼 사용이 가능합니다.
- [x] Xaml 영역에서 접근이 가능한 대부분의 컨트롤 속성들은 DependencyProperty 입니다.
- [x] DependencyProperty 속성을 등록은 static 생성자에서 하는 것이 일반적입니다.
- [x] 새로운 속성을 DependencyProperty를 통해 등록하기 위해서는 특별한 속성 래퍼(Wrapper) 선언이 필요합니다.
- [x] WPF에서의 Value Binding은 오직 DependencyProperty를 통해 선언 된 속성만이 가능합니다.
- [x] DependencyProperty 속성은 기본적으로 상위(부모)로 부터 값을 물려받을 수 있습니다.
- [x] Element Binding 대상과 타겟 속성 모두 반드시 DependencyProperty  가능합니다.
- [x] WPF는 DependencyProperty 고유의 의존 속성 덕분에 속성 값의 양을 엄청나게 줄일 수 있게 되었습니다.
- [x] DependencyProperty 클래스는 public set 속성이 단 하나도 존재하지 않습니다.
- [x] DependencyProperty 클래스는 public 생성자가 없기 때문에 인스턴스를 생성할 수가 없습니다.
- [x] DependencyProperty 클래스는 sealed 한정자로부터 보호받고 있기 때문에 클래스 상속이 불가능합니다.
- [x] DependencyProperty는 WPF .NET Framework에서 가장 많이 선언되어있는 클래스입니다.
- [x] CoerceValueCallback 이벤트를 통해 관련 값을 강제로 변환하도록 호출할 수 있습니다.
- [x] static Register메서드는 총 3개의 Override 파라메터 형태를 제공합니다.
- [x] DependencyProperty는 2개의 재정의 된 Override 메서드가 존재합니다. `GetHashCode()` `ToString()`
- [x] 사실 DependencyProperty 속성의 .ToString() 값은 일반 속성과 다를 바가 없습니다.
- [x] DependencyProperty 속성은 INotifyPropertyChanged 방식보다 복잡하지만 대신 더욱 더 강력합니다.
- [x] DependencyProperty는 충분히 WPF를 경험하고 배우는 것이 바람직합니다.
- [x] Winform에서는 DependencyProperty가 존재하지 않습니다.




## Declaration
DependencyProperty can be registered in two ways.
- [Standard](#21-Standard)
- [Extender](#22-Extender)

### 2.1. Standard
Standard method is to connect(register) directly to the `Owner UI` class through the `DependencyProperty.Register` method.
- [Int](#211-Standard-Int)
- [Boolean](#212-Standard-Boolean)
- [String](#213-String-Type)
- [Object](#214-Object-Type)
- [Geometry](#215-Geometry-Type)
- [Brush](#216-Brush-Type)
- [Double](#217-Double-Type)
- [ICommand](#218-ICommand-Type)

#### 2.1.1. [Standard] Int
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
 
#### 2.1.2. [Standard] Boolean
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

#### 2.1.3. [Standard] String
```csharp
public static readonly DependencyProperty PlaceHolderProperty = DependencyProperty.Register(
    "PlaceHolder", typeof(string), typeof(<class>), new PropertyMetadata(""));
```
```csharp
public string PlaceHolder
{
    get { return (string)this.GetValue(PlaceHolderProperty); }
    set { this.SetValue(PlaceHolderProperty, value); }
}
```

#### 2.1.4. [Standard] Object

It is actually the same as the Content Property included in the `ContentControl` class.  
If you inherit ContentControl and create a control that defines ContentPresenter, use Object-type DependencyProperty.

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
#### Exists Properties
- Content in `ContentControl` (Button, CheckBox, UserControl, Window ···)   
- Tag in `Control` (Button, Window, Grid, StackPanel ···)

#### 2.1.5. [Standard] Geometry
```csharp
public static readonly DependencyProperty DataProperty = DependencyProperty.Register(
    "Data", typeof(Geometry), typeof(<class>), new PropertyMetadata(null));
```
```csharp
public Geometry Data
{
    get { return (Geometry)this.GetValue(DataProperty); }
    set { this.SetValue(DataProperty, value); }
}
```
#### Exists Properties
- Data in `Path`

#### 2.1.6. [Standard] Brush
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


#### 2.1.7. [Standard] Double
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

#### 2.1.8. [Standard] ICommand
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
<br />

### 2.2. Extender
#### 2.2.1. [Extender] String
```csharp
class PasswordExtender
{
    public static readonly DependencyProperty PasswordProperty =
        DependencyProperty.RegisterAttached("Password",
        typeof(string), typeof(PasswordExtender),
        new FrameworkPropertyMetadata(string.Empty, OnPasswordPropertyChanged));
    public static string GetPassword(DependencyObject dp)
    {
        return (string)dp.GetValue(PasswordProperty);
    }

    public static void SetPassword(DependencyObject dp, string value)
    {
        dp.SetValue(PasswordProperty, value);
    }
    
    private static void OnPasswordPropertyChanged(DependencyObject sender,
        DependencyPropertyChangedEventArgs e)
    {
    }
}
```
<br />

### 3. Property Changed
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
<br />

### 4. CoerceValueCallback
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

    private static object CoercePassword(DependencyObject d, object value)
    {
        if (value == null)
        {
            return String.Empty;
        }

        return value;
    }
}
```
<br />

<br />

## 6. References
### 6.1 Community Docs
#### WPF Tutorial
> DependencyProperties [here.](https://www.wpftutorial.net/DependencyProperties.html)   
#### SO Documentation
> Dependency-Properties [here.](https://sodocumentation.net/wpf/topic/2914/dependency-properties)   
#### Microsoft Docs
> DependencyProperty Class [Here.](https://docs.microsoft.com/ko-kr/dotnet/api/system.windows.dependencyproperty?view=netframework-4.8)   
