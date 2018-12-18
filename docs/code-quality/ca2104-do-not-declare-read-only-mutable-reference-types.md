---
title: 'CA2104: não declarar tipos de referência mutáveis somente leitura'
ms.date: 11/01/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDeclareReadOnlyMutableReferenceTypes
- CA2104
helpviewer_keywords:
- CA2104
- DoNotDeclareReadOnlyMutableReferenceTypes
ms.assetid: 81b83ee5-4db5-4be0-9f8d-90b53894ec3b
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 13f1c4f19349d94cb7dedfd22a82dc86b6f33b5b
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50967069"
---
# <a name="ca2104-do-not-declare-read-only-mutable-reference-types"></a>CA2104: não declarar tipos de referência mutáveis somente leitura

|||
|-|-|
|NomeDoTipo|DoNotDeclareReadOnlyMutableReferenceTypes|
|CheckId|CA2104|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não são significativas|

> [!NOTE]
> CA2104 regra está obsoleto e será removido em uma versão futura do Visual Studio.

## <a name="cause"></a>Causa

Um tipo visível externamente contém um campo somente leitura visível externamente que é um tipo de referência mutável.

## <a name="rule-description"></a>Descrição da regra

Um tipo mutável é um tipo cujos dados da instância podem ser modificados. O <xref:System.Text.StringBuilder?displayProperty=fullName> classe é um exemplo de um tipo de referência mutável. Ele contém membros que podem alterar o valor de uma instância da classe. Um exemplo de um tipo de referência imutável é o <xref:System.String?displayProperty=fullName> classe. Depois que tiver sido instanciado, seu valor nunca pode ser alterados.

O modificador somente leitura ([readonly](/dotnet/csharp/language-reference/keywords/readonly) em C#, [ReadOnly](/dotnet/visual-basic/language-reference/modifiers/readonly) no Visual Basic, e [const](/cpp/cpp/const-cpp) em C++) em um tipo de referência campo (ou o ponteiro em C++) impede que o campo de que está sendo substituído por uma instância diferente do tipo de referência. No entanto, o modificador não impede que os dados da instância do campo que está sendo modificado por meio do tipo de referência.

Essa regra pode inadvertidamente mostrar uma violação para um tipo que é, na verdade, imutáveis. Nesse caso, é seguro suprimir o aviso.

Campos de matriz somente leitura são isentos dessa regra, mas em vez disso, causar uma violação do [CA2105: campos de matriz não devem ser somente leitura](../code-quality/ca2105-array-fields-should-not-be-read-only.md) regra.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, remova o modificador somente leitura ou, se uma alteração significativa é aceitável, substitua o campo com um tipo imutável.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso nessa regra, se o tipo de campo é imutável.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra uma declaração de campo que faz com que uma violação dessa regra:

[!code-cpp[FxCop.Security.MutableReferenceTypes#1](../code-quality/codesnippet/CPP/ca2104-do-not-declare-read-only-mutable-reference-types_1.cpp)]
[!code-csharp[FxCop.Security.MutableReferenceTypes#1](../code-quality/codesnippet/CSharp/ca2104-do-not-declare-read-only-mutable-reference-types_1.cs)]
[!code-vb[FxCop.Security.MutableReferenceTypes#1](../code-quality/codesnippet/VisualBasic/ca2104-do-not-declare-read-only-mutable-reference-types_1.vb)]