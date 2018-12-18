---
title: Implementando a coloração de sintaxe | Microsoft Docs
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
- syntax coloring, implementing
- editors [Visual Studio SDK], colorizing text
- text, colorizing in editors
ms.assetid: 96e762ca-efd0-41e7-8958-fda4897c8c7a
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 30a53b1fc04bd08835ccf0ff0b0edb2e5d117fcb
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51775024"
---
# <a name="implementing-syntax-coloring"></a>Implementando a coloração de sintaxe
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Quando o serviço de linguagem fornece colorização de sintaxe, o analisador converte uma linha de texto em uma matriz de itens de coloração e retorna os tipos de token correspondente a esse itens de coloração. O analisador deve retornar tipos de token que pertencem a uma lista de itens de coloração. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Exibe cada item que pode ser colorido na janela de código de acordo com os atributos atribuídos pelo objeto colorizador para o tipo de token apropriado.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] não especifica uma interface de analisador, e a implementação do analisador cabe completamente a você. No entanto, uma implementação de analisador padrão é fornecida no projeto do pacote de idiomas do Visual Studio. Para código gerenciado, a estrutura de pacote gerenciado (MPF) fornece suporte completo para colorir texto.  
  
 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar a coloração de sintaxe, consulte [instruções passo a passo: realçar texto](../../extensibility/walkthrough-highlighting-text.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  
  
## <a name="steps-followed-by-an-editor-to-colorize-text"></a>Etapas seguidas por um Editor para colorir o texto  
  
1.  O editor obtém o colorizador chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> objeto.  
  
2.  As chamadas do editor o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStateMaintenanceFlag%2A> método para determinar se o colorizador precisa o estado de cada linha a ser mantida fora o colorizador.  
  
3.  Se o colorizador requer que o estado seja mantido fora o colorizador, o editor chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStartState%2A> método para obter o estado da primeira linha.  
  
4.  Para cada linha no buffer, o editor chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método, que executa as seguintes etapas:  
  
    1.  A linha de texto é passada para um scanner para converter o texto em tokens. Cada token Especifica o texto do token e o tipo de token.  
  
    2.  O tipo de token é convertido em um índice em uma lista de itens de coloração.  
  
    3.  As informações de token são usadas para preencher uma matriz, de modo que cada elemento da matriz corresponde a um caractere na linha. Os valores armazenados na matriz são os índices para a lista de itens de coloração.  
  
    4.  O estado no final da linha é retornado para cada linha.  
  
5.  Se o colorizador requer que o estado seja mantido, o editor armazena em cache o estado para essa linha.  
  
6.  O editor processa a linha de texto usando as informações retornadas a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método. Isso exige as seguintes etapas:  
  
    1.  Para cada caractere na linha, obter o índice do item que pode ser colorido.  
  
    2.  Se usando os itens de coloração padrão, acesse a lista de itens de coloração do editor.  
  
    3.  Caso contrário, chame o serviço de linguagem <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> método para obter um item que pode ser colorido.  
  
    4.  Use as informações no item que pode ser colorido para renderizar o texto para a exibição.  
  
## <a name="managed-package-framework-colorizer"></a>Colorizador de estrutura de pacote gerenciado  
 A estrutura de pacote gerenciado (MPF) fornece todas as classes que são necessários para implementar um colorizador. Sua classe de serviço de linguagem deve herdar o <xref:Microsoft.VisualStudio.Package.LanguageService> de classe e implementar os métodos necessários. Você deve fornecer um analisador e scanner, Implementando a <xref:Microsoft.VisualStudio.Package.IScanner> interface e retornar uma instância dessa interface do <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método (um dos métodos que devem ser implementados no <xref:Microsoft.VisualStudio.Package.LanguageService> classe). Para obter mais informações, consulte [coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como: usar itens de coloração internos](../../extensibility/internals/how-to-use-built-in-colorable-items.md)   
 [Itens de coloração personalizados](../../extensibility/internals/custom-colorable-items.md)   
 [Desenvolver um serviço de linguagem herdado](../../extensibility/internals/developing-a-legacy-language-service.md)   
 [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

