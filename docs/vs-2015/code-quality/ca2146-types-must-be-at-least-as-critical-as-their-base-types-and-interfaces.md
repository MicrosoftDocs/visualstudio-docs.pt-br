---
title: 'CA2146: os tipos devem ser pelo menos tão críticos quanto seus tipos de base e interfaces | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2146
ms.assetid: 241fb784-1f6b-46e5-8ceb-c438e341d38e
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2316d6e555fa091d26392aee71b774489c81a379
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546387"
---
# <a name="ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces"></a>CA2146: Os tipos devem ser pelo menos tão críticos quanto seus tipos base e interfaces
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|TypesMustBeAtLeastAsCriticalAsBaseTypes|
|CheckId|CA2146|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo transparente é derivado de um tipo que é marcado com o <xref:System.Security.SecuritySafeCriticalAttribute> ou o <xref:System.Security.SecurityCriticalAttribute> , ou um tipo marcado com o <xref:System.Security.SecuritySafeCriticalAttribute> atributo é derivado de um tipo que é marcado com o <xref:System.Security.SecurityCriticalAttribute> atributo.

## <a name="rule-description"></a>Descrição da Regra
 Esta regra é acionada quando um tipo derivado tem um atributo de transparência de segurança que não é tão crítico quanto seu tipo de base ou interface implementada. Apenas os tipos críticos podem derivar os tipos de base críticos ou implementar interfaces críticos, e apenas os tipos críticos ou de segurança crítica podem derivar dos tipos de base críticos de segurança ou implementar interfaces críticas de segurança. As violações dessa regra na transparência de nível 2 resultam em um <xref:System.TypeLoadException> para o tipo derivado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir essa violação, marque o tipo derivado ou de implementação com um atributo de transparência que seja pelo menos tão crítico quanto o tipo base ou a interface.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 [!code-csharp[FxCop.Security.CA2146.TypesMustBeAtLeastAsCriticalAsBaseTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2146.typesmustbeatleastascriticalasbasetypes/cs/ca2146 - typesmustbeatleastascriticalasbasetypes.cs#1)]
