---
title: 'CA2200: relançar para preservar detalhes da pilha | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- RethrowToPreserveStackDetails
- CA2200
helpviewer_keywords:
- CA2200
- RethrowToPreserveStackDetails
ms.assetid: 046e1b98-c4dc-4515-874f-9c0de2285621
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6d63ef6ff3647742e931fd05f59c66b40059ad00
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546361"
---
# <a name="ca2200-rethrow-to-preserve-stack-details"></a>CA2200: Relançar para preservar detalhes da pilha
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|RethrowToPreserveStackDetails|
|CheckId|CA2200|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Uma exceção é relançada e a exceção é explicitamente especificada na `throw` instrução.

## <a name="rule-description"></a>Descrição da Regra
 Depois que uma exceção é lançada, parte das informações que ela transporta é o rastreamento de pilha. O rastreamento de pilha é uma lista da hierarquia de chamada de método que começa com o método que gera a exceção e termina com o método que captura a exceção. Se uma exceção for relançada especificando a exceção na `throw` instrução, o rastreamento de pilha será reiniciado no método atual e a lista de chamadas de método entre o método original que gerou a exceção e o método atual será perdido. Para manter as informações de rastreamento da pilha original com a exceção, use a `throw` instrução sem especificar a exceção.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, relance a exceção sem especificar a exceção explicitamente.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método, `CatchAndRethrowExplicitly` , que viola a regra e um método, `CatchAndRethrowImplicitly` que satisfaz a regra.

 [!code-csharp[FxCop.Usage.Rethrow#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.Rethrow/cs/FxCop.Usage.Rethrow.cs#1)]
 [!code-vb[FxCop.Usage.Rethrow#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.Rethrow/vb/FxCop.Usage.Rethrow.vb#1)]
