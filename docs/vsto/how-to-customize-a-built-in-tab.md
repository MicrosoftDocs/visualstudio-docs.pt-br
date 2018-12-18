---
title: 'Como: personalizar uma guia interna'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
- built-in tabs [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 30b4af116df218f3f778b9efa1e295fbadbad86a
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35257261"
---
# <a name="how-to-customize-a-built-in-tab"></a>Como: personalizar uma guia interna
  Você pode adicionar grupos e controles a uma guia interna. Uma guia interna é uma guia que já está na faixa de opções de um aplicativo do Microsoft Office. Por exemplo, o **dados** guia é uma guia interna no Excel. Quando você cria um grupo personalizado, ele é exibido por último na guia, mas você pode mover seu grupo de qualquer lugar na guia.  
  
 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  
  
> [!NOTE]  
>  Você pode adicionar grupos a uma guia interna, mas você não pode remover grupos internos de uma guia interna.  
  
### <a name="to-add-groups-to-a-built-in-tab"></a>Para adicionar grupos a uma guia interna  
  
1.  O arquivo de código da faixa de opções no botão direito do mouse **Gerenciador de soluções**e, em seguida, clique em **View Designer**.  
  
    > [!NOTE]  
    >  Se o arquivo de código da faixa de opções não aparecer na **Gerenciador de soluções**, você deve adicionar uma **item da faixa de opções** ao seu projeto. Ver [como: Introdução à personalização da faixa de opções](../vsto/how-to-get-started-customizing-the-ribbon.md).  
  
2.  Qualquer guia no designer de faixa de opções com o botão direito e, em seguida, clique em **propriedades**.  
  
3.  No **propriedades** janela, expanda o **ControlId** propriedade e, em seguida, defina a **ControlIdType** propriedade **Office**.  
  
4.  Defina as **OfficeId** propriedade para o *identificação de controle* da guia interna que você deseja personalizar.  
  
     A ID do controle é o nome que identifica exclusivamente a guias, grupos e controles que são criados em aplicativos do Microsoft Office.  
  
     Para obter uma lista de IDs de controle, consulte [arquivos de Ajuda do Office 2010: identificadores de controle de interface de usuário fluent do Office](http://go.microsoft.com/fwlink/?LinkID=181052).  
  
5.  Dos **controles de faixa de opções do Office** guia da **caixa de ferramentas**, arraste os grupos para a guia.  
  
    > [!NOTE]  
    >  Grupos internos não aparecem no designer. Portanto, a única maneira de determinar se você estiver trabalhando com uma guia interna é examinar o **ControlId** propriedade da guia.  
  
### <a name="to-position-groups-on-a-built-in-tab"></a>Para posicionar os grupos em uma guia interna  
  
1.  No Designer de faixa de opções, selecione um grupo personalizado.  
  
2.  No **propriedades** janela, expanda o **posição** propriedade.  
  
3.  Defina as **PositionType** propriedade para o valor apropriado:  
  
    -   **BeforeOfficeId** posiciona o grupo antes de um grupo interno especificado.  
  
    -   **AfterOfficeId** posiciona o grupo depois de um grupo interno especificado.  
  
4.  Defina as **OfficeId** propriedade para a ID do controle de um grupo interno.  
  
     Para obter uma lista de IDs de controle, consulte [arquivos de Ajuda do Office 2010: identificadores de controle de interface de usuário fluent do Office](http://go.microsoft.com/fwlink/?LinkID=181052).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [Designer de faixa de opções](../vsto/ribbon-designer.md)   
 [XML da faixa de opções](../vsto/ribbon-xml.md)   
 [Passo a passo: Criar uma guia personalizada usando o Designer de faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)   
 [Passo a passo: Criar uma guia personalizada usando o XML da faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)   
 [Como: Introdução à personalização da faixa de opções](../vsto/how-to-get-started-customizing-the-ribbon.md)   
 [Como: alterar a posição de uma guia na faixa de opções](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)   
 [Como: adicionar controles ao modo de exibição Backstage](../vsto/how-to-add-controls-to-the-backstage-view.md)   
 [Como: Add-in de mostrar erros de interface do usuário](../vsto/how-to-show-add-in-user-interface-errors.md)  
  
  