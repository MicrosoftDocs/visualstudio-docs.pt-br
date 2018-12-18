---
title: Analisando a qualidade do código gerenciado usando a análise de código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- code analysis,managed code
- managed code analyis
ms.assetid: 68510a55-da51-4381-81a5-0feba76b8b4f
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: e034db6fc7383ea5f944900713dffe1cc3e78473
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49263869"
---
# <a name="analyzing-managed-code-quality-by-using-code-analysis"></a>Analisando a qualidade do código gerenciado usando a análise de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar as ferramentas de análise de código no Visual Studio para descobrir problemas potenciais em seu código, como acesso a dados não seguro, violações de uso e problemas de design. Análise de código funciona no .NET Framework, nativo (C e C++) e aplicativos de banco de dados. Organiza as regras na análise de código para código gerenciado *conjuntos de regra* esse destino específico de problemas de codificação.  
  
## <a name="common-tasks"></a>Tarefas comuns  
  
|Tarefas comuns|Conteúdo de suporte|  
|------------------|------------------------|  
|**Obtenha experiência prática:** aprender os fundamentos da análise de código, corrigindo defeitos em um aplicativo simples do .NET Framework.|-   [Passo a passo: Analisando código gerenciado em busca de defeitos de código](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)|  
|**Configurar análise de código para um projeto:** regras de gerenciada de código são organizadas em conjuntos de regras que se destinam a áreas específicas, como segurança e design. Você pode usar um dos Microsoft regra padrão define ou criar seus próprios.|-   [Análise de código para visão geral do código gerenciado](../code-quality/code-analysis-for-managed-code-overview.md)<br />-   [Usando conjuntos de regras para agrupar regras de análise de código](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)<br />-   [Suprimir Avisos usando o atributo SuppressMessage](../code-quality/suppress-warnings-by-using-the-suppressmessage-attribute.md)|  
|**Executar análise de código:** você pode especificar a análise de código para ser executado automaticamente sempre que uma configuração de projeto é criada, e você pode executar a análise de código manualmente em um projeto.|-   [Como: habilitar e desabilitar análise de código automática](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)<br />-   [Como: executar análise de código manualmente](../code-quality/how-to-run-code-analysis-manually-for-managed-code.md)|  
|**Analisar resultados de análise de código:** erros e avisos de análise de código são listados na janela análise de código. Você pode escolher um aviso ou um título de erro para exibir informações adicionais sobre o aviso e para exibir e realce a linha de código fonte que disparou a regra. Você pode escolher a id do aviso para exibir informações detalhadas na biblioteca MSDN que inclui informações e exemplos de como resolver o problema.|-   [Como: Exibir defeitos de código gerenciado](../code-quality/how-to-view-managed-code-defects.md)<br />-   [Análise de código para avisos de código gerenciado](../code-quality/code-analysis-for-managed-code-warnings.md)<br />-   [Avisos por CheckId](../code-quality/code-analysis-warnings-for-managed-code-by-checkid.md)<br />-   [Métodos anônimos e análise de código](../code-quality/anonymous-methods-and-code-analysis.md)|  
|**Integrar a análise de código ao seu ciclo de vida de desenvolvimento:** políticas de Check-in no [!INCLUDE[esprscc](../includes/esprscc-md.md)] habilitar equipes de desenvolvimento para certificar-se de que todos os check-ins de código atendem a um conjunto comum de padrões de análise de código. Criar um item de trabalho para uma violação de regra de análise de código é um procedimento simples que você pode executar na janela lista de erros.|-   [Melhorando a qualidade do código com políticas de Check-in do projeto de equipe](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md)<br />-   [Como: sincronizar conjuntos de regras do projeto de código com a política de Check-in do projeto de equipe](../code-quality/how-to-synchronize-code-project-rule-sets-with-team-project-check-in-policy.md)<br />-   [Como: criar um Item de trabalho para um defeito de código gerenciado](../code-quality/how-to-create-a-work-item-for-a-managed-code-defect.md)|



