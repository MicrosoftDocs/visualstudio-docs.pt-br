---
title: Informações rápidas em um serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Quick Info, supporting in language services [managed package framework]
- IntelliSense, Quick Info
- language services [managed package framework], IntelliSense Quick Info
ms.assetid: 159ccb0b-f5d6-4912-b88b-e9612924ed5e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ffdfe9bfb9063828a90dd9cdf3452ca3684ff0a5
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31132138"
---
# <a name="quick-info-in-a-legacy-language-service"></a>Informações rápidas em um serviço de linguagem herdado
Informações rápidas do IntelliSense mostra informações sobre um identificador na fonte, quando o usuário coloca o cursor do identificador e seleciona **informações rápidas** do **IntelliSense** menu ou mantém o mouse cursor sobre o identificador. Isso faz com que uma dica de ferramenta exibida com informações sobre o identificador. Essas informações normalmente consistem o tipo de identificador. Quando o mecanismo de depuração está ativo, essas informações podem incluir o valor atual. O mecanismo de depuração fornece valores de expressão, enquanto o serviço de linguagem controla somente identificadores.  
  
 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações, consulte [passo a passo: exibindo dicas de ferramenta Inforapida](../../extensibility/walkthrough-displaying-quickinfo-tooltips.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API assim que possível. Isso melhorar o desempenho do seu serviço de linguagem e permitem que você aproveite os novos recursos do editor.  
  
 As classes de serviço de idioma do pacote gerenciado framework (MPF) oferecem suporte completo para exibir a dica de ferramenta informações rápidas do IntelliSense. Tudo o que você precisa fazer é fornecer o texto a ser exibido e habilitar o recurso de informações rápidas.  
  
 O texto a ser exibido é obtido chamando o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> analisador de método com um valor de razão de análise de <xref:Microsoft.VisualStudio.Package.ParseReason>. Esse motivo informa ao analisador para obter as informações de tipo (ou o que for apropriado a ser exibido na dica de ferramenta informações rápidas) para o identificador no local especificado no <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto. O <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto é passado para o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método.  
  
 O analisador deve analisar tudo até a posição no <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto para determinar os tipos de todos os identificadores. Em seguida, o analisador deve obter o identificador no local de solicitação de análise. Por fim, o analisador deve transmitir os dados de dica de ferramenta associados com esse identificador para o <xref:Microsoft.VisualStudio.Package.AuthoringScope> para esse objeto pode retornar o texto a partir do objeto de <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> método.  
  
## <a name="enabling-the-quick-info-feature"></a>Habilitar o recurso de informações rápidas  
 Para habilitar o recurso de informações rápidas, você deve definir o `CodeSense` e `QuickInfo` parâmetros nomeados do <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>. Esses atributos definidos a <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> e <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableQuickInfo%2A> propriedades.  
  
## <a name="implementing-the-quick-info-feature"></a>Implementar o recurso de informações rápidas  
 O <xref:Microsoft.VisualStudio.Package.ViewFilter> classe manipula a operação de informações rápidas do IntelliSense. Quando o <xref:Microsoft.VisualStudio.Package.ViewFilter> classe recebe o <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> comando, as chamadas de classe a <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método com a razão de análise de <xref:Microsoft.VisualStudio.Package.ParseReason> e o local do cursor no momento em que o <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> comando foi enviado. O <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> analisador do método deve, em seguida, analisar a origem até o local em questão e, em seguida, analisar o identificador no local especificado para determinar o que é exibido na dica de ferramenta informações rápidas.  
  
 A maioria dos analisadores fazer uma análise inicial do arquivo de origem inteiro e armazenam os resultados em uma árvore de análise. A análise completa é executada quando <xref:Microsoft.VisualStudio.Package.ParseReason> é passado para <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método. Outros tipos de análise, em seguida, podem usar a árvore de análise para obter as informações desejadas.  
  
 Por exemplo, o valor do motivo de análise de <xref:Microsoft.VisualStudio.Package.ParseReason> pode localizar o identificador no local de origem e procurar na árvore de análise para obter as informações de tipo. Essas informações de tipo é então passadas para o <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe e é retornado pelo <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> método.