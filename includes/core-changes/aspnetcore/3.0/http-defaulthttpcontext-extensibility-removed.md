---
ms.openlocfilehash: 7b5ae84d02b83a10a4b9e002fc2ed4ee0833b84c
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2019
ms.locfileid: "73198533"
---
### <a name="http-defaulthttpcontext-extensibility-removed"></a>HTTP: Usunięto rozszerzalność DefaultHttpContext

W ramach ulepszeń wydajności ASP.NET Core 3,0 została usunięta Funkcja rozszerzania `DefaultHttpContext`. Klasa jest teraz `sealed`. Aby uzyskać więcej informacji, zobacz [ASPNET/AspNetCore # 6504](https://github.com/aspnet/AspNetCore/pull/6504).

Jeśli testy jednostkowe używają `Mock<DefaultHttpContext>`, zamiast tego należy użyć `Mock<HttpContext>`.

W przypadku dyskusji zobacz [ASPNET/AspNetCore # 6534](https://github.com/aspnet/AspNetCore/issues/6534).

#### <a name="version-introduced"></a>Wprowadzona wersja

3.0

#### <a name="old-behavior"></a>Stare zachowanie

Klasy mogą pochodzić od `DefaultHttpContext`.

#### <a name="new-behavior"></a>Nowe zachowanie

Klasy nie mogą pochodzić od `DefaultHttpContext`.

#### <a name="reason-for-change"></a>Przyczyna zmiany

Rozszerzalność podano początkowo, aby umożliwić buforowanie `HttpContext`, ale wprowadza niepotrzebną złożoność i utrudnia inne optymalizacje.

#### <a name="recommended-action"></a>Zalecana akcja

Jeśli używasz `Mock<DefaultHttpContext>` w testach jednostkowych, zacznij korzystać z `Mock<HttpContext>`.

#### <a name="category"></a>Kategoria

ASP.NET Core

#### <a name="affected-apis"></a>Dotyczy interfejsów API

<xref:Microsoft.AspNetCore.Http.DefaultHttpContext?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:Microsoft.AspNetCore.Http.DefaultHttpContext`

-->
