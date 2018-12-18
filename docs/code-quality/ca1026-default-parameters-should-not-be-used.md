---
title: 'CA1026: parâmetros padrão não devem ser usados'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1026
- DefaultParametersShouldNotBeUsed
helpviewer_keywords:
- CA1026
- DefaultParametersShouldNotBeUsed
ms.assetid: 09643415-36ef-4d0f-9411-5721e14e2512
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ec4a248be45489eafcbd208329a52cfc06d8237f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49825306"
---
# <a name="ca1026-default-parameters-should-not-be-used"></a>CA1026: parâmetros padrão não devem ser usados

|||
|-|-|
|NomeDoTipo|DefaultParametersShouldNotBeUsed|
|CheckId|CA1026|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo visível externamente contém um método visível externamente que usa um parâmetro padrão.

## <a name="rule-description"></a>Descrição da regra
 Métodos que usam parâmetros padrão são permitidos sob o Common Language Specification (CLS); No entanto, a CLS permite que os compiladores para ignorar os valores que são atribuídos a esses parâmetros. Código que é escrito para os compiladores que ignoram valores de parâmetro padrão deve fornecer explicitamente os argumentos para cada parâmetro padrão. Para manter o comportamento desejado em todas as linguagens de programação, os métodos que usam parâmetros padrão devem ser substituídos com sobrecargas de método que forneçam os parâmetros padrão.

 O compilador ignora os valores de parâmetros padrão para a extensão gerenciadas para C++ quando acessa o código gerenciado. O compilador do Visual Basic dá suporte a métodos com parâmetros padrão que usam o [opcional](/dotnet/visual-basic/language-reference/modifiers/optional) palavra-chave.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, substitua o método que usa os parâmetros padrão com sobrecargas de método que fornecem os parâmetros padrão.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que usa os parâmetros padrão e os métodos sobrecarregados que fornecem uma funcionalidade equivalente.

 [!code-vb[FxCop.Design.DefaultParameters#1](../code-quality/codesnippet/VisualBasic/ca1026-default-parameters-should-not-be-used_1.vb)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1025: substituir argumentos repetitivos por matriz de parâmetros](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md)

## <a name="see-also"></a>Consulte também
 [Componentes de independência de linguagem e componentes independentes da linguagem](/dotnet/standard/language-independence-and-language-independent-components)