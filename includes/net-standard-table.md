---
ms.openlocfilehash: 9b8d28f7f5508b4ba7c46306b5e78aa3d53d95e0
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2019
ms.locfileid: "71263344"
---
| .NET Standard              | [1.0]  | [1.1]  | [1.2] | [1.3] | [1.4] | [1,5]              | [1.6]              | [2.0]               | [2,1] |
|----------------------------|--------|--------|-------|-------|-------|--------------------|--------------------|---------------------|---------------------
| .NET Core                  | 1.0    | 1.0    | 1.0   | 1.0   | 1.0   | 1.0                | 1.0                | 2.0                 | 3.0 |
| .NET Framework <sup>1</sup>| 4.5    | 4.5    | 4.5.1 | 4.6   | 4.6.1 | 4.6.1 <sup>2</sup> | 4.6.1 <sup>2</sup> | 4.6.1 <sup>2</sup>  | NIE DOTYCZY<sup>3</sup> |
| Mono                       | 4.6    | 4.6    | 4.6   | 4.6   | 4.6   | 4.6                | 4.6                | 5.4                 | 6.4 |
| Xamarin.iOS                | 10.0   | 10.0   | 10.0  | 10.0  | 10.0  | 10.0               | 10.0               | 10.14               | 12,16 |
| Xamarin.Mac                | 3.0    | 3.0    | 3.0   | 3.0   | 3.0   | 3.0                | 3.0                | 3.8                 | 5,16 |
| Xamarin.Android            | 7.0    | 7.0    | 7.0   | 7.0   | 7.0   | 7.0                | 7.0                | 8.0                 | 10.0 |
| Platforma uniwersalna systemu Windows | 10.0   | 10.0   | 10.0  | 10.0  | 10.0  | 10.0.16299         | 10.0.16299         | 10.0.16299          | TBD |
| Unity                      | 2018,1 | 2018,1 | 2018,1| 2018,1| 2018,1| 2018,1             |  2018,1            | 2018,1              | TBD |

<sup>1 wersje wymienione dla .NET Framework dotyczą zestawu SDK platformy .NET Core 2,0 i nowszych wersji narzędzi. Starsze wersje używają innego mapowania dla .NET Standard 1,5 i wyższych. [Narzędzia dla programu .NET Core Tools for Visual studio 2015 można pobrać](https://github.com/dotnet/core/blob/master/release-notes/download-archive.md) , jeśli nie można przeprowadzić uaktualnienia do programu visual Studio 2017.</sup>

<sup>2 wymienione tutaj wersje reprezentują reguły używane przez narzędzia NuGet do określenia, czy dana Biblioteka .NET Standard ma zastosowanie. Chociaż pakiet NuGet traktuje .NET Framework 4.6.1 jako obsługujący .NET Standard 1,5 do 2,0, istnieje kilka problemów z używaniem bibliotek .NET Standard, które zostały skompilowane dla tych wersji z .NET Framework 4.6.1 projektów. W przypadku projektów .NET Framework, które muszą korzystać z takich bibliotek, zalecamy uaktualnienie projektu do celu .NET Framework 4.7.2 lub wyższy.</sup>

<sup>3 .NET Framework nie obsługują .NET Standard 2,1 lub nowszych. Aby uzyskać więcej informacji, zapoznaj się z [ogłoszeniem .NET Standard 2,1](https://devblogs.microsoft.com/dotnet/announcing-net-standard-2-1/).</sup>

- Kolumny reprezentują wersje .NET Standard. Każda komórka nagłówka jest łączem do dokumentu, który pokazuje, które interfejsy API zostały dodane do tej wersji programu .NET Standard.
- Wiersze reprezentują różne implementacje platformy .NET.
- Numer wersji w każdej komórce wskazuje *minimalną* wersję implementacji, która będzie potrzebna, aby docelowa była wersja .NET Standard.
- Aby zapoznać się z tabelą interaktywną, zobacz [wersje .NET Standard](https://dotnet.microsoft.com/platform/dotnet-standard#versions).

[1.0]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.0.md
[1.1]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.1.md
[1.2]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.2.md
[1.3]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.3.md
[1.4]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.4.md
[1,5]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.5.md
[1.6]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.6.md
[2.0]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.0.md
[2,1]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.1.md
