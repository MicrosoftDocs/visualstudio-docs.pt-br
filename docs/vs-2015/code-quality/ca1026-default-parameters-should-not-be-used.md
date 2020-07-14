---
title: 'CA1026: os parâmetros padrão não devem ser usados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1026
- DefaultParametersShouldNotBeUsed
helpviewer_keywords:
- CA1026
- DefaultParametersShouldNotBeUsed
ms.assetid: 09643415-36ef-4d0f-9411-5721e14e2512
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a63d6e788dd1722d0c593469b225a4f1aeb4738d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548429"
---
# <a name="ca1026-default-parameters-should-not-be-used"></a>CA1026: Parâmetros padrão não devem ser usados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DefaultParametersShouldNotBeUsed|
|CheckId|CA1026|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo visível externamente contém um método visível externamente que usa um parâmetro padrão.

## <a name="rule-description"></a>Descrição da Regra
 Os métodos que usam parâmetros padrão são permitidos no Common Language Specification (CLS); no entanto, o CLS permite que os compiladores ignorem os valores atribuídos a esses parâmetros. O código que é escrito para compiladores que ignoram valores de parâmetro padrão deve fornecer explicitamente argumentos para cada parâmetro padrão. Para manter o comportamento que você deseja em linguagens de programação, os métodos que usam parâmetros padrão devem ser substituídos por sobrecargas de método que fornecem os parâmetros padrão.

 O compilador ignora os valores dos parâmetros padrão para a extensão gerenciada para C++ quando ele acessa o código gerenciado. O compilador Visual Basic dá suporte a métodos que têm parâmetros padrão que usam a palavra-chave [opcional](https://msdn.microsoft.com/library/4571ce88-a539-4115-b230-54eb277c6aa7) .

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, substitua o método que usa parâmetros padrão com sobrecargas de método que fornecem os parâmetros padrão.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que usa parâmetros padrão e os métodos sobrecarregados que fornecem uma funcionalidade equivalente.

 [!code-vb[FxCop.Design.DefaultParameters#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DefaultParameters/vb/FxCop.Design.DefaultParameters.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1025: Substituir argumentos repetitivos por matriz de parâmetros](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md)

## <a name="see-also"></a>Consulte Também
 [Componentes de independência de linguagem e componentes independentes da linguagem](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)
