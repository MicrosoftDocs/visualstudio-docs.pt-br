---
title: Noções básicas do serviço de linguagem herdada | Microsoft Docs
description: Saiba mais sobre os recursos essenciais disponíveis em serviços de linguagem herdados que permitem integrar uma linguagem de programação ao Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- languages, integrating into Visual Studio
- language services, integrating programming languages
- Visual Studio, integrating programming languages
- programming languages, integrating into Visual Studio
ms.assetid: c15e0ccb-e7c5-4dbb-affb-fe3d3244debe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fa3fc358e7557360f02a80f108bcbec74ae48e5f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074555"
---
# <a name="legacy-language-service-essentials"></a>Conceitos básicos do serviço de linguagem herdado
Você deve fornecer um serviço de linguagem para integrar uma linguagem de programação ao Visual Studio. Este tópico explica os recursos disponíveis em serviços de idioma herdados.

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para saber mais sobre a nova maneira de implementar um serviço de linguagem, consulte [extensões de serviço de editor e linguagem](../../extensibility/editor-and-language-service-extensions.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

 Os serviços de linguagem herdados fornecem os seguintes recursos:

|Recurso|Descrição|
|-------------|-----------------|
|Coloração de sintaxe|Faz com que a exibição do editor exiba cores e estilos de fonte diferentes para os diferentes elementos de um idioma. Essa diferenciação pode facilitar a leitura e edição de arquivos.<br /><br /> Para obter informações gerais, consulte [cores de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md).<br /><br /> Para obter informações sobre esse recurso na MPF (estrutura de pacote gerenciada), consulte [Coloring de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md).|
|Conclusão da instrução|Conclui uma instrução ou palavra-chave que o usuário começou a digitar. A conclusão da instrução ajuda os usuários a inserir instruções difíceis com mais facilidade, com menos digitação e menos chances de erro.<br /><br /> Para obter informações gerais, consulte [conclusão de instrução em um serviço de linguagem herdado](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md).<br /><br /> Para obter informações sobre esse recurso no MPF, consulte [preenchimento de palavras em um serviço de linguagem herdado](../../extensibility/internals/word-completion-in-a-legacy-language-service.md).|
|Correspondência de chaves|Realça os caracteres emparelhados, como chaves. Quando o usuário digita um caractere de fechamento, como "}", a correspondência de chaves realça o caractere de abertura correspondente, como "{". Quando há vários níveis de caracteres delimitados, esse recurso ajuda os usuários a confirmar que os caracteres delimitadores estão emparelhados corretamente.<br /><br /> Para obter informações sobre esse recurso no MPF, consulte [correspondência de chaves em um serviço de linguagem herdado](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md).|
|Dicas de ferramenta de informações de parâmetro|Exibe uma lista de possíveis assinaturas para o método sobrecarregado que o usuário está digitando no momento.<br /><br /> Para obter informações gerais, consulte [informações de parâmetro em um serviço de idioma herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md).<br /><br /> Para obter informações sobre esse recurso no MPF, consulte [informações de parâmetro em um serviço de linguagem herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md).|
|Marcadores de erro|Exibe um sublinhado vermelho ondulado, também conhecido como um ondulado, em texto que está sintaticamente incorreto. Marcadores de erro geralmente são usados para fazer com que os usuários saibam de palavras-chave incorretas, parênteses não fechados, caracteres inválidos e erros semelhantes.<br /><br /> Nas classes do MPF, os marcadores de erro são tratados automaticamente no <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> método da <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe.|

 Muitos desses recursos exigem que o serviço de linguagem analise o código-fonte. Geralmente, você pode reutilizar o código de geração de tokens e de análise para seu compilador ou intérprete.

 Os recursos a seguir estão relacionados ao suporte para linguagens de programação, mas não fazem parte dos serviços de linguagem:

| Recurso | Descrição |
|-----------------------| - |
| Avaliadores de expressão | Dá suporte ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador Validando pontos de interrupção e fornecendo uma lista de expressões a serem exibidas na janela depurar **automaticamente** .<br /><br /> Para obter mais informações, consulte [suporte ao serviço de linguagem para depuração](../../extensibility/internals/language-service-support-for-debugging.md). |
| Ferramentas de navegação de símbolos | Dá suporte ao **pesquisador de objetos**, **modo de exibição de classe**, **pesquisador de chamadas** e **resultados de Localizar símbolo**. |
