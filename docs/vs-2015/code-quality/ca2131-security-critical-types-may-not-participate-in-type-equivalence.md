---
title: 'CA2131: tipos críticos de segurança podem não participar do tipo equivalências | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2131
ms.assetid: 4170f3b1-6086-430d-8fba-837d5538c573
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ccd556a5929e56597de678ad4ad8ea6c101b7c7f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535883"
---
# <a name="ca2131-security-critical-types-may-not-participate-in-type-equivalence"></a>CA2131: Tipos críticos de segurança podem não participar da equivalência de tipo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|CriticalTypesMustNotParticipateInTypeEquivalence|
|CheckId|CA2131|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo participa da equivalência de tipo e o próprio tipo, ou um membro ou campo do tipo, é marcado com o <xref:System.Security.SecurityCriticalAttribute> atributo.

## <a name="rule-description"></a>Descrição da Regra
 Esta regra é acionada em qualquer tipo crítico ou em tipos que contenham métodos críticos ou campos que estejam participando da equivalência do tipo. Quando o CLR detecta esse tipo, ele não consegue carregá-lo com um <xref:System.TypeLoadException> em tempo de execução. Normalmente, essa regra só é acionada quando usuários implementam equivalência de tipo manualmente, em vez de depender de tlbimp e dos compiladores para fazer a equivalência do tipo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova o atributo SecurityCritical.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 Os exemplos a seguir demonstram uma interface, um método e um campo que fará com que essa regra seja acionada.

 [!code-csharp[FxCop.Security.CA2131.CriticalTypesMustNotParticipateInTypeEquivalence#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2131.criticaltypesmustnotparticipateintypeequivalence/cs/ca2131 - criticaltypesmustnotparticipateintypeequivalence.cs#1)]

## <a name="see-also"></a>Consulte Também
 [Código transparente de segurança, nível 2](https://msdn.microsoft.com/library/4d05610a-0da6-4f08-acea-d54c9d6143c0)
