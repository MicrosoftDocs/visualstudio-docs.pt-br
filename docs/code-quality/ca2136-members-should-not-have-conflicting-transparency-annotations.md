---
title: 'CA2136: os membros não devem ter anotações de transparência conflitantes'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2127
- SecurityTransparentAssembliesShouldNotContainSecurityCriticalCode
- CA2136
helpviewer_keywords:
- SecurityTransparentAssembliesShouldNotContainSecurityCriticalCode
- CA2127
ms.assetid: ff5a1d18-7c52-4da5-8990-60be83a8ea81
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 90970ca6be894719ea53ff6af725118626a52f20
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49903654"
---
# <a name="ca2136-members-should-not-have-conflicting-transparency-annotations"></a>CA2136: os membros não devem ter anotações de transparência conflitantes

|||
|-|-|
|NomeDoTipo|TransparencyAnnotationsShouldNotConflict|
|CheckId|CA2136|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Essa regra é acionada quando um membro de tipo é marcado com um <xref:System.Security> atributo de segurança que tem uma transparência diferente que o atributo de segurança de um contêiner do membro.

## <a name="rule-description"></a>Descrição da regra
 Os atributos de transparência são aplicados com base nos elementos de código de escopo maior a elementos de escopo menor. Os atributos de transparência dos elementos de código com escopo maior têm precedência sobre atributos de transparência dos elementos de código contidos no primeiro elemento. Por exemplo, uma classe que é marcada com o <xref:System.Security.SecurityCriticalAttribute> atributo não pode conter um método que é marcado com o <xref:System.Security.SecuritySafeCriticalAttribute> atributo.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir essa violação, remova o atributo de segurança do elemento de código que tem o menor escopo ou alterar seu atributo para ser o mesmo que o elemento de código que contém.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima avisos dessa regra.

## <a name="example"></a>Exemplo
 No exemplo a seguir, um método é marcado com o <xref:System.Security.SecuritySafeCriticalAttribute> atributo e é um membro de uma classe que é marcado com o <xref:System.Security.SecurityCriticalAttribute> atributo. O atributo de segurança de segurança deve ser removido.

 [!code-csharp[FxCop.Security.CA2136.TransparencyAnnotationsShouldNotConflict#1](../code-quality/codesnippet/CSharp/ca2136-members-should-not-have-conflicting-transparency-annotations_1.cs)]