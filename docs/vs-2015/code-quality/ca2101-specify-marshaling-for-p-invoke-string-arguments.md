---
title: 'CA2101: especificar o marshaling para argumentos de cadeia de caracteres P-Invoke | Microsoft Docs'
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ae65e922d1b4946300155bbf148abac574a2ec2a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544372"
---
# <a name="ca2101-specify-marshaling-for-pinvoke-string-arguments"></a>CA2101: especificar marshaling para argumentos da cadeia de caracteres P/Invoke
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|SpecifyMarshalingForPInvokeStringArguments|
|CheckId|CA2101|
|Categoria|Microsoft. Globalization|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um membro de invocação de plataforma permite chamadores parcialmente confiáveis, tem um parâmetro de cadeia de caracteres e não empacota explicitamente a cadeia de caracteres.

## <a name="rule-description"></a>Descrição da Regra
 Quando você converte de Unicode para ANSI, é possível que nem todos os caracteres Unicode possam ser representados em uma página de código ANSI específica. O *mapeamento de melhor ajuste* tenta resolver esse problema, substituindo um caractere para o caractere que não pode ser representado. O uso desse recurso pode causar uma possível vulnerabilidade de segurança porque você não pode controlar o caractere escolhido. Por exemplo, um código mal-intencionado poderia criar intencionalmente uma cadeia de caracteres Unicode que contenha personagens que não foram encontrados em uma página de código específica, que são convertidas em caracteres especiais do sistema de arquivos, como '.. ' ou '/'. Observe também que as verificações de segurança de caracteres especiais ocorrem com frequência antes que a cadeia de caracteres seja convertida em ANSI.

 O mapeamento de melhor ajuste é o padrão para a conversão não gerenciada, WChar para MByte. A menos que você desabilite explicitamente o mapeamento de melhor ajuste, seu código pode conter uma vulnerabilidade de segurança explorável devido a esse problema.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, desempacotar explicitamente os tipos de dados de cadeia de caracteres.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que viola essa regra e, em seguida, mostra como corrigir a violação.

 [!code-csharp[FxCop.Security.PinvokeAnsiUnicode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PinvokeAnsiUnicode/cs/FxCop.Security.PinvokeAnsiUnicode.cs#1)]
