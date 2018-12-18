---
title: Contido idiomas | Microsoft Docs
ms.date: 03/22/2018
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - contained languages
ms.assetid: b75bbb51-8e42-41b1-bece-09ab0b1f03cc
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9edaed1eef81d493bdd29311893caef93447e6f7
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39231738"
---
# <a name="contained-languages"></a>Idiomas independentes

*Contido idiomas* são linguagens que são contidas por outras linguagens. Por exemplo, o HTML no [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] páginas podem conter [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ou [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] scripts. Uma arquitetura de linguagem dual é necessária para o *. aspx* recursos do editor de arquivo para fornecer IntelliSense, colorização e outros recursos de edição para o HTML e a linguagem de script.

## <a name="implementation"></a>Implementação

A interface mais importante que você precisa implementar para idiomas independentes é a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> interface. Essa interface é implementada por qualquer linguagem que pode ser hospedada em um idioma principal. Ele fornece acesso para o serviço de linguagem colorizador, filtro de exibição de texto e ID de serviço de idioma primário. O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory> permite que você crie um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> interface. As etapas a seguir mostram como implementar uma linguagem independente:

1.  Use `QueryService()` para obter o idioma, ID de serviço e a ID de interface da <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory>.

2.  Para criar uma <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> interface, chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguageFactory.GetLanguage%2A> método. Passar uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> interface, um ou mais [IDs de item](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID>)e um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator> interface.

3.  O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator> interface, que é o objeto de coordenador de buffer de texto, fornece os serviços básicos que são necessárias para mapear os locais em um arquivo primário no buffer do idioma secundário.

     Por exemplo, em uma única *. aspx* arquivo, o arquivo primário inclui o ASP, HTML e todo o código que está contido. No entanto, o buffer secundário inclui apenas o código contido junto com quaisquer definições de classe, para tornar o buffer secundário de um arquivo de código válido. O coordenador de buffer manipula o trabalho de coordenação de edições de um buffer para outro.

4.  O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.SetSpanMappings%2A> método, que é o idioma principal, informa o coordenador de buffer que texto dentro de seu buffer é mapeado para o texto correspondente em um buffer secundário.

     A linguagem passa uma matriz do <xref:Microsoft.VisualStudio.TextManager.Interop.NewSpanMapping> estrutura, que atualmente inclui apenas um primário e um secundário span.

5.  O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.MapPrimaryToSecondarySpan%2A> método e o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.MapSecondaryToPrimarySpan%2A> método fornece o mapeamento do primário para um buffer secundário e vice-versa.