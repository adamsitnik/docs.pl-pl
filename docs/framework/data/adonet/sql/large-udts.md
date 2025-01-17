---
title: Duże UDT
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 420ae24e-762b-4e09-b4c3-2112c470ee49
ms.openlocfilehash: 33f4263c747ac2590234493ec7cb9e6048ed2b96
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794014"
---
# <a name="large-udts"></a>Duże UDT
Typy zdefiniowane przez użytkownika (UDTs) umożliwiają deweloperom rozbudowa systemu typu skalarnego serwera przez przechowywanie obiektów środowiska uruchomieniowego języka wspólnego (CLR) w bazie danych SQL Server. UDTs może zawierać wiele elementów i może mieć zachowania, w przeciwieństwie do tradycyjnych typów danych aliasów, które składają się z jednego typu danych systemu SQL Server.  
  
> [!NOTE]
> Aby skorzystać z rozszerzonej obsługi SqlClient dla dużych UDTs, należy zainstalować .NET Framework 3,5 SP1 (lub nowsze).  
  
 Wcześniej UDTs były ograniczone do maksymalnego rozmiaru wynoszącego 8 kilobajtów. W SQL Server 2008 to ograniczenie zostało usunięte dla UDTs o formacie <xref:Microsoft.SqlServer.Server.Format.UserDefined>.  
  
 Aby zapoznać się z pełną dokumentacją typów zdefiniowanych przez użytkownika, zapoznaj się z wersją usługi SQL Server Books Online dla używanej wersji SQL Server.  
  
 **Książka SQL Server online**  
  
