---
title: 'CA1060: mova os P-Invokes para a classe NativeMethods'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MovePInvokesToNativeMethodsClass
- CA1060
helpviewer_keywords:
- MovePInvokesToNativeMethodsClass
- CA1060
ms.assetid: 06686c8c-6ad3-42f7-a355-cbaefa347cfc
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: bf3e3f01eb6decb1ac2705655675455485bceb5b
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45551945"
---
# <a name="ca1060-move-pinvokes-to-nativemethods-class"></a>CA1060: mover P/Invokes para a classe NativeMethods

|||
|-|-|
|NomeDoTipo|MovePInvokesToNativeMethodsClass|
|CheckId|CA1060|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Um método usa os serviços de invocação de plataforma para acessar código não gerenciado e não é um membro de um dos **NativeMethods** classes.

## <a name="rule-description"></a>Descrição da regra

Métodos de invocação de plataforma, como aqueles que são marcados com o uso de <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> atributo ou métodos que são definidos usando o `Declare` palavra-chave em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], acessar código não gerenciado. Esses métodos devem ser em uma das seguintes classes:

- **NativeMethods** -essa classe não suprime as movimentações de pilha para permissão de código não gerenciado. (<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> não deve ser aplicada a essa classe.) Essa classe é para os métodos que podem ser usados em qualquer lugar, porque uma movimentação de pilha será executada.

- **SafeNativeMethods** -essa classe suprime as movimentações de pilha para permissão de código não gerenciado. (<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> é aplicada a essa classe.) Essa classe é para os métodos que são seguros chamar qualquer pessoa. Chamadores desses métodos não são necessárias para executar uma revisão de segurança completa para certificar-se de que o uso é seguro porque os métodos são inofensivos para qualquer chamador.

- **UnsafeNativeMethods** -essa classe suprime as movimentações de pilha para permissão de código não gerenciado. (<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> é aplicada a essa classe.) Essa classe é para os métodos que são potencialmente perigosos. Qualquer chamador desses métodos deve executar uma revisão de segurança completa para certificar-se de que o uso é seguro porque nenhuma movimentação de pilha será executada.

