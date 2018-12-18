---
title: Fundamentos do serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- languages, integrating into Visual Studio
- language services, integrating programming languages
- Visual Studio, integrating programming languages
- programming languages, integrating into Visual Studio
ms.assetid: c15e0ccb-e7c5-4dbb-affb-fe3d3244debe
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 344a7949c5058237d8599d69ea3b234e9a6e8e72
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49850159"
---
# <a name="legacy-language-service-essentials"></a>Conceitos básicos do serviço de linguagem herdado
Você deve fornecer um serviço de linguagem para integrar uma linguagem de programação no Visual Studio. Este tópico explica os recursos disponíveis nos serviços de linguagem herdada.  

 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações sobre a nova maneira de implementar um serviço de linguagem, consulte [Editor e extensões do serviço de linguagem](../../extensibility/editor-and-language-service-extensions.md).  

> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  

 Serviços de linguagem herdado fornecem os seguintes recursos:  

|Recurso|Descrição|  
|-------------|-----------------|  
|Coloração de sintaxe|Faz com que a exibição do editor exibir cores diferentes e estilos de fonte para os diferentes elementos de um idioma. Essa diferenciação pode tornar mais fácil de ler e editar arquivos.<br /><br /> Para obter informações gerais, consulte [coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md).<br /><br /> Para obter informações sobre esse recurso na estrutura de pacote gerenciado (MPF), consulte [coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md).|  
|Conclusão da instrução|Conclui uma instrução ou palavra-chave que o usuário começa a digitar. Preenchimento de declaração ajuda os usuários a inserir instruções difícil mais facilmente, com menos digitação e menos chances para erro.<br /><br /> Para obter informações gerais, consulte [preenchimento de declaração em um serviço de linguagem herdado](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md).<br /><br /> Para obter informações sobre esse recurso na MPF, consulte [preenchimento automático de palavras em um serviço de linguagem herdado](../../extensibility/internals/word-completion-in-a-legacy-language-service.md).|  
|Correspondência de chaves|Destaques emparelhado caracteres como chaves. Quando o usuário digita um caractere de fechamento, como "}", correspondência de chaves destaca correspondente a abertura de caractere, como "{". Quando há vários níveis de delimitar caracteres, esse recurso ajuda os usuários confirmar que os caracteres delimitadores estão emparelhados corretamente.<br /><br /> Para obter informações sobre esse recurso na MPF, consulte [correspondência de chaves em um serviço de linguagem herdado](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md).|  
|Dicas de ferramentas de informações de parâmetro|Exibe uma lista de assinaturas possíveis para o método sobrecarregado que o usuário está digitando no momento.<br /><br /> Para obter informações gerais, consulte [informações de parâmetro em um serviço de linguagem herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md).<br /><br /> Para obter informações sobre esse recurso na MPF, consulte [informações de parâmetro em um serviço de linguagem herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md).|  
|Marcadores de erro|Exibe um sublinhado vermelho ondulado, também conhecido como uma linha ondulado, sob o texto que está sintaticamente incorreto. Marcadores de erro geralmente são usados para tornar os usuários ciente das palavras-chave incorretas, não fechados parênteses, caracteres inválidos e erros semelhantes.<br /><br /> As classes MPF, marcadores de erro são tratadas automaticamente na <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> método da <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe.|  

 Muitos desses recursos exigem que o serviço de linguagem para analisar o código-fonte. Você geralmente pode reutilizar os tokens e analisar o código para o compilador ou interpretador.  

 Os recursos a seguir estão relacionados ao suporte para linguagens de programação, mas não fazem parte dos serviços de linguagem:  


| Recurso | Descrição |
|-----------------------| - |
| Avaliadores de expressão | Dá suporte a [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador validar pontos de interrupção e fornecendo uma lista de expressões a serem exibidos na **Autos** janela de depuração.<br /><br /> Para obter mais informações, consulte [suporte do serviço de linguagem para depuração](../../extensibility/internals/language-service-support-for-debugging.md). |
| Ferramentas de navegação de símbolo | Dá suporte à **Pesquisador de objetos**, **exibição de classe**, **Pesquisador de chamadas**, e **localizar resultados de símbolos**. |

