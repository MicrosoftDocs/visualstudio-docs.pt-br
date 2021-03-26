---
title: Preenchimento de palavra em um serviço de linguagem herdado | Microsoft Docs
description: O preenchimento de palavra pode ter suporte para um serviço de linguagem herdado no SDK do Visual Studio. Saiba como os serviços de linguagem herdados são implementados em um VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 360778e4dbc89130e8a533640fefb188047fe8ca
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074074"
---
# <a name="word-completion-in-a-legacy-language-service"></a>Preenchimento de palavra em um serviço de linguagem herdado
Preenchimento de palavra preenche os caracteres ausentes em uma palavra parcialmente digitada. Se houver apenas uma conclusão possível, a palavra será concluída quando o caractere de conclusão for inserido. Se a palavra parcial corresponder a mais de uma possibilidade, uma lista de conclusões possíveis será exibida. Um caractere de conclusão pode ser qualquer caractere que não seja usado para identificadores.

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para obter mais informações, consulte [estendendo o editor e os serviços de linguagem](../../extensibility/extending-the-editor-and-language-services.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="implementation-steps"></a>Etapas de implementação

1. Quando o usuário seleciona a **palavra completa** no menu do **IntelliSense** , o <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> comando é enviado para o serviço de idioma.

2. A <xref:Microsoft.VisualStudio.Package.ViewFilter> classe captura o comando e chama o <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> método com o motivo da análise de <xref:Microsoft.VisualStudio.Package.ParseReason> .

3. <xref:Microsoft.VisualStudio.Package.Source>Em seguida, a classe chama o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método para obter a lista de preenchimentos de palavras possíveis e, em seguida, exibe as palavras em uma lista de dicas de ferramenta usando a <xref:Microsoft.VisualStudio.Package.CompletionSet> classe.

    Se houver apenas uma palavra correspondente, a <xref:Microsoft.VisualStudio.Package.Source> classe concluirá a palavra.

   Como alternativa, se o verificador retornar o valor do gatilho <xref:Microsoft.VisualStudio.Package.TokenTriggers> quando o primeiro caractere de um identificador for digitado, a <xref:Microsoft.VisualStudio.Package.Source> classe detectará isso e chamará o <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> método com o motivo da análise de <xref:Microsoft.VisualStudio.Package.ParseReason> . Nesse caso, o analisador deve detectar a presença de um caractere de seleção de membro e fornecer uma lista de membros.

## <a name="enabling-support-for-the-complete-word"></a>Habilitando o suporte para a palavra completa
 Para habilitar o suporte para preenchimento de palavra, defina o `CodeSense` parâmetro nomeado passado para o <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> atributo de usuário associado ao pacote de idioma. Isso define a <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> Propriedade na <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe.

 O analisador deve retornar uma lista de declarações em resposta ao valor do motivo da análise <xref:Microsoft.VisualStudio.Package.ParseReason> , para que o Word Complete opere.

## <a name="implementing-complete-word-in-the-parsesource-method"></a>Implementando a palavra completa no método de análise
 Para preenchimento do Word, a <xref:Microsoft.VisualStudio.Package.Source> classe chama o <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> método na <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe para obter uma lista de possíveis correspondências de palavras. Você deve implementar a lista em uma classe derivada da <xref:Microsoft.VisualStudio.Package.Declarations> classe. Consulte a <xref:Microsoft.VisualStudio.Package.Declarations> classe para obter detalhes sobre os métodos que você deve implementar.

 Se a lista contiver apenas uma única palavra, a <xref:Microsoft.VisualStudio.Package.Source> classe inserirá automaticamente essa palavra no lugar da palavra parcial. Se a lista contiver mais de uma palavra, a <xref:Microsoft.VisualStudio.Package.Source> classe apresentará uma lista de dicas de ferramenta da qual o usuário pode selecionar a opção apropriada.

 Examine também o exemplo de uma <xref:Microsoft.VisualStudio.Package.Declarations> implementação de classe na [conclusão de um membro em um serviço de linguagem herdado](../../extensibility/internals/member-completion-in-a-legacy-language-service.md).
