---
title: Implementando a coloração de sintaxe | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring, implementing
- editors [Visual Studio SDK], colorizing text
- text, colorizing in editors
ms.assetid: 96e762ca-efd0-41e7-8958-fda4897c8c7a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 5502bd30378130e5977d427acb9df5b73226a05b
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31131844"
---
# <a name="implementing-syntax-coloring"></a>Implementando a coloração de sintaxe
Quando o serviço de linguagem fornece coloração de sintaxe, o analisador converte uma linha de texto em uma matriz de itens pode ser coloridos e retorna os tipos de token correspondente a esses itens pode ser coloridos. O analisador deve retornar tipos de token que pertencem a uma lista de itens pode ser coloridos. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Exibe cada item pode ser colorido na janela de código de acordo com os atributos atribuídos pelo objeto colorizador para o tipo de token apropriado.  
  
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] não especifica uma interface, o analisador e implementação de analisador é completamente cabe a você. No entanto, uma implementação de analisador padrão é fornecida no projeto de pacote de idiomas do Visual Studio. Para código gerenciado, a estrutura de pacote gerenciado (MPF) fornece suporte completo para colorir o texto.  
  
 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar a coloração de sintaxe, consulte [passo a passo: texto realçando](../../extensibility/walkthrough-highlighting-text.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API assim que possível. Isso melhorar o desempenho do seu serviço de linguagem e permitem que você aproveite os novos recursos do editor.  
  
## <a name="steps-followed-by-an-editor-to-colorize-text"></a>Etapas seguidas por um Editor para colorir texto  
  
1.  O editor obtém o colorizador chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> método o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> objeto.  
  
2.  As chamadas do editor de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStateMaintenanceFlag%2A> método para determinar se o colorizador precisa ser o estado de cada linha a serem mantidos fora do colorizador.  
  
3.  Se o colorizador requer que o estado seja mantido fora o colorizador, o editor chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStartState%2A> método para obter o estado da primeira linha.  
  
4.  Para cada linha no buffer, o editor chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método, que executa as seguintes etapas:  
  
    1.  A linha de texto é passada para o scanner para converter o texto em tokens. Cada token Especifica o texto do token e o tipo de token.  
  
    2.  O tipo de token é convertido em um índice em uma lista de itens pode ser colorido.  
  
    3.  As informações de token são usadas para preencher uma matriz, de modo que cada elemento da matriz corresponde a um caractere na linha. Os valores armazenados na matriz são os índices para a lista de itens pode ser colorido.  
  
    4.  O estado no final da linha é retornado para cada linha.  
  
5.  Se o colorizador requer que o estado seja mantido, o editor armazena em cache o estado para aquela linha.  
  
6.  O editor processa a linha de texto usando as informações retornadas do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método. Isso exige as seguintes etapas:  
  
    1.  Para cada caractere na linha, obter o índice do item pode ser colorido.  
  
    2.  Se usando os itens de padrão pode ser colorido, acesse a lista de itens pode ser colorido do editor.  
  
    3.  Caso contrário, chamar o serviço de linguagem <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> método para obter um item pode ser colorido.  
  
    4.  Use as informações no item pode ser colorido para processar o texto na exibição.  
  
## <a name="managed-package-framework-colorizer"></a>Pacote gerenciado Framework colorizador  
 A estrutura de pacote gerenciado (MPF) fornece todas as classes que são necessários para implementar um colorizador. A classe de serviço de linguagem deve herdar o <xref:Microsoft.VisualStudio.Package.LanguageService> classe e implemente os métodos necessários. Você deve fornecer um scanner e parser Implementando o <xref:Microsoft.VisualStudio.Package.IScanner> de interface e retornar uma instância da interface do <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método (um dos métodos que devem ser implementados no <xref:Microsoft.VisualStudio.Package.LanguageService> classe). Para obter mais informações, consulte [coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como: usar itens pode ser coloridos internos](../../extensibility/internals/how-to-use-built-in-colorable-items.md)   
 [Itens pode ser coloridos personalizados](../../extensibility/internals/custom-colorable-items.md)   
 [Desenvolver um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)   
 [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)