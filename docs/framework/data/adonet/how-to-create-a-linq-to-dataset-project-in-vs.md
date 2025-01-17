---
title: Tworzenie projektu LINQ to DataSet w programie Visual Studio
ms.date: 08/15/2018
ms.assetid: 49ba6cb0-cdd2-4571-aeaa-25bf0f40e9b3
ms.openlocfilehash: 8b905c65575c3c567459d843b2a5d1606bc63228
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783780"
---
# <a name="how-to-create-a-linq-to-dataset-project-in-visual-studio"></a>Instrukcje: Tworzenie projektu LINQ to DataSet w programie Visual Studio

Różne typy projektów LINQ wymagają niektórych odwołań zestawów i importowanych przestrzeni nazw (Visual Basic [) lub dyrektyw](../../../csharp/language-reference/keywords/using-directive.md) (C#). Minimalne wymaganie dla LINQ to odwołanie do *System. Core. dll* i `using` dyrektywy for <xref:System.Linq>.

Te wymagania są udostępniane domyślnie w przypadku tworzenia nowego C# projektu aplikacji konsolowej w programie Visual Studio 2017. Jeśli uaktualniasz projekt ze starszej wersji programu Visual Studio, może być konieczne ręczne podanie tych odwołań związanych z LINQ.

LINQ to DataSet wymaga dwóch dodatkowych odwołań do plików *System. Data. dll* i *System. Data. DataSetExtensions. dll*.

> [!NOTE]
> W przypadku kompilowania z poziomu wiersza polecenia należy ręcznie odwoływać się do bibliotek DLL związanych z LINQ w *%ProgramFiles%\Reference Assemblies\Microsoft\Framework\v3.5*.

## <a name="to-enable-linq-to-dataset-functionality"></a>Aby włączyć funkcję LINQ to DataSet

Wykonaj następujące kroki, aby włączyć funkcję LINQ to DataSet w istniejącym projekcie.

1. Dodaj odwołania do system **. Core**, **System. Data**i **System. Data. DataSetExtensions**.

   W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy węzeł **odwołania** i wybierz polecenie **Dodaj odwołanie**. W oknie dialogowym **Menedżer odwołań** wybierz kolejno pozycje **System. Core**, **System. Data**i **System. Data. DataSetExtensions**. Kliknij przycisk **OK**.

1. Dodaj dyrektywy [using](../../../csharp/language-reference/keywords/using-directive.md) (lub [importuje instrukcje](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) w Visual Basic) dla elementu **System. Data** i **System. LINQ**.

   ```csharp
   using System.Data;
   using System.Linq;
   ```

1. Opcjonalnie Dodaj `using` dyrektywę (lub `Imports` instrukcję) dla elementu **System. Data. Common** lub **System. Data. SqlClient**, w zależności od sposobu łączenia się z bazą danych.

## <a name="see-also"></a>Zobacz także

- [Wprowadzenie do LINQ to DataSet](getting-started-linq-to-dataset.md)
