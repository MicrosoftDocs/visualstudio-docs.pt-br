---
title: 'CA2230: Usar parâmetros para argumentos variáveis'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UseParamsForVariableArguments
- CA2230
helpviewer_keywords:
- CA2230
- UseParamsForVariableArguments
ms.assetid: bf98b733-4855-4110-9f16-eba5a9e79421
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b3318a9f5bd65c6b9514519936cc52e037e0c215
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55944982"
---
# <a name="ca2230-use-params-for-variable-arguments"></a>CA2230: Usar parâmetros para argumentos variáveis

|||
|-|-|
|NomeDoTipo|UseParamsForVariableArguments|
|CheckId|CA2230|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido contém um método público ou protegido que usa o `VarArgs` convenção de chamada.

## <a name="rule-description"></a>Descrição da regra
 O `VarArgs` convenção de chamada é usada com determinadas definições de método que levam a um número variável de parâmetros. Um método usando o `VarArgs` convenção de chamada não é Common Language Specification (CLS) em conformidade e pode não estar acessível em linguagens de programação.

 No C#, o `VarArgs` convenção de chamada é usada quando a lista de parâmetros do método termina com o `__arglist` palavra-chave. Visual Basic não oferece suporte a `VarArgs` convenção de chamada e Visual C++ permite que seu uso apenas em código não gerenciado que usa a elipse `...` notação.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra no C#, use o [params](/dotnet/csharp/language-reference/keywords/params) palavra-chave, em vez de `__arglist`.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra dois métodos, um que viola a regra e um que satisfaz a regra.

 [!code-csharp[FxCop.Usage.UseParams#1](../code-quality/codesnippet/CSharp/ca2230-use-params-for-variable-arguments_1.cs)]

## <a name="see-also"></a>Consulte também

- <xref:System.Reflection.CallingConventions?displayProperty=fullName>
- [Componentes de independência de linguagem e componentes independentes da linguagem](/dotnet/standard/language-independence-and-language-independent-components)