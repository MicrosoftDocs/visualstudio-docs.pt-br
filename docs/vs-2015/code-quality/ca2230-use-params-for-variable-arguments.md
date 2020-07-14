---
title: 'CA2230: usar params para argumentos de variável | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseParamsForVariableArguments
- CA2230
helpviewer_keywords:
- CA2230
- UseParamsForVariableArguments
ms.assetid: bf98b733-4855-4110-9f16-eba5a9e79421
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ce66e04272618b9df2ab1957af305bb9bf40ee9c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540355"
---
# <a name="ca2230-use-params-for-variable-arguments"></a>CA2230: Usar parâmetros para argumentos variáveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|UseParamsForVariableArguments|
|CheckId|CA2230|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido contém um método público ou protegido que usa a `VarArgs` Convenção de chamada.

## <a name="rule-description"></a>Descrição da Regra
 A `VarArgs` Convenção de chamada é usada com determinadas definições de método que usam um número variável de parâmetros. Um método que usa a `VarArgs` Convenção de chamada não é compatível com CLS (Common Language Specification) e pode não estar acessível em linguagens de programação.

 No C#, a `VarArgs` Convenção de chamada é usada quando a lista de parâmetros de um método termina com a `__arglist` palavra-chave. Visual Basic não oferece suporte à `VarArgs` Convenção de chamada e Visual C++ permite seu uso somente em código não gerenciado que usa a `...` notação de elipse.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra em C#, use a palavra-chave [params](https://msdn.microsoft.com/library/1690815e-b52b-4967-8380-5780aff08012) em vez de `__arglist` .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra dois métodos, um que viola a regra e outra que satisfaz a regra.

 [!code-csharp[FxCop.Usage.UseParams#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.UseParams/cs/FxCop.Usage.UseParams.cs#1)]

## <a name="see-also"></a>Consulte Também
 <xref:System.Reflection.CallingConventions?displayProperty=fullName>[Independência de idioma e componentes independentes de linguagem](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)
