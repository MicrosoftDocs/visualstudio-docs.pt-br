---
title: 'CA2134: os métodos devem manter a transparência consistente ao substituir os métodos base | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2134
ms.assetid: 3b17e487-0326-442e-90e1-dc0ba9cdd3f2
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fe9a84280b0124eed6bb0cfffae9c1ec2942bddf
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547713"
---
# <a name="ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods"></a>CA2134: Os métodos devem manter uma transparência consistente durante a substituição dos métodos base
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|MethodsMustOverrideWithConsistentTransparency|
|CheckId|CA2134|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Essa regra é acionada quando um método marcado com o <xref:System.Security.SecurityCriticalAttribute> substitui um método que é transparente ou marcado com <xref:System.Security.SecuritySafeCriticalAttribute> . A regra também é acionada quando um método que é transparente ou marcado com o <xref:System.Security.SecuritySafeCriticalAttribute> substitui um método que é marcado com um <xref:System.Security.SecurityCriticalAttribute> .

 A regra é aplicada durante a substituição de um método virtual ou a implementação de uma interface.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra é acionada em tentativas de alterar a acessibilidade de segurança de um método além da cadeia de herança. Por exemplo, se um método virtual em uma classe base for transparente ou de segurança crítica, a classe derivada deverá substituí-la por um método transparente ou de segurança crítica. Por outro lado, se a segurança da máquina virtual for crítica, a classe derivada deverá substituí-la por um método crítico de segurança. A mesma regra se aplica à implementação de métodos de interface.

 As regras de transparência são impostas quando o código é compilado JIT em vez de em tempo de execução, para que o cálculo de transparência não tenha informações de tipo dinâmico. Portanto, o resultado do cálculo de transparência deve ser capaz de ser determinado exclusivamente dos tipos estáticos que estão sendo compilados em JIT, independentemente do tipo dinâmico.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere a transparência do método que está substituindo um método virtual ou implementando uma interface para corresponder à transparência do método virtual ou da interface.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir avisos desta regra. As violações dessa regra resultarão em um tempo <xref:System.TypeLoadException> de execução para assemblies que usam transparência de nível 2.

## <a name="examples"></a>Exemplos

### <a name="code"></a>Código
 [!code-csharp[FxCop.Security.CA2134.MethodsMustOverrideWithConsistentTransparency#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2134.methodsmustoverridewithconsistenttransparency/cs/ca2134 - methodsmustoverridewithconsistenttransparency.cs#1)]

## <a name="see-also"></a>Consulte Também
 [Código transparente de segurança, nível 2](https://msdn.microsoft.com/library/4d05610a-0da6-4f08-acea-d54c9d6143c0)
