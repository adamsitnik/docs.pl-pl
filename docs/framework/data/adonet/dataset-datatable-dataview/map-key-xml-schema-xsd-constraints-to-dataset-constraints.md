---
title: Mapowanie ograniczeń key schematu XML (XSD) na ograniczenia elementu DataSet
ms.date: 03/30/2017
ms.assetid: 22664196-f270-4ebc-a169-70e16a83dfa1
ms.openlocfilehash: 670c07dd83e880b79c1ccf0c5af00d253b83f827
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040078"
---
# <a name="map-key-xml-schema-xsd-constraints-to-dataset-constraints"></a>Mapowanie ograniczeń key schematu XML (XSD) na ograniczenia elementu DataSet
W schemacie można określić ograniczenie klucza dla elementu lub atrybutu przy użyciu elementu **klucza** . Element lub atrybut, w którym określono ograniczenie klucza, muszą mieć unikatowe wartości w dowolnym wystąpieniu schematu i nie może mieć wartości null.  
  
 Ograniczenie klucza jest podobne do ograniczenia UNIQUE, z tą różnicą, że kolumna, w której zdefiniowano ograniczenie klucza nie może mieć wartości null.  
  
 Poniższa tabela zawiera opis atrybutów **msdata** , które można określić w elemencie **Key** .  
  
|Nazwa atrybutu|Opis|  
|--------------------|-----------------|  
|**msdata: ConstraintName**|Jeśli ten atrybut jest określony, jego wartość jest używana jako nazwa ograniczenia. W przeciwnym razie atrybut **name** zawiera wartość nazwy ograniczenia.|  
|**msdata: PrimaryKey**|Jeśli `PrimaryKey="true"` jest obecny, właściwość ograniczenia **IsPrimaryKey** ma wartość **true**, co sprawia, że jest kluczem podstawowym. Właściwość Column **AllowDBNull** ma wartość **false**, ponieważ klucze podstawowe nie mogą mieć wartości null.|  
  
 W przypadku konwertowania schematu, w którym jest określone ograniczenie klucza, proces mapowania tworzy unikatowe ograniczenie dla tabeli z właściwością Column **AllowDBNull** ustawioną na **wartość false** dla każdej kolumny ograniczenia. Właściwość **IsPrimaryKey** ograniczenia UNIQUE jest również ustawiona na **wartość false** , chyba że określono `msdata:PrimaryKey="true"` w elemencie **Key** . Jest to takie samo jak ograniczenie unikatowe w schemacie, w którym `PrimaryKey="true"`.  
  
 W poniższym przykładzie schematu element **klucza** określa ograniczenie klucza elementu **CustomerID** .  
  
```xml  
<xs:schema id="cod"  
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
        <xs:element name="CompanyName" type="xs:string" minOccurs="0" />  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
<xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:key  msdata:PrimaryKey="true"  
       msdata:ConstraintName="KeyCustID"  
          name="KeyConstCustomerID" >  
     <xs:selector xpath=".//Customers" />  
     <xs:field xpath="CustomerID" />  
    </xs:key>  
 </xs:element>  
</xs:schema>   
```  
  
 Element **klucza** określa, że wartości elementu podrzędnego **IDKlienta** elementu **Customers** muszą mieć unikatowe wartości i nie może zawierać wartości null. W przypadku tłumaczenia schematu języka definicji schematu XML (XSD) proces mapowania tworzy poniższą tabelę:  
  
```text  
Customers(CustomerID, CompanyName, Phone)  
```  
  
 Mapowanie schematu XML tworzy również **UniqueConstraint** w kolumnie **IDKlienta** , jak pokazano w poniższym <xref:System.Data.DataSet>. (Dla uproszczenia są wyświetlane tylko odpowiednie właściwości.)  
  
```text  
      DataSetName: MyDataSet  
TableName: customers  
  ColumnName: CustomerID  
      AllowDBNull: False  
      Unique: True  
  ConstraintName: KeyCustID  
      Table: customers  
      Columns: CustomerID   
      IsPrimaryKey: True  
```  
  
 W wygenerowanym **zestawie danych** Właściwość **IsPrimaryKey** **UniqueConstraint** ma **wartość true** , ponieważ schemat określa `msdata:PrimaryKey="true"` w elemencie **Key** .  
  
 Wartość właściwości **ConstraintName** **UniqueConstraint** w **zestawie danych** jest wartością atrybutu **msdata: ConstraintName** określonego w elemencie **Key** w schemacie.  
  
## <a name="see-also"></a>Zobacz także

- [Mapowanie ograniczeń schematu XML (XSD) na ograniczenia elementu DataSet](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [Generowanie relacji elementu DataSet na podstawie schematu XML (XSD)](generating-dataset-relations-from-xml-schema-xsd.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
