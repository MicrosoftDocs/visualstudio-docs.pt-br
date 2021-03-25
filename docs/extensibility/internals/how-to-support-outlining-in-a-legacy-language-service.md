---
title: 'Como: dar suporte à estrutura de tópicos em um serviço de linguagem herdada | Microsoft Docs'
description: Saiba como fornecer suporte para estrutura de tópicos, expansão ou recolhimento de diferentes regiões de texto em um serviço de linguagem herdado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 0c275a6a466cc58187293f6ebd84a39fdf8064e6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078679"
---
# <a name="how-to-support-outlining-in-a-legacy-language-service"></a>Como: dar suporte à estrutura de tópicos em um serviço de linguagem herdada
A estrutura de tópicos é usada para expandir ou recolher diferentes regiões de texto. A maneira como a estrutura de tópicos é usada pode ser definida de forma diferente por idiomas diferentes. Para obter mais informações, consulte [Estrutura de tópicos](../../ide/outlining.md).

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para obter mais informações sobre a nova maneira de implementar a estrutura de tópicos, consulte [Walkthrough: contorno](../../extensibility/walkthrough-outlining.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

 O seguinte demonstra como dar suporte a esse comando para seu serviço de idioma.

## <a name="to-support-outlining"></a>Para dar suporte à estrutura de tópicos

1. Implemente <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage> em seu objeto de serviço de idioma.

2. Chame <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> no objeto de sessão de estrutura de tópicos atual para adicionar novas regiões de estrutura de tópicos.

## <a name="robust-programming"></a>Programação robusta
 Quando um usuário seleciona **recolher em definições** no menu de **estrutura de tópicos** , o IDE chama o serviço de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningCapableLanguage.CollapseToDefinitions%2A> idioma.

 Quando esse método é chamado, o IDE passa um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> ponteiro (um ponteiro para um buffer de texto) e um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession> (um ponteiro para a sessão de estrutura de tópicos atual).

 Você pode chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsOutliningSession.AddOutlineRegions%2A> método para várias regiões de estrutura de tópicos especificando essas regiões no `rgOutlnReg` parâmetro. O `rgOutlnReg` parâmetro é uma <xref:Microsoft.VisualStudio.TextManager.Interop.NewOutlineRegion> estrutura. Esse processo permite especificar diferentes características da região oculta, como se uma região específica é expandida ou recolhida.

> [!NOTE]
> Tenha cuidado ao ocultar caracteres de nova linha. O texto oculto deve se estender do início da primeira linha até o último caractere da última linha em uma seção, deixando o caractere de nova linha final visível.

## <a name="see-also"></a>Confira também
- [Como fornecer suporte a texto oculto em um serviço de idioma herdado](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)
- [Como fornecer suporte expandido para estrutura de tópicos em um serviço de linguagem herdado](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)
