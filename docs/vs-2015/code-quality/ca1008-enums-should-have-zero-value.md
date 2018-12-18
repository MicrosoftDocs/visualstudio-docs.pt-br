---
title: 'CA1008: Enums devem ter valor zero | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CA1008
- EnumsShouldHaveZeroValue
helpviewer_keywords:
- CA1008
- EnumsShouldHaveZeroValue
ms.assetid: 3503a73c-360c-416d-8ee4-c2aa44365a05
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 69e60b0f2ee8106b04507722f1b3094e1bbdbbc8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49874820"
---
# <a name="ca1008-enums-should-have-zero-value"></a>CA1008: os enums devem ter valor zero
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|EnumsShouldHaveZeroValue|
|CheckId|CA1008|
|Categoria|Microsoft.Design|
|Alteração Significativa|Separação de não - quando você for solicitado a adicionar um **None** valor para uma enumeração de sinalizador de não. Quebrando - quando você for solicitado a renomear ou remover quaisquer valores de enumeração.|

## <a name="cause"></a>Causa
 Uma enumeração sem um aplicado <xref:System.FlagsAttribute?displayProperty=fullName> não define um membro que tem um valor de zero; ou uma enumeração que tem um aplicadas <xref:System.FlagsAttribute> define um membro que tem um valor de zero, mas seu nome não for 'None' ou a enumeração define vários com valor zero membros.

## <a name="rule-description"></a>Descrição da Regra
 O valor padrão de uma enumeração não inicializada, assim como outros tipos de valor é zero. Uma enumeração não flags−attributed deve definir um membro que tenha o valor de zero para que o valor padrão é um valor válido da enumeração. Se apropriado, o membro nome 'None'. Caso contrário, atribua zero para o membro usado com mais frequência. Observe que, por padrão, se o valor do primeiro membro da enumeração não está definido na declaração, seu valor é zero.

 Se uma enumeração que tem o <xref:System.FlagsAttribute> aplicado define um membro com valor de zero, seu nome deve ser 'None' para indicar que não há valores foram definidos na enumeração. Usando um membro com valor zero para qualquer outra finalidade é diferente da finalidade o uso da <xref:System.FlagsAttribute> em que o AND e ou operadores bit a bit são inúteis com o membro. Isso significa que somente um membro deve ser atribuído o valor zero. Observe que, se vários membros que têm o valor zero ocorre em uma enumeração de sinalizadores atribuída, `Enum.ToString()` retorna resultados incorretos para os membros que não são zero.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra para enumerações não flags−attributed, definir um membro que tem o valor de zero. Essa é uma alteração sem interrupções. Para enumerações atribuído de sinalizadores que definem um membro com valor de zero, nomeie esse membro 'None' e excluir outros membros que têm um valor igual a zero; Isso é uma alteração significativa.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra, exceto para as enumerações atribuído de sinalizadores que foram enviados anteriormente.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra duas enumerações que atendem à regra e uma enumeração, `BadTraceOptions`, que viola a regra.

 [!code-cpp[FxCop.Design.EnumsZeroValue#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumsZeroValue/cpp/FxCop.Design.EnumsZeroValue.cpp#1)]
 [!code-csharp[FxCop.Design.EnumsZeroValue#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumsZeroValue/cs/FxCop.Design.EnumsZeroValue.cs#1)]
 [!code-vb[FxCop.Design.EnumsZeroValue#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.EnumsZeroValue/vb/FxCop.Design.EnumsZeroValue.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2217: não marcar enums com FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

 [CA1700: não nomear valores de enum como 'Reservados'](../code-quality/ca1700-do-not-name-enum-values-reserved.md)

 [CA1712: não usar valores de enum como prefixo com o nome do tipo](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)

 [CA1028: o armazenamento de enum deve ser Int32](../code-quality/ca1028-enum-storage-should-be-int32.md)

 [CA1027: marcar enums com FlagsAttribute](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>Consulte também
 <xref:System.Enum?displayProperty=fullName>



