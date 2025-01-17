---
title: Atrybuty w formantach formularzy systemu Windows
ms.date: 03/30/2017
helpviewer_keywords:
- attributes [Windows Forms]
- attributes [Windows Forms], data binding properties
- attributes [Windows Forms], control properties
- attributes [Windows Forms], classes
ms.assetid: 2c5640e9-6c6c-49d7-a5e4-a768f6be7853
ms.openlocfilehash: 9dd4c2aabe1517b66d8e499de3cf2671bb94e0d6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2019
ms.locfileid: "61954378"
---
# <a name="attributes-in-windows-forms-controls"></a>Atrybuty w formantach formularzy systemu Windows
.NET Framework oferuje różne atrybuty, które można zastosować do elementów członkowskich niestandardowych kontrolek i składników. Niektóre z tych atrybutów wpływać na zachowania w czasie wykonywania klasy i inne osoby mają wpływ na zachowanie czasu projektowania.  
  
## <a name="attributes-for-control-and-component-properties"></a>Atrybuty kontrolki i właściwości składnika  
 W poniższej tabeli przedstawiono atrybuty, które można zastosować do właściwości lub innych elementów członkowskich niestandardowych kontrolek i składników. Na przykład, który używa wiele z tych atrybutów, zobacz [jak: Stosowanie atrybutów w kontrolkach formularzy Windows Forms](how-to-apply-attributes-in-windows-forms-controls.md).  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|<xref:System.ComponentModel.AmbientValueAttribute>|Określa wartość do przekazania do właściwości, aby spowodować, że właściwości, które można pobrać wartości z innego źródła. Jest to nazywane *otoczenie*.|  
|<xref:System.ComponentModel.BrowsableAttribute>|Określa, czy właściwość lub zdarzenie ma być wyświetlany w **właściwości** okna.|  
|<xref:System.ComponentModel.CategoryAttribute>|Określa nazwę kategorii, w której ma zostać pogrupowana właściwość lub zdarzenie, kiedy jest wyświetlany w <xref:System.Windows.Forms.PropertyGrid> kontrolki jest ustawiona na <xref:System.Windows.Forms.PropertySort.Categorized> trybu.|  
|<xref:System.ComponentModel.DefaultValueAttribute>|Określa domyślną wartość dla właściwości.|  
|<xref:System.ComponentModel.DescriptionAttribute>|Określa opis dla właściwości lub zdarzenia.|  
|<xref:System.ComponentModel.DisplayNameAttribute>|Określa nazwę wyświetlaną dla właściwości, zdarzenia lub `public void` metodę, która nie przyjmuje żadnych argumentów.|  
|<xref:System.ComponentModel.EditorAttribute>|Określa użyć, aby zmienić właściwość w edytorze.|  
|<xref:System.ComponentModel.EditorBrowsableAttribute>|Określa, że właściwość lub metoda jest widoczne w edytorze.|  
|<xref:System.ComponentModel.Design.HelpKeywordAttribute>|Określa kontekst słowo kluczowe dla klasy lub składowej.|  
|<xref:System.ComponentModel.LocalizableAttribute>|Określa, czy właściwość powinien być zlokalizowany.|  
|<xref:System.ComponentModel.PasswordPropertyTextAttribute>|Wskazuje, czy obiekt tekst reprezentujący jest zasłonięte przez znaki, takie jak gwiazdki.|  
|<xref:System.ComponentModel.ReadOnlyAttribute>|Określa, czy właściwość, którą jest powiązany ten atrybut jest tylko do odczytu lub odczytu i zapisu w czasie projektowania.|  
|<xref:System.ComponentModel.RefreshPropertiesAttribute>|Wskazuje, że siatki właściwości, należy odświeżyć po zmianie wartości właściwości skojarzonej.|  
|<xref:System.ComponentModel.TypeConverterAttribute>|Określa, jakiego typu jako konwertera dla obiektu, ten atrybut jest powiązany z.|  
  
## <a name="attributes-for-data-binding-properties"></a>Atrybuty dla właściwości powiązania danych  
 W poniższej tabeli przedstawiono atrybuty, które można zastosować, aby określić, jak Twoje niestandardowe formanty i składniki wchodzić w interakcje przy użyciu powiązania danych.  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|<xref:System.ComponentModel.BindableAttribute>|Określa, czy właściwość jest zwykle używana do powiązania.|  
|<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|Określa źródło danych i właściwości elementu członkowskiego danych dla składnika.|  
|<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|Określa domyślną właściwość powiązania dla składnika.|  
|<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|Określa źródło danych i właściwości elementu członkowskiego danych dla składnika.|  
|<xref:System.ComponentModel.AttributeProviderAttribute>|Włącza atrybutu przekierowania.|  
  
## <a name="attributes-for-classes"></a>Atrybuty klasy  
 W poniższej tabeli przedstawiono atrybuty, które można zastosować, aby określić zachowanie niestandardowe formanty i składniki w czasie projektowania.  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|<xref:System.ComponentModel.DefaultEventAttribute>|Określa domyślne zdarzenie dla składnika.|  
|<xref:System.ComponentModel.DefaultPropertyAttribute>|Określa domyślną właściwość dla składnika.|  
|<xref:System.ComponentModel.DesignerAttribute>|Określa klasę, używaną do zaimplementowania usług pomocy technicznej czasu projektowania dla składnika.|  
|<xref:System.ComponentModel.DesignerCategoryAttribute>|Określa, że Projektant klasy należy do określonej kategorii.|  
|<xref:System.ComponentModel.ToolboxItemAttribute>|Reprezentuje atrybut elementu przybornika.|  
|<xref:System.ComponentModel.ToolboxItemFilterAttribute>|Określa ciąg filtru i typ filtru dla elementu przybornika.|  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Attribute>
- [Instrukcje: Stosowanie atrybutów w kontrolkach formularzy Windows Forms](how-to-apply-attributes-in-windows-forms-controls.md)
- [Rozszerzenie obsługi w czasie projektowania](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))
- [Opracowywanie niestandardowych kontrolek formularzy Windows Forms za pomocą programu .NET Framework](developing-custom-windows-forms-controls.md)
