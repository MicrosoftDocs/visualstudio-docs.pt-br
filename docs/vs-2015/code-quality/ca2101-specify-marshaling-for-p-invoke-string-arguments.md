---
title: 'CA2101: Especificar marshaling para argumentos de cadeia de caracteres P-Invoke | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyMarshalingForPInvokeStringArguments
- CA2101
helpviewer_keywords:
- CA2101
- SpecifyMarshalingForPInvokeStringArguments
ms.assetid: 9d1abfc3-d320-41e0-9f6e-60cefe6ffe1b
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 11916609f2efa9c0b6e208548ba51795bd276015
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58923557"
---
# <a name="ca2101-specify-marshaling-for-pinvoke-string-arguments"></a>CA2101: Especificar marshaling para argumentos de cadeias de caracteres P/Invoke
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|SpecifyMarshalingForPInvokeStringArguments|
|CheckId|CA2101|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Uma invocação de plataforma permite chamadores parcialmente confiáveis, o membro tem um parâmetro de cadeia de caracteres e não realizar marshaling explicitamente a cadeia de caracteres.

## <a name="rule-description"></a>Descrição da Regra
 Quando você converte de Unicode para ANSI, é possível que nem todos os caracteres Unicode podem ser representados em uma página de código ANSI específica. *Mapeamento de melhor ajuste* tenta resolver esse problema substituindo um caractere para o caractere que não pode ser representado. O uso desse recurso pode causar uma vulnerabilidade de segurança potencial porque não é possível controlar o caractere que é escolhido. Por exemplo, um código mal-intencionado pode criar uma cadeia de caracteres Unicode que contém caracteres que não são encontrados em uma página de código em particular, que são convertidos em caracteres especiais do sistema de arquivos, como intencionalmente '.. ' ou '/'. Observe também que as verificações de segurança para caracteres especiais com frequência ocorrerem antes que a cadeia de caracteres é convertida em ANSI.

 Mapeamento de melhor ajuste é o padrão para a conversão não gerenciado, WChar para MByte. A menos que você desabilita explicitamente o mapeamento de melhor ajuste, seu código pode conter uma vulnerabilidade de segurança explorável por causa desse problema.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, explicitamente realizar marshaling de tipos de dados de cadeia de caracteres.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que viola essa regra e, em seguida, mostra como corrigir a violação.

 [!code-csharp[FxCop.Security.PinvokeAnsiUnicode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PinvokeAnsiUnicode/cs/FxCop.Security.PinvokeAnsiUnicode.cs#1)]
