---
title: 'CA2205: usar equivalentes gerenciados da API do Win32'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
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
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 8c88feb35a4699770b7a05a266168e0c3ad347e4
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47860103"
---
# <a name="ca2205-use-managed-equivalents-of-win32-api"></a>CA2205: usar equivalentes gerenciados da API do Win32

|||
|-|-|
|NomeDoTipo|UseManagedEquivalentsOfWin32Api|
|CheckId|CA2205|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Uma invocação de plataforma método é definido e um método com a funcionalidade equivalente existe na biblioteca de classes do .NET Framework.

## <a name="rule-description"></a>Descrição da regra

Uma plataforma de invocação de método é usado para chamar uma função DLL não gerenciada e é definida usando o <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> atributo, ou o `Declare` palavra-chave no Visual Basic. Método de invocação de uma plataforma definida incorretamente pode resultar em exceções de tempo de execução devido a problemas como uma função equivocado, com defeito de mapeamento de tipos de dados de valor de parâmetro e retorno e especificações de campo incorreto, como a convenção de chamada e o caractere Defina. Se estiver disponível, é mais simples e menos propenso a chamar o método gerenciado equivalente que to definir e chamar o método não gerenciado diretamente. Chamando uma plataforma de invocar o método também podem levar a problemas de segurança adicionais que precisam ser resolvidos.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, substitua a chamada para a função não gerenciada por uma chamada para seu equivalente gerenciado.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Suprima um aviso nessa regra, se o método de substituição sugerida não fornece a funcionalidade necessária.

## <a name="example"></a>Exemplo

A exemplo a seguir mostra uma plataforma de invocação de definição do método que viola a regra. Além disso, as chamadas para a plataforma de invocação de método e o método gerenciado equivalente são mostrados.

[!code-csharp[FxCop.Usage.ManagedEquivalents#1](../code-quality/codesnippet/CSharp/ca2205-use-managed-equivalents-of-win32-api_1.cs)]
[!code-vb[FxCop.Usage.ManagedEquivalents#1](../code-quality/codesnippet/VisualBasic/ca2205-use-managed-equivalents-of-win32-api_1.vb)]

## <a name="related-rules"></a>Regras relacionadas

- [CA1404: chamar GetLastError logo depois de P/Invoke](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md)
- [CA1060: mover P/Invokes para a classe NativeMethods](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)
- [CA1400: os pontos de entrada de P-Invoke devem existir](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)
- [CA1401: os P/Invokes não devem estar visíveis](../code-quality/ca1401-p-invokes-should-not-be-visible.md)
- [CA2101: especificar marshaling para argumentos de cadeia de caracteres P/Invoke](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)