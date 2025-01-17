---
title: Wykonanie podzapytania w operacji grupowania (LINQ w C#)
description: Jak wykonanie podzapytania w operacji grupowania, za pomocą LINQ w C#.
ms.date: 12/01/2016
ms.assetid: d75a588e-9b6f-4f37-b195-f99ec8503855
ms.openlocfilehash: a3757a7d358a310dd1404f85e34178f6e561bcb9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61688426"
---
# <a name="perform-a-subquery-on-a-grouping-operation"></a>Wykonywanie podzapytania w operacji grupowania

W tym artykule przedstawiono dwa różne sposoby, aby utworzyć zapytanie, porządkuje źródła danych w grupach, a następnie indywidualnie wykonuje podzapytania w każdej grupie. Podstawowa technika w każdym przykładzie jest do grupowania elementów źródła przy użyciu *kontynuacji* o nazwie `newGroup`i generować nowy podzapytania względem `newGroup`. Podzapytania ten jest wykonywany dla każdej nowej grupy, który jest tworzony przez zapytanie zewnętrzne. Należy pamiętać, że w tym konkretnym przykładzie końcowych danych wyjściowych nie jest grupą, ale prosty sekwencję typów anonimowych.  
  
Aby uzyskać więcej informacji na temat grupy, zobacz [group — klauzula](../language-reference/keywords/group-clause.md).  
  
Aby uzyskać więcej informacji dotyczących kontynuacji, zobacz [do](../language-reference/keywords/into.md). W poniższym przykładzie użyto struktury danych w pamięci jako źródło danych, ale te same zasady mają zastosowanie dla każdego rodzaju źródła danych LINQ.  
  
## <a name="example"></a>Przykład

> [!NOTE]
> Ten przykład zawiera odwołania do obiektów, które są zdefiniowane w przykładowym kodzie w [kwerenda dotycząca kolekcji obiektów](query-a-collection-of-objects.md).

[!code-csharp[csProgGuideLINQ#23](~/samples/snippets/csharp/concepts/linq/how-to-perform-a-subquery-on-a-grouping-operation_1.cs)] 

Zapytania w powyższym fragmencie mogą również będą zapisywane przy użyciu składni metody. Poniższy fragment kodu zawiera zapytanie semantycznie równoważne napisane przy użyciu składni metody.

[!code-csharp[csProgGuideLINQ#86](~/samples/snippets/csharp/concepts/linq/how-to-perform-a-subquery-on-a-grouping-operation_2.cs)]

## <a name="see-also"></a>Zobacz także

- [Language Integrated Query (LINQ)](index.md)
