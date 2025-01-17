---
title: Tworzenie interfejsów ogólnych typu VariantC#()
ms.date: 07/20/2015
ms.assetid: 30330ec4-9df2-4838-a535-6c406d0ed4df
ms.openlocfilehash: 4ba72f28cd2ddd800f169387cc2c742159d4cb1b
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2019
ms.locfileid: "69595310"
---
# <a name="creating-variant-generic-interfaces-c"></a>Tworzenie interfejsów ogólnych typu VariantC#()

Parametry typu ogólnego można zadeklarować w interfejsach jako współvariant lub kontrawariantne. *Kowariancja* umożliwia metodom interfejsu posiadanie bardziej pochodnych typów zwracanych niż te zdefiniowane przez parametry typu ogólnego. *Kontrawariancja* umożliwia metodom interfejsu posiadanie typów argumentów, które są mniej pochodne niż określone przez parametry ogólne. Ogólny interfejs, który ma parametry typu generycznego lub kontrawariantne, nazywa się *wariantem*.

> [!NOTE]
> .NET Framework 4 wprowadziła obsługę wariancji dla kilku istniejących interfejsów ogólnych. Aby uzyskać listę interfejsów wariantów w .NET Framework, zobacz [Wariancja w interfejsachC#ogólnych ()](./variance-in-generic-interfaces.md).

## <a name="declaring-variant-generic-interfaces"></a>Deklarowanie interfejsów ogólnych typu Variant

Można zadeklarować interfejsy ogólne wariantu przy użyciu `in` słów `out` kluczowych i dla parametrów typu ogólnego.

> [!IMPORTANT]
> `ref`, `in`, i `out` parametry w C# nie mogą być wariantem. Typy wartości nie obsługują również wariancji.

Za pomocą `out` słowa kluczowego można zadeklarować współwariant parametru typu ogólnego. Typ współwariantu musi spełniać następujące warunki:

- Typ jest używany tylko jako typ zwracany metod interfejsu i nie jest używany jako typ argumentów metody. Jest to zilustrowane w poniższym przykładzie, w którym typ `R` jest zadeklarowany jako współvariant.

    ```csharp
    interface ICovariant<out R>
    {
        R GetSomething();
        // The following statement generates a compiler error.
        // void SetSomething(R sampleArg);

    }
    ```

    Istnieje jeden wyjątek dla tej reguły. Jeśli masz delegata generycznego kontrawariantne jako parametr metody, możesz użyć typu jako parametru typu ogólnego dla delegata. Jest to zilustrowane przez typ `R` w poniższym przykładzie. Aby uzyskać więcej informacji, zobacz [Wariancja wC#delegatach ()](./variance-in-delegates.md) i [Korzystanie z wariancji dla delegatów () funkcji Func i Action (C#)](./using-variance-for-func-and-action-generic-delegates.md).

    ```csharp
    interface ICovariant<out R>
    {
        void DoSomething(Action<R> callback);
    }
    ```

- Typ nie jest używany jako ograniczenie ogólne metod interfejsu. Jest to zilustrowane w poniższym kodzie.

    ```csharp
    interface ICovariant<out R>
    {
        // The following statement generates a compiler error
        // because you can use only contravariant or invariant types
        // in generic constraints.
        // void DoSomething<T>() where T : R;
    }
    ```

Parametry typu ogólnego kontrawariantne można zadeklarować za pomocą `in` słowa kluczowego. Typ kontrawariantne może być używany tylko jako typ argumentów metody, a nie jako zwracany typ metod interfejsu. Typ kontrawariantne może być również używany dla ograniczeń ogólnych. Poniższy kod przedstawia sposób deklarowania interfejsu kontrawariantne i używania ograniczenia ogólnego dla jednej z jej metod.

```csharp
interface IContravariant<in A>
{
    void SetSomething(A sampleArg);
    void DoSomething<T>() where T : A;
    // The following statement generates a compiler error.
    // A GetSomething();
}
```

Istnieje również możliwość obsługi zarówno kowariancji, jak i kontrawariancja w tym samym interfejsie, ale dla różnych parametrów typu, jak pokazano w poniższym przykładzie kodu.

```csharp
interface IVariant<out R, in A>
{
    R GetSomething();
    void SetSomething(A sampleArg);
    R GetSetSomethings(A sampleArg);
}
```

## <a name="implementing-variant-generic-interfaces"></a>Implementowanie interfejsów ogólnych typu Variant

W klasach można zaimplementować interfejsy ogólne o zmiennej, korzystając z tej samej składni, która jest używana dla interfejsów niezmienna. Poniższy przykład kodu pokazuje, jak zaimplementować interfejs współvariant w klasie generycznej.

```csharp
interface ICovariant<out R>
{
    R GetSomething();
}
class SampleImplementation<R> : ICovariant<R>
{
    public R GetSomething()
    {
        // Some code.
        return default(R);
    }
}
```

Klasy implementujące interfejsy Variant są niezmienne. Rozważmy na przykład poniższy kod.

```csharp
// The interface is covariant.
ICovariant<Button> ibutton = new SampleImplementation<Button>();
ICovariant<Object> iobj = ibutton;

// The class is invariant.
SampleImplementation<Button> button = new SampleImplementation<Button>();
// The following statement generates a compiler error
// because classes are invariant.
// SampleImplementation<Object> obj = button;
```

## <a name="extending-variant-generic-interfaces"></a>Rozszerzanie interfejsów ogólnych typu Variant

Po rozłączeniu uniwersalnego interfejsu wariantowego należy użyć `in` słów kluczowych i `out` , aby jawnie określić, czy interfejs pochodny obsługuje wariancję. Kompilator nie wywnioskuje wariancji z rozszerzanego interfejsu. Rozważmy na przykład następujące interfejsy.

```csharp
interface ICovariant<out T> { }
interface IInvariant<T> : ICovariant<T> { }
interface IExtCovariant<out T> : ICovariant<T> { }
```

W interfejsie parametr `T` typu generycznego jest niezmienny, natomiast w `IExtCovariant<out T>` parametrze typu jest współwariant, chociaż oba interfejsy rozszerzającą ten sam interfejs. `IInvariant<T>` Ta sama reguła jest stosowana do parametrów typu ogólnego kontrawariantne.

Można utworzyć interfejs, który rozszerza zarówno interfejs, w którym parametr `T` typu generycznego to współwariant, jak i interfejs, w którym jest kontrawariantne, jeśli w rozszerzanym interfejsie parametr `T` typu generycznego jest niezmienny. Jest to zilustrowane w poniższym przykładzie kodu.

```csharp
interface ICovariant<out T> { }
interface IContravariant<in T> { }
interface IInvariant<T> : ICovariant<T>, IContravariant<T> { }
```

Jeśli jednak parametr `T` typu generycznego jest zadeklarowany jako współwariant w jednym interfejsie, nie można zadeklarować go kontrawariantne w interfejsie rozszerzającym lub na odwrót. Jest to zilustrowane w poniższym przykładzie kodu.

```csharp
interface ICovariant<out T> { }
// The following statement generates a compiler error.
// interface ICoContraVariant<in T> : ICovariant<T> { }
```

### <a name="avoiding-ambiguity"></a>Unikanie niejednoznaczności

Podczas implementowania interfejsów ogólnych typu Variant WARIANCJA może czasami prowadzić do niejednoznaczności. Należy to uniknąć.

Na przykład w przypadku jawnego zaimplementowania tego samego uniwersalnego interfejsu wariantu z różnymi parametrami typu ogólnego w jednej klasie można utworzyć niejednoznaczność. Kompilator nie generuje błędu w tym przypadku, ale nie jest określony, która implementacja interfejsu zostanie wybrana w czasie wykonywania. Może to prowadzić do delikatnych usterek w kodzie. Rozważmy następujący przykład kodu.

```csharp
// Simple class hierarchy.
class Animal { }
class Cat : Animal { }
class Dog : Animal { }

// This class introduces ambiguity
// because IEnumerable<out T> is covariant.
class Pets : IEnumerable<Cat>, IEnumerable<Dog>
{
    IEnumerator<Cat> IEnumerable<Cat>.GetEnumerator()
    {
        Console.WriteLine("Cat");
        // Some code.
        return null;
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        // Some code.
        return null;
    }

    IEnumerator<Dog> IEnumerable<Dog>.GetEnumerator()
    {
        Console.WriteLine("Dog");
        // Some code.
        return null;
    }
}
class Program
{
    public static void Test()
    {
        IEnumerable<Animal> pets = new Pets();
        pets.GetEnumerator();
    }
}
```

W tym przykładzie nie określono `pets.GetEnumerator` metody wybieranej między `Cat` i `Dog`. Może to spowodować problemy w kodzie.

## <a name="see-also"></a>Zobacz także

- [Wariancja w interfejsachC#ogólnych ()](./variance-in-generic-interfaces.md)
- [Korzystanie z wariancji dla delegatów dla funkcjiC#Func i Action ()](./using-variance-for-func-and-action-generic-delegates.md)
