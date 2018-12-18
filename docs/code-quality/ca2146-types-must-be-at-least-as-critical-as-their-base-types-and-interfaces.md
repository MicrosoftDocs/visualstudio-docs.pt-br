---
title: 'CA2146: tipos devem ser pelo menos críticos como tipos base e interfaces'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2146
ms.assetid: 241fb784-1f6b-46e5-8ceb-c438e341d38e
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8f0550061102c7f785dfe69d1505801a60648e9b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49895893"
---
# <a name="ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces"></a>CA2146: tipos devem ser pelo menos críticos como tipos base e interfaces

|||
|-|-|
|NomeDoTipo|TypesMustBeAtLeastAsCriticalAsBaseTypes|
|CheckId|CA2146|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo transparente é derivado de um tipo que é marcado com o <xref:System.Security.SecuritySafeCriticalAttribute> ou o <xref:System.Security.SecurityCriticalAttribute>, ou um tipo que é marcado com o <xref:System.Security.SecuritySafeCriticalAttribute> atributo é derivado de um tipo que é marcado com o <xref:System.Security.SecurityCriticalAttribute> atributo.

## <a name="rule-description"></a>Descrição da regra
 Esta regra é acionada quando um tipo derivado tem um atributo de transparência de segurança que não é tão crítico quanto seu tipo de base ou interface implementada. Apenas os tipos críticos podem derivar os tipos de base críticos ou implementar interfaces críticos, e apenas os tipos críticos ou de segurança crítica podem derivar dos tipos de base críticos de segurança ou implementar interfaces críticas de segurança. As violações desta regra de transparência de nível 2 resultam em um <xref:System.TypeLoadException> para o tipo derivado.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir essa violação, marque o tipo derivado ou implementação com um atributo de transparência é pelo menos tão crítico como o tipo base ou interface.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 [!code-csharp[FxCop.Security.CA2146.TypesMustBeAtLeastAsCriticalAsBaseTypes#1](../code-quality/codesnippet/CSharp/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces_1.cs)]