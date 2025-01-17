---
title: 'Instrukcje: UtwórzC++ Unię C przy użyciu atrybutów (C#)'
ms.date: 07/20/2015
ms.assetid: 85f35e56-26e0-4d31-9f3a-89bd4005e71a
ms.openlocfilehash: fdadc9505b93f40c66001ac36345efada2edd270
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2019
ms.locfileid: "69595374"
---
# <a name="how-to-create-a-cc-union-by-using-attributes-c"></a>Instrukcje: Utwórz element C/C++ Union przy użyciu atrybutów (C#)
Przy użyciu atrybutów można dostosować sposób, w jaki struktury są ułożone w pamięci. Na przykład można utworzyć element, który jest znany jako Unia w C/C++ przy użyciu `StructLayout(LayoutKind.Explicit)` atrybutów i. `FieldOffset`  
  
## <a name="example"></a>Przykład  
 W tym segmencie kodu wszystkie pola, które `TestUnion` są uruchamiane w tej samej lokalizacji w pamięci.  
  
```csharp  
// Add a using directive for System.Runtime.InteropServices.  
  
       [System.Runtime.InteropServices.StructLayout(LayoutKind.Explicit)]  
       struct TestUnion  
       {  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public int i;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public double d;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public char c;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public byte b;  
       }  
```  
  
## <a name="example"></a>Przykład  
 Poniżej znajduje się kolejny przykład, w którym pola zaczynają się od różnych jawnie ustawionych lokalizacji.  
  
```csharp  
// Add a using directive for System.Runtime.InteropServices.  
  
       [System.Runtime.InteropServices.StructLayout(LayoutKind.Explicit)]  
       struct TestExplicit  
       {  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public long lg;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public int i1;  
  
           [System.Runtime.InteropServices.FieldOffset(4)]  
           public int i2;  
  
           [System.Runtime.InteropServices.FieldOffset(8)]  
           public double d;  
  
           [System.Runtime.InteropServices.FieldOffset(12)]  
           public char c;  
  
           [System.Runtime.InteropServices.FieldOffset(14)]  
           public byte b;  
       }  
```  
  
 Dwa pola `i1` liczb całkowitych i `i2`, współużytkują te same lokalizacje `lg`pamięci co. Ten rodzaj kontroli nad układem struktury jest przydatny podczas korzystania z wywołania platformy.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Reflection>
- <xref:System.Attribute>
- [Przewodnik programowania w języku C#](../../index.md)
- [Atrybuty](../../../../standard/attributes/index.md)
- [OdbicieC#()](../reflection.md)
- [Atrybuty (C#)](./index.md)
- [Tworzenie atrybutów niestandardowych (C#)](./creating-custom-attributes.md)
- [Uzyskiwanie dostępu do atrybutów przyC#użyciu odbicia ()](./accessing-attributes-by-using-reflection.md)
