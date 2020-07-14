---
title: 'CA1025: substituir argumentos repetitivos por matriz params | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1025
- ReplaceRepetitiveArgumentsWithParamsArray
helpviewer_keywords:
- ReplaceRepetitiveArgumentsWithParamsArray
- CA1025
ms.assetid: f009b340-dea3-4459-8fe1-2143aa8b5d0b
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 84809341d7898aeb3defe0447f2a2f1142eb460a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546621"
---
# <a name="ca1025-replace-repetitive-arguments-with-params-array"></a>CA1025: Substituir argumentos repetitivos por matriz de parâmetros
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ReplaceRepetitiveArgumentsWithParamsArray|
|CheckId|CA1025|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método público ou protegido em um tipo público tem mais de três parâmetros, e seus últimos três parâmetros são do mesmo tipo.

## <a name="rule-description"></a>Descrição da Regra
 Use uma matriz de parâmetros em vez de argumentos repetidos quando o número exato de argumentos for desconhecido e os argumentos da variável forem do mesmo tipo, ou podem ser passados como o mesmo tipo. Por exemplo, o <xref:System.Console.WriteLine%2A> método fornece uma sobrecarga de finalidade geral que usa uma matriz de parâmetros para aceitar qualquer número de <xref:System.Object> argumentos.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, substitua os argumentos repetidos por uma matriz de parâmetros.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É sempre seguro suprimir um aviso dessa regra; no entanto, esse design pode causar problemas de usabilidade.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra.

 [!code-csharp[FxCop.Design.RepeatArgs#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.RepeatArgs/cs/FxCop.Design.RepeatArgs.cs#1)]
