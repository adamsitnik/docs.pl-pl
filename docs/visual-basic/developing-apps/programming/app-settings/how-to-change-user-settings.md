---
title: 'Instrukcje: Zmień ustawienia użytkownika w Visual Basic'
ms.date: 07/20/2015
helpviewer_keywords:
- user settings [Visual Basic], changing in Visual Basic
- user settings
- My.Settings object [Visual Basic], changing user settings
- examples [Visual Basic], changing user settings
ms.assetid: 41250181-c594-4854-9988-8183b9eb03cf
ms.openlocfilehash: 553ebc5b0d6381f56783df8be83344f96a21dd8e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968405"
---
# <a name="how-to-change-user-settings-in-visual-basic"></a>Instrukcje: Zmień ustawienia użytkownika w Visual Basic
Ustawienie użytkownika można zmienić, przypisując nową wartość do właściwości ustawienia w `My.Settings` obiekcie.  
  
 `My.Settings` Obiekt uwidacznia każde ustawienie jako właściwość. Nazwa właściwości jest taka sama jak nazwa ustawienia, a typ właściwości jest taki sam jak typ ustawienia. **Zakres** ustawienia określa, czy właściwość jest tylko do odczytu: Właściwość dla ustawienia zakresu **aplikacji**jest tylko do odczytu, podczas gdy właściwość dla ustawienia zakresu **użytkownika**ma wartość odczyt i zapis. Aby uzyskać więcej informacji, zobacz [My. Settings Object](../../../../visual-basic/language-reference/objects/my-settings-object.md).  
  
> [!NOTE]
> Chociaż można zmienić i zapisać wartości ustawień zakresu użytkownika w czasie wykonywania, ustawienia zakresu aplikacji są tylko do odczytu i nie można ich programowo zmienić. Ustawienia zakresu aplikacji można zmienić podczas tworzenia aplikacji za pomocą **projektanta projektu** lub edytując plik konfiguracyjny aplikacji. Aby uzyskać więcej informacji, zobacz [Zarządzanie ustawieniami aplikacji (.NET)](/visualstudio/ide/managing-application-settings-dotnet).  
  
## <a name="example"></a>Przykład  
 Ten przykład zmienia wartość `Nickname` ustawienia użytkownika.  
  
 [!code-vb[VbVbalrMyResources#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#7)]  
  
 Aby ten przykład działał, aplikacja musi mieć `Nickname` ustawienie użytkownika o typie. `String`  
  
 Aplikacja zapisuje ustawienia użytkownika po zamknięciu aplikacji. Aby natychmiast zapisać ustawienia, wywołaj `My.Settings.Save` metodę. Aby uzyskać więcej informacji, zobacz [jak: Utrwalaj ustawienia użytkownika w](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)Visual Basic.  
  
## <a name="see-also"></a>Zobacz także

- [My.Settings, obiekt](../../../../visual-basic/language-reference/objects/my-settings-object.md)
- [Instrukcje: Odczytaj ustawienia aplikacji w Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)
- [Instrukcje: Utrwalanie ustawień użytkownika w Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)
- [Instrukcje: Tworzenie siatek właściwości dla ustawień użytkownika w Visual Basic](../../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)
- [Zarządzanie ustawieniami aplikacji (.NET)](/visualstudio/ide/managing-application-settings-dotnet)
