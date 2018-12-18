---
title: 'Como: dar suporte a estrutura de tópicos em um serviço de linguagem herdado | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], collapse to definitions command
- language services, supporting Collapse to Definitions command
- hidden text, Collapse to Definitions command
ms.assetid: bb6e74c3-93e4-4ef7-afc7-1c9b342f083b
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: fb596c8fbc7ab3c354b5b8d3e2a116ee752f06a4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51724123"
---
# <a name="how-to-support-outlining-in-a-legacy-language-service"></a>Como: dar suporte a estrutura de tópicos em um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Estrutura de tópicos é usada para expandir ou recolher a diferentes regiões do texto. A forma de estrutura de tópicos é usada pode ser definido de forma diferente por diferentes idiomas. Para obter mais informações, consulte [Estrutura de tópicos](../../ide/outlining.md).  
  
 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar a estrutura de tópicos, consulte [instruções passo a passo: estrutura de tópicos](../../extensibility/walkthrough-outlining.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  
  
 O exemplo a seguir demonstra como dar suporte a esse comando para seu serviço de linguagem.  
  
### <a name="to-support-outlining"></a>Para dar suporte à estrutura de tópicos  
  
1.  Implementar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage> em seu objeto de serviço de linguagem.  
  
2.  Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> no objeto de sessão de estrutura de tópicos atual para adicionar novas regiões de estrutura de tópicos.  
  
## <a name="robust-programming"></a>Programação robusta  
 Quando um usuário seleciona **recolher para definições** sobre o **estrutura de tópicos** menu, as chamadas IDE <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage.CollapseToDefinitions%2A> no seu serviço de linguagem.  
  
 Quando este método é chamado, o IDE passa em uma <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> ponteiro (um ponteiro para um buffer de texto) e um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession> (um ponteiro para a sessão de estrutura de tópicos atual).  
  
 Você pode chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> método para várias regiões de estrutura de tópicos, especificando essas regiões no `rgOutlnReg` parâmetro. O `rgOutlnReg` parâmetro é um <xref:Microsoft.VisualStudio.TextManager.Interop.NewOutlineRegion> estrutura. Esse processo permite que você especifique diferentes características da região oculta, como se uma região específica é expandida ou recolhida.  
  
> [!NOTE]
>  Tenha cuidado sobre a ocultação de caracteres de nova linha. Texto oculto deve estender desde o início da primeira linha até o último caractere da última linha em uma seção, deixando o caractere de nova linha final visível.  
  
## <a name="see-also"></a>Consulte também  
 [Como: fornecer suporte a texto oculto em um serviço de linguagem herdado](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)   
 [Como fornecer suporte estendido à estrutura de tópicos em um serviço de linguagem herdado](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

