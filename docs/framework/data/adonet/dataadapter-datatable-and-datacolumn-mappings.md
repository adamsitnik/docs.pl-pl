---
title: Element DataAdapter DataTable i mapowania elementu DataColumn
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d023260a-a66a-4c39-b8f4-090cd130e730
ms.openlocfilehash: a9c81c8554c0fb393c10ed69f84c8b2d936ec1e6
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040128"
---
# <a name="dataadapter-datatable-and-datacolumn-mappings"></a>Element DataAdapter DataTable i mapowania elementu DataColumn
Element **DataAdapter** zawiera kolekcję obiektów <xref:System.Data.Common.DataTableMapping>, w których właściwość **TableMappings** jest równa zero lub więcej. **DataTableMapping** zapewnia mapowanie wzorca między danymi zwracanymi z zapytania do źródła danych i <xref:System.Data.DataTable>. Nazwę **DataTableMapping** można przesłać zamiast nazwy **DataTable** do metody **Fill** elementu **DataAdapter**. Poniższy przykład tworzy **DataTableMapping** o nazwie **AuthorsMapping** dla tabeli **autorów** .  
  
```vb  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors")  
```  
  
```csharp  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors");  
```  
  
 **DataTableMapping** umożliwia używanie nazw kolumn w **elemencie DataTable** , które różnią się od tych w bazie danych. Element **DataAdapter** używa mapowania, aby dopasować kolumny po zaktualizowaniu tabeli.  
  
 Jeśli nie określisz nazwy **TableName** lub **DataTableMapping** podczas wywoływania metody **Fill** lub **Update** elementu **DataAdapter**, obiekt **DataAdapter** szuka **DataTableMapping** o nazwie "Table". Jeśli **DataTableMapping** nie istnieje, **tabelaname tabeli** **DataTable** ma wartość "Table". Można określić domyślny **DataTableMapping** , tworząc **DataTableMapping** o nazwie "Table".  
  
 Poniższy przykład kodu tworzy **DataTableMapping** (z przestrzeni nazw <xref:System.Data.Common>) i tworzy mapowanie domyślne dla określonego elementu **DataAdapter** przez nadanie jej nazwy "Table". Następnie przykład mapuje kolumny z pierwszej tabeli w wyniku zapytania (tabela **Customers** bazy danych **Northwind** ) do zestawu większej liczby przyjaznych nazw użytkowników w tabeli **Klienci Northwind** w <xref:System.Data.DataSet>. W przypadku kolumn, które nie są zamapowane, używana jest nazwa kolumny ze źródła danych.  
  
```vb  
Dim mapping As DataTableMapping = _  
  adapter.TableMappings.Add("Table", "NorthwindCustomers")  
mapping.ColumnMappings.Add("CompanyName", "Company")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode")  
  
adapter.Fill(custDS)  
```  
  
```csharp  
DataTableMapping mapping =   
  adapter.TableMappings.Add("Table", "NorthwindCustomers");  
mapping.ColumnMappings.Add("CompanyName", "Company");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode");  
  
adapter.Fill(custDS);  
```  
  
 W bardziej zaawansowanych sytuacjach możesz zdecydować, że chcesz, aby ten sam element **DataAdapter** obsługiwał ładowanie różnych tabel z różnymi mapowaniami. W tym celu wystarczy dodać dodatkowe obiekty **DataTableMapping** .  
  
 Gdy metoda **Fill** jest przenoszona do wystąpienia **zestawu danych** i nazwy **DataTableMapping** , jeśli istnieje mapowanie o tej nazwie, jest ono używane; w przeciwnym razie zostanie użyta **tabela DataTable** o tej nazwie.  
  
 Poniższe przykłady umożliwiają utworzenie **DataTableMapping** z nazwą **klientów** i nazwą **elementu DataTable** **BizTalkSchema**. Następnie przykład mapuje wiersze zwracane przez instrukcję SELECT do **elementu DataTable** **BizTalkSchema** .  
  
