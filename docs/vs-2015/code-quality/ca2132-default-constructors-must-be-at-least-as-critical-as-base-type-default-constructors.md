---
title: 'CA2132: construtores padrão devem ser pelo menos tão críticos quanto os construtores padrão de tipo base | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2132
ms.assetid: e758afa1-8bde-442a-8a0a-bd1ea7b0ce4d
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 401aa6f5ebec4dac99bedba6f12478c7c48d1dc5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540810"
---
# <a name="ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors"></a>CA2132: Construtores padrão devem ser pelo menos tão críticos quanto construtores padrão do tipo base
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DefaultConstructorsMustHaveConsistentTransparency|
|CheckId|CA2132|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

> [!NOTE]
> Esse aviso é aplicado somente ao código que está executando o CoreCLR (a versão do CLR que é específica para aplicativos Web do Silverlight).

## <a name="cause"></a>Causa
 O atributo Transparency do construtor padrão de uma classe derivada não é tão crítico quanto a transparência da classe base.

## <a name="rule-description"></a>Descrição da Regra
 Tipos e membros que <xref:System.Security.SecurityCriticalAttribute> não podem ser usados pelo código do aplicativo do Silverlight. Os tipos de segurança crítica e os membros só podem ser usados por código confiável no .NET Framework para a biblioteca de classes do Silverlight. Como uma construção pública ou protegida em uma classe derivada deve ter a mesma transparência maior que sua classe base, uma classe em um aplicativo não pode ser derivada de uma classe marcada como SecurityCritical.

 Para o código de plataforma do CoreCLR, se um tipo base tiver um construtor padrão público ou não Transparent protegido, o tipo derivado deverá obedecer às regras de herança de construtor padrão. O tipo derivado também deve ter um construtor padrão e esse construtor deve ser, pelo menos, como construtor padrão crítico do tipo base.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir a violação, remova o tipo ou não derive do tipo de segurança não transparente.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir avisos desta regra. As violações dessa regra pelo código do aplicativo resultarão na recusa do CoreCLR para carregar o tipo com um <xref:System.TypeLoadException> .

### <a name="code"></a>Código
 [!code-csharp[FxCop.Security.CA2132.DefaultConstructorsMustHaveConsistentTransparency#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2132.defaultconstructorsmusthaveconsistenttransparency/cs/ca2132 - defaultconstructorsmusthaveconsistenttransparency.cs#1)]

### <a name="comments"></a>Comentários
