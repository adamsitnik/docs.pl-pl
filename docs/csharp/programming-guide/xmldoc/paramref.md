---
title: <paramref> — C# Przewodnik programowania
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- paramref
- <paramref>
helpviewer_keywords:
- <paramref> C# XML tag
- paramref C# XML tag
ms.assetid: 756c24c1-f591-40e8-a838-559761539b0b
ms.openlocfilehash: 43e98565ff7294ebb6fa7e71d1be17522dbb15de
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72523400"
---
# <a name="paramref-c-programming-guide"></a>\<paramref > (C# Przewodnik programowania)
## <a name="syntax"></a>Składnia  
  
```xml  
<paramref name="name"/>  
```  
  
## <a name="parameters"></a>Parametry  
 `name`  
 Nazwa parametru, do którego się odwołuje. Ujmij nazwę w znaki podwójnego cudzysłowu ("").  
  
## <a name="remarks"></a>Uwagi  
 Tag \<paramref > umożliwia wskazanie, że słowo w komentarzach do kodu, na przykład w \<summary > lub \<remarks > bloku odwołuje się do parametru. Plik XML można przetworzyć, aby sformatować ten wyraz w sposób niezależny, na przykład za pomocą czcionki pogrubionej lub kursywy.  
  
 Kompiluj z [-doc](../../language-reference/compiler-options/doc-compiler-option.md) , aby przetwarzać komentarze dokumentacji do pliku.  
  
## <a name="example"></a>Przykład  
 [!code-csharp[csProgGuideDocComments#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#7)]  
  
## <a name="see-also"></a>Zobacz także

- [Przewodnik programowania w języku C#](../index.md)
- [Zalecane tagi przeznaczone do komentarzy dokumentacji](./recommended-tags-for-documentation-comments.md)
