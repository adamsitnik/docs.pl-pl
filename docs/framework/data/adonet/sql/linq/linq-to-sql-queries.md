---
title: Zapytania LINQ to SQL
ms.date: 03/30/2017
ms.assetid: f4897aaa-7f44-4c20-a471-b948c2971aae
ms.openlocfilehash: a170beae3a9f0c923502028f5579de1f3916c07d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793001"
---
# <a name="linq-to-sql-queries"></a>Zapytania LINQ to SQL
Zapytania są [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] definiowane przy użyciu takiej samej składni jak w programie. [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] Jedyną różnicą jest to, że obiekty, do których odwołują się zapytania, są mapowane na elementy w bazie danych. Aby uzyskać więcej informacji, zobacz [wprowadzenie do zapytań LINQC#()](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]tłumaczy zapytania zapisane w równoważne zapytania SQL i wysyła je do serwera w celu przetworzenia. Dokładniej mówiąc, aplikacja używa [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] interfejsu API do żądania wykonania zapytania. Następnie [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] dostawca przekształca zapytanie w tekst SQL i deleguje wykonywanie do dostawcy ADO. Dostawca ADO zwraca wyniki zapytania jako `DataReader`. Dostawca tłumaczy wyniki ADO <xref:System.Linq.IQueryable> na kolekcję obiektów użytkownika. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]  
  
> [!NOTE]
> Większość metod i operatorów na .NET Framework typów wbudowanych ma bezpośrednie tłumaczenia na SQL. [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] Nie można przetłumaczyć generowania wyjątków czasu wykonywania. Aby uzyskać więcej informacji, zobacz [Mapowanie typu SQL-CLR](sql-clr-type-mapping.md).  
  
 W poniższej tabeli przedstawiono podobieństwa i różnice między [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] elementami zapytania i. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]  
  
|Element|Zapytanie LINQ|[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]Dotyczących|  
|----------|----------------|----------------------------------------------------------------------|  
|Zwracany typ zmiennej lokalnej, która przechowuje zapytanie (dla zapytań, które zwracają sekwencje)|Ogólnego`IEnumerable`|Ogólnego`IQueryable`|  
|Określanie źródła danych|Używa klauzuli `from` (Visual Basic) lub (C# `From`|Ten|  
|Filtrowanie|`Where` Używaklauzuli/ `where`|Ten|  
|Grupowanie|`Group…By` Używaklauzuli/ `groupby`|Ten|  
|Zaznaczanie (Projekcja)|`Select` Używaklauzuli/ `select`|Ten|  
|Odroczone względem natychmiastowego wykonania|Zobacz [wprowadzenie do zapytań LINQ (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)|Ten|  
|Implementowanie sprzężeń|`Join` Używaklauzuli/ `join`|`Join` Może używać / <xref:System.Data.Linq.Mapping.AssociationAttribute> klauzuli, ale bardziej efektywnie korzysta z atrybutu. `join` Aby uzyskać więcej informacji, zobacz [wykonywanie zapytań w relacjach](querying-across-relationships.md).|  
|Zdalne a wykonywanie lokalne||Aby uzyskać więcej informacji, [Zobacz zdalne a Wykonanie](remote-vs-local-execution.md)lokalne.|  
|Przesyłanie strumieniowe i wykonywanie zapytań w pamięci podręcznej|Nie dotyczy w przypadku lokalnego scenariusza pamięci||  
  
## <a name="see-also"></a>Zobacz także

- [Wprowadzenie do zapytań LINQ (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)
- [Podstawowe operacje zapytań LINQ](../../../../../csharp/programming-guide/concepts/linq/basic-linq-query-operations.md)
- [Relacje typów w operacjach zapytań LINQ](../../../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)
- [Pojęcia dotyczące zapytań](query-concepts.md)
