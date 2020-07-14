---
title: 'CA2142: o código transparent não deve ser protegido com LinkDemands | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2142
ms.assetid: 6dc59053-5dd9-4583-bf10-5f339107e59f
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: aa6bd9dcacc5fb863199c740a71c824f14739052
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546426"
---
# <a name="ca2142-transparent-code-should-not-be-protected-with-linkdemands"></a>CA2142: O código transparente não deve ser protegido com LinkDemands
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|TransparentMethodsShouldNotBeProtectedWithLinkDemands|
|CheckId|CA2142|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método transparente requer uma <xref:System.Security.Permissions.SecurityAction> ou outras demandas de segurança.

## <a name="rule-description"></a>Descrição da Regra
 Esta regra é acionada em métodos transparentes que exigem LinkDemands para serem acessados. O código transparente de segurança não deve ser responsável por verificar a segurança de uma operação e, assim, não deve exigir permissões. Como os métodos transparentes devem ser neutros à segurança, eles não devem tomar decisões de segurança. Além disso, o código crítico seguro, que toma decisões de segurança, não deve depender do código Transparent para ter feito essa decisão anteriormente.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova a demanda de link no método transparente ou marque o método com <xref:System.Security.SecuritySafeCriticalAttribute> atributo se ele estiver executando verificações de segurança, como demandas de segurança.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 No exemplo a seguir, a regra é acionada no método porque o método é transparente e é marcado com um LinkDemand <xref:System.Security.PermissionSet> que contém um <xref:System.Security.Permissions.SecurityAction> .

 [!code-csharp[FxCop.Security.CA2142.TransparentMethodsShouldNotBeProtectedWithLinkDemands#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2142.transparentmethodsshouldnotbeprotectedwithlinkdemands/cs/ca2142 -transparentmethodsshouldnotbeprotectedwithlinkdemands.cs#1)]

 Não suprima um aviso nessa regra.
