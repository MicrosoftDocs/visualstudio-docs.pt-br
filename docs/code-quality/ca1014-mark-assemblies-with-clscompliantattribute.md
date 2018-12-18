---
title: 'CA1014: marcar assemblies com CLSCompliantAttribute'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1014
- MarkAssembliesWithClsCompliant
helpviewer_keywords:
- CA1014
- MarkAssembliesWithClsCompliant
ms.assetid: 4fe57449-cf45-4745-bcd2-6345f1ed266d
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 3375d3a88a9776190887252cff7c2f9accb5fd4e
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547273"
---
# <a name="ca1014-mark-assemblies-with-clscompliantattribute"></a>CA1014: marcar assemblies com CLSCompliantAttribute

|||
|-|-|
|NomeDoTipo|MarkAssembliesWithClsCompliant|
|CheckId|CA1014|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um assembly não tem o <xref:System.CLSCompliantAttribute?displayProperty=fullName> atributo aplicado a ele.

## <a name="rule-description"></a>Descrição da regra
 A CLS (Common Language Specification) define restrições de nomenclatura, tipos de dados e regras que assemblies deverão respeitar se forem usados em todas as linguagens de programação. Um bom design determina que todos os assemblies indiquem explicitamente a conformidade com CLS com <xref:System.CLSCompliantAttribute>. Se o atributo não estiver presente em um assembly, o assembly não está em conformidade.

 É possível que um assembly compatível com CLS contêm tipos ou membros que não estão em conformidade de tipo.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, adicione o atributo ao assembly. Em vez de todo o assembly como não compatível de marcação, você deve determinar o tipo ou membros de tipo não estão em conformidade e marcam esses elementos como tal. Se possível, você deve fornecer uma alternativa compatível com CLS para membros não compatíveis para que o maior público possível possa acessar toda a funcionalidade do seu assembly.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra. Se você não quiser que o assembly esteja em conformidade, aplique o atributo e defina seu valor como `false`.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um assembly que tem o <xref:System.CLSCompliantAttribute?displayProperty=fullName> atributo aplicado que o declara compatíveis com CLS.

 [!code-csharp[FxCop.Design.AssembliesCls#1](../code-quality/codesnippet/CSharp/ca1014-mark-assemblies-with-clscompliantattribute_1.cs)]
 [!code-cpp[FxCop.Design.AssembliesCls#1](../code-quality/codesnippet/CPP/ca1014-mark-assemblies-with-clscompliantattribute_1.cpp)]
 [!code-vb[FxCop.Design.AssembliesCls#1](../code-quality/codesnippet/VisualBasic/ca1014-mark-assemblies-with-clscompliantattribute_1.vb)]

## <a name="see-also"></a>Consulte também

- <xref:System.CLSCompliantAttribute?displayProperty=fullName>
- [Componentes de independência de linguagem e componentes independentes da linguagem](/dotnet/standard/language-independence-and-language-independent-components)