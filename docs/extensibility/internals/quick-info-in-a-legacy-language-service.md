---
title: Informações rápidas em um serviço de linguagem herdada | Microsoft Docs
description: Saiba mais sobre o suporte para a operação de informações rápidas do IntelliSense para exibir informações sobre um identificador.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Quick Info, supporting in language services [managed package framework]
- IntelliSense, Quick Info
- language services [managed package framework], IntelliSense Quick Info
ms.assetid: 159ccb0b-f5d6-4912-b88b-e9612924ed5e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 90cab5683c7a13aec25b15d75da0117beee34721
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060881"
---
# <a name="quick-info-in-a-legacy-language-service"></a>Informações rápidas em um serviço de linguagem herdado
As informações rápidas do IntelliSense mostram informações sobre um identificador na origem quando o usuário posiciona o cursor no identificador e seleciona **informações rápidas** no menu do **IntelliSense** ou mantém o cursor do mouse sobre o identificador. Isso faz com que uma dica de ferramenta apareça com informações sobre o identificador. Normalmente, essas informações consistem no tipo de identificador. Quando o mecanismo de depuração está ativo, essas informações podem incluir o valor atual. O mecanismo de depuração fornece valores de expressão, enquanto o serviço de linguagem manipula somente identificadores.

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para obter mais informações, consulte [Walkthrough: exibindo dicas de ferramenta QuickInfo](../../extensibility/walkthrough-displaying-quickinfo-tooltips.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

 As classes de serviço de linguagem MPF (Managed Package Framework) fornecem suporte completo para exibir a dica de ferramenta de informações rápidas do IntelliSense. Tudo o que você precisa fazer é fornecer o texto a ser exibido e habilitar o recurso de informações rápidas.

 O texto a ser exibido é obtido chamando-se o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> analisador de método com um valor de motivo de análise de <xref:Microsoft.VisualStudio.Package.ParseReason> . Esse motivo informa o analisador para obter as informações de tipo (ou qualquer que seja apropriado para ser exibido na dica de ferramenta de informações rápidas) para o identificador no local especificado no <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto. O <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto é o que foi passado para o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método.

 O analisador deve analisar tudo até a posição no objeto a <xref:Microsoft.VisualStudio.Package.ParseRequest> fim de determinar os tipos de todos os identificadores. Em seguida, o analisador deve obter o identificador no local da solicitação de análise. Por fim, o analisador deve passar os dados da dica de ferramenta associados a esse identificador para o <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto para que o objeto possa retornar o texto do <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> método.

## <a name="enabling-the-quick-info-feature"></a>Habilitando o recurso de informações rápidas
 Para habilitar o recurso de informações rápidas, você deve definir `CodeSense` os `QuickInfo` parâmetros nomeados e do <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> . Esses atributos definem <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> as <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableQuickInfo%2A> Propriedades e.

## <a name="implementing-the-quick-info-feature"></a>Implementando o recurso de informações rápidas
 A <xref:Microsoft.VisualStudio.Package.ViewFilter> classe manipula a operação de informações rápidas do IntelliSense. Quando a <xref:Microsoft.VisualStudio.Package.ViewFilter> classe recebe o <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> comando, a classe chama o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método com o motivo da análise de <xref:Microsoft.VisualStudio.Package.ParseReason> e o local do cursor no momento em que o <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> comando foi enviado. O <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> analisador de método deve analisar a origem até o local fornecido e, em seguida, analisar o identificador no local especificado para determinar o que será exibido na dica de ferramenta de informações rápidas.

 A maioria dos analisadores realiza uma análise inicial de todo o arquivo de origem e armazena os resultados em uma árvore de análise. A análise completa é realizada quando <xref:Microsoft.VisualStudio.Package.ParseReason> é passada para o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método. Outros tipos de análise podem usar a árvore de análise para obter as informações desejadas.

 Por exemplo, o valor do motivo da análise de <xref:Microsoft.VisualStudio.Package.ParseReason> pode encontrar o identificador no local de origem e procurar na árvore de análise para obter as informações de tipo. Essas informações de tipo são passadas para a <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe e retornadas pelo <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> método.