1. [Zdefiniowane przez użytkownika typy CLR](https://go.microsoft.com/fwlink/?LinkId=98366)  
  
## <a name="retrieving-udt-schemas-using-getschema"></a>Pobieranie schematów UDT przy użyciu GetSchema  
 Metoda zwraca informacje o schemacie <xref:System.Data.DataTable>bazy danych w. <xref:System.Data.SqlClient.SqlConnection> <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> Aby uzyskać więcej informacji, zobacz [SQL Server kolekcje schematów](../sql-server-schema-collections.md).  
  
### <a name="getschematable-column-values-for-udts"></a>Wartości kolumn getschemacollection dla UDTs  
 <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> Metoda zwraca,<xref:System.Data.DataTable> która opisuje metadane kolumn. <xref:System.Data.SqlClient.SqlDataReader> W poniższej tabeli opisano różnice w metadanych kolumn dla dużych UDTs między SQL Server 2005 i SQL Server 2008.  
  
|SqlDataReader — kolumna|SQL Server 2005|SQL Server 2008 i nowsze|  
|--------------------------|---------------------|-------------------------------|  
|`ColumnSize`|Różni się|Różni się|  
|`NumericPrecision`|255|255|  
|`NumericScale`|255|255|  
|`DataType`|`Byte[]`|Wystąpienie UDT|  
|`ProviderSpecificDataType`|`SqlTypes.SqlBinary`|Wystąpienie UDT|  
|`ProviderType`|21 (`SqlDbType.VarBinary`)|29 (`SqlDbType.Udt`)|  
|`NonVersionedProviderType`|29 (`SqlDbType.Udt`)|29 (`SqlDbType.Udt`)|  
|`DataTypeName`|`SqlDbType.VarBinary`|Nazwa trzech części określona jako *Database. SchemaName. TypeName*.|  
|`IsLong`|Różni się|Różni się|  
  
## <a name="sqldatareader-considerations"></a>Zagadnienia dotyczące elementu SqlDataReader  
 <xref:System.Data.SqlClient.SqlDataReader> Została rozszerzona począwszy od SQL Server 2008, aby obsługiwała pobieranie dużych wartości UDT. Jak duże wartości UDT są przetwarzane przez <xref:System.Data.SqlClient.SqlDataReader> zależą od używanej wersji SQL Server, a także `Type System Version` od określonego w parametrach połączenia. Aby uzyskać więcej informacji, zobacz <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
 Następujące metody <xref:System.Data.SqlClient.SqlDataReader> będą <xref:System.Data.SqlTypes.SqlBinary> zwracały zamiast UDT, gdy `Type System Version` ustawiono wartość SQL Server 2005:  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
 Następujące metody zwracają tablicę `Byte[]` zamiast UDT, `Type System Version` gdy ustawiono wartość SQL Server 2005:  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetValue%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
 Należy zauważyć, że nie są wykonywane żadne konwersje dla bieżącej wersji ADO.NET.  
  
## <a name="specifying-sqlparameters"></a>Specifying SqlParameters  
 Następujące <xref:System.Data.SqlClient.SqlParameter> właściwości zostały rozszerzone, aby współpracować z dużymi UDTs.  
  
|Właściwość SqlParameter|Opis|  
|---------------------------|-----------------|  
|<xref:System.Data.SqlClient.SqlParameter.Value%2A>|Pobiera lub ustawia obiekt, który reprezentuje wartość parametru. Domyślny ma wartość null. Właściwość może mieć wartość `SqlBinary`lub `Byte[]`być obiektem zarządzanym.|  
|<xref:System.Data.SqlClient.SqlParameter.SqlValue%2A>|Pobiera lub ustawia obiekt, który reprezentuje wartość parametru. Domyślny ma wartość null. Właściwość może mieć wartość `SqlBinary`lub `Byte[]`być obiektem zarządzanym.|  
|<xref:System.Data.SqlClient.SqlParameter.Size%2A>|Pobiera lub ustawia rozmiar wartości parametru, który ma zostać rozpoznany. Wartość domyślna to 0. Właściwość może być liczbą całkowitą reprezentującą rozmiar wartości parametru. W przypadku dużych UDTs może to być rzeczywisty rozmiar UDT lub-1 dla nieznane.|  
  
## <a name="retrieving-data-example"></a>Przykład pobierania danych  
 Poniższy fragment kodu pokazuje, jak pobrać duże dane UDT. Zmienna zakłada prawidłowe połączenie z bazą danych SQL Server `commandString` , a zmienna przyjmuje prawidłową instrukcję SELECT z kolumną klucza podstawowego na liście. `connectionString`  
  
```csharp  
using (SqlConnection connection = new SqlConnection(   
    connectionString, commandString))  
{  
  connection.Open();  
  SqlCommand command = new SqlCommand(commandString);  
  SqlDataReader reader = command.ExecuteReader();  
  while (reader.Read())  
  {  
    // Retrieve the value of the Primary Key column.  
    int id = reader.GetInt32(0);  
  
    // Retrieve the value of the UDT.  
    LargeUDT udt = (LargeUDT)reader[1];  
  
    // You can also use GetSqlValue and GetValue.  
    // LargeUDT udt = (LargeUDT)reader.GetSqlValue(1);  
    // LargeUDT udt = (LargeUDT)reader.GetValue(1);  
  
    Console.WriteLine(  
     "ID={0} LargeUDT={1}", id, udt);  
  }  
reader.close  
}  
```  
  
```vb  
Using connection As New SqlConnection( _  
    connectionString, commandString)  
    connection.Open()  
    Dim command As New SqlCommand(commandString, connection)  
    Dim reader As SqlDataReader  
    reader = command.ExecuteReader  
  
    While reader.Read()  
      ' Retrieve the value of the Primary Key column.  
      Dim id As Int32 = reader.GetInt32(0)  
  
      ' Retrieve the value of the UDT.  
      Dim udt As LargeUDT = CType(reader(1), LargeUDT)  
  
     ' You can also use GetSqlValue and GetValue.  
     ' Dim udt As LargeUDT = CType(reader.GetSqlValue(1), LargeUDT)  
     ' Dim udt As LargeUDT = CType(reader.GetValue(1), LargeUDT)  
  
      ' Print values.  
      Console.WriteLine("ID={0} LargeUDT={1}", id, udt)  
    End While  
    reader.Close()  
End Using  
```  
  
## <a name="see-also"></a>Zobacz także

- [Konfigurowanie parametrów i typów danych parametrów](../configuring-parameters-and-parameter-data-types.md)
- [Pobieranie informacji o schemacie bazy danych](../retrieving-database-schema-information.md)
- [Mapowanie typu danych serwera SQL](../sql-server-data-type-mappings.md)
- [Dane binarne i dużej wartości w programie SQL Server](sql-server-binary-and-large-value-data.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
