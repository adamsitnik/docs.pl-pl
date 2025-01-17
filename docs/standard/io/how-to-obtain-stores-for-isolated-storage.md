---
title: 'Instrukcje: Uzyskiwanie magazynów dla izolowanego magazynu'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- stores, obtaining
- storing data using isolated storage, obtaining stores
- isolated storage, obtaining stores
- data stores, obtaining
- data storage using isolated storage, obtaining stores
ms.assetid: fcb6b178-d526-47c4-b029-e946f880f9db
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d6fbc78c379951e05869a433875d057c49d44594
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/13/2019
ms.locfileid: "70969256"
---
# <a name="how-to-obtain-stores-for-isolated-storage"></a>Instrukcje: Uzyskiwanie magazynów dla izolowanego magazynu
Izolowany magazyn uwidacznia wirtualny system plików w przedziale danych. <xref:System.IO.IsolatedStorage.IsolatedStorageFile> Klasa dostarcza wiele metod współpracy z izolowanym magazynem. Aby utworzyć i pobrać magazyny <xref:System.IO.IsolatedStorage.IsolatedStorageFile> , program udostępnia trzy metody statyczne:  
  
- <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A>zwraca magazyn izolowany przez użytkownika i zestaw.  
  
- <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForDomain%2A>zwraca magazyn izolowany przez domenę i zestaw.  
  
     Obie metody pobierają magazyn, który należy do kodu, z którego są wywoływane.  
  
- Metoda <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> statyczna zwraca izolowany magazyn, który jest określony przez przekazanie w kombinacji parametrów zakresu.  
  
 Poniższy kod zwraca magazyn izolowany przez użytkownika, zestaw i domenę.  
  
 [!code-cpp[Conceptual.IsolatedStorage#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source6.cpp#6)]
 [!code-csharp[Conceptual.IsolatedStorage#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source6.cs#6)]
 [!code-vb[Conceptual.IsolatedStorage#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source6.vb#6)]  
  
 Możesz użyć <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> metody, aby określić, że magazyn powinien być mobilny przy użyciu profilu użytkownika mobilnego. Aby uzyskać szczegółowe informacje na temat sposobu konfigurowania tego programu, zobacz [typy izolacji](../../../docs/standard/io/types-of-isolation.md).  
  
 Izolowane magazyny uzyskane z różnych zestawów są domyślnie różne w różnych sklepach. Możesz uzyskać dostęp do magazynu innego zestawu lub domeny przez przekazanie dowodu zestawu lub domeny w parametrach <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> metody. Wymaga to uprawnienia dostępu do wydzielonej pamięci masowej przez tożsamość domeny aplikacji. Aby uzyskać więcej informacji, zobacz <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> przeciążania metod.  
  
 Metody <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A>, <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForDomain%2A>i zwracają<xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> obiekt<xref:System.IO.IsolatedStorage.IsolatedStorageFile> . Aby ułatwić podjęcie decyzji, który typ izolacji jest najbardziej odpowiedni dla danej sytuacji, zobacz [typy izolacji](../../../docs/standard/io/types-of-isolation.md). Jeśli masz obiekt izolowanego pliku magazynu, możesz użyć odizolowanych metod magazynu do odczytu, zapisu, tworzenia i usuwania plików i katalogów.  
  
 Nie istnieje mechanizm, który uniemożliwia przekazanie <xref:System.IO.IsolatedStorage.IsolatedStorageFile> obiektu do kodu, który nie ma wystarczających uprawnień dostępu do pobrania samego sklepu. Tożsamości domen i zestawów oraz uprawnienia izolowanego magazynu są sprawdzane tylko wtedy, gdy <xref:System.IO.IsolatedStorage.IsolatedStorage> jest uzyskiwane odwołanie do obiektu, <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A>zazwyczaj <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForDomain%2A>w metodzie, lub <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> . Ochrona odwołań do <xref:System.IO.IsolatedStorage.IsolatedStorageFile> obiektów jest z tego względu odpowiedzialnością za kod, który używa tych odwołań.  
  
## <a name="example"></a>Przykład  
 Poniższy kod zawiera prosty przykład klasy pobierającej magazyn izolowany przez użytkownika i zestaw. Kod można zmienić, aby pobrać magazyn izolowany według użytkownika, domeny i zestawu przez dodanie <xref:System.IO.IsolatedStorage.IsolatedStorageScope.Domain?displayProperty=nameWithType> do argumentów <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> , które są przekazywane przez metodę.  
  
 Po uruchomieniu kodu można potwierdzić, że magazyn został utworzony, wpisując **Storeadm/list** w wierszu polecenia. Spowoduje to uruchomienie [Narzędzia izolowanego magazynu (Storeadm. exe)](../../../docs/framework/tools/storeadm-exe-isolated-storage-tool.md) i wyświetlenie listy wszystkich aktualnie wyizolowanych magazynów dla danego użytkownika.  
  
 [!code-cpp[Conceptual.IsolatedStorage#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source6.cpp#7)]
 [!code-csharp[Conceptual.IsolatedStorage#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source6.cs#7)]
 [!code-vb[Conceptual.IsolatedStorage#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source6.vb#7)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- <xref:System.IO.IsolatedStorage.IsolatedStorageScope>
- [Wydzielona pamięć masowa](../../../docs/standard/io/isolated-storage.md)
- [Typy izolacji](../../../docs/standard/io/types-of-isolation.md)
- [Zestawy w środowisku .NET](../assembly/index.md)
