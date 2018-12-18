---
title: 'CA2101: Especificar marshaling para argumentos de cadeia de caracteres P-Invoke | Microsoft Docs'
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
ms.openlocfilehash: ffe39953f36ee8af31611bca8ce8d390f102b085
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49813843"
---
# <a name="ca2101-specify-marshaling-for-pinvoke-string-arguments"></a>CA2101: especificar marshaling para argumentos da cadeia de caracteres P/Invoke
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



