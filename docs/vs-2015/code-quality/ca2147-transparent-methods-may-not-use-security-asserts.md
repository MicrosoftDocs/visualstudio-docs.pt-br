---
title: 'CA2147: Métodos transparentes talvez não usem segurança declara | Microsoft Docs'
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
- SecurityTransparentCodeShouldNotAssert
- CA2147
- CA2128
helpviewer_keywords:
- CA2128
- SecurityTransparentCodeShouldNotAssert
ms.assetid: 5d31e940-e599-4b23-9b28-1c336f8d910e
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6542a2063d076cb57750015039f413b2faf4bca4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49921622"
---
# <a name="ca2147-transparent-methods-may-not-use-security-asserts"></a>CA2147: os métodos transparentes talvez não usem declarações de segurança
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|SecurityTransparentCodeShouldNotAssert|
|CheckId|CA2147|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Código que está marcado como <xref:System.Security.SecurityTransparentAttribute> não tem permissões suficientes para declarar.

## <a name="rule-description"></a>Descrição da Regra
 Esta regra analisa todos os métodos e tipos em um assembly que é qualquer um dos 100% transparente ou misto transparente/crítico e sinaliza qualquer uso declarativo ou obrigatório do <xref:System.Security.CodeAccessPermission.Assert%2A>.

 No tempo de execução, todas as chamadas para <xref:System.Security.CodeAccessPermission.Assert%2A> no código transparent fará com que um <xref:System.InvalidOperationException> seja lançada. Isso pode ocorrer em ambos os assemblies de 100% transparente e também em assemblies mistos transparente/crítico em que um tipo ou método é declarado transparente, mas inclui um Assert declarativa ou imperativa.

 O [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 2.0 introduziu um recurso chamado *transparência*. Tipos, campos, interfaces, classes e métodos individuais podem ser transparente ou crítica.

 O código transparente não é permitido para elevar privilégios de segurança. Portanto, todas as permissões concedidas ou exigidas dele automaticamente são passadas por meio do código para o domínio de aplicativo do chamador ou o host. As elevações exemplos de declarações, LinkDemands, SuppressUnmanagedCode, e `unsafe` código.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para resolver o problema, a marcar o código que chama o Assert com o <xref:System.Security.SecurityCriticalAttribute>, ou remover o Assert.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima uma mensagem a partir dessa regra.

## <a name="example"></a>Exemplo
 Este código falhará caso `SecurityTestClass` é transparente, quando o `Assert` método lança um <xref:System.InvalidOperationException>.

 [!code-csharp[FxCop.Security.CA2147.TransparentMethodsMustNotUseSecurityAsserts#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2147.transparentmethodsmustnotusesecurityasserts/cs/ca2147 - transparentmethodsmustnotusesecurityasserts.cs#1)]

## <a name="example"></a>Exemplo
 Uma opção é o método SecurityTransparentMethod no exemplo a seguir de revisão de código e se o método é considerado seguro para elevação, marcar SecurityTransparentMethod com seguro-crítica isso requer que uma detalhada, completa e sem erros de segurança auditoria deve ser executada no método junto com qualquer explicativos que ocorrem dentro do método em Assert:

 [!code-csharp[FxCop.Security.SecurityTransparentCode2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SecurityTransparentCode2/cs/FxCop.Security.SecurityTransparentCode2.cs#1)]

 Outra opção é remover o Assert do código e permitir que qualquer arquivo subsequente de fluxo de demandas de permissão e/s além SecurityTransparentMethod ao chamador. Isso permite que verificações de segurança. Nesse caso, nenhuma auditoria de segurança geralmente é necessário, porque as demandas de permissão fluirão para o chamador e/ou o domínio do aplicativo. Demandas de permissão de perto são controladas pela política de segurança, concessões de permissão de código-fonte e ambiente de hospedagem.

## <a name="see-also"></a>Consulte também
 [Avisos de segurança](../code-quality/security-warnings.md)



