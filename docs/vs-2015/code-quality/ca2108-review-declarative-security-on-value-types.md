---
title: 'CA2108: examinar a segurança declarativa em tipos de valor | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
helpviewer_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
ms.assetid: d62bffdd-3826-4d52-a708-1c646c5d48c2
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 03918353b66c36698b5d17b332da052b6d95c87a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544385"
---
# <a name="ca2108-review-declarative-security-on-value-types"></a>CA2108: Examinar a segurança declarativa em tipos de valor
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ReviewDeclarativeSecurityOnValueTypes|
|CheckId|CA2108|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo de valor público ou protegido é protegido por um [dados e modelagem](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6) ou [demandas de link](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d).

## <a name="rule-description"></a>Descrição da Regra
 Os tipos de valor são alocados e inicializados por seus construtores padrão antes da execução de outros construtores. Se um tipo de valor for protegido por uma demanda ou LinkDemand e o chamador não tiver permissões que atendam à verificação de segurança, qualquer Construtor diferente do padrão falhará e uma exceção de segurança será lançada. O tipo de valor não é desalocado; Ele é deixado no estado definido por seu construtor padrão. Não assuma que um chamador que passa uma instância do tipo de valor tenha permissão para criar ou acessar a instância.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Não é possível corrigir uma violação dessa regra, a menos que você remova a verificação de segurança do tipo e use verificações de segurança em nível de método em seu lugar. Observe que corrigir a violação dessa maneira não impedirá que os chamadores com permissões inadequadas obtenham instâncias do tipo de valor. Você deve garantir que uma instância do tipo Value, em seu estado padrão, não exponha informações confidenciais e não possa ser usada de forma prejudicial.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você pode suprimir um aviso dessa regra se qualquer chamador puder obter instâncias do tipo de valor em seu estado padrão sem passar uma ameaça à segurança.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma biblioteca que contém um tipo de valor que viola essa regra. Observe que o `StructureManager` tipo supõe que um chamador que passa uma instância do tipo Value tem permissão para criar ou acessar a instância.

 [!code-csharp[FxCop.Security.DemandOnValueType#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.DemandOnValueType/cs/FxCop.Security.DemandOnValueType.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir demonstra o ponto fraco da biblioteca.

 [!code-csharp[FxCop.Security.TestDemandOnValueType#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestDemandOnValueType/cs/FxCop.Security.TestDemandOnValueType.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **Construtor personalizado de estrutura: falha na solicitação.** 
 **Novos valores SecuredTypeStructure 100 100** 
 **Novos valores SecuredTypeStructure 200 200**
## <a name="see-also"></a>Consulte Também
 [Dados e modelagem de](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6) [demandas de link](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)