Essas classes são declaradas como `internal` (`Friend`, no Visual Basic) e declarar um construtor particular para impedir que novas instâncias que está sendo criado. Os métodos nessas classes devem estar `static` e `internal` (`Shared` e `Friend` no Visual Basic).

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, o método move ao apropriado **NativeMethods** classe. Para a maioria dos aplicativos, mover P/Invokes para uma nova classe chamada **NativeMethods** é suficiente.

 No entanto, se você estiver desenvolvendo bibliotecas para uso em outros aplicativos, você deve considerar definir duas outras classes que são chamados **SafeNativeMethods** e **UnsafeNativeMethods**. Essas classes se parecer com o **NativeMethods** classe; no entanto, eles são marcados por meio de um atributo especial chamado **SuppressUnmanagedCodeSecurityAttribute**. Quando esse atributo é aplicado, o tempo de execução não executará uma movimentação de pilha completa para certificar-se de que todos os chamadores tenham a **UnmanagedCode** permissão. Normalmente, o tempo de execução verifica essa permissão na inicialização. Porque não é possível executar a verificação, ele bastante pode melhorar o desempenho de chamadas para esses métodos não gerenciados, ele também permite que o código que tem permissões limitadas para chamar esses métodos.

 No entanto, você deve usar esse atributo com muito cuidado. Ele pode ter sérias implicações de segurança se for implementado incorretamente...

 Para obter informações sobre como implementar os métodos, consulte o **NativeMethods** exemplo, **SafeNativeMethods** exemplo, e **UnsafeNativeMethods** exemplo.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir declara um método que viola essa regra. Para corrigir a violação, o **RemoveDirectory** P/Invoke devem ser movido para uma classe adequada que foi desenvolvida para manter somente P/Invokes.

 [!code-vb[FxCop.Design.DllImportNativeMethods#1](../code-quality/codesnippet/VisualBasic/ca1060-move-p-invokes-to-nativemethods-class_1.vb)]
 [!code-csharp[FxCop.Design.DllImportNativeMethods#1](../code-quality/codesnippet/CSharp/ca1060-move-p-invokes-to-nativemethods-class_1.cs)]

## <a name="nativemethods-example"></a>Exemplo de NativeMethods

### <a name="description"></a>Descrição
 Porque o **NativeMethods** classe não deve ser marcado com o uso **SuppressUnmanagedCodeSecurityAttribute**, P/Invokes são colocados nele exigirá **UnmanagedCode** permissão. Como a maioria dos aplicativos executados do computador local e executar com confiança total, isso geralmente não é um problema. No entanto, se você estiver desenvolvendo bibliotecas reutilizáveis, você deve considerar definir um **SafeNativeMethods** ou **UnsafeNativeMethods** classe.

 A exemplo a seguir mostra uma **Interaction.Beep** método que encapsula o **MessageBeep** função em user32.dll. O **MessageBeep** P/Invoke é colocado na **NativeMethods** classe.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.NativeMethods#1](../code-quality/codesnippet/CSharp/ca1060-move-p-invokes-to-nativemethods-class_2.cs)]
 [!code-vb[FxCop.Design.NativeMethods#1](../code-quality/codesnippet/VisualBasic/ca1060-move-p-invokes-to-nativemethods-class_2.vb)]

## <a name="safenativemethods-example"></a>Exemplo de SafeNativeMethods

### <a name="description"></a>Descrição
 Métodos P/Invoke, que podem ser expostos com segurança para qualquer aplicativo e que não têm efeitos colaterais devem ser colocados em uma classe chamada **SafeNativeMethods**. Você não precisa solicitar permissões e não é necessário prestar muita atenção à qual eles são chamados de.

 A exemplo a seguir mostra uma **TickCount** propriedade que encapsula o **GetTickCount** função de kernel32.dll.

### <a name="code"></a>Código
 [!code-vb[FxCop.Design.NativeMethodsSafe#1](../code-quality/codesnippet/VisualBasic/ca1060-move-p-invokes-to-nativemethods-class_3.vb)]
 [!code-csharp[FxCop.Design.NativeMethodsSafe#1](../code-quality/codesnippet/CSharp/ca1060-move-p-invokes-to-nativemethods-class_3.cs)]

## <a name="unsafenativemethods-example"></a>Exemplo de UnsafeNativeMethods

### <a name="description"></a>Descrição
 Métodos P/Invoke, que não pode ser chamado com segurança e que pode causar efeitos colaterais devem ser colocados em uma classe chamada **UnsafeNativeMethods**. Esses métodos devem ser verificados rigorosamente para certificar-se de que eles não são expostos ao usuário inadvertidamente. A regra [CA2118: revisar uso de SuppressUnmanagedCodeSecurityAttribute](../code-quality/ca2118-review-suppressunmanagedcodesecurityattribute-usage.md) pode ajudar com isso. Como alternativa, os métodos devem ter outra permissão que é exigida em vez de **UnmanagedCode** quando usá-los.

 A exemplo a seguir mostra uma **Cursor.Hide** método que encapsula o **ShowCursor** função em user32.dll.

### <a name="code"></a>Código
 [!code-vb[FxCop.Design.NativeMethodsUnsafe#1](../code-quality/codesnippet/VisualBasic/ca1060-move-p-invokes-to-nativemethods-class_4.vb)]
 [!code-csharp[FxCop.Design.NativeMethodsUnsafe#1](../code-quality/codesnippet/CSharp/ca1060-move-p-invokes-to-nativemethods-class_4.cs)]

## <a name="see-also"></a>Consulte também

- [Avisos de design](../code-quality/design-warnings.md)