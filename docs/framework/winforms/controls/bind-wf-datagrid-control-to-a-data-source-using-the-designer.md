---
title: 'Instrukcje: wiązanie kontrolki DataGrid formularzy systemu Windows ze źródłem danych przy użyciu narzędzia Projektant'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- datasets [Windows Forms], binding to DataGrid control
- data binding [Windows Forms], DataGrid control
- DataGrid control [Windows Forms], data binding
- Windows Forms controls, data binding
- bound controls [Windows Forms]
ms.assetid: 4e96e3d0-b1cc-4de1-8774-bc9970ec4554
ms.openlocfilehash: 665a1af990aaf615c763c1c2eae508024d9de5c7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917825"
---
# <a name="how-to-bind-the-windows-forms-datagrid-control-to-a-data-source-using-the-designer"></a>Instrukcje: wiązanie kontrolki DataGrid formularzy systemu Windows ze źródłem danych przy użyciu narzędzia Projektant

> [!NOTE]
> Formant zastępuje i dodaje funkcję <xref:System.Windows.Forms.DataGrid> do <xref:System.Windows.Forms.DataGrid> kontrolki; jednak kontrolka jest zachowywana w celu zapewnienia zgodności z poprzednimi wersjami i w przyszłości, jeśli wybierzesz opcję. <xref:System.Windows.Forms.DataGridView> Aby uzyskać więcej informacji, zobacz [różnice między kontrolkami DataGridView i DataGrid Windows Forms](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).

 Formant Windows Forms <xref:System.Windows.Forms.DataGrid> jest specjalnie zaprojektowany do wyświetlania informacji ze źródła danych. Formant można powiązać w czasie projektowania przez ustawienie <xref:System.Windows.Forms.DataGrid.DataSource%2A> właściwości i <xref:System.Windows.Forms.DataGrid.DataMember%2A> lub w czasie <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> wykonywania przez wywołanie metody. Mimo że można wyświetlać dane z różnych źródeł danych, najbardziej typowe źródła to zestawy danych i ich widoki.

 Jeśli źródło danych jest dostępne w czasie projektowania — na przykład, jeśli formularz zawiera wystąpienie zestawu danych lub widok danych — można powiązać siatkę ze źródłem danych w czasie projektowania. Następnie możesz wyświetlić podgląd danych, które będą wyglądały jak w siatce.

 Możesz również programowo powiązać siatkę w czasie wykonywania. Jest to przydatne, gdy chcesz ustawić źródło danych na podstawie informacji uzyskanych w czasie wykonywania. Na przykład aplikacja może pozwolić, aby użytkownik określił nazwę tabeli do wyświetlenia. Jest to również konieczne w sytuacjach, gdy źródło danych nie istnieje w czasie projektowania. Obejmuje to źródła danych, takie jak tablice, kolekcje, niewpisane zestawy danych i czytniki danych.

 Poniższa procedura wymaga projektu **aplikacji systemu Windows** z formularzem zawierającym <xref:System.Windows.Forms.DataGrid> kontrolkę. Aby uzyskać informacje na temat konfigurowania takiego projektu, zobacz [How to: Utwórz projekt](/visualstudio/ide/step-1-create-a-windows-forms-application-project) aplikacji Windows Forms i [instrukcje: Dodaj formanty do Windows Forms](how-to-add-controls-to-windows-forms.md). W programie Visual Studio 2005 <xref:System.Windows.Forms.DataGrid> formant domyślnie nie znajduje się w **przyborniku** . Aby uzyskać informacje o dodawaniu, [zobacz How to: Dodaj elementy do przybornika](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms165355(v=vs.100)). Ponadto w programie Visual Studio 2005 można użyć okna **źródła danych** dla powiązania danych czasu projektowania. Aby uzyskać więcej informacji [, zobacz Powiązywanie kontrolek z danymi w programie Visual Studio](/visualstudio/data-tools/bind-controls-to-data-in-visual-studio).

## <a name="to-data-bind-the-datagrid-control-to-a-single-table-in-the-designer"></a>Do danych — powiązywanie formantu DataGrid z pojedynczą tabelą w projektancie

1. Ustaw <xref:System.Windows.Forms.DataGrid.DataSource%2A> właściwość kontrolki na obiekt zawierający elementy danych, które chcesz powiązać z.

2. Jeśli źródłem danych jest zestaw danych, ustaw <xref:System.Windows.Forms.DataGrid.DataMember%2A> właściwość na nazwę tabeli, z którą ma zostać utworzone powiązanie.

3. Jeśli źródłem danych jest zestaw danych lub widok danych oparty na tabeli zestawu danych, Dodaj kod do formularza, aby wypełnić zestaw danych.

     Dokładny kod, którego używasz, zależy od tego, gdzie zestaw danych pobiera dane. Jeśli zestaw danych jest wypełniany bezpośrednio z bazy danych, zazwyczaj wywoływana jest `Fill` Metoda adaptera danych, tak jak w poniższym przykładzie kodu, który wypełnia zestaw danych o nazwie: `DsCategories1`

    ```vb
    sqlDataAdapter1.Fill(DsCategories1)
    ```

    ```csharp
    sqlDataAdapter1.Fill(DsCategories1);
    ```

    ```cpp
    sqlDataAdapter1->Fill(dsCategories1);
    ```

4. Obowiązkowe Dodaj odpowiednie style tabeli i Style kolumn do siatki.

     Jeśli nie ma żadnych stylów tabeli, zostanie wyświetlona tabela, ale z minimalnym formatowaniem i wszystkimi kolumnami widocznymi.

## <a name="to-data-bind-the-datagrid-control-to-multiple-tables-in-a-dataset-in-the-designer"></a>Do danych — powiązywanie formantu DataGrid z wieloma tabelami w zestawie danych w projektancie

1. Ustaw <xref:System.Windows.Forms.DataGrid.DataSource%2A> właściwość kontrolki na obiekt zawierający elementy danych, które chcesz powiązać z.

2. Jeśli zestaw danych zawiera powiązane tabele (czyli jeśli zawiera obiekt relacji), ustaw <xref:System.Windows.Forms.DataGrid.DataMember%2A> właściwość na nazwę tabeli nadrzędnej.

3. Napisz kod, aby wypełnić zestaw danych.

## <a name="see-also"></a>Zobacz także

- [DataGrid, kontrolka — omówienie](datagrid-control-overview-windows-forms.md)
- [Instrukcje: Dodawanie tabel i kolumn do kontrolki DataGrid Windows Forms](how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)
- [DataGrid, kontrolka](datagrid-control-windows-forms.md)
- [Wiązanie danych formularzy Windows Forms](../windows-forms-data-binding.md)
- [Uzyskiwanie dostępu do danych w programie Visual Studio](/visualstudio/data-tools/accessing-data-in-visual-studio)
