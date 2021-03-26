---
title: Interfaces de serviço de linguagem herdada | Microsoft Docs
description: Saiba mais sobre as interfaces disponíveis no SDK do Visual Studio que fornecem recursos de serviço de linguagem herdado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IVsLanguageInfo interface
- language services, objects
ms.assetid: 03b2d507-f463-417e-bc22-bdac68eeda52
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 77647daeae2cf6e3bc76f9b0f2a58608b5bb28a4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074503"
---
# <a name="legacy-language-service-interfaces"></a>Interfaces de serviço de linguagem herdada
Para qualquer linguagem de programação específica, pode haver apenas uma instância de um serviço de linguagem por vez. No entanto, um único serviço de linguagem pode servir mais de um editor.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Não associa um serviço de linguagem a nenhum editor específico. Portanto, ao solicitar uma operação de serviço de idioma, você deve identificar o editor apropriado como um parâmetro.

## <a name="common-interfaces-associated-with-language-services"></a>Interfaces comuns associadas aos serviços de linguagem
 O editor Obtém o serviço de linguagem chamando <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> o VSPackage apropriado. A ID de serviço (SID) passada nesta chamada identifica o serviço de idioma que está sendo solicitado.

 Você pode implementar as interfaces do serviço de idioma principal em qualquer número de classes separadas. No entanto, uma abordagem comum é implementar as seguintes interfaces em uma única classe:

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock> (opcional)

  A <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> interface deve ser implementada em todos os serviços de linguagem. Ele fornece informações sobre o serviço de idioma, como o nome localizado do idioma, as extensões de nome de arquivo associadas ao serviço de linguagem e como recuperar um Colorizer.

## <a name="additional-language-service-interfaces"></a>Interfaces de serviço de idioma adicional
 Outras interfaces podem ser fornecidas com o serviço de idioma. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] solicita uma instância separada dessas interfaces para cada instância do buffer de texto. Portanto, você deve implementar cada uma dessas interfaces em seu próprio objeto. A tabela a seguir mostra as interfaces que exigem uma instância por instância de buffer de texto.

|Interface|Descrição|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|Gerencia adorners de janela de código, como a barra suspensa. Você pode obter essa interface usando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> método. Há uma <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> por janela de código.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|Palavras-chave e delimitadores de idioma colore. Você pode obter essa interface usando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> método. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> é chamado no momento do pintura. Evite o trabalho de computação intensiva dentro <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> ou o desempenho pode ser afetado.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|Fornece dicas de ferramentas de parâmetro IntelliSense. Quando o serviço de linguagem reconhece um caractere que indica que os dados do método devem ser exibidos, como um parêntese de abertura, ele chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> método para notificar a exibição de texto de que o serviço de idioma está pronto para exibir uma dica de ferramenta de informações de parâmetro. Em seguida, a exibição de texto chama o serviço de idioma usando os métodos da <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> interface para obter as informações necessárias para exibir a dica de ferramenta.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|Fornece a conclusão da instrução IntelliSense. Quando o serviço de idioma está pronto para exibir uma lista de conclusão, ele chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> método na exibição de texto. Em seguida, a exibição de texto chama o serviço de idioma usando métodos no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> objeto.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|Permite a modificação da exibição de texto usando o manipulador de comandos. A classe na qual você implementa a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> interface também deve implementar a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. A exibição de texto recupera o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> objeto consultando o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> objeto que é passado para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método. Deve haver um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> objeto para cada exibição.|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|Intercepta comandos que o usuário digita na janela de código. Monitorar a saída de sua <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> implementação para fornecer informações de conclusão personalizadas e exibir a modificação<br /><br /> Para passar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> objeto para a exibição de texto, chame <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> .|

## <a name="see-also"></a>Confira também
- [Desenvolvendo um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)
- [Lista de verificação: Criando um serviço de linguagem herdado](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)
