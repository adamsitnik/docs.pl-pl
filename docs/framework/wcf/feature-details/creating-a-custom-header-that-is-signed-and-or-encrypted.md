---
title: Tworzenie podpisanego i/lub zaszyfrowanego niestandardowego nagłówka
ms.date: 03/30/2017
ms.assetid: e8668b37-c79f-4714-9de5-afcb88b9ff02
ms.openlocfilehash: d737647f8c0442a3d6fa0d077a1ffe2c251ea043
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/10/2019
ms.locfileid: "70856177"
---
# <a name="creating-a-custom-header-that-is-signed-and-or-encrypted"></a>Tworzenie podpisanego i/lub zaszyfrowanego niestandardowego nagłówka
Podczas wywoływania usługi niezwiązanej z usługą WCF przy użyciu klienta WCF czasami konieczne jest użycie niestandardowych nagłówków protokołu SOAP. W programie WCF występuje błąd kanonizacji, który uniemożliwia tworzenie niestandardowych nagłówków podpisanych i szyfrowanych podczas pracy z usługą nieobsługującą usług WCF. Problem jest spowodowany niepoprawnym kanonizacją domyślnych przestrzeni nazw XML. Jest to problematyczne tylko podczas wywoływania usług innych niż usługi WCF z niestandardowymi nagłówkami, które są podpisane i/lub szyfrowane.  Gdy usługa otrzymuje komunikat zawierający podpisany i/lub zaszyfrowany nagłówek niestandardowy, nie można zweryfikować podpisu. To obejście pozwala uniknąć błędu kanonizacji, umożliwia współdziałanie z usługami nieobsługującymi usług WCF, ale nie uniemożliwia współdziałania z usługami WCF.  
  
## <a name="defining-the-custom-header"></a>Definiowanie niestandardowego nagłówka  
 Niestandardowe nagłówki są definiowane przez zdefiniowanie kontraktu komunikatu i oznaczenie elementów członkowskich, które mają być wysyłane jako nagłówki z <xref:System.ServiceModel.MessageHeaderAttribute> atrybutem. Aby obejść problem z kanonizacją, należy upewnić się, że Serializator XML deklaruje przestrzeń nazw dla niestandardowego nagłówka z prefiksem zamiast deklaracji domyślnej przestrzeni nazw. Poniższy kod pokazuje, jak zdefiniować typ danych, który będzie używany jako nagłówek komunikatu z prawidłową deklaracją przestrzeni nazw.  
  
```csharp
[System.CodeDom.Compiler.GeneratedCodeAttribute("svcutil", "3.0.4506.648")]  
[System.SerializableAttribute()]  
[System.Diagnostics.DebuggerStepThroughAttribute()]  
[System.ComponentModel.DesignerCategoryAttribute("code")]  
[System.Xml.Serialization.XmlTypeAttribute(AnonymousType=true, Namespace="http://www.example.org/getMessage/")]  
public partial class msgHeaderElement  
{  
   // Define the XML namespace and force it to use an ‘h’ prefix  
    [System.Xml.Serialization.XmlNamespaceDeclarations]  
    public System.Xml.Serialization.XmlSerializerNamespaces _xsns = new System.Xml.Serialization.XmlSerializerNamespaces(new System.Xml.XmlQualifiedName[] { new System.Xml.XmlQualifiedName("h", "http://www.example.org/getMessage/") });  
  
    private string msgHeaderInputField;  
  [System.Xml.Serialization.XmlElementAttribute(Form=System.Xml.Schema.XmlSchemaForm.Unqualified, Order=0)]  
    public string msgHeaderInput  
    {  
        get  
        {  
            return this.msgHeaderInputField;  
        }  
        set  
        {  
            this.msgHeaderInputField = value;  
        }  
    }  
}  
```  
  
 Ten kod deklaruje nowy typ o `msgHeaderElement` nazwie, który zostanie Zserializowany za pomocą serializatora XML. Gdy wystąpienie tego typu jest serializowane, zdefiniuje przestrzeń nazw z prefiksem "h", co spowoduje obejście błędu kanonizacji.  Następnie kontrakt wiadomości zdefiniuje wystąpienie `msgHeaderElement` i oznaczy go <xref:System.ServiceModel.MessageHeaderAttribute> atrybutem, jak pokazano w poniższym przykładzie.  
  
```csharp
[MessageContract]  
public  class MyMessageContract  
{  
   // other message contents...  
   [MessageHeader(ProductionLevel=ProtectionLevel.EncryptAndSign)]  
   public msgHeaderElement;  
   // other message contents...  
}  
```  
  
## <a name="see-also"></a>Zobacz także

- [Domyślny kontrakt komunikatów](../../../../docs/framework/wcf/samples/default-message-contract.md)
- [Kontrakty komunikatów](../../../../docs/framework/wcf/samples/message-contracts.md)
- [Używanie kontraktów komunikatu](../../../../docs/framework/wcf/feature-details/using-message-contracts.md)
