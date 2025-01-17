---
title: Przykłady kodu ADO.NET
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c119657a-9ce6-4940-91e4-ac1d5f0d9584
ms.openlocfilehash: 86d5fc63168330502f81dfa464fcd2c04f014760
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785060"
---
# <a name="adonet-code-examples"></a>Przykłady kodu ADO.NET
Na listach w tym temacie przedstawiono sposób pobierania danych z bazy danych przy użyciu następujących technologii ADO.NET:

- ADO.NET dostawcy danych:

  - [Klient SqlClient](#sqlclient) (`System.Data.SqlClient`)

  - [OLEDB](#oledb) (`System.Data.OleDb`)

  - [Odbc](#odbc) (`System.Data.Odbc`)

  - [OracleClient](#oracleclient) (`System.Data.OracleClient`)

- ADO.NET Entity Framework:

  - [LINQ to Entities](#linq-to-entities)

  - [Wpisane ObjectQuery](#typed-objectquery)

  - [EntityClient](#entityclient) (`System.Data.EntityClient`)

- [LINQ to SQL](#linq-to-sql)

## <a name="adonet-data-provider-examples"></a>Przykłady dostawcy danych ADO.NET
Poniższe listy kodu przedstawiają sposób pobierania danych z bazy danych przy użyciu dostawców danych ADO.NET. Dane są zwracane w `DataReader`. Aby uzyskać więcej informacji, zobacz [pobieranie danych za pomocą elementu DataReader](retrieving-data-using-a-datareader.md).

### <a name="sqlclient"></a>SqlClient
W kodzie w tym przykładzie przyjęto założenie, że można `Northwind` nawiązać połączenie z przykładową bazą danych na Microsoft SQL Server. Kod tworzy <xref:System.Data.SqlClient.SqlCommand> do wybierania wierszy z tabeli Products, <xref:System.Data.SqlClient.SqlParameter> dodając, aby ograniczyć wyniki do wierszy z jednostką CenaJednostkowa większą niż określona wartość parametru, w tym przypadku 5. <xref:System.Data.SqlClient.SqlConnection> Jest otwarty`using` wewnątrz bloku, co zapewnia, że zasoby są zamykane i usuwane po zakończeniu działania kodu. Kod wykonuje polecenie przy użyciu <xref:System.Data.SqlClient.SqlDataReader>i wyświetla wyniki w oknie konsoli.

 [!code-csharp[DataWorks SampleApp.SqlClient#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.SqlClient/CS/source.cs#1)]
 [!code-vb[DataWorks SampleApp.SqlClient#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.SqlClient/VB/source.vb#1)]

### <a name="oledb"></a>OleDb
W kodzie w tym przykładzie przyjęto założenie, że można nawiązać połączenie z przykładową bazą danych Northwind programu Microsoft Access. Kod tworzy <xref:System.Data.OleDb.OleDbCommand> do wybierania wierszy z tabeli Products, <xref:System.Data.OleDb.OleDbParameter> dodając, aby ograniczyć wyniki do wierszy z jednostką CenaJednostkowa większą niż określona wartość parametru, w tym przypadku 5. Program jest otwarty wewnątrz `using` bloku, co zapewnia, że zasoby są zamykane i usuwane po zakończeniu działania kodu. <xref:System.Data.OleDb.OleDbConnection> Kod wykonuje polecenie przy użyciu <xref:System.Data.OleDb.OleDbDataReader>i wyświetla wyniki w oknie konsoli.

 [!code-csharp[DataWorks SampleApp.OleDb#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.OleDb/CS/source.cs#1)]
 [!code-vb[DataWorks SampleApp.OleDb#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.OleDb/VB/source.vb#1)]

### <a name="odbc"></a>Odbc
W kodzie w tym przykładzie przyjęto założenie, że można nawiązać połączenie z przykładową bazą danych Northwind programu Microsoft Access. Kod tworzy <xref:System.Data.Odbc.OdbcCommand> do wybierania wierszy z tabeli Products, <xref:System.Data.Odbc.OdbcParameter> dodając, aby ograniczyć wyniki do wierszy z jednostką CenaJednostkowa większą niż określona wartość parametru, w tym przypadku 5. <xref:System.Data.Odbc.OdbcConnection> Jest otwarty`using` wewnątrz bloku, co zapewnia, że zasoby są zamykane i usuwane po zakończeniu działania kodu. Kod wykonuje polecenie przy użyciu <xref:System.Data.Odbc.OdbcDataReader>i wyświetla wyniki w oknie konsoli.

[!code-csharp[DataWorks SampleApp.Odbc#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.Odbc/CS/source.cs#1)] 
[!code-vb[DataWorks SampleApp.Odbc#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.Odbc/VB/source.vb#1)] 

### <a name="oracleclient"></a>OracleClient
Kod w tym przykładzie założono połączenie z DEMONSTRACJą. Klient na serwerze Oracle. Należy również dodać odwołanie do pliku System. Data. OracleClient. dll. Kod zwraca dane w <xref:System.Data.OracleClient.OracleDataReader>.

 [!code-csharp[DataWorks SampleApp.Oracle#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.Oracle/CS/source.cs#1)]
 [!code-vb[DataWorks SampleApp.Oracle#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.Oracle/VB/source.vb#1)]

## <a name="entity-framework-examples"></a>Przykłady Entity Framework
Poniższe listy kodu pokazują, jak pobrać dane ze źródła danych, badając jednostki w Entity Data Model (EDM). Te przykłady używają modelu opartego na przykładowej bazie danych Northwind. Aby uzyskać więcej informacji na temat Entity Framework, zobacz [Entity Framework Omówienie](./ef/overview.md).

### <a name="linq-to-entities"></a>LINQ do Jednostek
Kod w tym przykładzie używa zapytania LINQ do zwracania danych jako obiektów kategorii, które są rzutowane jako typ anonimowy, który zawiera tylko właściwości IDKategorii i CategoryName. Aby uzyskać więcej informacji, zobacz [LINQ to Entities przegląd](./ef/language-reference/linq-to-entities.md).

```csharp
using System;
using System.Linq;
using System.Data.Objects;
using NorthwindModel;

class LinqSample
{
    public static void ExecuteQuery()
    {
        using (NorthwindEntities context = new NorthwindEntities())
        {
            try
            {
                var query = from category in context.Categories
                            select new
                            {
                                categoryID = category.CategoryID,
                                categoryName = category.CategoryName
                            };

                foreach (var categoryInfo in query)
                {
                    Console.WriteLine("\t{0}\t{1}",
                        categoryInfo.categoryID, categoryInfo.categoryName);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

```vb
Option Explicit On
Option Strict On

Imports System
Imports System.Linq
Imports System.Data.Objects
Imports NorthwindModel

Class LinqSample
    Public Shared Sub ExecuteQuery()
        Using context As NorthwindEntities = New NorthwindEntities()
            Try
                Dim query = From category In context.Categories _
                            Select New With _
                            { _
                                .categoryID = category.CategoryID, _
                                .categoryName = category.CategoryName _
                            }

                For Each categoryInfo In query
                    Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                        categoryInfo.categoryID, categoryInfo.categoryName)
                Next
            Catch ex As Exception
                Console.WriteLine(ex.Message)
            End Try
        End Using
    End Sub
End Class
```

### <a name="typed-objectquery"></a>Wpisane ObjectQuery
Kod w tym przykładzie używa <xref:System.Data.Objects.ObjectQuery%601> do zwracania danych jako kategorii obiektów. Aby uzyskać więcej informacji, zobacz [zapytania dotyczące obiektów](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896241(v=vs.100)).

```csharp
using System;
using System.Data.Objects;
using NorthwindModel;

class ObjectQuerySample
{
    public static void ExecuteQuery()
    {
        using (NorthwindEntities context = new NorthwindEntities())
        {
            ObjectQuery<Categories> categoryQuery = context.Categories;

            foreach (Categories category in 
                categoryQuery.Execute(MergeOption.AppendOnly))
            {
                Console.WriteLine("\t{0}\t{1}",
                    category.CategoryID, category.CategoryName);
            }
        }
    }
}
```

```vb
Option Explicit On
Option Strict On

Imports System
Imports System.Data.Objects
Imports NorthwindModel

Class ObjectQuerySample
    Public Shared Sub ExecuteQuery()
        Using context As NorthwindEntities = New NorthwindEntities()
            Dim categoryQuery As ObjectQuery(Of Categories) = context.Categories

            For Each category As Categories In _
                categoryQuery.Execute(MergeOption.AppendOnly)
                Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                    category.CategoryID, category.CategoryName)
            Next
        End Using
    End Sub
End Class
```

### <a name="entityclient"></a>EntityClient
Kod w tym przykładzie używa <xref:System.Data.EntityClient.EntityCommand> do wykonywania zapytania Entity SQL. To zapytanie zwraca listę rekordów reprezentujących wystąpienia typu jednostki kategorii. <xref:System.Data.EntityClient.EntityDataReader> Służy do uzyskiwania dostępu do rekordów danych w zestawie wyników. Aby uzyskać więcej informacji, zobacz [EntityClient Provider for the Entity Framework](./ef/entityclient-provider-for-the-entity-framework.md).

```csharp
using System;
using System.Data;
using System.Data.Common;
using System.Data.EntityClient;
using NorthwindModel;

class EntityClientSample
{
    public static void ExecuteQuery()
    {
        string queryString =
            @"SELECT c.CategoryID, c.CategoryName 
                FROM NorthwindEntities.Categories AS c";

        using (EntityConnection conn =
            new EntityConnection("name=NorthwindEntities"))
        {
            try
            {
                conn.Open();
                using (EntityCommand query = new EntityCommand(queryString, conn))
                {
                    using (DbDataReader rdr = 
                        query.ExecuteReader(CommandBehavior.SequentialAccess))
                    {
                        while (rdr.Read())
                        {
                            Console.WriteLine("\t{0}\t{1}", rdr[0], rdr[1]);
                        }
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

```vb
Option Explicit On
Option Strict On

Imports System
Imports System.Data
Imports System.Data.Common
Imports System.Data.EntityClient
Imports NorthwindModel

Class EntityClientSample
    Public Shared Sub ExecuteQuery()
        Dim queryString As String = _
            "SELECT c.CategoryID, c.CategoryName " & _
                "FROM NorthwindEntities.Categories AS c"

        Using conn As EntityConnection = _
            New EntityConnection("name=NorthwindEntities")

            Try
                conn.Open()
                Using query As EntityCommand = _
                New EntityCommand(queryString, conn)
                    Using rdr As DbDataReader = _
                        query.ExecuteReader(CommandBehavior.SequentialAccess)
                        While rdr.Read()
                            Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                                              rdr(0), rdr(1))
                        End While
                    End Using
                End Using
            Catch ex As Exception
                Console.WriteLine(ex.Message)
            End Try
        End Using 
    End Sub
End Class
```

## <a name="linq-to-sql"></a>LINQ do SQL
Kod w tym przykładzie używa zapytania LINQ do zwracania danych jako obiektów kategorii, które są rzutowane jako typ anonimowy, który zawiera tylko właściwości IDKategorii i CategoryName. Ten przykład jest oparty na kontekście danych Northwind. Aby uzyskać więcej informacji, zobacz [wprowadzenie](./sql/linq/getting-started.md).

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Northwind;

    class LinqSqlSample
    {
        public static void ExecuteQuery()
        {
            using (NorthwindDataContext db = new NorthwindDataContext())
            {
                try
                {
                    var query = from category in db.Categories
                                select new
                                {
                                    categoryID = category.CategoryID,
                                    categoryName = category.CategoryName
                                };

                    foreach (var categoryInfo in query)
                    {
                        Console.WriteLine("vbTab {0} vbTab {1}",
                            categoryInfo.categoryID, categoryInfo.categoryName);
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine(ex.Message);
                }
            }
        }
    }
```

```vb
Option Explicit On
Option Strict On

Imports System
Imports System.Collections.Generic
Imports System.Linq
Imports System.Text
Imports Northwind

Class LinqSqlSample
    Public Shared Sub ExecuteQuery()
        Using db As NorthwindDataContext = New NorthwindDataContext()
            Try
                Dim query = From category In db.Categories _
                                Select New With _
                                { _
                                    .categoryID = category.CategoryID, _
                                    .categoryName = category.CategoryName _
                                }

                For Each categoryInfo In query
                    Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                            categoryInfo.categoryID, categoryInfo.categoryName)
                Next
            Catch ex As Exception
                Console.WriteLine(ex.Message)
            End Try
            End Using 
    End Sub
End Class
```

## <a name="see-also"></a>Zobacz także

- [Omówienie ADO.NET](ado-net-overview.md)
- [Pobieranie i modyfikowanie danych ADO.NET](retrieving-and-modifying-data.md)
- [Tworzenie aplikacji danych](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/h0y4a0f6(v=vs.120))
- [Wykonywanie zapytania dotyczącego Entity Data Model (zadania Entity Framework)](https://docs.microsoft.com/previous-versions/bb738455(v=vs.90))
- [Instrukcje: Wykonaj zapytanie zwracające obiekty typu anonimowego](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738512(v=vs.100))
