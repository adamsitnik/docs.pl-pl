---
title: Narzędzie generatora serializatora XML (Sgen.exe)
ms.date: 03/30/2017
ms.assetid: cc1d1f1c-fb26-4be9-885a-3fe84c81cec6
ms.openlocfilehash: 492337973f71b10dc061353b7083f596b402ae29
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392708"
---
# <a name="xml-serializer-generator-tool-sgenexe"></a>Narzędzie generatora serializatora XML (Sgen.exe)
Generator serializatora XML tworzy zestawu serializacji XML dla typów w określonym zestawie w celu zwiększenia wydajności uruchamiania <xref:System.Xml.Serialization.XmlSerializer> po serializuje lub deserializuje obiektów określonego typu.  
  
## <a name="syntax"></a>Składnia  
  
```console  
sgen [options]  
```  
  
## <a name="parameters"></a>Parametry  
  
|Opcja|Opis|  
|------------|-----------------|  
|**/a @ no__t-1ssembly @ no__t-2:** _filename_|Generuje kod serializacji dla wszystkich typów zawartych w zestawie lub pliku wykonywalnym określonym przez *filename*. Można uwzględnić tylko jeden PLik. Jeśli ten argument jest powtarzany, nazwisko PLik jest używany.|  
|**/c @ no__t-1ompiler @ no__t-2:** _Opcje_|Określa opcje do przekazania do kompilatora C#. Wszystkie opcje csc.exe są obsługiwane, gdy przekazywane do kompilator. To może posłużyć do określenia zestawu powinny być podpisane i określ PLik klucza.|  
|**/d @ no__t-1ebug @ no__t-2**|Generuje obrazu, który może być używany z debugera.|  
|**/f @ no__t-1orce @ no__t-2**|Wymusza zastępowanie istniejącego zestawu o tej samej nazwie. Wartość domyślna to **false**.|  
|**/help lub/?**|Wyświetla składnię polecenia i opcje narzędzia.|  
|**/k @ no__t-1eep @ no__t-2**|Pomija usuwanie wygenerowanych PLików źródłowych i innych PLików tymczasowych po zostały skompilowane do zestawu serializacji. To może posłużyć do określenia, czy to narzędzie jest generowania kodu serializacji dla danego typu.|  
|**/n @ no__t-1ologo @ no__t-2**|Pomija wyświetlanie transparentu startowego firmy Microsoft.|  
|**/o @ no__t-1ut @ no__t-2:** _ścieżka_|Określa katalog, w którym chcesz zapisać wygenerowanego zestawu. **Uwaga:**  Nazwa wygenerowanego zestawu składa się z nazwy zestawu wejściowego i "XmlSerializers. dll".|  
|**/p @ no__t-1roxytypes @ no__t-2**|Generuje kod serializacji tylko dla typów serwera proxy usług sieci Web XML.|  
|**/r @ no__t-1eference @ no__t-2:** _assemblyfiles_|Określa zestawy, które są określone przez typy wymagające serializacji XML. Akceptuje wiele plików zestawów rozdzielonych przecinkami.|  
|**/s @ no__t-1ilent @ no__t-2**|Pomija wyświetlanie komunikatów o sukcesie.|  
|**/t @ no__t-1ype @ no__t-2:** _Typ_|Generuje kod serializacji tylko dla określonego typu.|  
|**/v @ no__t-1erbose @ no__t-2**|Wyświetla pełne dane wyjściowe dla debugowania. Wyświetla listę typów z zestawu docelowego, który nie może być serializowany z <xref:System.Xml.Serialization.XmlSerializer>.|  
|**/?**|Wyświetla składnię polecenia i opcje narzędzia.|  
  
## <a name="remarks"></a>Uwagi  
 Gdy generator serializatorów XML nie jest używany, <xref:System.Xml.Serialization.XmlSerializer> generuje kod serializacji i zestaw serializacji dla każdego typu za każdym razem, gdy aplikacja jest uruchamiana. Aby zwiększyć wydajność uruchamiania serializacji XML, należy użyć narzędzia Sgen. exe w celu wygenerowania tych zestawów z góry. Zestawy te można następnie wdrażać za pomocą aplikacji.  
  
 Generator serializatora XML może również zwiększyć wydajność klientów korzystających z serwerów proxy usług sieci Web XML do komunikowania się z serwerami, ponieważ ten proces serializacji nie będą powodować wydajności trafień, gdy typ jest ładowany po raz pierwszy.  
  
 Nie można używać tych wygenerowanych zestawów po stronie serwera usługi sieci Web. Narzędzie to jest tylko dla klientów usługi sieci Web i scenariusze ręczne serializacji.  
  
 Jeśli zestawu zawierającego typ do serializacji nosi MyType.dll, następnie zestawu skojarzonego serializacji będzie miał nazwę MyType.XmlSerializers.dll.  
  
## <a name="examples"></a>Przykłady  
 Następujące polecenie tworzy zestaw o nazwie Data.XmlSerializers.dll dla wszystkich typów, które są zawarte w zestawie o nazwie Data.dll serializacji.  
  
```console  
sgen Data.dll   
```  
  
 Zestaw Data.XmlSerializers.dll można odwoływać się z kodu, który musi serializacji i deserializacji typów w Data.dll.  
  
## <a name="see-also"></a>Zobacz także

- [Narzędzia](../../../docs/framework/tools/index.md)
- [Wiersze polecenia](../../../docs/framework/tools/developer-command-prompt-for-vs.md)
