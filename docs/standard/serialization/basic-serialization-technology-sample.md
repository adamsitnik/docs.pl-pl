---
title: Przykład technologii serializacji podstawowej
ms.date: 03/30/2017
ms.assetid: 9d824e16-08d1-4a36-bc7f-2388c1f75f34
ms.openlocfilehash: e5dcc9ec7cf6f996c97262b14020552286c530da
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353142"
---
# <a name="basic-serialization-technology-sample"></a>Przykład technologii serializacji podstawowej

[Pobierz przykład](https://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Runtime%20Serialization/Basic.zip.exe)

Ten przykład pokazuje możliwości środowiska uruchomieniowego języka wspólnego do serializacji grafu obiektów w pamięci do strumienia. Ten przykład może używać <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> lub <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> do serializacji. Połączonej listy wypełniany danymi, jest serializacji lub deserializacji z strumienia PLiku lub. W obu przypadkach zostanie wyświetlona lista, aby zobaczyć wyniki. Połączona lista jest typu `LinkedList`, typu zdefiniowanego przez ten przykład.

Komentarzy w PLikach źródłowych kodu i build.proj uzyskać więcej informacji o serializacji.

### <a name="to-build-the-sample-using-the-command-prompt"></a>Aby skompilować przykład za pomocą wiersza polecenia

1. Przejdź do jednego z podkatalogi specyficzne dla języka w katalogu Technologies\Serialization\Runtime Serialization\Basic, za pomocą wiersza polecenia.

2. Wpisz **MSBuild SerializationCS. sln**, **MSBuild SerializationJSL. sln** lub **MSBuild SerializationVB. sln**, w zależności od wybranego języka programowania, w wierszu polecenia.

### <a name="to-build-the-sample-using-visual-studio"></a>Aby skompilować przykład za pomocą programu Visual Studio

1. Otwórz Eksploratora plików i przejdź do jednego z podkatalogów właściwych dla języka dla przykładu.

2. Kliknij dwukrotnie ikonę PLiku SerializationCS.sln, SerializationJSL.sln lub SerializationVB.sln, w zależności od wybranych przez siebie język programowania, aby otworzyć go w programie Visual Studio.

3. W menu **kompilacja** wybierz opcję **Kompiluj rozwiązanie**.

 Przykładowa aplikacja zostanie skompilowana w domyślnym podkatalogu \Bin lub \bin\Debug.

### <a name="to-run-the-sample"></a>Aby uruchomić przykład

1. Przejdź do katalogu zawierającego wbudowanych PLiku wykonywalnego.

2. Wpisz **Serialization. exe**wraz z wartościami parametrów, które chcesz, w wierszu polecenia.

  > [!NOTE]
  > Ten przykład kompiluje aplikację konsolową. Należy uruchomić go za pomocą wiersza polecenia, aby można było wyświetlić dane wyjściowe.

## <a name="remarks"></a>Uwagi

Przykładowa aplikacja akceptuje parametry wiersza polecenia wskazujące, który test ma zostać wykonany. Aby serializować listę składającą się z 10 węzłów do pliku o nazwie **test. XML** przy użyciu programu formatującego protokołu SOAP, należy użyć parametrów **SX test. XML 10**.

Na przykład:

```console
Serialize.exe -sx Test.xml 10
```

Aby zdeserializować plik **test. XML** z poprzedniego przykładu, użyj parametrów **DX test. XML**.

Na przykład:

```console
Serialize.exe -dx Test.xml
```

W dwóch przykładach powyżej "x" w przełączniku wiersza polecenia wskazuje, że chcesz serializacji SOAP XML. W swoim miejscu możesz użyć "b", aby użyć serializacji binarnej. Jeśli chcesz spróbować serializacji z bardzo dużej liczby węzłów, można przekierować dane wyjściowe z konsoli do PLiku.

Na przykład:

```console
Serialize.exe -sb Test.bin 10000 >somefile.txt
```

Poniższe punktory krótko opisują klasy i technologie używane w tym przykładzie.

- Środowisko wykonawcze serializacji

  - <xref:System.Runtime.Serialization.IFormatter> służy do odwoływania się do <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> lub <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> obiektu.

  - <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> służy do serializacji połączonej listy do strumienia w formacie binarnym. Binarny program formatujący używa formatu tylko <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> rozumie typu. Jednak dane są zwięzły.

  - <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> służy do serializacji połączonej listy do strumienia w formacie protokołu SOAP. Protokołu SOAP jest to standardowy format.

- We/Wy strumienia

  - <xref:System.IO.Stream>Służy do serializacji i deserializacji. Typem określonego strumienia użytym w tym przykładzie jest typ <xref:System.IO.FileStream>. Jednak można użyć serializacji z dowolnego typu opracowane na podstawie <xref:System.IO.Stream>.

  - <xref:System.IO.File> służy do tworzenia obiektów <xref:System.IO.FileStream> do odczytu i tworzenia plików na dysku.

  - <xref:System.IO.FileStream> używany do serializacji i deserializacji połączonych list.

## <a name="see-also"></a>Zobacz także

- <xref:System.IO>
- <xref:System.IO.File>
- <xref:System.IO.FileStream>
- <xref:System.IO.Stream>
- <xref:System.Random>
- <xref:System.Runtime.Serialization>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>
- <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>
- <xref:System.Runtime.Serialization.IFormatter>
- <xref:System.SerializableAttribute>
- <xref:System.Xml.Serialization>
- [Serializacja podstawowa](../../../docs/standard/serialization/basic-serialization.md)
- [Serializacja binarna](../../../docs/standard/serialization/binary-serialization.md)
- [Kontrolowanie serializacji XML przy użyciu atrybutów](../../../docs/standard/serialization/controlling-xml-serialization-using-attributes.md)
- [Wprowadzenie do serializacji XML](../../../docs/standard/serialization/introducing-xml-serialization.md)
- [Serializacja](../../../docs/standard/serialization/index.md)
- [Serializacja XML i SOAP](../../../docs/standard/serialization/xml-and-soap-serialization.md)
