---
title: Zapewnianie integralności danych za pomocą wartości skrótu
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generating hash
- verifying hash codes
- cryptography [.NET Framework], hash
- data integrity
- checking hash codes
- encryption [.NET Framework], hash
- hash
ms.assetid: 33660f33-b70f-4dca-8c87-ab35cfc2961a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 995f54e81a48fb3f809d99981ad135974544eb28
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353171"
---
# <a name="ensuring-data-integrity-with-hash-codes"></a>Zapewnianie integralności danych za pomocą wartości skrótu
Wartość skrótu to wartość liczbowa o stałej długości, która jednoznacznie identyfikuje dane. Wartości skrótu przedstawiają duże ilości danych jako dużo mniejsze wartości liczbowe, dlatego są używane z podpisami cyfrowymi. Wartość skrótu można podpisywać bardziej wydajnie niż podpisywanie większej wartości. Wartości skrótu są również przydatne do sprawdzania integralności danych wysyłanych za pomocą niezabezpieczonych kanałów. Wartość skrótu odebranych danych może być porównywana z wartością skrótu danych, która została wysłana w celu określenia, czy dane zostały zmienione.  
  
 W tym temacie opisano sposób generowania i weryfikowania kodów skrótów przy użyciu klas w <xref:System.Security.Cryptography?displayProperty=nameWithType> przestrzeni nazw.  
  
## <a name="generating-a-hash"></a>Generowanie skrótu  
 Zarządzane klasy skrótów mogą mieszać tablicę bajtów lub obiekt strumienia zarządzanego. W poniższym przykładzie jest używany algorytm skrótu SHA1 do tworzenia wartości skrótu dla ciągu. W przykładzie użyto <xref:System.Text.UnicodeEncoding> klasy do przekonwertowania ciągu na tablicę bajtów, które są zmieszane przy <xref:System.Security.Cryptography.SHA1Managed> użyciu klasy. Wartość skrótu zostanie następnie wyświetlona w konsoli programu.  

 Ze względu na kolizje problemów z algorytmem SHA1 firma Microsoft zaleca SHA256ą lub lepszą.
  
 [!code-csharp[GeneratingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/generatingahash/cs/program.cs#1)]
 [!code-vb[GeneratingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/generatingahash/vb/program.vb#1)]  
  
 Ten kod będzie wyświetlał następujący ciąg do konsoli:  
  
 `59 4 248 102 77 97 142 201 210 12 224 93 25 41 100 197 213 134 130 135`  
  
## <a name="verifying-a-hash"></a>Weryfikowanie skrótu  
 Dane można porównać do wartości skrótu, aby określić jej integralność. Zwykle dane są zmieszane w określonym czasie, a wartość skrótu jest chroniona w jakiś sposób. Później można ponownie wykonać mieszanie danych i porównywać ją z wartością chronioną. W przypadku dopasowania wartości skrótu dane nie zostały zmienione. Jeśli wartości nie są zgodne, dane zostały uszkodzone. Aby ten system działał, chroniony skrót musi być zaszyfrowany lub przechowywany jako wpis tajny ze wszystkich niezaufanych stron.  
  
 Poniższy przykład porównuje poprzednią wartość skrótu ciągu z nową wartością skrótu. Ten przykład powoduje pętlę przez każdy bajt wartości skrótu i wykonuje porównanie.  
  
 [!code-csharp[VerifyingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/verifyingahash/cs/program.cs#1)]
 [!code-vb[VerifyingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/verifyingahash/vb/program.vb#1)]  
  
 Jeśli dwie wartości skrótów są zgodne, ten kod wyświetla następujące polecenie w konsoli programu:  
  
```console  
The hash codes match.  
```  
  
 Jeśli nie są zgodne, kod wyświetla następujące elementy:  
  
```console  
The hash codes do not match.  
```  
  
## <a name="see-also"></a>Zobacz także

- [Usługi kryptograficzne](../../../docs/standard/security/cryptographic-services.md)
