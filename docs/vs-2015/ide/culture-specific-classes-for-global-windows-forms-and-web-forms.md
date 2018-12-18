---
title: Classes específicas de cultura para Windows Forms e Web Forms globais | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- globalization [Windows Forms], classes
- Web applications [.NET Framework], globalization
- culture, culture-specific classes
- numbers, international
- localization [Windows Forms], classes
- globalization [Visual Studio], culture-specific classes
- Windows Forms, localization
- international applications [Visual Studio], data formats
- time [Visual Studio], international
- dates [Visual Studio], international
- culture
- international characters
- currency formats
- ASP.NET, globalization
- classes [Visual Studio], culture-specific
- localization [Visual Studio], culture-specific classes
ms.assetid: 0d06a0a4-f887-4f7c-bde7-1d543c06f803
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: bbd599864cfd1e5af770ab4305380d10c71b622a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49283279"
---
# <a name="culture-specific-classes-for-global-windows-forms-and-web-forms"></a>Classes específicas de cultura para Windows Forms e Web Forms globais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Cada cultura tem diferentes convenções para exibir datas, hora, números, moeda e outras informações. O namespace <xref:System.Globalization> contém classes que podem ser usadas para modificar o modo como os valores específicos de cultura são exibidos, como <xref:System.Globalization.DateTimeFormatInfo>, **Calendário** e <xref:System.Globalization.NumberFormatInfo>.  
  
## <a name="using-the-culture-setting"></a>Usando a configuração de cultura  
 Mas, na maioria das vezes, você usará a configuração de cultura armazenada no aplicativo ou no painel de controle **Opções Regionais** para determinar automaticamente as convenções no tempo de execução e formatar as informações adequadamente. Para obter mais informações sobre como configurar a cultura, consulte [How to: Set the Culture and UI Culture for Windows Forms Globalization (Como definir a cultura e a cultura da interface do usuário para globalização do Windows Forms)](http://msdn.microsoft.com/en-us/694e049f-0b91-474a-9789-d35124f248f0) ou [How to: Set the Culture and UI Culture for ASP.NET Web Page Globalization (Como definir a cultura e cultura da interface do usuário para globalização de página da Web do ASP.NET)](http://msdn.microsoft.com/library/76091f86-f967-4687-a40f-de87bd8cc9a0). As classes que formatam informações automaticamente de acordo com a configuração de cultura são chamadas classes específicas de cultura. Alguns métodos específicos de cultura são <xref:System.IFormattable.ToString%2A?displayProperty=fullName>, <xref:System.Console.WriteLine%2A?displayProperty=fullName> e <xref:System.String.Format%2A?displayProperty=fullName>. Algumas funções específicas de cultura (na linguagem do Visual Basic) são `MonthName` e `WeekDayName`.  
  
 Por exemplo, o código a seguir mostra como você pode usar o método <xref:System.IFormattable.ToString%2A> para formatar a moeda para a cultura atual:  
  
```vb  
' Put the Imports statements at the beginning of the code module  
Imports System.Threading  
Imports System.Globalization  
' Display a number with the culture-specific currency formatting  
Dim MyInt As Integer = 100  
Console.WriteLine(MyInt.ToString("C", Thread.CurrentThread.CurrentCulture))  
  
```  
  
```csharp  
// Put the using statements at the beginning of the code module  
using System.Threading;  
using System.Globalization;  
// Display a number with the culture-specific currency formatting  
int myInt = 100;  
Console.WriteLine(myInt.ToString("C", Thread.CurrentThread.CurrentCulture));  
```  
  
 Se a cultura for definida como "fr-FR", você verá isto na janela de saída:  
  
 `100,00`  
  
 Se a cultura for definida como "en-US", você verá isto na janela de saída:  
  
 `$100.00`  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.IFormattable.ToString%2A?displayProperty=fullName>   
 <xref:System.Globalization.DateTimeFormatInfo>   
 <xref:System.Globalization.NumberFormatInfo>   
 <xref:System.Globalization.Calendar>   
 <xref:System.Console.WriteLine%2A?displayProperty=fullName>   
 <xref:System.String.Format%2A?displayProperty=fullName>   
 [Globalizando e localizando aplicativos](../ide/globalizing-and-localizing-applications.md)

