---
title: Elementy DataSet, DataTable i DataView
ms.date: 03/30/2017
ms.assetid: 6d4c4b69-8919-4224-8a65-6cca1c61b48f
ms.openlocfilehash: 1744f6c6d8ea3c28a8dab30c0d201ae1dacc7ee3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786196"
---
# <a name="datasets-datatables-and-dataviews"></a>Elementy DataSet, DataTable i DataView
ADO.NET <xref:System.Data.DataSet> to reprezentacja danych znajdujących się w pamięci, która zapewnia spójny relacyjny model programowania niezależnie od źródła danych, które zawiera. <xref:System.Data.DataSet> Reprezentuje kompletny zestaw danych, w tym tabele, które zawierają, porządkują i ograniczają dane, a także relacje między tabelami.  
  
 Istnieje kilka sposobów pracy z <xref:System.Data.DataSet>, które mogą być stosowane niezależnie lub w połączeniu. Można:  
  
- <xref:System.Data.DataTable>Programowe tworzenie, <xref:System.Data.DataRelation>, i <xref:System.Data.Constraint> wewnątrz <xref:System.Data.DataSet> i wypełnianie tabel danymi.  
  
- Wypełnij tabele danych z istniejącego relacyjnego źródła danych `DataAdapter`przy użyciu. <xref:System.Data.DataSet>  
  
- Ładowanie i utrwalanie <xref:System.Data.DataSet> zawartości przy użyciu XML. Aby uzyskać więcej informacji, zobacz [Używanie języka XML w zestawie danych](using-xml-in-a-dataset.md).  
  
 Silnie wpisaną <xref:System.Data.DataSet> można również transportować za pomocą usługi sieci Web XML. Projekt <xref:System.Data.DataSet> ułatwia transportowanie danych przy użyciu usług sieci Web XML. Aby zapoznać się z omówieniem usług sieci Web XML, zobacz [Omówienie usług sieci Web XML](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w9fdtx28(v=vs.100)). Przykład <xref:System.Data.DataSet> korzystania z usługi sieci Web XML można znaleźć w temacie wykorzystywanie [zestawu danych z usługi sieci Web XML](consuming-a-dataset-from-an-xml-web-service.md).  
  
## <a name="in-this-section"></a>W tej sekcji  
 [Tworzenie elementu DataSet](creating-a-dataset.md)  
 Opisuje składnię tworzenia wystąpienia <xref:System.Data.DataSet>obiektu.  
  
 [Dodawanie elementu DataTable do elementu DataSet](adding-a-datatable-to-a-dataset.md)  
 Opisuje sposób tworzenia i dodawania tabel i kolumn do <xref:System.Data.DataSet>.  
  
 [Dodawanie elementów DataRelation](adding-datarelations.md)  
 Opisuje sposób tworzenia relacji między tabelami w <xref:System.Data.DataSet>.  
  
 [Nawigowanie w elementach DataRelation](navigating-datarelations.md)  
 Opisuje sposób użycia relacji między tabelami w a <xref:System.Data.DataSet> w celu zwrócenia podrzędnych lub nadrzędnych wierszy relacji nadrzędny-podrzędny.  
  
 [Scalanie zawartości elementu DataSet](merging-dataset-contents.md)  
 Opisuje <xref:System.Data.DataSet>sposób scalania zawartości jednej <xref:System.Data.DataTable>lub <xref:System.Data.DataRow> tablicy w innej <xref:System.Data.DataSet>.  
  
 [Kopiowanie zawartości elementu DataSet](copying-dataset-contents.md)  
 Opisuje sposób tworzenia kopii <xref:System.Data.DataSet> programu, która może zawierać schemat, a także określone dane.  
  
 [Obsługa zdarzeń elementu DataSet](handling-dataset-events.md)  
 Opisuje zdarzenia <xref:System.Data.DataSet> a i sposobu ich używania.  
  
 [Typizowane elementy DataSet](typed-datasets.md)  
 Omawia wpisany typ <xref:System.Data.DataSet> i sposób jego tworzenia i używania.  
  
 [Elementy DataTable](datatables.md)  
 Opisuje sposób tworzenia <xref:System.Data.DataTable>, definiowania schematu i manipulowania danymi.  
  
 [Elementy DataTableReader](datatablereaders.md)  
 Opisuje sposób tworzenia i używania <xref:System.Data.DataTableReader>.  
  
 [Elementy DataView](dataviews.md)  
 Opisuje sposób tworzenia i pracy `DataViews` ze zdarzeniami oraz pracy z <xref:System.Data.DataView> nim.  
  
 [Używanie języka XML w elemencie DataSet](using-xml-in-a-dataset.md)  
 Opisuje sposób <xref:System.Data.DataSet> interakcji z danymi XML jako źródła danych, w tym ładowanie i utrwalanie zawartości <xref:System.Data.DataSet> w postaci danych XML.  
  
 [Korzystanie z elementu DataSet w usłudze internetowej XML](consuming-a-dataset-from-an-xml-web-service.md)  
 Zawiera opis sposobu tworzenia usługi sieci Web XML, która używa <xref:System.Data.DataSet> do przesyłania danych.  
  
## <a name="related-sections"></a>Sekcje pokrewne  
 [Nowości w programie ADO.NET](../whats-new.md)  
 Wprowadza funkcje, które są nowe w ADO.NET.  
  
 [Omówienie ADO.NET](../ado-net-overview.md)  
 Zawiera wprowadzenie do projektowania i składników ADO.NET.  
  
 [Wypełnianie zestawu danych z elementu DataAdapter](../populating-a-dataset-from-a-dataadapter.md)  
 Opisuje sposób ładowania **zestawu danych** z danymi ze źródła danych.  
  
 [Aktualizowanie źródeł danych za pomocą elementów DataAdapters](../updating-data-sources-with-dataadapters.md)  
 Opisuje sposób rozwiązywania zmian w danych w **zestawie** danych z powrotem do źródła danych.  
  
 [Dodawanie istniejących ograniczeń do zestawu danych](../adding-existing-constraints-to-a-dataset.md)  
 Opisuje sposób wypełniania **zestawu danych** z informacjami o kluczu podstawowym ze źródła danych.  
  
## <a name="see-also"></a>Zobacz także

- [ADO.NET](../index.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
