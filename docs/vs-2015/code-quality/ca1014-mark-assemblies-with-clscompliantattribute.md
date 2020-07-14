---
title: 'CA1014: Marcar assemblies com o CLSCompliantAttribute | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1014
- MarkAssembliesWithClsCompliant
helpviewer_keywords:
- CA1014
- MarkAssembliesWithClsCompliant
ms.assetid: 4fe57449-cf45-4745-bcd2-6345f1ed266d
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c6dc131a2bb5f0c54943213fbb42561a0c72d95c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545464"
---
# <a name="ca1014-mark-assemblies-with-clscompliantattribute"></a>CA1014: Marcar assemblies com CLSCompliantAttribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|MarkAssembliesWithClsCompliant|
|CheckId|CA1014|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um assembly não tem o <xref:System.CLSCompliantAttribute?displayProperty=fullName> atributo aplicado a ele.

## <a name="rule-description"></a>Descrição da Regra
 A CLS (Common Language Specification) define restrições de nomenclatura, tipos de dados e regras que assemblies deverão respeitar se forem usados em todas as linguagens de programação. Um bom design dita que todos os assemblies indicam explicitamente a conformidade com CLS com <xref:System.CLSCompliantAttribute> . Se o atributo não estiver presente em um assembly, o assembly não será compatível.

 É possível que um assembly em conformidade com CLS contenha tipos ou membros de tipo que não estejam em conformidade.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione o atributo ao assembly. Em vez de marcar o assembly inteiro como não compatível, você deve determinar quais tipos ou membros de tipo não são compatíveis e marcar esses elementos como tal. Se possível, você deve fornecer uma alternativa em conformidade com CLS para membros não compatíveis para que o público mais amplo possível acesse toda a funcionalidade do seu assembly.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. Se você não quiser que o assembly esteja em conformidade, aplique o atributo e defina seu valor como `false` .

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um assembly que tem o <xref:System.CLSCompliantAttribute?displayProperty=fullName> atributo aplicado que declara em conformidade com CLS.

 [!code-cpp[FxCop.Design.AssembliesCls#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCls/cpp/FxCop.Design.AssembliesCls.cpp#1)]
 [!code-csharp[FxCop.Design.AssembliesCls#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCls/cs/FxCop.Design.AssembliesCls.cs#1)]
 [!code-vb[FxCop.Design.AssembliesCls#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCls/vb/FxCop.Design.AssembliesCls.vb#1)]

## <a name="see-also"></a>Consulte Também
 <xref:System.CLSCompliantAttribute?displayProperty=fullName>[Independência de idioma e componentes independentes de linguagem](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)
