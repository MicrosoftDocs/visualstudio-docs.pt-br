---
title: 'CA2143: Métodos transparentes não devem usar demandas de segurança | Microsoft Docs'
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
- CA2143
ms.assetid: 5d3923d7-cf40-4512-bc5c-0db0e0d6e25a
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: bdce17c529193848d1e68cf44e006470e0965151
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49879604"
---
# <a name="ca2143-transparent-methods-should-not-use-security-demands"></a>CA2143: os métodos transparentes não devem usar demandas de segurança
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|TransparentMethodsShouldNotDemand|
|CheckId|CA2143|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo transparente ou método declarativamente é marcado com um <xref:System.Security.Permissions.SecurityAction?displayProperty=fullName> `.Demand` demanda ou o método chama o <xref:System.Security.CodeAccessPermission.Demand%2A?displayProperty=fullName> método.

## <a name="rule-description"></a>Descrição da Regra
 O código transparente de segurança não deve ser responsável por verificar a segurança de uma operação e, assim, não deve exigir permissões. O código transparente de segurança deve usar demandas completas para tomar decisões de segurança e o código crítico de segurança não deve confiar no código transparente para fazer a demanda completa. Qualquer código que executa verificações de segurança, como demandas de segurança, em vez disso, deve ser seguro-crítica.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Em geral, para corrigir uma violação dessa regra, marque o método com o <xref:System.Security.SecuritySafeCriticalAttribute> atributo. Você também pode remover a demanda.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 A regra de arquivos com o código a seguir como um método transparente faz uma exigência de segurança declarativa.

 [!code-csharp[FxCop.Security.CA2143.TransparentMethodsShouldNotDemand#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2143.transparentmethodsshouldnotdemand/cs/ca2143 - transparentmethodsshouldnotdemand.cs#1)]

## <a name="see-also"></a>Consulte também
 [CA2142: código transparente não deve ser protegido com LinkDemands](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md)



