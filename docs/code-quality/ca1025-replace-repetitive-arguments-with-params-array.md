---
title: 'CA1025: substituir argumentos repetitivos por matriz de parâmetros'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1025
- ReplaceRepetitiveArgumentsWithParamsArray
helpviewer_keywords:
- ReplaceRepetitiveArgumentsWithParamsArray
- CA1025
ms.assetid: f009b340-dea3-4459-8fe1-2143aa8b5d0b
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 027ec9b19bcf8a4a10e8b973b86e57be2dbc6be7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49838316"
---
# <a name="ca1025-replace-repetitive-arguments-with-params-array"></a>CA1025: substituir argumentos repetitivos por matriz de parâmetros

|||
|-|-|
|NomeDoTipo|ReplaceRepetitiveArgumentsWithParamsArray|
|CheckId|CA1025|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um método público ou protegido em um tipo público tem mais de três parâmetros e seus três últimos parâmetros são do mesmo tipo.

## <a name="rule-description"></a>Descrição da regra
 Use uma matriz de parâmetros em vez de argumentos repetidos, quando o número exato de argumentos é desconhecido e os argumentos variáveis forem do mesmo tipo, ou podem ser passados como o mesmo tipo. Por exemplo, o <xref:System.Console.WriteLine%2A> método fornece uma sobrecarga de uso geral que usa uma matriz de parâmetros para aceitar qualquer número de <xref:System.Object> argumentos.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, substitua os argumentos repetidos com uma matriz de parâmetros.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É sempre seguro suprimir um aviso nessa regra; No entanto, esse design pode causar problemas de usabilidade.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra.

 [!code-csharp[FxCop.Design.RepeatArgs#1](../code-quality/codesnippet/CSharp/ca1025-replace-repetitive-arguments-with-params-array_1.cs)]