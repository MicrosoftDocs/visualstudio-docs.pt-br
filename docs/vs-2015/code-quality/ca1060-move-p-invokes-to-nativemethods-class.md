---
title: 'CA1060: mover P-invoca para a classe NativeMethods | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MovePInvokesToNativeMethodsClass
- CA1060
helpviewer_keywords:
- MovePInvokesToNativeMethodsClass
- CA1060
ms.assetid: 06686c8c-6ad3-42f7-a355-cbaefa347cfc
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e01ad9fc4fc57917c123404d8863d04240585793
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533426"
---
# <a name="ca1060-move-pinvokes-to-nativemethods-class"></a>CA1060: mover P/Invokes para a classe NativeMethods
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|MovePInvokesToNativeMethodsClass|
|CheckId|CA1060|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método usa serviços de invocação de plataforma para acessar código não gerenciado e não é membro de uma das classes **NativeMethods** .

## <a name="rule-description"></a>Descrição da Regra
 Métodos de invocação de plataforma, como aqueles que são marcados usando o <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> atributo ou métodos que são definidos usando a `Declare` palavra-chave no [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] , acessam código não gerenciado. Esses métodos devem estar em uma das seguintes classes:

- **NativeMethods** -essa classe não suprime as movimentações de pilha para a permissão de código não gerenciado. ( <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> não deve ser aplicado a esta classe.) Essa classe é para métodos que podem ser usados em qualquer lugar, pois uma movimentação de pilha será executada.

- **SafeNativeMethods** -essa classe suprime as movimentações de pilha para a permissão de código não gerenciado. ( <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> é aplicado a esta classe.) Essa classe é para métodos que são seguros para qualquer pessoa chamar. Os chamadores desses métodos não são necessários para executar uma revisão de segurança completa para garantir que o uso seja seguro, pois os métodos são inofensivos para qualquer chamador.

- **UnsafeNativeMethods** -essa classe suprime as movimentações de pilha para a permissão de código não gerenciado. ( <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> é aplicado a esta classe.) Essa classe é para métodos que são potencialmente perigosos. Qualquer chamador desses métodos deve executar uma revisão de segurança completa para garantir que o uso seja seguro, pois nenhuma movimentação de pilha será executada.

  Essas classes são declaradas como `internal` ( `Friend` , em Visual Basic) e declaram um Construtor privado para impedir que novas instâncias sejam criadas. Os métodos nessas classes devem ser `static` e `internal` ( `Shared` e `Friend` em Visual Basic).

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, mova o método para a classe **NativeMethods** apropriada. Para a maioria dos aplicativos, mover P/Invokes para uma nova classe denominada **NativeMethods** é suficiente.

 No entanto, se você estiver desenvolvendo bibliotecas para uso em outros aplicativos, considere definir duas outras classes que são chamadas **SafeNativeMethods** e **UnsafeNativeMethods**. Essas classes se assemelham à classe **NativeMethods** ; no entanto, elas são marcadas usando um atributo especial chamado **SuppressUnmanagedCodeSecurityAttribute**. Quando esse atributo é aplicado, o tempo de execução não executa uma movimentação de pilha completa para garantir que todos os chamadores tenham a permissão **UnmanagedCode** . O tempo de execução normalmente verifica essa permissão na inicialização. Como a verificação não é executada, ela pode melhorar muito o desempenho de chamadas para esses métodos não gerenciados, além de permitir o código que tem permissões limitadas para chamar esses métodos.

 No entanto, você deve usar esse atributo com muito cuidado. Ela poderá ter implicações de segurança sérias se ela for implementada incorretamente.

 Para obter informações sobre como implementar os métodos, consulte o exemplo de **NativeMethods** , o exemplo de **SafeNativeMethods** e o exemplo de **UnsafeNativeMethods** .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir declara um método que viola essa regra. Para corrigir a violação, o **RemoveDirectory** P/Invoke deve ser movido para uma classe apropriada que foi projetada para manter apenas P/Invokes.

 [!code-csharp[FxCop.Design.DllImportNativeMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.DllImportNativeMethods/cs/FxCop.Design.DllImportNativeMethods.cs#1)]
 [!code-vb[FxCop.Design.DllImportNativeMethods#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DllImportNativeMethods/vb/FxCop.Design.DllImportNativeMethods.vb#1)]

## <a name="nativemethods-example"></a>Exemplo de NativeMethods

### <a name="description"></a>Descrição
 Como a classe **NativeMethods** não deve ser marcada usando **SuppressUnmanagedCodeSecurityAttribute**, P/Invokes que são colocados nela exigirão permissão **UnmanagedCode** . Como a maioria dos aplicativos é executada a partir do computador local e executada com confiança total, normalmente isso não é um problema. No entanto, se você estiver desenvolvendo bibliotecas reutilizáveis, considere definir uma classe **SafeNativeMethods** ou **UnsafeNativeMethods** .

 O exemplo a seguir mostra um método de **interação. Beep** que encapsula a função **MessageBeep** de user32.dll. O P/Invoke **MessageBeep** é colocado na classe **NativeMethods** .

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.NativeMethods#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethods/cs/FxCop.Design.NativeMethods.cs#1)]
 [!code-vb[FxCop.Design.NativeMethods#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethods/vb/FxCop.Design.NativeMethods.vb#1)]

## <a name="safenativemethods-example"></a>Exemplo de SafeNativeMethods

### <a name="description"></a>Descrição
 Os métodos P/Invoke que podem ser expostos com segurança a qualquer aplicativo e que não têm nenhum efeito colateral devem ser colocados em uma classe denominada **SafeNativeMethods**. Você não precisa solicitar permissões e não precisa pagar muita atenção para onde elas são chamadas.

 O exemplo a seguir mostra uma propriedade **Environment.** semique encapsula a função **ObterContagemMarcaEscala** de kernel32.dll.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.NativeMethodsSafe#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsSafe/cs/FxCop.Design.NativeMethodsSafe.cs#1)]
 [!code-vb[FxCop.Design.NativeMethodsSafe#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsSafe/vb/FxCop.Design.NativeMethodsSafe.vb#1)]

## <a name="unsafenativemethods-example"></a>Exemplo de UnsafeNativeMethods

### <a name="description"></a>Descrição
 Métodos P/Invoke que não podem ser chamados com segurança e que podem causar efeitos colaterais devem ser colocados em uma classe denominada **UnsafeNativeMethods**. Esses métodos devem ser verificados rigorosamente para garantir que eles não sejam expostos ao usuário involuntariamente. A regra [CA2118: examinar o uso do SuppressUnmanagedCodeSecurityAttribute](../code-quality/ca2118-review-suppressunmanagedcodesecurityattribute-usage.md) pode ajudar com isso. Como alternativa, os métodos devem ter outra permissão exigida em vez de **UnmanagedCode** ao usá-los.

 O exemplo a seguir mostra um método **cursor. Hide** que encapsula a função de " **addcursor** " de user32.dll.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.NativeMethodsUnsafe#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsUnsafe/cs/FxCop.Design.NativeMethodsUnsafe.cs#1)]
 [!code-vb[FxCop.Design.NativeMethodsUnsafe#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NativeMethodsUnsafe/vb/FxCop.Design.NativeMethodsUnsafe.vb#1)]

## <a name="see-also"></a>Consulte Também
 [Avisos de design](../code-quality/design-warnings.md)
