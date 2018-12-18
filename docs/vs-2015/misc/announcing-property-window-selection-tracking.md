---
title: Anunciando o acompanhamento de seleção de janela de propriedade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], property pages support
- property pages, tracking selection
- Properties window, tracking selection
- selection, tracking
- editors [Visual Studio SDK], Properties window support
ms.assetid: a7536f82-afd7-4894-9a60-84307fb92b7e
caps.latest.revision: 13
manager: douge
ms.openlocfilehash: 9639e0347689fc99e0b43c4b69394b522af984da
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49246734"
---
# <a name="announcing-property-window-selection-tracking"></a>Anunciando a seleção da janela de propriedades de controle
Se você quiser trabalhar com o **propriedades** janela ou o **propriedade** páginas, por exemplo, um formulário, texto ou uma seleção para o qual você deseja ver as propriedades, em seguida, você deve ter um conhecimento completo de como você Coordene a seleção. Por exemplo, você deve saber se você tem uma seleção única ou várias seleções. Em seguida, você precisa anunciar seu tipo de seleção (um ou vários) no IDE usando o <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> interface. Essa interface fornece informações necessárias para o **propriedades** janela.  
  
### <a name="to-announce-selection-to-the-environment"></a>Anunciar a seleção para o ambiente  
  
1.  Chame `QueryInterface` para <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>.  
  
    1.  Para fazer isso, use o ponteiro do site passado para o modo de exibição quando ela foi criada.  
  
    2.  Chame `QueryService` do modo de exibição para o `SID_STrackSelection` service.  
  
         Isso retorna um ponteiro para <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>.  
  
2.  Chame o <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> método sempre que for alterado sua seleção e passe um ponteiro para um objeto que implementa <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>.  
  
     O objeto de contêiner de seleção pode usar única ou várias seleções e contém as informações de seleção em um `IDispatch` objeto. Chamar o <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> método notifica o **propriedades** janela que a seleção é alterada. O **propriedades** janela, em seguida, usa os objetos no <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> para determinar se ocorreram única ou várias seleções, e quais são as seleções do objeto real.  
  
     Se você especificar uma seleção múltipla, em seguida, a **propriedades** janela localiza a interseção entre propriedades comuns para os objetos. Se você especificar a seleção de um único objeto, em seguida, a **propriedades** janela exibe todas as propriedades de um objeto.  
  
## <a name="see-also"></a>Consulte também  
 [Estendendo propriedades](../extensibility/internals/extending-properties.md)   
 [Páginas de propriedade](../extensibility/internals/property-pages.md)