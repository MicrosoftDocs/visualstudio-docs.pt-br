---
title: 'CA1404: chame GetLastError imediatamente após o P-Invoke'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CallGetLastErrorImmediatelyAfterPInvoke
- CA1404
helpviewer_keywords:
- CallGetLastErrorImmediatelyAfterPInvoke
- CA1404
ms.assetid: 52ae9eff-50f9-4b2f-8039-ca7e49fba88e
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 4e9a339a4b665f892c3e3e63c77ba0dee5891df8
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45552036"
---
# <a name="ca1404-call-getlasterror-immediately-after-pinvoke"></a>CA1404: chamar GetLastError logo depois de P/Invoke

|||
|-|-|
|NomeDoTipo|CallGetLastErrorImmediatelyAfterPInvoke|
|CheckId|CA1404|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa

É feita uma chamada para o <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A?displayProperty=fullName> método ou o equivalente Win32 `GetLastError` função e a chamada que vem imediatamente antes, não seja uma plataforma de invocação de método.

## <a name="rule-description"></a>Descrição da regra
 Uma plataforma de chamar código não gerenciado do método acessos e é definido usando o `Declare` palavra-chave na [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ou o <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> atributo. Em geral, em caso de falha, funções não gerenciadas chamam Win32 `SetLastError` função para definir um código de erro que está associado com a falha. O chamador da função com falha chamadas Win32 `GetLastError` função para recuperar o código de erro e determinar a causa da falha. O código de erro é mantido em uma base por thread e é substituído pela próxima chamada para `SetLastError`. Depois que uma chamada para uma plataforma com falha invocar o método, o código gerenciado pode recuperar o código de erro chamando o <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> método. Como o código de erro pode ser substituído por chamadas internas de outros métodos de biblioteca de classe gerenciada, o `GetLastError` ou <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> método deve ser chamado imediatamente após a chamada de método de invocação de plataforma.

 A regra ignora chamadas para os seguintes membros gerenciados quando eles ocorrem entre a chamada para a plataforma de invocação de método e a chamada para <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A>. Esses membros não alteram o erro de código e são úteis para determinar o sucesso de alguma plataforma invocam chamadas de método.

- <xref:System.IntPtr.Zero?displayProperty=fullName>

- <xref:System.IntPtr.op_Equality%2A?displayProperty=fullName>

- <xref:System.IntPtr.op_Inequality%2A?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.SafeHandle.IsInvalid%2A?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, mova a chamada para <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> para que fique imediatamente após a chamada para a plataforma de invocação de método.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, se o código entre a plataforma de invocar a chamada de método e o <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> chamada de método não pode implicitamente ou explicitamente fazem com que o código de erro alterar.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que viola a regra e um método que satisfaz a regra.

 [!code-vb[FxCop.Interoperability.LastErrorPInvoke#1](../code-quality/codesnippet/VisualBasic/ca1404-call-getlasterror-immediately-after-p-invoke_1.vb)]
 [!code-csharp[FxCop.Interoperability.LastErrorPInvoke#1](../code-quality/codesnippet/CSharp/ca1404-call-getlasterror-immediately-after-p-invoke_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1060: mover P/Invokes para a classe NativeMethods](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)

 [CA1400: os pontos de entrada de P-Invoke devem existir](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)

 [CA1401: os P/Invokes não devem estar visíveis](../code-quality/ca1401-p-invokes-should-not-be-visible.md)

 [CA2101: especificar marshaling para argumentos de cadeia de caracteres P/Invoke](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

 [CA2205: usar equivalentes gerenciados da API do Win32](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md)