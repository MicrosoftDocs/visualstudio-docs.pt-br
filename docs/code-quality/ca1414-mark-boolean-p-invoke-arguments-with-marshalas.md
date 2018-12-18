---
title: 'CA1414: marque os argumentos P-Invoke boolianos com MarshalAs'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1414
- MarkBooleanPInvokeArgumentsWithMarshalAs
helpviewer_keywords:
- CA1414
- MarkBooleanPInvokeArgumentsWithMarshalAs
ms.assetid: c0c84cf5-7701-4897-9114-66fc4b895699
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: a5936c07646201ab3988dd7cc792f758ed698063
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45548946"
---
# <a name="ca1414-mark-boolean-pinvoke-arguments-with-marshalas"></a>CA1414: marcar argumentos P/Invoke boolianos com MarshalAs

|||
|-|-|
|NomeDoTipo|MarkBooleanPInvokeArgumentsWithMarshalAs|
|CheckId|CA1414|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Uma plataforma de invocação de método de declaração inclui um <xref:System.Boolean?displayProperty=fullName> parâmetro ou valor retornado, mas o <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=fullName> atributo não é aplicado ao valor de parâmetro ou retornado.

## <a name="rule-description"></a>Descrição da regra
 Uma plataforma de chamar código não gerenciado do método acessos e é definido usando o `Declare` palavra-chave na [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ou o <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>. <xref:System.Runtime.InteropServices.MarshalAsAttribute> Especifica o comportamento de marshaling que é usado para converter tipos de dados entre código gerenciado e não gerenciado. Tipos de muitos dados simples, como <xref:System.Byte?displayProperty=fullName> e <xref:System.Int32?displayProperty=fullName>, ter uma única representação em código não gerenciado e não exigem a especificação de seu comportamento de marshaling; o common language runtime fornece o comportamento correto automaticamente.

 O <xref:System.Boolean> tipo de dados tem várias representações em código não gerenciado. Quando o <xref:System.Runtime.InteropServices.MarshalAsAttribute> não for especificado, o padrão de empacotamento de comportamento para o <xref:System.Boolean> tipo de dados é <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>. Isso é um inteiro de 32 bits, que não é apropriado em todas as circunstâncias. A representação de booliana é necessário para o método não gerenciado deve ser determinada e combinada para apropriado <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>. UnmanagedType.Bool é o tipo BOOL Win32, que é sempre de 4 bytes. UnmanagedType.U1 deve ser usado para C++ `bool` ou outros tipos de 1 byte.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, aplique <xref:System.Runtime.InteropServices.MarshalAsAttribute> para o <xref:System.Boolean> parâmetro ou valor retornado. Defina o valor do atributo como apropriado <xref:System.Runtime.InteropServices.UnmanagedType>.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra. Mesmo se o comportamento de marshaling padrão é apropriado, o código mais facilmente é mantido quando o comportamento é especificado explicitamente.

## <a name="example"></a>Exemplo

A exemplo a seguir mostra os métodos que são marcados com os devidos a invocação de plataforma <xref:System.Runtime.InteropServices.MarshalAsAttribute> atributos.

 [!code-csharp[FxCop.Interoperability.BoolMarshalAs#1](../code-quality/codesnippet/CSharp/ca1414-mark-boolean-p-invoke-arguments-with-marshalas_1.cs)]
 [!code-vb[FxCop.Interoperability.BoolMarshalAs#1](../code-quality/codesnippet/VisualBasic/ca1414-mark-boolean-p-invoke-arguments-with-marshalas_1.vb)]
 [!code-cpp[FxCop.Interoperability.BoolMarshalAs#1](../code-quality/codesnippet/CPP/ca1414-mark-boolean-p-invoke-arguments-with-marshalas_1.cpp)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1901: as declarações P/Invoke devem ser portáteis](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)

 [CA2101: especificar marshaling para argumentos de cadeia de caracteres P/Invoke](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>
- [Interoperação com código não gerenciado](/dotnet/framework/interop/index)