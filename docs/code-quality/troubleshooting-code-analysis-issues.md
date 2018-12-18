---
title: Solucionando problemas de análise do código
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: troubleshooting
ms.assetid: 61c7e44d-2780-4df5-9bcb-49e40c1152fc
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f1c80e7421569804f6d6781b117522dd1ef1dea8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49885860"
---
# <a name="troubleshooting-code-analysis-issues"></a>Solucionando problemas de análise do código
Este tópico contém informações de solução de problemas para os seguintes problemas de análise de código do Visual Studio.

-   [Alterações em uma Regra do Visual Studio 2010 Não Afetarão as Versões Anteriores do Visual Studio](#ChildRuleSetChangesInPreviousVersions)

##  <a name="ChildRuleSetChangesInPreviousVersions"></a> Alterações em uma Regra do Visual Studio 2010 Não Afetarão as Versões Anteriores do Visual Studio
 Ao criar um conjunto de regras no [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)] que contém um conjunto de regras filho, uma alteração no conjunto de regras filho pode não ser aplicada em execuções de análise de código em computadores que usam uma versão anterior do Visual Studio. Para resolver esse problema, é necessário forçar uma reescrita de conjunto de regras pai, que é o conjunto de regras que contém o conjunto de regras filho.

1. Abra o conjunto de regras pai no [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)].

2. Faça uma alteração, como adicionar ou remover uma regra e salve o conjunto de regras.

3. Abra o conjunto de regras, reverta a alteração e, em seguida, salve o conjunto de regras novamente.

## <a name="see-also"></a>Consulte também
 [Analisando a qualidade do aplicativo](../code-quality/analyzing-application-quality-by-using-code-analysis-tools.md) [analisando a qualidade do código gerenciado](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md) [usando conjuntos de regras para agrupar regras de análise de código](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)