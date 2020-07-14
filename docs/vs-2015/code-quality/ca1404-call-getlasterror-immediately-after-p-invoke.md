---
title: 'CA1404: chamar GetLastError imediatamente após P-Invoke | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CallGetLastErrorImmediatelyAfterPInvoke
- CA1404
helpviewer_keywords:
- CallGetLastErrorImmediatelyAfterPInvoke
- CA1404
ms.assetid: 52ae9eff-50f9-4b2f-8039-ca7e49fba88e
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 54ac9a4d56136d9e981ae038a0b219aa4cb4774e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544489"
---
# <a name="ca1404-call-getlasterror-immediately-after-pinvoke"></a>CA1404: chamar GetLastError logo depois de P/Invoke
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|CallGetLastErrorImmediatelyAfterPInvoke|
|CheckId|CA1404|
|Categoria|Microsoft. Interoperability|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 É feita uma chamada ao <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A?displayProperty=fullName> método ou à função Win32 equivalente `GetLastError` , e a chamada que vem imediatamente antes não é para um método de invocação de plataforma.

## <a name="rule-description"></a>Descrição da Regra
 Um método de invocação de plataforma acessa código não gerenciado e é definido usando a `Declare` palavra-chave in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ou o <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> atributo. Geralmente, após a falha, as funções não gerenciadas chamam a função do Win32 `SetLastError` para definir um código de erro associado à falha. O chamador da função com falha chama a função do Win32 `GetLastError` para recuperar o código de erro e determinar a causa da falha. O código de erro é mantido por thread e é substituído pela próxima chamada para `SetLastError` . Depois de uma chamada para um método de invocação de plataforma com falha, o código gerenciado pode recuperar o código de erro chamando o <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> método. Como o código de erro pode ser substituído por chamadas internas de outros métodos de biblioteca de classes gerenciadas, o `GetLastError` <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> método ou deve ser chamado imediatamente após a chamada de método de invocação de plataforma.

 A regra ignora chamadas para os seguintes membros gerenciados quando eles ocorrem entre a chamada para o método de invocação de plataforma e a chamada para <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> . Esses membros não alteram o código de erro e são úteis para determinar o sucesso de algumas chamadas de método de invocação de plataforma.

- <xref:System.IntPtr.Zero?displayProperty=fullName>

- <xref:System.IntPtr.op_Equality%2A?displayProperty=fullName>

- <xref:System.IntPtr.op_Inequality%2A?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.SafeHandle.IsInvalid%2A?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, mova a chamada para para <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> que ela imediatamente siga a chamada para o método de invocação de plataforma.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o código entre a chamada de método da plataforma Invoke e a <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> chamada do método não puder explicitamente ou implicitamente fazer com que o código de erro seja alterado.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que viola a regra e um método que satisfaz a regra.

 [!code-csharp[FxCop.Interoperability.LastErrorPInvoke#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LastErrorPInvoke/cs/FxCop.Interoperability.LastErrorPInvoke.cs#1)]
 [!code-vb[FxCop.Interoperability.LastErrorPInvoke#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LastErrorPInvoke/vb/FxCop.Interoperability.LastErrorPInvoke.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1060: mover P/Invokes para a classe NativeMethods](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)

 [CA1400: os pontos de entrada P/Invoke devem existir](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)

 [CA1401: P/Invokes não devem estar visíveis](../code-quality/ca1401-p-invokes-should-not-be-visible.md)

 [CA2101: especificar o marshaling para argumentos de cadeia de caracteres P/Invoke](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

 [CA2205: Usar equivalentes gerenciados da API do Win32](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md)
