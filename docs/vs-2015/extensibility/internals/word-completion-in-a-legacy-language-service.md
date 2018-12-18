---
title: Conclusão do Word em um serviço de linguagem herdado | Microsoft Docs
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
- language services [managed package framework], IntelliSense Complete Word
- IntelliSense, Complete Word
- Complete Word
ms.assetid: 0ace5ac3-f9e1-4e6d-add4-42967b1f96a6
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 40a7e387ceb5fe88f059539634ae654ba076454f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51801713"
---
# <a name="word-completion-in-a-legacy-language-service"></a>Preenchimento de palavra em um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Preenchimento automático de palavras preenche os caracteres ausentes em uma palavra parcial digitada. Se houver somente uma conclusão possível, a palavra é concluída quando o caractere de preenchimento é inserido. Se a palavra parcial corresponde a mais de uma possibilidade, é exibida uma lista de possíveis conclusões. Um caractere de preenchimento pode ser qualquer caractere que não é usado para identificadores.  
  
 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações, consulte [estender o Editor e os serviços de linguagem](../../extensibility/extending-the-editor-and-language-services.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  
  
## <a name="implementation-steps"></a>Etapas de implementação  
  
1. Quando o usuário seleciona **completar palavra** da **IntelliSense** menu, o <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> comando é enviado para o serviço de linguagem.  
  
2. O <xref:Microsoft.VisualStudio.Package.ViewFilter> captura de classe de comando e chama o <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> método com a razão de análise de <xref:Microsoft.VisualStudio.Package.ParseReason>.  
  
3. O <xref:Microsoft.VisualStudio.Package.Source> classe, em seguida, chama o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método para obter a lista de preenchimentos de palavra possíveis e, em seguida, exibe as palavras em uma dica de ferramenta listam usando o <xref:Microsoft.VisualStudio.Package.CompletionSet> classe.  
  
    Se houver apenas uma palavra correspondente, o <xref:Microsoft.VisualStudio.Package.Source> classe completa a palavra.  
  
   Como alternativa, se o scanner retorna o valor de disparador <xref:Microsoft.VisualStudio.Package.TokenTriggers> quando o primeiro caractere de um identificador é digitado, o <xref:Microsoft.VisualStudio.Package.Source> classe detecta isso e chama o <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> método com a razão de análise de <xref:Microsoft.VisualStudio.Package.ParseReason>. Nesse caso, o analisador deve detectar a presença de um caractere de seleção de membro e fornecer uma lista de membros.  
  
## <a name="enabling-support-for-the-complete-word"></a>Habilitando o suporte para completar palavra  
 Para habilitar o suporte para o conjunto de conclusão do word a `CodeSense` chamado parâmetro passado para o <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> associado ao pacote de idioma do atributo de usuário. Isso define a <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> propriedade no <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe.  
  
 O analisador deve retornar uma lista de declarações em resposta ao valor do motivo de análise <xref:Microsoft.VisualStudio.Package.ParseReason>, para preenchimento automático de palavras operar.  
  
## <a name="implementing-complete-word-in-the-parsesource-method"></a>Implementando completar palavra no método ParseSource  
 Para preenchimento automático de palavras, o <xref:Microsoft.VisualStudio.Package.Source> chamado pela classe de <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> método no <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe para obter uma lista de correspondências de palavra possíveis. Você deve implementar a lista em uma classe que deriva de <xref:Microsoft.VisualStudio.Package.Declarations> classe. Consulte o <xref:Microsoft.VisualStudio.Package.Declarations> classe para obter detalhes sobre os métodos que você deve implementar.  
  
 Se a lista contém apenas uma única palavra, em seguida, a <xref:Microsoft.VisualStudio.Package.Source> classe insere automaticamente essa palavra em vez da palavra parcial. Se a lista contiver mais de uma palavra, o <xref:Microsoft.VisualStudio.Package.Source> classe apresenta uma lista de dica de ferramenta da qual o usuário pode selecionar a opção apropriada.  
  
 Observe também o exemplo de um <xref:Microsoft.VisualStudio.Package.Declarations> implementação de classe no [preenchimento de membro em um serviço de linguagem herdado](../../extensibility/internals/member-completion-in-a-legacy-language-service.md).

