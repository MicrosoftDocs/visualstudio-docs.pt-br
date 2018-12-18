---
title: 'CA2142: o código transparente não deve ser protegido com LinkDemands'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2142
ms.assetid: 6dc59053-5dd9-4583-bf10-5f339107e59f
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4ce7243630179aede0ce20aba998f6cb5eed0100
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49887157"
---
# <a name="ca2142-transparent-code-should-not-be-protected-with-linkdemands"></a>CA2142: o código transparente não deve ser protegido com LinkDemands

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