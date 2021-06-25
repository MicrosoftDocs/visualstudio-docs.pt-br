---
title: Preenchimento de palavras em um serviço de linguagem herddo | Microsoft Docs
description: O preenchimento de palavras pode ter suporte para um serviço de linguagem herdado no SDK do Visual Studio. Saiba como os serviços de linguagem herdada são implementados em um VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- language services [managed package framework], IntelliSense Complete Word
- IntelliSense, Complete Word
- Complete Word
ms.assetid: 0ace5ac3-f9e1-4e6d-add4-42967b1f96a6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ea386aea3a17b0fb0d93ff9872f92e86a166be5c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902625"
---
# <a name="word-completion-in-a-legacy-language-service"></a>Preenchimento de palavra em um serviço de linguagem herdado
O preenchimento de palavras preenche os caracteres ausentes em uma palavra com tipo parcial. Se houver apenas uma conclusão possível, a palavra será concluída quando o caractere de conclusão for inserido. Se a palavra parcial corresponde a mais de uma possibilidade, uma lista de possíveis preenchimentos será exibida. Um caractere de conclusão pode ser qualquer caractere que não seja usado para identificadores.

 Os serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais nova de implementar recursos de serviço de linguagem é usar extensões MEF. Para saber mais, confira [Estendendo o Editor e os Serviços de Linguagem.](../../extensibility/extending-the-editor-and-language-services.md)

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor assim que possível. Isso melhorará o desempenho do serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="implementation-steps"></a>Etapas de implementação

1. Quando o usuário seleciona **Completar Palavra** no menu **IntelliSense,** o <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> comando é enviado para o serviço de linguagem.

2. A <xref:Microsoft.VisualStudio.Package.ViewFilter> classe captura o comando e chama o método com o motivo da análise de <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> <xref:Microsoft.VisualStudio.Package.ParseReason> .

3. Em seguida, a classe chama o método para obter a lista de <xref:Microsoft.VisualStudio.Package.Source> possíveis preenchimentos de palavras e exibe as palavras em uma lista de dicas <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> de ferramenta usando a classe <xref:Microsoft.VisualStudio.Package.CompletionSet> .

    Se houver apenas uma palavra correspondente, a <xref:Microsoft.VisualStudio.Package.Source> classe concluirá a palavra.

   Como alternativa, se o scanner retornar o valor do gatilho quando o primeiro caractere de um identificador for digitado, a classe detectará isso e chamará o método com o motivo da análise <xref:Microsoft.VisualStudio.Package.TokenTriggers> <xref:Microsoft.VisualStudio.Package.Source> de <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> <xref:Microsoft.VisualStudio.Package.ParseReason> . Nesse caso, o analisador deve detectar a presença de um caractere de seleção de membro e fornecer uma lista de membros.

## <a name="enabling-support-for-the-complete-word"></a>Habilitando o suporte para a palavra completa
 Para habilitar o suporte para preenchimento de palavras, de conjunto de parâmetros nomeados passado para o atributo `CodeSense` de usuário associado ao pacote de <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> idiomas. Isso define a <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> propriedade na <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe .

 O analisador deve retornar uma lista de declarações em resposta ao valor do motivo da análise , para que a <xref:Microsoft.VisualStudio.Package.ParseReason> conclusão da palavra opere.

## <a name="implementing-complete-word-in-the-parsesource-method"></a>Implementando o Complete Word no método ParseSource
 Para preenchimento de palavras, <xref:Microsoft.VisualStudio.Package.Source> a classe chama o método na classe para obter uma lista de <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> <xref:Microsoft.VisualStudio.Package.AuthoringScope> possíveis correspondeções de palavras. Você deve implementar a lista em uma classe derivada da <xref:Microsoft.VisualStudio.Package.Declarations> classe . Consulte a <xref:Microsoft.VisualStudio.Package.Declarations> classe para obter detalhes sobre os métodos que você deve implementar.

 Se a lista contiver apenas uma única palavra, a classe inserirá automaticamente <xref:Microsoft.VisualStudio.Package.Source> essa palavra no lugar da palavra parcial. Se a lista contiver mais de uma palavra, a classe apresentará uma lista de dicas de ferramenta da qual o usuário <xref:Microsoft.VisualStudio.Package.Source> pode selecionar a escolha apropriada.

 Veja também o exemplo de uma implementação <xref:Microsoft.VisualStudio.Package.Declarations> de classe em Conclusão de Membro em um Serviço de Linguagem [Herddo.](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)
