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
DependencyPropery는 닷넷프레임워크 WPF의 가장 깊은 곳에 숨어 있는 중요한 설계 기반 중 하나의 클래스입니다.   

이 클래스는 닷넷프레임워크로부터 sealed를 통해 보호 받고 있으며, 이를 통해 등록된 속성은 단순히 필드 값을 저장하는 것 뿐만 아니라 클래스 내부에서 제공하는 다양한 기능들을 활용할 수 있다는 점에서 1차원적인 일반 Property와는 특별한 차별점을 두고 있습니다. 

가장 중요한 점은 데이터 바인딩을위한 모든 기반이 준비되어 있다는 것입니다. 무언가를 바인딩하면 변경 될 때 알림을 보낼수도 있습니다. 

특히 MVVM 개발 방법론에서는 이미 닷넷프레임워크에서 제공되고 있는 DependencyProperty가 고정적으로 한정되어 있기 때문에 Binding사용을 더욱 더 적극적으로 활용하기 위해서는 반드시 이 기술이 필요합니다.
## 1. Orverview
DependencyProperty는 WPF의 핵심적인 설계 요소 중 하나입니다. 이는 하나의 단일 기능이 아닌 여러 개념과 논리 구조가 복합적으로 포함되어 있기 때문에 심도 있고 깊이 있는 연구가 필요한 부분이며  기술의 범위와 깊이에 있어 다소 높은 난이도를 필요로 합니다.
#### 1.1. Class Version 
The first target version of DependencyProperty is based on .NET Frmaeowrk `3.0`
| Target Name    | Version                                                                                  |
|:---------------|:-----------------------------------------------------------------------------------------|
| .NET           | 5.0                                                                                      |
| .NET Core      | 3.0, 3.1                                                                                 |
| .NET Framework | 3.0, 3.5, 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2, 4.8              |

##### _So .NET Framework 2.0 doesn't allow us to use DependencyProperty?_   
> That's right. WPF starts at 3.0. :smile:

#### 1.2. Class Information
| Assembly             | Namespace                   | Class Access        | Base Class      |
|:---------------------|:----------------------------|:--------------------|:----------------|
| WindowsBase.dll      | System.Windows              | `sealed`            | `Object`        |

#### 1.3. Class Structure
DependencyPropery 클래스의 Access 권한은 `sealed`이므로 사용자 정의 클래스에서 직접적으로 상속받을 수 없는 구조를 갖고 있습니다.

```csharp
namespace System.Windows
{
    public sealed class DependencyProperty
    {

    }   
}
```

## 2. Declaration
DependencyProperty는 두 가지 방식으로 등록할 수 있습니다.
- [Standard](#21-Standard)
- [Extender](#22-Extender)

### 2.1. Standard
Standard 방식은 `DependencyProperty.Register` 메서드를 통해 `Owner UI`클래스에 바로 연결(등록)하는 방식입니다.
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

### 2.1.3. [Standard] String
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

#### 2.1.4. [Standard] Object
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

#### 2.1.5. [Standard] Geometry
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

### 2.2. Extender
- [String](#221-Extend-String)

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
## 5. Quiz Time
1. 다음 중 DependencyProperty의 클래스 접근제한자로 알맞은 것은?   
- ① Abstruct   
- ② Sealed   
- ③ Virtual   
- ④ struct   

2. DependencyProperty를 사용하기 위해 필요한 Namespace를 고르시오.   
- ① using System;   
- ② using System.Windows;   
- ③ using System.Windows.Threading;   
- ④ using System.ComponentModel;   

3. DependencyProperty는 닷넷프레임워크의 어느 Assembly에서 제공하는 클래스인가?   
- ① System.dll;   
- ② System.Windows.dll;   
- ③ WindowsBase.dll;   
- ④ PresentationFramework.dll;  

## 6. References
### 6.1 Community Docs
#### WPF Tutorial
> DependencyProperties [here.](https://www.wpftutorial.net/DependencyProperties.html)   
#### So Documentation
> Dependency-Properties [here.](https://sodocumentation.net/wpf/topic/2914/dependency-properties)   
#### Microsoft Docs
> DependencyProperty Class [Here.](https://docs.microsoft.com/ko-kr/dotnet/api/system.windows.dependencyproperty?view=netframework-4.8)   

