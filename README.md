## DependencyProperty
  
이 리포지토리는 WPF DependencyPropery (의존 속성) 클래스의 개념과 기술을 활용하는데 필요한 설명을 다루는 리포지토리입니다.

<a href="https://github.com/devncore/devncore"><strong>더 알아보기 »</strong></a>
  
| Star | License | Activity |
|:----:|:-------:|:--------:|
| <a href="https://github.com/devncore/dependencyproperty/stargazers"><img src="https://img.shields.io/github/stars/devncore/dependencyproperty" alt="Github Stars"></a> | <img src="https://img.shields.io/github/license/devncore/dependencyproperty" alt="License"> | <a href="https://github.com/devncore/dependencyproperty/pulse"><img src="https://img.shields.io/github/commit-activity/m/devncore/dependencyproperty" alt="Commits-per-month"></a> |

<br />

## DependencyProperty란? 
DependencyProperty 클래스는 WPF .Net Framework 내부에 숨겨져 있는 가장 중요한 설계 기반 중 하나입니다.

이 클래스는 .Net Framework에서 `sealed`를 통해 보호됩니다. 이 속성은 필드 값을 저장할 뿐만 아니라 클래스 내에서 제공되는 다양한 기능을 활용한다는 점에서 1차원적인 일반적 속성과 다릅니다. 가장 중요한 것은 데이터 바인딩 사용에 대한 기반을 가지고 있다는 것입니다. 또한 바인딩할 때마다 알림(Callback)을 구현할 수도 있습니다.

이러한 특성 덕분에 이 기술은 바인딩을 더욱 적극적으로 사용하는 데 필수적입니다. 또한 MVVM 패턴을 통한 개발을 제대로 하기 위해서도 반드시 잘 활용할 수 있어야 합니다.

### 클래스 버전
DependencyProperty의 첫 번째 대상 버전은 `.NET Framework '3.0'`에 기반을 두고 있습니다.

| Target Name    | Version                                                                                  |
|:---------------|:-----------------------------------------------------------------------------------------|
| .NET           | 5.0 ~ 6.0                                                                                 |
| .NET Core      | 3.0 ~ 3.1                                                                                 |
| .NET Framework | 3.0 ~ 4.8 |

### 클래스 정보
| 어셈블리              | 네임스페이스                 | 클래스 재선언 여부   | 부모 클래스       |
|:---------------------|:----------------------------|:--------------------|:----------------|
| WindowsBase.dll      | System.Windows              | sealed            | Object        |

### Class Structure
DependencyProperty 클래스의 액세스 권한은 **sealed**를 통해 보호되고 있으며 사용자 지정 클래스에서 직접 상속할 수 없는 구조를 가지고 있습니다.

```csharp
namespace System.Windows
{
    public sealed class DependencyProperty
    {

    }   
}
```
<br />

## DependencyProperty 구현

### Int
```csharp
public static readonly DependencyProperty AgeProperty = DependencyProperty.Register(
    "Age", typeof(int), typeof(<class>), new PropertyMetadata(0));
    
public int Age
{
    get { return (int)this.GetValue(AgeProperty); }
    set { this.SetValue(AgeProperty, value); }
}
```
 
### Boolean
```csharp
public static readonly DependencyProperty IsUsedProperty = DependencyProperty.Register(
    "IsUsed", typeof(bool), typeof(<class>), new PropertyMetadata(false));
    
public bool IsUsed 
{ 
    get { return (bool)this.GetValue(IsUsedProperty); }
    set { this.SetValue(IsUsedProperty, value); }
}
```

### String(Standard)
```csharp
public static readonly DependencyProperty PlaceHolderProperty = DependencyProperty.Register(
    "PlaceHolder", typeof(string), typeof(<class>), new PropertyMetadata(""));
    
public string PlaceHolder
{
    get { return (string)this.GetValue(PlaceHolderProperty); }
    set { this.SetValue(PlaceHolderProperty, value); }
}
```

### String(Extender)
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

### Object

It is actually the same as the Content Property included in the `ContentControl` class.  
If you inherit ContentControl and create a control that defines ContentPresenter, use Object-type DependencyProperty.
 - **`Content`** in `ContentControl` _(Button, CheckBox, UserControl, Window ···)_  
 - **`Tag`** in `Control` _(Button, Window, Grid, StackPanel ···)_
