---
title: 'Como: impedir que o Outlook exiba uma região de formulário'
description: Saiba como você pode impedir Microsoft Office Outlook exiba uma região de formulário para um item específico.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], canceling display
- canceling form region display
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f6e6b00e8e26d261aac18dd48af1d912bd6ffad1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899543"
---
# <a name="how-to-prevent-outlook-from-displaying-a-form-region"></a>Como: impedir que o Outlook exiba uma região de formulário
  Pode haver situações em que você não deseja Microsoft Office o Outlook exiba uma região de formulário para um determinado item. Por exemplo, se um item de contato não contiver um endereço comercial, você poderá impedir que uma região de formulário que mostra o local da empresa em um mapa apareça.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="to-prevent-outlook-from-displaying-a-form-region"></a>Para impedir que o Outlook exiba uma região de formulário

1. Abra o arquivo de código para a região de formulário que você deseja modificar.

2. Expanda o formulário região de código de **fábrica** .

3. Adicione código ao `FormRegionInitializing` manipulador de eventos que define a <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> propriedade da <xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs> classe como **true**.

   Neste exemplo, se o item de contato não contiver um endereço, a <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> propriedade será definida como **true** e a região do formulário não será exibida.

## <a name="example"></a>Exemplo
 [!code-csharp[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#1)]
 [!code-vb[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#1)]

## <a name="see-also"></a>Confira também
- [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)
- [Walkthrough: criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [Como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [Walkthrough: criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [Walkthrough: importar uma região de formulário projetada no Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
