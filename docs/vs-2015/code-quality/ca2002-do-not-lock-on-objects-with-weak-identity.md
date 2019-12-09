---
title: 'CA2002: Não bloquear objetos com identidade fraca | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotLockOnObjectsWithWeakIdentity
- CA2002
helpviewer_keywords:
- CA2002
- DoNotLockOnObjectsWithWeakIdentity
ms.assetid: 16100b39-c6fc-452b-8fca-8b459a26c286
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 557f91d8b00274642accbbfc05b4a60789615bfc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667756"
---
# <a name="ca2002-do-not-lock-on-objects-with-weak-identity"></a>CA2002: Não bloquear objetos com identidade fraca
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotLockOnObjectsWithWeakIdentity|
|CheckId|CA2002|
|Categoria|Microsoft. confiabilidade|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um thread tenta adquirir um bloqueio em um objeto que tem uma identidade fraca.

## <a name="rule-description"></a>Descrição da Regra
 Diz-se que um objeto tem uma identidade fraca quando puder ser acessado diretamente em todos os limites de domínio do aplicativo. Um thread que tente adquirir um bloqueio em um objeto com uma identidade fraca pode ser bloqueado por um segundo thread em um domínio de aplicativo diferente com um bloqueio no mesmo objeto. Os tipos a seguir têm uma identidade fraca e são sinalizados pela regra:

- <xref:System.MarshalByRefObject>

- <xref:System.ExecutionEngineException>

- <xref:System.OutOfMemoryException>

- <xref:System.StackOverflowException>

- <xref:System.String>

- <xref:System.Reflection.MemberInfo>

- <xref:System.Reflection.ParameterInfo>

- <xref:System.Threading.Thread>

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, use um objeto de um tipo que não esteja na lista na seção Descrição.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="related-rules"></a>Regras relacionadas
 [CA2213: os campos descartáveis devem ser descartados](../code-quality/ca2213-disposable-fields-should-be-disposed.md)

## <a name="example"></a>{1&gt;Exemplo&lt;1}
 O exemplo a seguir mostra alguns bloqueios de objeto que violam a regra.

 [!code-csharp[FxCop.Reliability.LockWeakObjects#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Reliability.LockWeakObjects/cs/FxCop.Reliability.LockWeakObjects.cs#1)]
 [!code-vb[FxCop.Reliability.LockWeakObjects#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Reliability.LockWeakObjects/vb/FxCop.Reliability.LockWeakObjects.vb#1)]

## <a name="see-also"></a>Consulte também
 <xref:System.Threading.Monitor> <xref:System.AppDomain>
 [instrução do lock](https://msdn.microsoft.com/library/656da1a4-707e-4ef6-9c6e-6d13b646af42) [instrução SyncLock](https://msdn.microsoft.com/library/14501703-298f-4d43-b139-c4b6366af176)
