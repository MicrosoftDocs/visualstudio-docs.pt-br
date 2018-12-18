---
title: 'CA2241: fornecer argumentos corretos para métodos de formatação'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2241
- Provide correct arguments to formatting methods
- ProvideCorrectArgumentsToFormattingMethods
helpviewer_keywords:
- ProvideCorrectArgumentsToFormattingMethods
- CA2241
ms.assetid: 83639bc4-4c91-4a07-a40e-dc5e49a84494
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 6ef5b2f3b7244762e69d87882cbf2caae63cb34b
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547874"
---
# <a name="ca2241-provide-correct-arguments-to-formatting-methods"></a>CA2241: fornecer argumentos corretos para métodos de formatação

|||
|-|-|
|NomeDoTipo|ProvideCorrectArgumentsToFormattingMethods|
|CheckId|CA2241|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 O `format` argumento passado para um método, como de cadeia de caracteres <xref:System.Console.WriteLine%2A>, <xref:System.Console.Write%2A>, ou <xref:System.String.Format%2A?displayProperty=fullName> não contém um item de formato que corresponde a cada argumento de objeto, ou vice-versa.

## <a name="rule-description"></a>Descrição da regra
 Os argumentos para métodos como <xref:System.Console.WriteLine%2A>, <xref:System.Console.Write%2A>, e <xref:System.String.Format%2A> consistem em uma cadeia de formato, seguida por várias <xref:System.Object?displayProperty=fullName> instâncias. A cadeia de caracteres de formato consiste em texto e itens de formato inserido no formato {índice [, alinhamento] [: formatString]}. 'index' é um inteiro baseado em zero que indica qual dos objetos a serem formatados. Se um objeto não tem um índice correspondente na cadeia de caracteres de formato, o objeto será ignorado. Se o objeto especificado por 'index' não existe, um <xref:System.FormatException?displayProperty=fullName> é gerada em tempo de execução.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, forneça um item de formato para cada argumento de objeto e fornecer um argumento de objeto para cada item de formato.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra dois violações da regra.

 [!code-vb[FxCop.Usage.FormattingArguments#1](../code-quality/codesnippet/VisualBasic/ca2241-provide-correct-arguments-to-formatting-methods_1.vb)]
 [!code-csharp[FxCop.Usage.FormattingArguments#1](../code-quality/codesnippet/CSharp/ca2241-provide-correct-arguments-to-formatting-methods_1.cs)]