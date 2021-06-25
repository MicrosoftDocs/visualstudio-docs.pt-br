---
title: Interfaces de serviço de linguagem herd | Microsoft Docs
description: Saiba mais sobre as interfaces disponíveis no SDK Visual Studio que fornecem recursos herdados do serviço de linguagem.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IVsLanguageInfo interface
- language services, objects
ms.assetid: 03b2d507-f463-417e-bc22-bdac68eeda52
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 75697e1d212b24b743fed62284b384985749fe7b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898598"
---
# <a name="legacy-language-service-interfaces"></a>Interfaces de serviço de linguagem herdada
Para qualquer linguagem de programação específica, pode haver apenas uma instância de um serviço de linguagem por vez. No entanto, um único serviço de linguagem pode atender a mais de um editor.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] não associa um serviço de linguagem a nenhum editor específico. Portanto, ao solicitar uma operação de serviço de linguagem, você deve identificar o editor apropriado como um parâmetro.

## <a name="common-interfaces-associated-with-language-services"></a>Interfaces comuns associadas aos Serviços de Linguagem
 O editor obtém seu serviço de linguagem chamando <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> no VSPackage apropriado. A SID (ID de serviço) passada nessa chamada identifica o serviço de linguagem que está sendo solicitado.

 Você pode implementar as interfaces de serviço de linguagem principal em qualquer número de classes separadas. No entanto, uma abordagem comum é implementar as seguintes interfaces em uma única classe:

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>

- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock> (opcional)

  A <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> interface deve ser implementada em todos os serviços de linguagem. Ele fornece informações sobre seu serviço de linguagem, como o nome localizado do idioma, as extensões de nome de arquivo associadas ao serviço de linguagem e como recuperar um colorizador.

## <a name="additional-language-service-interfaces"></a>Interfaces adicionais do serviço de linguagem
 Outras interfaces podem ser fornecidas com seu serviço de linguagem. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] solicita uma instância separada dessas interfaces para cada instância do buffer de texto. Portanto, você deve implementar cada uma dessas interfaces em seu próprio objeto. A tabela a seguir mostra interfaces que exigem uma instância por instância de buffer de texto.

|Interface|Descrição|
|---------------|-----------------|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|Gerencia adornos de janela de código, como a barra listada. Você pode obter essa interface usando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> método . Há um por <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> janela de código.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|Colore palavras-chave de linguagem e delimitadores. Você pode obter essa interface usando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> método . <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> é chamado no momento da pintura. Evite o trabalho com uso intensivo de computação <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> dentro ou o desempenho possa ser prejudicado.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|Fornece dicas de ferramenta de parâmetro do IntelliSense. Quando o serviço de linguagem reconhece um caractere que indica que os dados do método devem ser exibidos, como um parêntese aberto, ele chama o método para notificar a exibição de texto de que o serviço de linguagem está pronto para exibir uma Dica de Ferramenta de Informações de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> Parâmetro. Em seguida, a exibição de texto chama de volta para o serviço de linguagem usando os métodos da interface para obter as informações necessárias <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> para exibir a dica de ferramenta.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|Fornece a conclusão da instrução IntelliSense. Quando o serviço de idioma estiver pronto para exibir uma lista de conclusão, ele chamará <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> o método na exibição de texto. Em seguida, a exibição de texto chama de volta para o serviço de linguagem usando métodos no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> objeto .|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|Permite a modificação da exibição de texto usando o manipulador de comandos. A classe na qual você implementa a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> interface também deve implementar a interface <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> . A exibição de texto recupera <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> o objeto consultando o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> objeto que é passado para o método <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> . Deve haver um objeto <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> para cada exibição.|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|Intercepta comandos que o usuário digita na janela de código. Monitorar a saída de sua <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> implementação para fornecer informações de conclusão personalizadas e exibir modificação<br /><br /> Para passar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> objeto para a exibição de texto, chame <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> .|

## <a name="see-also"></a>Confira também
- [Desenvolvendo um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)
- [Lista de verificação: Criando um serviço de linguagem herdado](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)
