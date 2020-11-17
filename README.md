# DependencyProperty
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
[![GPLv3 license](https://img.shields.io/badge/License-GPLv3-blue.svg)](http://perso.crans.org/besson/LICENSE.html)

## Ncoresoft Repository
> Ncoresoft Git. [here.](https://github.com/ncoresoftsource/ncoresoftgit)

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

```csharp
public int AspectRatioWidth
{
    get { return (int)this.GetValue(AspectRatioWidthProperty); }
    set { this.SetValue(AspectRatioWidthProperty, value); }
}

public static readonly DependencyProperty AspectRatioWidthProperty = DependencyProperty.Register(
  "AspectRatioWidth", typeof(int), typeof(CampImage), new PropertyMetadata(16));
```

## 4. Opensource
