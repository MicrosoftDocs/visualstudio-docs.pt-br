---
title: 'CA2205: Usar equivalentes gerenciados da API do Win32'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UseManagedEquivalentsOfWin32Api
- CA2205
helpviewer_keywords:
- UseManagedEquivalentsOfWin32Api
- CA2205
ms.assetid: 1c65ab59-3e50-4488-a727-3969c7f6cbe4
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 6481bbcca68c7471e4f25c7629e3b55fa407d175
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231713"
---
# <a name="ca2205-use-managed-equivalents-of-win32-api"></a>CA2205: Usar equivalentes gerenciados da API do Win32

|||
|-|-|
|NomeDoTipo|UseManagedEquivalentsOfWin32Api|
|CheckId|CA2205|
|Categoria|Microsoft.Usage|
|Alteração significativa|Sem interrupção|

## <a name="cause"></a>Causa

Um método de invocação de plataforma é definido e um método com a funcionalidade equivalente existe no .NET.

## <a name="rule-description"></a>Descrição da regra

Um método de invocação de plataforma é usado para chamar uma função DLL não gerenciada e é <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> definido usando o atributo `Declare` ou a palavra-chave em Visual Basic. Um método de invocação de plataforma definido incorretamente pode levar a exceções de tempo de execução devido a problemas como uma função de nome incorreta, mapeamento com falha de parâmetros e tipos de dados de valor de retorno, e especificações de campo incorretas, como a Convenção de chamada e o caractere Definição. Se disponível, é mais simples e menos propenso a erros chamar o método equivalente gerenciado do que definir e chamar o método não gerenciado diretamente. Chamar um método de plataforma Invoke também pode levar a problemas de segurança adicionais que precisam ser resolvidos.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, substitua a chamada à função não gerenciada por uma chamada para seu equivalente gerenciado.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Suprimir um aviso dessa regra se o método de substituição sugerido não fornecer a funcionalidade necessária.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra uma definição de método de invocação de plataforma que viola a regra. Além disso, as chamadas para o método de invocação de plataforma e o método gerenciado equivalente são mostradas.

[!code-csharp[FxCop.Usage.ManagedEquivalents#1](../code-quality/codesnippet/CSharp/ca2205-use-managed-equivalents-of-win32-api_1.cs)]
[!code-vb[FxCop.Usage.ManagedEquivalents#1](../code-quality/codesnippet/VisualBasic/ca2205-use-managed-equivalents-of-win32-api_1.vb)]

## <a name="related-rules"></a>Regras relacionadas

- [CA1404: Chamar GetLastError imediatamente após P/Invoke](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md)
- [CA1060: Mover P/Invokes para a classe NativeMethods](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)
- [CA1400: Os pontos de entrada P/Invoke devem existir](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)
- [CA1401: P/Invokes não devem ser visíveis](../code-quality/ca1401-p-invokes-should-not-be-visible.md)
- [CA2101: Especificar o marshaling para argumentos de cadeia de caracteres P/Invoke](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)