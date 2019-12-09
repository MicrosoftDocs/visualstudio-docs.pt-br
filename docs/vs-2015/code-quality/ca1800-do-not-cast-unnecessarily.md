---
title: 'CA1800: não converter desnecessariamente | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1800
- DoNotCastUnnecessarily
helpviewer_keywords:
- DoNotCastUnnecessarily
- CA1800
ms.assetid: b79a010a-6627-421e-8955-6007e32fa808
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 466309cef8905faa9b659e2d3652975d815767fb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663101"
---
# <a name="ca1800-do-not-cast-unnecessarily"></a>CA1800: não converter desnecessariamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotCastUnnecessarily|
|CheckId|CA1800|
|Categoria|Microsoft. performance|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método executa conversões duplicadas em um de seus argumentos ou variáveis locais. Para uma análise completa por essa regra, o assembly testado deve ser criado usando informações de depuração e o arquivo de banco de dados do programa (. pdb) associado deve estar disponível.

## <a name="rule-description"></a>Descrição da Regra
 As conversões duplicadas diminui o desempenho, especialmente quando as conversões são realizadas em instruções de iteração compactas. Para operações de conversão duplicadas explícitas, armazene o resultado da conversão em uma variável local e use a variável local em vez das operações de conversão duplicadas.

 Se o C# operador `is` for usado para testar se a conversão terá sucesso antes da execução da conversão real, considere testar o resultado do operador `as` em vez disso. Isso fornece a mesma funcionalidade sem a operação de conversão implícita que é executada pelo operador `is`.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, modifique a implementação do método para minimizar o número de operações de conversão.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra ou ignorar completamente a regra, se o desempenho não for uma preocupação.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que viola a regra usando o C# operador `is`. Um segundo método satisfaz a regra substituindo o operador `is` por um teste em relação ao resultado do operador `as`, o que diminui o número de operações de conversão por iteração de duas para uma.

 [!code-csharp[FxCop.Performance.UnnecessaryCastsAsIs#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCastsAsIs/cs/FxCop.Performance.UnnecessaryCastsAsIs.cs#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método, `start_Click`, que tem várias conversões explícitas duplicadas, que violam a regra e um método, `reset_Click`, que satisfaz a regra armazenando a conversão em uma variável local.

 [!code-csharp[FxCop.Performance.UnnecessaryCasts#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCasts/cs/FxCop.Performance.UnnecessaryCasts.cs#1)]
 [!code-vb[FxCop.Performance.UnnecessaryCasts#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.UnnecessaryCasts/vb/FxCop.Performance.UnnecessaryCasts.vb#1)]

## <a name="see-also"></a>Consulte também
 [como](https://msdn.microsoft.com/library/a9be126b-cbf4-4990-a70d-d0e1983cad0e) [está](https://msdn.microsoft.com/library/bc62316a-d41f-4f90-8300-c6f4f0556e43)
