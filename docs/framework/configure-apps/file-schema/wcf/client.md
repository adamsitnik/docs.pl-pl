---
title: <client>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.ServiceModel/client
- http://schemas.microsoft.com/.NetConfiguration/v2.0#client
ms.assetid: bf0f7031-76c8-4e7e-a6c6-9ad9119134be
ms.openlocfilehash: 7aa3755be97a839cb576d53852b75cfe50e39276
ms.sourcegitcommit: 559259da2738a7b33a46c0130e51d336091c2097
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/22/2019
ms.locfileid: "72773944"
---
# <a name="client"></a>\<client >
Element `client` definiuje listę punktów końcowych, z którymi klient może się połączyć.

[ **\<configuration >** ](../configuration-element.md) \
&nbsp; &nbsp;[ **\<system. serviceModel >** ](system-servicemodel.md) \
&nbsp; &nbsp; &nbsp; &nbsp; **\<client >**

## <a name="syntax"></a>Składnia

```xml
<system.serviceModel>
  <client>
    <endpoint>
    </endpoint>
    <metadata>
    </metadata>
  </client>
</system.serviceModel>
```

## <a name="attributes-and-elements"></a>Atrybuty i elementy
 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.

### <a name="attributes"></a>Atrybuty
 Brak

### <a name="child-elements"></a>Elementy podrzędne

|Element|Opis|
|-------------|-----------------|
|[\<endpoint >](endpoint-of-client.md)|Zawiera kolekcję elementów punktu końcowego, które określają punkty końcowe, z którymi ten klient może się połączyć.|
|[\<metadata >](metadata.md)|Zawiera ustawienia dotyczące przetwarzania metadanych.|

### <a name="parent-elements"></a>Elementy nadrzędne

|Element|Opis|
|-------------|-----------------|
|[\<system. serviceModel >](system-servicemodel.md)|Element główny wszystkich elementów konfiguracji Windows Communication Foundation (WCF).|

## <a name="remarks"></a>Uwagi
 Sekcja `client` definiuje listę punktów końcowych, z którymi klient może się połączyć. Każdy punkt końcowy wymieniony w sekcji Client definiuje własne powiązanie, zachowanie i kontrakt. Jest on jednoznacznie identyfikowany przez kombinację atrybutów `name` i `contract`. Kod klienta określa `name`, aby połączyć się z punktem końcowym dla usługi implementującej przez klienta. Jeśli atrybut `name` zostanie pominięty, punkt końcowy działa jako domyślny punkt końcowy dla wdrażanego kontraktu.

 Ponadto ta sekcja określa również ustawienia przetwarzania metadanych.

## <a name="example"></a>Przykład

```xml
<client>
  <endpoint address="/HelloWorld/"
            bindingConfiguration="usingDefaults"
            name="MyBinding"
            binding="customBinding"
            contract="HelloWorld">
    <addressProperties actingAs="http://www.microsoft.com/TestActor"
                       identityData="BasicReadWrite"
                       identityType="Spn"
                       isAddressPrivate="false">
  </endpoint>
</client>
```

## <a name="see-also"></a>Zobacz także

- <xref:System.ServiceModel.Configuration.ClientSection>
- <xref:System.ServiceModel.Configuration.MetadataElement>
- [Konfiguracja klienta programu WCF](../../../wcf/feature-details/client-configuration.md)
- [Klienci](../../../wcf/feature-details/clients.md)
