---
title: 'CA2141: métodos transparentes não devem atender a LinkDemands | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2141
ms.assetid: 2957f5f7-c511-4180-ba80-752034f10a77
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a7c54b472e91aa2be1d8e5bb1a9c32c26c0cb299
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142701"
---
# <a name="ca2141transparent-methods-must-not-satisfy-linkdemands"></a>CA2141:Transparent métodos não devem atender a LinkDemands
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|TransparentMethodsMustNotSatisfyLinkDemands|
|CheckId|CA2141|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método de segurança transparente chama um método em um assembly que não está marcado com o <xref:System.Security.AllowPartiallyTrustedCallersAttribute> atributo (APTCA) ou um método transparente de segurança atende a uma <xref:System.Security.Permissions.SecurityAction> `.LinkDemand` para um tipo ou um método.

## <a name="rule-description"></a>Descrição da Regra
 Que satisfazem um LinkDemand é uma operação confidencial de segurança que pode causar a não intencional de elevação de privilégio. Código transparente de segurança não deve atender a LinkDemands, porque ele não está sujeito aos mesmos requisitos de auditoria de segurança como o código de segurança crítica. Os métodos transparentes em assemblies de nível 1 de conjunto de regras de segurança fará com que todas as LinkDemands atendem a ser convertido em demandas completas em tempo de execução, o que pode causar problemas de desempenho. Em assemblies de nível 2 de conjunto de regras de segurança, os métodos transparentes não serão compilado no compilador just-in-time (JIT), caso eles tentem atender a um LinkDemand.

 Em assemblies que usee segurança de nível 2, tentativas por um método transparente de segurança para atender a um LinkDemand ou chamar um método em um assembly não-APTCA gera um <xref:System.MethodAccessException>; em assemblies de nível 1 de LinkDemand se torna uma demanda completa.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, marque o método de acesso com o <xref:System.Security.SecurityCriticalAttribute> ou <xref:System.Security.SecuritySafeCriticalAttribute> de atributo ou remover o LinkDemand do método acessado.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 Neste exemplo, um método transparente tenta chamar um método que tem um LinkDemand. Essa regra será acionado nesse código.

 [!code-csharp[FxCop.Security.CA2141.TransparentMethodsMustNotSatisfyLinkDemands#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2141.transparentmethodsmustnotsatisfylinkdemands/cs/ca2141 - transparentmethodsmustnotsatisfylinkdemands.cs#1)]
