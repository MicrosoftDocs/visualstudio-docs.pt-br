---
title: 'Como: evitar que o Outlook exiba uma região de formulário'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], canceling display
- canceling form region display
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 1ec9f45b2055a7a56e067440d216482877da14c2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949052"
---
# <a name="how-to-prevent-outlook-from-displaying-a-form-region"></a>Como: evitar que o Outlook exiba uma região de formulário
  Pode haver situações em que você quer que o Microsoft Office Outlook para exibir uma região de formulário para um determinado item. Por exemplo, se um item de contato não contiver um endereço comercial, você pode impedir que uma região de formulário que mostra o local da empresa em um mapa apareça.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
## <a name="to-prevent-outlook-from-displaying-a-form-region"></a>Para impedir que o Outlook exiba uma região de formulário  
  
1. Abra o arquivo de código para a região do formulário que você deseja modificar.  
  
2. Expanda o **fábrica de região de formulário** região de código.  
  
3. Adicione código para o `FormRegionInitializing` manipulador de eventos que define o <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> propriedade da <xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs> classe para **true**.  
  
   Neste exemplo, se o item de contato não contiver um endereço, o <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> estiver definida como **verdadeiro**, e a região do formulário não é exibida.  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#1)]
 [!code-vb[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#1)]  
  
## <a name="see-also"></a>Consulte também  
 [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)   
 [Passo a passo: Criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)   
 [Como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)   
 [Passo a passo: Criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)   
 [Passo a passo: Importar de uma região de formulário projetada no Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)  
  
  