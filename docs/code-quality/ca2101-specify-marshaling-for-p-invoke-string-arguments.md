---
title: 'CA2101: especifique o marshaling para argumentos de cadeia de caracteres de P-Invoke'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyMarshalingForPInvokeStringArguments
- CA2101
helpviewer_keywords:
- CA2101
- SpecifyMarshalingForPInvokeStringArguments
ms.assetid: 9d1abfc3-d320-41e0-9f6e-60cefe6ffe1b
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 21b3ab30ff6672149fe05359f33ad932706a8a91
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49867306"
---
# <a name="ca2101-specify-marshaling-for-pinvoke-string-arguments"></a>CA2101: especificar marshaling para argumentos da cadeia de caracteres P/Invoke

|||
|-|-|
|NomeDoTipo|SpecifyMarshalingForPInvokeStringArguments|
|CheckId|CA2101|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Uma invocação de plataforma permite chamadores parcialmente confiáveis, o membro tem um parâmetro de cadeia de caracteres e não realizar marshaling explicitamente a cadeia de caracteres.

## <a name="rule-description"></a>Descrição da regra
 Quando você converte de Unicode para ANSI, é possível que nem todos os caracteres Unicode podem ser representados em uma página de código ANSI específica. *Mapeamento de melhor ajuste* tenta resolver esse problema substituindo um caractere para o caractere que não pode ser representado. O uso desse recurso pode causar uma vulnerabilidade de segurança potencial porque não é possível controlar o caractere que é escolhido. Por exemplo, um código mal-intencionado pode criar uma cadeia de caracteres Unicode que contém caracteres que não são encontrados em uma página de código em particular, que são convertidos em caracteres especiais do sistema de arquivos, como intencionalmente '.. ' ou '/'. Observe também que as verificações de segurança para caracteres especiais com frequência ocorrerem antes que a cadeia de caracteres é convertida em ANSI.

 Mapeamento de melhor ajuste é o padrão para a conversão não gerenciado, WChar para MByte. A menos que você desabilita explicitamente o mapeamento de melhor ajuste, seu código pode conter uma vulnerabilidade de segurança explorável por causa desse problema.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, explicitamente realizar marshaling de tipos de dados de cadeia de caracteres.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que viola essa regra e, em seguida, mostra como corrigir a violação.

 [!code-csharp[FxCop.Security.PinvokeAnsiUnicode#1](../code-quality/codesnippet/CSharp/ca2101-specify-marshaling-for-p-invoke-string-arguments_1.cs)]