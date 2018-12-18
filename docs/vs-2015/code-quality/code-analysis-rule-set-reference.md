---
title: Referência de conjunto de regras de análise de código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- code analysis, rule sets
ms.assetid: 5874e854-e298-4d2e-bbe4-95e899d22587
caps.latest.revision: 45
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 928b838a4172537ec12937b02c3deab2cf666ddd
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49279156"
---
# <a name="code-analysis-rule-set-reference"></a>Referência do conjunto de regras da análise de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você configura para a análise de código gerenciado projetos de código em [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], ou [!INCLUDE[vsPro](../includes/vspro-md.md)]você verá uma lista dos internas *conjuntos de regra*. Você pode usar qualquer um dos conjuntos de regras padrões de computação, ou você pode personalizar uma conjunto de regras para atender às suas necessidades de projeto.  
  
## <a name="available-rule-sets"></a>Conjuntos de regras disponíveis  
 A tabela a seguir lista os conjuntos de regra padrão:  
  
|||  
|-|-|  
|[Conjunto de regras Todas as Regras](../code-quality/all-rules-rule-set.md)|Este conjunto contém todas as regras. Executar este conjunto de regras pode resultar em um grande número de avisos relatados. Use este conjunto de regras para obter uma visão abrangente de todos os problemas em seu código. Isso pode ajudá-lo a decidir quais regras mais restritos conjuntos são mais apropriados para execução em seus projetos.|  
|[Conjunto de regras básicas de correção para código gerenciado](../code-quality/basic-correctness-rules-rule-set-for-managed-code.md)|Estas regras enfocam erros lógicos e comuns cometidos no uso de APIs de estrutura. Inclua este conjunto de regras para expandir a lista de avisos relatados pelas regras recomendadas mínimas.|  
|[Conjunto de regras básicas de diretrizes de design para código gerenciado](../code-quality/basic-design-guideline-rules-rule-set-for-managed-code.md)|Estas regras enfocam a imposição de práticas recomendadas para tornar seu código mais fácil de entender e usar. Inclua este conjunto se o seu projeto incluir código de biblioteca ou se você quiser impor práticas recomendadas para o código de fácil manutenção de regras.|  
|[Conjunto de regras de correção estendido para código gerenciado](../code-quality/extended-correctness-rules-rule-set-for-managed-code.md)|Estas regras expandem as regras básicas de correção para maximizar os erros de uso de lógica e do framework que são relatados. Ênfase extra é colocado em cenários específicos, como aplicativos móveis e interoperabilidade de COM. Considere incluir essa regra definir se um desses cenários se aplica ao seu projeto ou para localizar problemas adicionais em seu projeto.|  
|[Conjunto de regras estendidas de diretrizes de design para código gerenciado](../code-quality/extended-design-guidelines-rules-rule-set-for-managed-code.md)|Estas regras expandem as regras de diretrizes de design básico para maximizar os problemas de usabilidade e facilidade de manutenção que são relatados. Ênfase extra é colocado em diretrizes de nomenclatura. Considere a possibilidade de incluir este conjunto se o seu projeto incluir código de biblioteca ou se você quiser impor os mais altos padrões para escrever o código de fácil manutenção de regras.|  
|[Conjunto de regras de globalização para código gerenciado](../code-quality/globalization-rules-rule-set-for-managed-code.md)|Estas regras enfocam os problemas que impedem que os dados em seu aplicativo sejam exibidos corretamente quando usados em diferentes idiomas, localidades e culturas. Inclua este conjunto se o aplicativo está localizado ou globalizado de regras.|  
|[Conjunto de regras mínimas gerenciado para código gerenciado](../code-quality/managed-minimun-rules-rule-set-for-managed-code.md)|Estas regras enfocam os problemas mais críticos em seu código para o qual análise de código é o mais preciso.  Essas regras são em pequenas número e eles destinam-se apenas à execução em edições limitadas do Visual Studio.  Use Minimumrecommendedrules com outras edições do Visual Studio.|  
|[Conjunto de regras recomendadas gerenciado para código gerenciado](../code-quality/managed-recommended-rules-rule-set-for-managed-code.md)|Estas regras enfocam os problemas mais críticos do código, inclusive falhas potenciais de segurança, falhas do aplicativo e outros erros importantes de lógica e design. Você deve incluir este conjunto de regras em qualquer conjunto personalizado que criar para seus projetos.|  
|[Conjunto de regras mínimas misto](../code-quality/mixed-minimum-rules-rule-set.md)|Estas regras enfocam os problemas mais críticos em seus projetos do C++ que dão suporte a Common Language Runtime, inclusive falhas potenciais de segurança e falhas do aplicativo. Você deve incluir essa regra definida em qualquer conjunto personalizado que você criar para seus projetos em C++ que dão suporte a Common Language Runtime.|  
|[Conjunto de regras recomendadas misto](../code-quality/mixed-recommended-rules-rule-set.md)|Estas regras enfocam os problemas mais críticos e comuns em seus projetos do C++ que dão suporte a Common Language Runtime, inclusive falhas potenciais de segurança, falhas do aplicativo e outros erros importantes de lógica e design. Você deve incluir essa regra definida em qualquer conjunto personalizado que você criar para seus projetos em C++ que dão suporte a Common Language Runtime.  Esse conjunto de regras foi projetado para ser configurado com a edição do Visual Studio Professional e superior.|  
|[Conjunto de regras mínimas nativo](../code-quality/native-minimum-rules-rule-set.md)|Estas regras enfocam os problemas mais críticos do código nativo, inclusive falhas potenciais de segurança e falhas do aplicativo. Você deve incluir este conjunto de regras em qualquer conjunto personalizado que criar para seus projetos nativos.|  
|[Conjunto de regras recomendadas nativo](../code-quality/native-recommended-rules-rule-set.md)|Estas regras enfocam os problemas mais críticos e comuns no seu código nativo, inclusive falhas potenciais de segurança e falhas do aplicativo.  Você deve incluir este conjunto de regras em qualquer conjunto personalizado que criar para seus projetos nativos.  Esse conjunto de regras foi projetado para trabalhar com a edição do Visual Studio Professional e superior.|  
|[Conjunto de regras de segurança para código gerenciado](../code-quality/security-rules-rule-set-for-managed-code.md)|Este conjunto contém todas as regras de segurança da Microsoft. Inclua este conjunto de regras para maximizar o número de possíveis problemas de segurança que são relatados.|



