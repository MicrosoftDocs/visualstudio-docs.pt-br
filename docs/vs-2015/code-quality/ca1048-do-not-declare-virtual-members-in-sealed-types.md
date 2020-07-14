---
title: 'CA1048: não declarar membros virtuais em tipos lacrados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDeclareVirtualMembersInSealedTypes
- CA1048
helpviewer_keywords:
- DoNotDeclareVirtualMembersInSealedTypes
- CA1048
ms.assetid: 5dcf4a30-6f98-48a8-b8cc-7b89ea757262
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 19ae3a4fdc620343f18aa0845c33e1d73529adfe
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546790"
---
# <a name="ca1048-do-not-declare-virtual-members-in-sealed-types"></a>CA1048: Não declarar membros virtuais em tipos selados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotDeclareVirtualMembersInSealedTypes|
|CheckId|CA1048|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público é lacrado e declara um método que é ambos `virtual` ( `Overridable` em Visual Basic) e não final. Essa regra não relata violações para tipos delegados, que devem seguir esse padrão.

## <a name="rule-description"></a>Descrição da Regra
 Os tipos declaram métodos como virtuais de forma que a herança de tipos possa substituir a implementação do método virtual. Por definição, você não pode herdar de um tipo lacrado, tornando um método virtual em um tipo lacrado sem sentido.

 Os compiladores Visual Basic .NET e C# não permitem que os tipos violem essa regra.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, torne o método não virtual ou torne o tipo herdável.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. Deixar o tipo em seu estado atual pode causar problemas de manutenção e não fornece nenhum benefício.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra.

 [!code-cpp[FxCop.Design.SealedVirtual#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.SealedVirtual/cpp/FxCop.Design.SealedVirtual.cpp#1)]
