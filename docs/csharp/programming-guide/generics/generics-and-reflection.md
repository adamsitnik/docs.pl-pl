---
title: Typy ogólne i odbicie C# — Przewodnik programowania
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- generics [C#], reflection
- reflection [C#], generic types
ms.assetid: 162fd9b4-dd5b-4abb-8c9b-e44e21e2f451
ms.openlocfilehash: be4b72414af8e5a18145330f5c44ae9a79a567cb
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659891"
---
# <a name="generics-and-reflection-c-programming-guide"></a>Typy ogólne i odbicie (Przewodnik programowania w języku C#)
Ponieważ środowisko uruchomieniowe języka wspólnego (CLR) ma dostęp do ogólnych informacji o typie w czasie wykonywania, można użyć odbicia w celu uzyskania informacji o typach ogólnych w taki sam sposób jak w przypadku typów innych niż ogólne. Aby uzyskać więcej informacji, zobacz [typy ogólne w czasie wykonywania](./generics-in-the-run-time.md).  
  
 W .NET Framework 2,0 kilka nowych członków jest dodawanych do <xref:System.Type> klasy w celu włączenia informacji w czasie wykonywania dla typów ogólnych. Zapoznaj się z dokumentacją dotyczącą tych klas, aby uzyskać więcej informacji na temat korzystania z tych metod i właściwości. <xref:System.Reflection.Emit> Przestrzeń nazw zawiera również nowych członków, którzy obsługują typy ogólne. Zobacz [How to: Zdefiniuj typ ogólny przy użyciu emisji](../../../framework/reflection-and-codedom/how-to-define-a-generic-type-with-reflection-emit.md)odbicia.  
  
 Aby zapoznać się z listą warunków niewariantów dla terminów używanych w odbiciu ogólnym <xref:System.Type.IsGenericType%2A> , zobacz uwagi dotyczące właściwości.  
  
|Nazwa elementu członkowskiego system. Type|Opis|  
|-----------------------------|-----------------|  
|<xref:System.Type.IsGenericType%2A>|Zwraca wartość true, jeśli typ jest ogólny.|  
|<xref:System.Type.GetGenericArguments%2A>|Zwraca tablicę `Type` obiektów reprezentujących argumenty typu dostarczone dla typu konstruowanego lub parametry typu definicji typu ogólnego.|  
|<xref:System.Type.GetGenericTypeDefinition%2A>|Zwraca podstawową definicję typu ogólnego dla bieżącego konstruowanego typu.|  
|<xref:System.Type.GetGenericParameterConstraints%2A>|Zwraca tablicę `Type` obiektów, która reprezentuje ograniczenia dotyczące bieżącego parametru typu ogólnego.|  
|<xref:System.Type.ContainsGenericParameters%2A>|Zwraca wartość true, jeśli typ lub dowolny z zawartych w nim typów lub metod zawierają parametry typu, dla których nie dostarczono określonych typów.|  
|<xref:System.Type.GenericParameterAttributes%2A>|Pobiera kombinację `GenericParameterAttributes` flag, które opisują specjalne ograniczenia bieżącego parametru typu ogólnego.|  
|<xref:System.Type.GenericParameterPosition%2A>|W przypadku `Type` obiektu, który reprezentuje parametr typu, pobiera pozycję parametru typu z listy parametrów typu w definicji typu ogólnego lub definicji metody ogólnej, która deklaruje parametr typu.|  
|<xref:System.Type.IsGenericParameter%2A>|Pobiera wartość wskazującą, czy bieżący `Type` reprezentuje parametr typu ogólnego lub definicji metody.|  
|<xref:System.Type.IsGenericTypeDefinition%2A>|Pobiera wartość wskazującą, czy bieżący <xref:System.Type> reprezentuje definicję typu ogólnego, z której można utworzyć inne typy ogólne. Zwraca wartość true, jeśli typ reprezentuje definicję typu ogólnego.|  
|<xref:System.Type.DeclaringMethod%2A>|Zwraca metodę rodzajową, która definiuje bieżący parametr typu ogólnego, lub wartość null, jeśli parametr typu nie został zdefiniowany przez metodę rodzajową.|  
|<xref:System.Type.MakeGenericType%2A>|Zastępuje elementy tablicy typów dla parametrów typu bieżącej definicji typu ogólnego i zwraca <xref:System.Type> obiekt reprezentujący wynikowy typ skonstruowany.|  
  
 Ponadto członkowie <xref:System.Reflection.MethodInfo> klasy włączają informacje w czasie wykonywania dla metod ogólnych. Zobacz uwagi dotyczące właściwości, aby zapoznać się z listą niezmiennej warunków używanych do odzwierciedlenia metod ogólnych. <xref:System.Reflection.MethodBase.IsGenericMethod%2A>  
  
|System.Reflection.MemberInfo Member Name|Opis|  
|----------------------------------------------|-----------------|  
|<xref:System.Reflection.MethodBase.IsGenericMethod%2A>|Zwraca wartość true, jeśli metoda jest ogólna.|  
|<xref:System.Reflection.MethodInfo.GetGenericArguments%2A>|Zwraca tablicę typu obiektów, która reprezentuje argumenty typu konstruowanej metody ogólnej lub parametry typu definicji metody ogólnej.|  
|<xref:System.Reflection.MethodInfo.GetGenericMethodDefinition%2A>|Zwraca podstawową definicję metody ogólnej dla bieżącej metody skonstruowanej.|  
|<xref:System.Reflection.MethodBase.ContainsGenericParameters%2A>|Zwraca wartość true, jeśli metoda lub dowolny z jej typów zawiera wszystkie parametry typu, dla których nie dostarczono określonych typów.|  
|<xref:System.Reflection.MethodBase.IsGenericMethodDefinition%2A>|Zwraca wartość true, jeśli <xref:System.Reflection.MethodInfo> bieżąca reprezentuje definicję metody ogólnej.|  
|<xref:System.Reflection.MethodInfo.MakeGenericMethod%2A>|Zastępuje elementy tablicy typów dla parametrów typu bieżącej definicji metody ogólnej i zwraca <xref:System.Reflection.MethodInfo> obiekt reprezentujący wynikową metodę skonstruowaną.|  
  
## <a name="see-also"></a>Zobacz także

- [Przewodnik programowania w języku C#](../index.md)
- [Typy ogólne](./index.md)
- [Odbicie i typy ogólne](../../../framework/reflection-and-codedom/reflection-and-generic-types.md)
- [Typy ogólne](../../../standard/generics/index.md)