```csharp
public static readonly DependencyProperty ContentProperty = DependencyProperty.Register(
    "Content", typeof(object), typeof(<class>), new PropertyMetadata(""));
    
public object Content
{
    get { return (object)this.GetValue(ContentProperty); }
    set { this.SetValue(ContentProperty, value); }
}
```

### Geometry
 - **`Data`** in `Path`
```csharp
public static readonly DependencyProperty DataProperty = DependencyProperty.Register(
    "Data", typeof(Geometry), typeof(<class>), new PropertyMetadata(null));
    
public Geometry Data
{
    get { return (Geometry)this.GetValue(DataProperty); }
    set { this.SetValue(DataProperty, value); }
}
```

### Brush
```csharp
public static readonly DependencyProperty FillProperty = DependencyProperty.Register(
    "Fill", typeof(Brush), typeof(<class>), new PropertyMetadata(null));
    
public Brush Fill
{
    get { return (Brush)this.GetValue(FillProperty); }
    set { this.SetValue(FillProperty, value); }
}
```

### Double
```csharp
public static readonly DependencyProperty IconWidthProperty = DependencyProperty.Register(
    "IconWidth", typeof(double), typeof(<class>), new PropertyMetadata(0));
    
public double IconWidth
{
    get { return (double)this.GetValue(IconWidthProperty); }
    set { this.SetValue(IconWidthProperty, value); }
}
```

### ICommand
```csharp
public static readonly DependencyProperty SelectionCommandProperty = DependencyProperty.Register(
    "SelectionCommand", typeof(ICommand), typeof(<class>));
    
public ICommand SelectionCommand
{
    get { return (ICommand)this.GetValue(SelectionCommandProperty); }
    set { this.SetValue(SelectionCommandProperty, value); }
}
```

### Property Changed

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

### CoerceValueCallback

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


## DependencyProperty를 얼마나 알고 있습니까?

- [x] DependencyProperty 속성은 일반적인 속성처럼 사용이 가능합니다. [확인](#using-property)
- [ ] OverrideMetadata 재정의는 일반적으로 static 생성자에서 하는 것이 좋습니다.  [확인](#overridemetadata-method)
- [x] Xaml 영역에서 접근이 가능한 대부분의 컨트롤 속성들은 DependencyProperty 입니다.
- [x] DependencyProperty 속성 등록은 static 생성자에서 하는 것이 일반적입니다.
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
<br />

### Using Property
DependencyProperty 속성은 기본적으로 일반 속성처럼 사용이 가능합니다. 따라서 아래와 같이 `get`, `set`을 자유롭게 사용할 수 있습니다.

```csharp
Button btn = new Button();
btn.Content = "James";
btn.Width = 100;
btn.Height = 50;
double width = btn.Width;
double height = btn.Height;
string Content = btn.Content.ToString();
```

Xaml 영역에서는 구조의 특성상 get을 사용할 수는 없지만 set은 마찬가지로 기본 속성처럼 자유롭게 사용할 수 있습니다.
```xaml
<Button Content="Elena" Width="100" Height="50"/>
```

### OverrideMetadata Method
OverrideMetadata는 컨트롤(클래스)의 `Default` 값이나 ChangedCallback, CoerceValueCallback 방식을 재정의할 수 있도록 하는 기능을 제공합니다. Metadata는 이미 DependencyProperty를 등록(Register)할 때 정의하지만 이 메서드를 통해 재정의할 수 있기 때문에 CoerceValueCallback에 의해 내부적으로 처리되는 콜백 시스템을 재구성할 수 있습니다.

```csharp
public class Pizza : Control
{
    static Pizza()
    {
        DefaultStyleKeyProperty.OverrideMetadata(typeof(Pizza), 
            new PropertyMetadata(typeof(Pizza));
    }
}
```
<br />

***

## References
📑  **[WPF Tutorial](https://www.wpftutorial.net/DependencyProperties.html)** &nbsp; DependencyProperties  
📑  **[SO Documentation](https://sodocumentation.net/wpf/topic/2914/dependency-properties)** &nbsp; Dependency-Properties   
📑  **[Microsoft Docs](https://docs.microsoft.com/ko-kr/dotnet/api/system.windows.dependencyproperty?view=netframework-4.8)** &nbsp; DependencyProperty Class
 
