---
title: Elementy DataRow i DataRowView
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8f5eec26-b809-4aca-8778-7e202356d856
ms.openlocfilehash: 7c76435b8a0f7a874504813d91d5eda929d08f67
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786424"
---
# <a name="datarows-and-datarowviews"></a>Elementy DataRow i DataRowView
A <xref:System.Data.DataView> uwidacznia wyliczalną <xref:System.Data.DataRowView> kolekcję obiektów. Obiekty **DataRowView** uwidaczniają wartości jako tablice obiektów, które są indeksowane przez nazwę lub odwołanie porządkowe kolumny w tabeli źródłowej. Możesz uzyskać dostęp do <xref:System.Data.DataRow> programu, który jest udostępniany przez **DataRowView** , <xref:System.Data.DataRowView.Row%2A> przy użyciu właściwości **DataRowView**.  
  
 Podczas wyświetlania wartości przy użyciu **DataRowView** <xref:System.Data.DataView.RowStateFilter%2A> Właściwość **widoku** danych określa, która wersja wiersza podstawowego elementu **DataRow** jest uwidoczniona. Aby uzyskać informacje o uzyskiwaniu dostępu do różnych wersji wierszy przy użyciu elementu **DataRow**, zobacz [Stany wiersza i wersje wierszy](row-states-and-row-versions.md).  
  
 Poniższy przykład kodu wyświetla wszystkie bieżące i oryginalne wartości w tabeli.  
  
```vb  
Dim catView As DataView = New DataView(catDS.Tables("Categories"))  
Console.WriteLine("Current Values:")  
WriteView(catView)  
Console.WriteLine("Original Values:")  
catView.RowStateFilter = DataViewRowState.ModifiedOriginal  
WriteView(catView)      
  
Public Shared Sub WriteView(thisDataView As DataView)  
  Dim rowView As DataRowView  
  Dim i As Integer  
  
  For Each rowView In thisDataView  
    For i = 0 To thisDataView.Table.Columns.Count - 1  
      Console.Write(rowView(i) & vbTab)  
    Next  
    Console.WriteLine()  
  Next  
End Sub  
```  
  
```csharp  
DataView catView = new DataView(catDS.Tables["Categories"]);  
Console.WriteLine("Current Values:");  
WriteView(catView);  
Console.WriteLine("Original Values:");  
catView.RowStateFilter = DataViewRowState.ModifiedOriginal;  
WriteView(catView);  
  
public static void WriteView(DataView thisDataView)  
{  
  foreach (DataRowView rowView in thisDataView)  
  {  
    for (int i = 0; i < thisDataView.Table.Columns.Count; i++)  
      Console.Write(rowView[i] + "\t");  
    Console.WriteLine();  
  }  
}  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Data.DataRowVersion>
- <xref:System.Data.DataViewRowState>
- <xref:System.Data.DataView>
- <xref:System.Data.DataRowView>
- [Elementy DataView](dataviews.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