```vb  
Dim mapping As ITableMapping = _  
  adapter.TableMappings.Add("Customers", "BizTalkSchema")  
mapping.ColumnMappings.Add("CustomerID", "ClientID")  
mapping.ColumnMappings.Add("CompanyName", "ClientName")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIP")  
  
adapter.Fill(custDS, "Customers")  
```  
  
```csharp  
ITableMapping mapping =   
  adapter.TableMappings.Add("Customers", "BizTalkSchema");  
mapping.ColumnMappings.Add("CustomerID", "ClientID");  
mapping.ColumnMappings.Add("CompanyName", "ClientName");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIP");  
  
adapter.Fill(custDS, "Customers");  
```  
  
> [!NOTE]
> Jeśli nie podano nazwy kolumny źródłowej dla mapowania kolumn lub nie podano nazwy tabeli źródłowej dla mapowania tabeli, automatycznie generowane są domyślne nazwy. Jeśli nie podano kolumny źródłowej dla mapowania kolumn, mapowanie kolumny otrzymuje przyrostową domyślną nazwę **SourceColumn** *N,* rozpoczynając od **SourceColumn1**. Jeśli nie podano nazwy tabeli źródłowej dla mapowania tabeli, mapowanie tabeli uzyskuje przyrostową domyślną nazwę elementu **SourceName** *N*, rozpoczynając od **SourceTable1**.  
  
> [!NOTE]
> Zalecamy uniknięcie konwencji nazewnictwa elementu **SourceColumn** *N* dla mapowania kolumn lub elementu **sources** *n* dla mapowania tabeli, ponieważ dostarczona nazwa może powodować konflikt z istniejącą domyślną nazwą mapowania kolumn w  **Nazwa ColumnMappingcollection** lub mapowanie tabeli w **DataTableMappingCollection**. Jeśli podana nazwa już istnieje, zostanie zgłoszony wyjątek.  
  
## <a name="handling-multiple-result-sets"></a>Obsługa wielu zestawów wyników  
 Jeśli **Właściwość SelectCommand** zwraca wiele tabel, **Wypełnij** automatycznie generuje nazwy tabel z przyrostowymi wartościami dla tabel w **zestawie danych**, rozpoczynając od określonej nazwy tabeli i kontynuując w formularzu **TableName** *N*, zaczynając od **TableName1**. Mapowania tabeli można użyć, aby zamapować automatycznie wygenerowaną nazwę tabeli na nazwę, która ma być określona dla tabeli w **zestawie danych**. Na przykład dla elementu **SelectCommand** , który zwraca dwie tabele, **klienci** i **zamówienia**, wydaj następujące wywołanie do **wypełnienia**.  
  
```vb  
adapter.Fill(customersDataSet, "Customers")  
```  

```csharp  
adapter.Fill(customersDataSet, "Customers");  
```  

 W **zestawie danych**są tworzone dwie tabele: **Customers** i **Customers1**. Mapowania tabel można użyć, aby upewnić się, że druga tabela ma nazwę **Orders** zamiast **Customers1**. W tym celu należy zmapować tabelę źródłową **Customers1** do **kolejności**tabel **zestawu danych** , jak pokazano w poniższym przykładzie.  
  
```vb  
adapter.TableMappings.Add("Customers1", "Orders")  
adapter.Fill(customersDataSet, "Customers")  
```  

```csharp  
adapter.TableMappings.Add("Customers1", "Orders");  
adapter.Fill(customersDataSet, "Customers");  
```
  
## <a name="see-also"></a>Zobacz także

- [Elementy DataAdapter i DataReaders](dataadapters-and-datareaders.md)
- [Pobieranie i modyfikowanie danych ADO.NET](retrieving-and-modifying-data.md)
- [Omówienie ADO.NET](ado-net-overview.md)
