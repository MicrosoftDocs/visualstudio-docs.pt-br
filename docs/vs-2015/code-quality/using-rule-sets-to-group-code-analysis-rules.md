---
title: Usando conjuntos de regras para agrupar regras de análise de código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.codeanalysis.rulesets.learnmore
helpviewer_keywords:
- code analysis, rule sets
ms.assetid: ed0f3a2a-1516-42e2-92de-b8986dc75d42
caps.latest.revision: 38
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a8af8cbc27a61369640a80dbccb4d99dd2466f3a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49220578"
---
# <a name="using-rule-sets-to-group-code-analysis-rules"></a>Usando conjuntos de regras para agrupar regras de análise de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você configura a análise de código no [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], ou [!INCLUDE[vsPro](../includes/vspro-md.md)], você pode escolher entre uma lista dos internas da Microsoft *conjuntos de regra*. Um conjunto de regras é um agrupamento lógico de regras de análise de código que identificam problemas direcionados e condições específicas. Por exemplo, você pode aplicar um conjunto de regras que foi criado para examinar o código para as APIs disponíveis publicamente, ou você pode aplicar um conjunto de regras que inclui apenas o mínimo de regras recomendado. Você também pode aplicar um conjunto de regras que inclui todas as regras.  
  
 Você pode personalizar uma regra definida, adicionando ou excluindo regras ou alterando as regras na **Error List** janela como avisos ou erros. Conjuntos de regras personalizado podem atender uma necessidade para seu ambiente de desenvolvimento específico. Quando você personaliza um conjunto de regras, a página de conjunto de regra fornece pesquisa e ferramentas para ajudá-lo no processo de filtragem.  
  
## <a name="common-tasks"></a>Tarefas comuns  
  
|Tarefa|Conteúdo relacionado|  
|----------|---------------------|  
|**Obtenha experiência prática:** Use as ferramentas de análise de código para especificar uma regra personalizada definem para encontrar e corrigir problemas em um aplicativo simples do .NET Framework.|-   [Passo a passo: Configurando e usando um conjunto de regras personalizado](../code-quality/walkthrough-configuring-and-using-a-custom-rule-set.md)|  
|**Configurar análise de código para um projeto:** escolher uma regra existente definida para um projeto, o site da Web ou a solução.|-   [Como: configurar a análise de código para um projeto de código gerenciado](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)<br />-   [Usando conjuntos de regras para especificar as regras do C++ para execução](../code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run.md)<br />-   [Como: configurar a análise de código para um aplicativo Web ASP.NET](../code-quality/how-to-configure-code-analysis-for-an-aspnet-web-application.md)<br />-   [Como: especificar conjuntos de regras para vários projetos em uma solução](../code-quality/how-to-specify-managed-code-rule-sets-for-multiple-projects-in-a-solution.md)|  
|**Personalizar um conjunto de regras:** especificar regras para aplicar ao seu projeto.|-   [Criando conjuntos de regras personalizado](../code-quality/creating-custom-code-analysis-rule-sets.md)|  
|**Entender os conjuntos de regras internas:** exibir as regras de análise de código que compõem os conjuntos de regras internas.|-   [Referência de conjunto de regras de análise de código](../code-quality/code-analysis-rule-set-reference.md)|  
|**Integrar a análise de código com o Team Foundation Server:** [!INCLUDE[esprtfs](../includes/esprtfs-md.md)] check-in políticas permitem que as equipes de desenvolvimento certificar-se de que todos os check-ins de código atendem a um conjunto comum de padrões de análise de código.|-   [Como: sincronizar conjuntos de regras do projeto de código com a política de Check-in do projeto de equipe](../code-quality/how-to-synchronize-code-project-rule-sets-with-team-project-check-in-policy.md)|



