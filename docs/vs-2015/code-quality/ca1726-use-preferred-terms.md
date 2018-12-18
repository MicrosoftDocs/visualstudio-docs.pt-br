---
title: 'CA1726: Usar termos preferenciais | Microsoft Docs'
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
- UsePreferredTerms
- CA1726
helpviewer_keywords:
- UsePreferredTerms
ms.assetid: 642b2acd-3a33-4d1f-b0a7-67073ae73be2
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c17514d00be7b0a3303b1c5bf703702fe564e0d1
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49220513"
---
# <a name="ca1726-use-preferred-terms"></a>CA1726: usar termos preferenciais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte [CA1726: usar termos preferenciais](https://docs.microsoft.com/visualstudio/code-quality/ca1726-use-preferred-terms) em docs.microsoft.com.  
  
|||  
|-|-|  
|NomeDoTipo|UsePreferredTerms|  
|CheckId|CA1726|  
|Categoria|Microsoft.Naming|  
|Alteração Significativa|Interrupção - quando acionado em assemblies<br /><br /> Separação de não - quando disparado em parâmetros de tipo|  
  
## <a name="cause"></a>Causa  
 O nome de um identificador visível externamente inclui um termo para o qual existe um termo preferido, alternativo. Como alternativa, o nome inclui o termo sinalizador ou sinalizadores.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Esta regra analisa um identificador em tokens. Cada token único e cada combinação contígua de token dupla é comparado com os termos que são criados para a regra e na seção preterido de dicionários personalizados. A tabela a seguir mostra os termos que são incorporados a regra e suas alternativas preferenciais.  
  
|Termo obsoleto|Termo preferencial|  
|-------------------|--------------------|  
|não são|Não são|  
|Cancelada|Cancelado|  
|Não é possível|Não é possível|  
|ComPlus|EnterpriseServices|  
|Não foi possível|Não foi|  
|Didnt|DidNot|  
|Doesnt|Não|  
|Não|Não|  
|Sinalizador ou sinalizadores|Não há nenhum termo de substituição. Não use.|  
|não tinha|HadNot|  
|Ainda não|HasNot|  
|ainda não|HaveNot|  
|Índices|Índices|  
|não é|IsNot|  
|Logon|LogOn|  
|Logoff|Fazer LogOff|  
|Shouldnt|ShouldNot|  
|Logon|Entrar|  
|Aprovação|SignOut|  
|Wasnt|WasNot|  
|não foram|Não foram|  
|Não quer|Vai|  
|Wouldnt|WouldNot|  
|Gravável|Gravável|  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Para corrigir uma violação dessa regra, substitua o termo com o termo preferencial de alternativo.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 Suprima um aviso nessa regra somente se o nome do identificador é intencional e se relacionam especificamente a termo original em vez do termo preferencial.  
  
## <a name="related-rules"></a>Regras relacionadas  
 [Avisos de Nomenclatura](../code-quality/naming-warnings.md)

