---
title: Como dar suporte à delineamento em um serviço de linguagem herdado | Microsoft Docs
description: Saiba como fornecer suporte para delineamento, expansão ou regiões diferentes de texto em um serviço de linguagem herdável.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], collapse to definitions command
- language services, supporting Collapse to Definitions command
- hidden text, Collapse to Definitions command
ms.assetid: bb6e74c3-93e4-4ef7-afc7-1c9b342f083b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 028d1a9aae21aae8c6368e4eea3820aabd200be6
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901793"
---
# <a name="how-to-support-outlining-in-a-legacy-language-service"></a>Como dar suporte à delineamento em um serviço de linguagem herdados
A estrutura de estrutura de texto é usada para expandir ou regiões diferentes de texto. A maneira como a delineamento é usada pode ser definida de forma diferente por linguagens diferentes. Para obter mais informações, consulte [Estrutura de tópicos](../../ide/outlining.md).

 Os serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais nova de implementar recursos de serviço de linguagem é usar extensões MEF. Para saber mais sobre a nova maneira de implementar a delineamento, consulte [Passo a passo: Delineando](../../extensibility/walkthrough-outlining.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor assim que possível. Isso melhorará o desempenho do serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

 O exemplo a seguir demonstra como dar suporte a esse comando para seu serviço de linguagem.

## <a name="to-support-outlining"></a>Para dar suporte à delineamento

1. Implemente <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage> em seu objeto de serviço de linguagem.

2. Chame <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> no objeto de sessão delineamento atual para adicionar novas regiões de contorno.

## <a name="robust-programming"></a>Programação robusta
 Quando um usuário seleciona **Collapse To Definitions** no menu **Estrutura de** estrutura de texto, o IDE chama em seu serviço de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage.CollapseToDefinitions%2A> linguagem.

 Quando esse método é chamado, o IDE passa um ponteiro (um ponteiro para um buffer de texto) e um (um ponteiro para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> a sessão delineamento <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession> atual).

 Você pode chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> método para várias regiões de contorno especificando essas regiões no `rgOutlnReg` parâmetro . O `rgOutlnReg` parâmetro é uma estrutura <xref:Microsoft.VisualStudio.TextManager.Interop.NewOutlineRegion> . Esse processo permite especificar características diferentes da região oculta, como se uma região específica é expandida ou recolhido.

> [!NOTE]
> Tenha cuidado ao ocultar caracteres de nova linha. O texto oculto deve se estender do início da primeira linha para o último caractere da última linha em uma seção, deixando o caractere de nova linha final visível.

## <a name="see-also"></a>Confira também
- [Como fornecer suporte a texto oculto em um serviço de linguagem herdados](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)
- [Como fornecer suporte expandido delineamento em um serviço de linguagem herdado](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)
