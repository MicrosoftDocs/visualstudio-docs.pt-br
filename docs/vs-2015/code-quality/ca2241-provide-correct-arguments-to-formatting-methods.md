---
title: 'CA2241: Fornecer argumentos corretos para métodos de formatação | Microsoft Docs'
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
- CA2241
- Provide correct arguments to formatting methods
- ProvideCorrectArgumentsToFormattingMethods
helpviewer_keywords:
- ProvideCorrectArgumentsToFormattingMethods
- CA2241
ms.assetid: 83639bc4-4c91-4a07-a40e-dc5e49a84494
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: d66e6c8efed7847420a4abc1773a9514ef44074f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49884934"
---
# <a name="ca2241-provide-correct-arguments-to-formatting-methods"></a>CA2241: fornecer argumentos corretos para métodos de formatação
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ProvideCorrectArgumentsToFormattingMethods|
|CheckId|CA2241|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 O `format` argumento passado para um método, como de cadeia de caracteres <xref:System.Console.WriteLine%2A>, <xref:System.Console.Write%2A>, ou <xref:System.String.Format%2A?displayProperty=fullName> não contém um item de formato que corresponde a cada argumento de objeto, ou vice-versa.

## <a name="rule-description"></a>Descrição da Regra
 Os argumentos para métodos como <xref:System.Console.WriteLine%2A>, <xref:System.Console.Write%2A>, e <xref:System.String.Format%2A> consistem em uma cadeia de formato, seguida por várias <xref:System.Object?displayProperty=fullName> instâncias. A cadeia de caracteres de formato consiste em texto e itens de formato inserido no formato {índice [, alinhamento] [: formatString]}. 'index' é um inteiro baseado em zero que indica qual dos objetos a serem formatados. Se um objeto não tem um índice correspondente na cadeia de caracteres de formato, o objeto será ignorado. Se o objeto especificado por 'index' não existe, um <xref:System.FormatException?displayProperty=fullName> é gerada em tempo de execução.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, forneça um item de formato para cada argumento de objeto e fornecer um argumento de objeto para cada item de formato.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra dois violações da regra.

 [!code-csharp[FxCop.Usage.FormattingArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.FormattingArguments/cs/FxCop.Usage.FormattingArguments.cs#1)]
 [!code-vb[FxCop.Usage.FormattingArguments#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.FormattingArguments/vb/FxCop.Usage.FormattingArguments.vb#1)]



