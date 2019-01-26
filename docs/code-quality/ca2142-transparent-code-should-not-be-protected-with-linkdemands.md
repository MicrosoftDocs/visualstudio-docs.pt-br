---
title: 'CA2142: O código transparente não deve ser protegido com LinkDemands'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- CA2142
ms.assetid: 6dc59053-5dd9-4583-bf10-5f339107e59f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5ad4ca58848412944d28874554383caf178c2af4
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54970845"
---
# <a name="ca2142-transparent-code-should-not-be-protected-with-linkdemands"></a>CA2142: O código transparente não deve ser protegido com LinkDemands

|||
|-|-|
|NomeDoTipo|TransparentMethodsShouldNotBeProtectedWithLinkDemands|
|CheckId|CA2142|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método transparente requer um <xref:System.Security.Permissions.SecurityAction> ou outra exigência de segurança.

## <a name="rule-description"></a>Descrição da regra
 Essa regra é acionada em métodos transparentes que exigem LinkDemands para acessá-los. O código transparente de segurança não deve ser responsável por verificar a segurança de uma operação e, assim, não deve exigir permissões. Porque os métodos transparentes devem para ser segurança neutra, eles deverão não tomar decisões de segurança. Além disso, código crítico seguro, que toma decisões de segurança, não deve ser confiando no código transparente para feitas anteriormente essa decisão.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, remova a demanda de link no método transparente ou marcar o método com <xref:System.Security.SecuritySafeCriticalAttribute> verificações de atributo se ele está executando a segurança, como demandas de segurança.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 No exemplo a seguir, a regra é acionada no método porque o método é transparente e é marcado com um LinkDemand <xref:System.Security.PermissionSet> que contém um <xref:System.Security.Permissions.SecurityAction>.

 [!code-csharp[FxCop.Security.CA2142.TransparentMethodsShouldNotBeProtectedWithLinkDemands#1](../code-quality/codesnippet/CSharp/ca2142-transparent-code-should-not-be-protected-with-linkdemands_1.cs)]

 Não suprima um aviso nessa regra.