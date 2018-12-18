---
title: 'CA2134: Os métodos devem manter uma transparência consistente durante a substituição de métodos de base | Microsoft Docs'
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
- CA2134
ms.assetid: 3b17e487-0326-442e-90e1-dc0ba9cdd3f2
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 218114a87b3f81fb4b422852b6d92f952474f668
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49844192"
---
# <a name="ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods"></a>CA2134: os métodos devem manter uma transparência consistente durante a substituição dos métodos base
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|MethodsMustOverrideWithConsistentTransparency|
|CheckId|CA2134|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Essa regra é acionada quando um método marcado com o <xref:System.Security.SecurityCriticalAttribute> substitui um método transparente ou marcado com o <xref:System.Security.SecuritySafeCriticalAttribute>. A regra também é acionado quando um método transparente ou marcado com o <xref:System.Security.SecuritySafeCriticalAttribute> substitui um método marcado com um <xref:System.Security.SecurityCriticalAttribute>.

 A regra é aplicada durante a substituição de um método virtual ou a implementação de uma interface.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra é acionada em tentativas de alterar a acessibilidade de segurança de um método na cadeia de herança. Por exemplo, se um método virtual em uma classe base é transparente ou de segurança crítica, em seguida, a classe derivada deve substitui-lo com um método transparente ou de segurança crítica. Por outro lado, se o virtual é crítico para segurança, a classe derivada deve substituí-la com um método crítico de segurança. A mesma regra se aplica para implementar métodos de interface.

 Regras de transparência são aplicadas quando o código é o JIT compilado em vez de no tempo de execução para que o cálculo de transparência não tem informações de tipo dinâmico. Portanto, o resultado do cálculo de transparência deve ser capaz de ser determinada exclusivamente dos tipos estáticos que está sendo compilado por JIT, independentemente do tipo dinâmico.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere a transparência do método que está substituindo um método virtual ou implementar uma interface para coincidir com a transparência da virtual ou o método de interface.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima avisos dessa regra. As violações dessa regra resultará em um tempo de execução <xref:System.TypeLoadException> para assemblies que usam a transparência de nível 2.

## <a name="examples"></a>Exemplos

### <a name="code"></a>Código
 [!code-csharp[FxCop.Security.CA2134.MethodsMustOverrideWithConsistentTransparency#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2134.methodsmustoverridewithconsistenttransparency/cs/ca2134 - methodsmustoverridewithconsistenttransparency.cs#1)]

## <a name="see-also"></a>Consulte também
 [Código transparente de segurança, nível 2](http://msdn.microsoft.com/library/4d05610a-0da6-4f08-acea-d54c9d6143c0)



