---
title: Referência do conjunto de regras de análise de código | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
helpviewer_keywords:
- code analysis, rule sets
ms.assetid: 5874e854-e298-4d2e-bbe4-95e899d22587
caps.latest.revision: 45
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e480869d5b13ecc051deaa97b0bfd2532519d18f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535714"
---
# <a name="code-analysis-rule-set-reference"></a>Referência do conjunto de regras da análise de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você configura a análise de código para projetos de código gerenciado no [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] , [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] ou [!INCLUDE[vsPro](../includes/vspro-md.md)] é apresentada uma lista de *conjuntos de regras*internos. Você pode usar um dos conjuntos de regras padrão ou pode personalizar um conjunto de regras para se adequar aos requisitos do projeto.

## <a name="available-rule-sets"></a>Conjuntos de regras disponíveis
 A tabela a seguir lista os conjuntos de regras padrão:

|Item|Valor|
|-|-|
|[Conjunto de regras Todas as Regras](../code-quality/all-rules-rule-set.md)|Esse conjunto de regras contém todas as regras. A execução desse conjunto de regras pode resultar em um grande número de avisos sendo relatados. Use este conjunto de regras para obter uma visão abrangente de todos os problemas em seu código. Isso pode ajudá-lo a decidir quais dos conjuntos de regras mais concentrados são mais apropriados para serem executados para seus projetos.|
|[Conjunto de regras básicas de correção para código gerenciado](../code-quality/basic-correctness-rules-rule-set-for-managed-code.md)|Essas regras se concentram em erros lógicos e erros comuns feitos no uso de APIs de estrutura. Inclua este conjunto de regras para expandir na lista de avisos relatados pelas regras mínimas recomendadas.|
|[Conjunto de regras básicas de diretrizes de design para código gerenciado](../code-quality/basic-design-guideline-rules-rule-set-for-managed-code.md)|Essas regras se concentram em impor práticas recomendadas para facilitar a compreensão e o uso do seu código. Inclua este conjunto de regras se seu projeto incluir código de biblioteca ou se você quiser impor práticas recomendadas para um código facilmente passível de manutenção.|
|[Conjunto de regras de correção estendido para código gerenciado](../code-quality/extended-correctness-rules-rule-set-for-managed-code.md)|Essas regras expandem as regras básicas de correção para maximizar os erros de uso de lógica e de estrutura que são relatados. A ênfase extra é feita em cenários específicos, como interoperabilidade COM e aplicativos móveis. Considere incluir esse conjunto de regras se um desses cenários se aplicar ao seu projeto ou para encontrar problemas adicionais em seu projeto.|
|[Conjunto de regras estendidas de diretrizes de design para código gerenciado](../code-quality/extended-design-guidelines-rules-rule-set-for-managed-code.md)|Essas regras expandem as regras básicas de diretriz de design para maximizar a usabilidade e os problemas de manutenção relatados. A ênfase extra é feita nas diretrizes de nomenclatura. Considere incluir esse conjunto de regras se seu projeto incluir código de biblioteca ou se você quiser impor os padrões mais altos para escrever código de manutenção.|
|[Conjunto de regras de globalização para código gerenciado](../code-quality/globalization-rules-rule-set-for-managed-code.md)|Essas regras se concentram em problemas que impedem que os dados em seu aplicativo sejam exibidos corretamente quando usados em diferentes idiomas, localidades e culturas. Inclua este conjunto de regras se seu aplicativo for localizado ou globalizado.|
|[Conjunto de regras mínimas gerenciado para código gerenciado](../code-quality/managed-minimun-rules-rule-set-for-managed-code.md)|Essas regras concentram-se nos problemas mais críticos no seu código para os quais a análise de código é a mais precisa.  Essas regras são pequenas em número e devem ser executadas apenas em edições limitadas do Visual Studio.  Use MinimumRecommendedRules. RuleSet com outras edições do Visual Studio.|
|[Conjunto de regras recomendadas gerenciado para código gerenciado](../code-quality/managed-recommended-rules-rule-set-for-managed-code.md)|Essas regras concentram-se nos problemas mais críticos em seu código, incluindo possíveis falhas de segurança, falhas de aplicativo e outros erros importantes de lógica e design. Você deve incluir esse conjunto de regras em qualquer conjunto personalizado de regras que você criar para seus projetos.|
|[Conjunto de regras mínimas misto](../code-quality/mixed-minimum-rules-rule-set.md)|Essas regras concentram-se nos problemas mais críticos em seus projetos em C++ que dão suporte ao Common Language Runtime, incluindo falhas potenciais de segurança e falhas do aplicativo. Você deve incluir esse conjunto de regras em qualquer conjunto personalizado de regras que você criar para seus projetos C++ que dão suporte ao Common Language Runtime.|
|[Conjunto de regras recomendadas misto](../code-quality/mixed-recommended-rules-rule-set.md)|Essas regras se concentram nos problemas mais comuns e críticos em seus projetos em C++ que dão suporte ao Common Language Runtime, incluindo possíveis falhas de segurança, falhas do aplicativo e outros erros importantes de lógica e design. Você deve incluir esse conjunto de regras em qualquer conjunto personalizado de regras que você criar para seus projetos C++ que dão suporte ao Common Language Runtime.  Esse conjunto de regras foi projetado para ser configurado com o Visual Studio Professional Edition e superior.|
|[Conjunto de regras mínimas nativo](../code-quality/native-minimum-rules-rule-set.md)|Essas regras concentram-se nos problemas mais críticos em seu código nativo, incluindo falhas potenciais de segurança e falhas do aplicativo. Você deve incluir esse conjunto de regras em qualquer conjunto personalizado de regras que você criar para seus projetos nativos.|
|[Conjunto de regras recomendadas nativo](../code-quality/native-recommended-rules-rule-set.md)|Essas regras concentram-se nos problemas mais críticos e comuns em seu código nativo, incluindo falhas potenciais de segurança e aplicativos.  Você deve incluir esse conjunto de regras em qualquer conjunto personalizado de regras que você criar para seus projetos nativos.  Esse conjunto de regras foi projetado para funcionar com o Visual Studio Professional Edition e superior.|
|[Conjunto de regras de segurança para código gerenciado](../code-quality/security-rules-rule-set-for-managed-code.md)|Esse conjunto de regras contém todas as regras de segurança da Microsoft. Inclua este conjunto de regras para maximizar o número de possíveis problemas de segurança que são relatados.|
