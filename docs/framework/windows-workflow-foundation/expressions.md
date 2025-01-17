---
title: Wyrażenia — WF
ms.date: 03/30/2017
ms.assetid: c42341a9-43a1-462c-bffb-c5de004aa428
ms.openlocfilehash: 62b278825de6242075e89e3b243b6d6d8ef4d599
ms.sourcegitcommit: 1e72e2990220b3635cebc39586828af9deb72d8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/26/2019
ms.locfileid: "71306204"
---
# <a name="expressions"></a>Wyrażenia

Wyrażenie Windows Workflow Foundation (WF) to wszelkie działania zwracające wynik. Wszystkie działania wyrażeń są wyprowadzane <xref:System.Activities.Activity%601>pośrednio z, która <xref:System.Activities.OutArgument> zawiera właściwość <xref:System.Activities.Activity%601.Result%2A> o nazwie jako wartość zwracana działania. [!INCLUDE[wf1](../../../includes/wf1-md.md)]jest dostarczany z szerokim zakresem działań związanych z wyrażeniami <xref:System.Activities.Expressions.VariableValue%601> prostymi, takimi jak i <xref:System.Activities.Expressions.VariableReference%601>, które zapewniają dostęp do pojedynczej zmiennej przepływu pracy za <xref:Microsoft.VisualBasic.Activities.VisualBasicReference%601> pośrednictwem działań operatora, do złożonych działań, takich jak i <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> tej oferty dostęp do pełnego zakresu Visual Basic języka w celu utworzenia wyniku. Dodatkowe działania dotyczące wyrażeń można tworzyć poprzez wyprowadzanie z <xref:System.Activities.CodeActivity%601> lub <xref:System.Activities.NativeActivity%601>.

## <a name="using-expressions"></a>Używanie wyrażeń
 Projektant przepływu pracy <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> używa <xref:Microsoft.VisualBasic.Activities.VisualBasicReference%601> i dla wszystkich wyrażeń <xref:Microsoft.CSharp.Activities.CSharpValue%601> w projektach Visual Basic i i <xref:Microsoft.CSharp.Activities.CSharpReference%601> dla wyrażeń w C# projektach przepływu pracy.

> [!NOTE]
> Obsługa C# wyrażeń w projektach przepływu pracy została wprowadzona w .NET Framework 4,5. Aby uzyskać więcej informacji, zobacz [ C# Expressions](csharp-expressions.md).

 Przepływy pracy utworzone przez projektanta są zapisywane w języku XAML, gdzie wyrażenia są ujęte w nawiasy kwadratowe, jak w poniższym przykładzie.

```xml
<Sequence xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
  <Sequence.Variables>
    <Variable x:TypeArguments="x:Int32" Default="1" Name="a" />
    <Variable x:TypeArguments="x:Int32" Default="2" Name="b" />
    <Variable x:TypeArguments="x:Int32" Default="3" Name="c" />
    <Variable x:TypeArguments="x:Int32" Default="0" Name="r" />
  </Sequence.Variables>
  <Assign>
    <Assign.To>
      <OutArgument x:TypeArguments="x:Int32">[r]</OutArgument>
    </Assign.To>
    <Assign.Value>
      <InArgument x:TypeArguments="x:Int32">[a + b + c]</InArgument>
    </Assign.Value>
  </Assign>
</Sequence>
```

 Podczas definiowania przepływu pracy w kodzie, można użyć dowolnego działania wyrażeń. W poniższym przykładzie pokazano sposób użycia kompozycji działań operatora w celu dodania trzech liczb:

```csharp
Variable<int> a = new Variable<int>("a", 1);
Variable<int> b = new Variable<int>("b", 2);
Variable<int> c = new Variable<int>("c", 3);
Variable<int> r = new Variable<int>("r", 0);

Sequence w = new Sequence
{
    Variables = { a, b, c, r },
    Activities =
    {
        new Assign {
            To = new OutArgument<int>(r),
            Value = new InArgument<int> {
                Expression = new Add<int, int, int> {
                    Left = new Add<int, int, int> {
                        Left = new InArgument<int>(a),
                        Right = new InArgument<int>(b)
                    },
                    Right = new InArgument<int>(c)
                }
            }
        }
    }
};
```

 Ten sam przepływ pracy można wyrazić bardziej kompaktowo przy C# użyciu wyrażeń lambda, jak pokazano w następującym przykładzie:
  
```csharp
Variable<int> a = new Variable<int>("a", 1);
Variable<int> b = new Variable<int>("b", 2);
Variable<int> c = new Variable<int>("c", 3);
Variable<int> r = new Variable<int>("r", 0);

Sequence w = new Sequence
{
    Variables = { a, b, c, r },
    Activities = 
    {
        new Assign {
            To = new OutArgument<int>(r),
            Value = new InArgument<int>((ctx) => a.Get(ctx) + b.Get(ctx) + c.Get(ctx))
        }
    }
};
```

## <a name="extending-available-expressions-with-custom-expression-activities"></a>Rozszerzanie dostępnych wyrażeń z niestandardowymi działaniami wyrażeń

 Wyrażenia w [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] programie mają rozszerzalny Zezwalanie na tworzenie dodatkowych działań wyrażeń. Poniższy przykład pokazuje działanie zwracające sumę trzech wartości całkowitych.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Activities;

namespace ExpressionsDemo
{
    public sealed class AddThreeValues : CodeActivity<int>
    {
        public InArgument<int> Value1 { get; set; }
        public InArgument<int> Value2 { get; set; }
        public InArgument<int> Value3 { get; set; }

        protected override int Execute(CodeActivityContext context)
        {
            return Value1.Get(context) +
                   Value2.Get(context) +
                   Value3.Get(context);
        }
    }
}
```

 Przy użyciu tego nowego działania można ponownie napisać poprzedni przepływ pracy, który dodał trzy wartości, jak pokazano w następującym przykładzie:

```csharp
Variable<int> a = new Variable<int>("a", 1);
Variable<int> b = new Variable<int>("b", 2);
Variable<int> c = new Variable<int>("c", 3);
Variable<int> r = new Variable<int>("r", 0);

Sequence w = new Sequence
{
    Variables = { a, b, c, r },
    Activities =
    {
        new Assign {
            To = new OutArgument<int>(r),
            Value = new InArgument<int> {
                Expression = new AddThreeValues() {
                    Value1 = new InArgument<int>(a),
                    Value2 = new InArgument<int>(b),
                    Value3 = new InArgument<int>(c)
                }
            }
        }
    }
};
```

 Aby uzyskać więcej informacji na temat używania wyrażeń w kodzie, zobacz [Tworzenie przepływów pracy, działań i wyrażeń przy użyciu kodu](authoring-workflows-activities-and-expressions-using-imperative-code.md).
