---
title: 'Como: alterar a posição de uma guia na faixa de opções'
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 08bbdf81023be466d30e49215fc0dbe1d3812f20
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35255383"
---
# <a name="how-to-change-the-position-of-a-tab-on-the-ribbon"></a>Como: alterar a posição de uma guia na faixa de opções
  Você pode alterar a ordem das guias personalizadas em uma faixa de opções usando o **guia Editor de coleção**. Você pode posicionar guias personalizadas antes ou depois de uma guia interna na faixa de opções. Uma guia interna é uma guia que já está na faixa de opções de um aplicativo do Microsoft Office. Por exemplo, o **dados** guia é uma guia interna no Excel.  
  
 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  
  
### <a name="to-change-the-order-of-tabs-on-the-ribbon"></a>Para alterar a ordem das guias na faixa de opções  
  
1.  Selecione o arquivo de código da faixa de opções (*. vb* ou *. CS* arquivo) em **Gerenciador de soluções**.  
  
2.  Sobre o **modo de exibição** menu, clique em **Designer**.  
  
3.  O Designer de faixa de opções com o botão direito e, em seguida, clique em **propriedades**.  
  
4.  No **propriedades** janela, selecione a **guias** propriedade e, em seguida, clique no botão de reticências (![elipse de designer móvel ASP.NET](../sharepoint/media/mwellipsis.gif "ASP.NET para dispositivos móveis Elipse de Designer")).  
  
     O **guia Editor de coleção** é exibida.  
  
5.  No **guia Editor de coleção**, no **membros** lista, selecione a guia que você deseja mover e clique em cima ou para baixo as setas para alterar a ordem de tabulação.  
  
### <a name="to-position-a-tab-before-or-after-a-built-in-tab-on-the-ribbon"></a>Para posicionar uma guia antes ou depois de uma guia interna na faixa de opções  
  
1.  No Designer de faixa de opções, selecione uma guia personalizada.  
  
2.  No **propriedades** janela, expanda o **ControlId** propriedade e, em seguida, certifique-se de que o valor da **ControlIdType** propriedade é definida como **personalizado**.  
  
3.  No **propriedades** janela, expanda o **posição** propriedade.  
  
4.  Defina as **PositionType** propriedade para o valor apropriado:  
  
    -   **BeforeOfficeId** posiciona o grupo antes de uma guia interna especificada.  
  
    -   **AfterOfficeId** posiciona o grupo depois de uma guia interna especificada.  
  
5.  Defina as **OfficeId** propriedade para a ID de controle de uma guia interna.  
  
     Para obter uma lista de IDs de controle, consulte [arquivos de Ajuda do Office 2010: identificadores de controle de interface de usuário fluent do Office](http://go.microsoft.com/fwlink/?LinkID=181052).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [Designer de faixa de opções](../vsto/ribbon-designer.md)   
 [XML da faixa de opções](../vsto/ribbon-xml.md)   
 [Passo a passo: Criar uma guia personalizada usando o Designer de faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)   
 [Passo a passo: Criar uma guia personalizada usando o XML da faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)  
  
  