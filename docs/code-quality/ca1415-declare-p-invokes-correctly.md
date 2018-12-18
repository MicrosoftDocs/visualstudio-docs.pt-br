---
title: 'CA1415: declare os P-Invokes corretamente'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1415
- DeclarePInvokesCorrectly
helpviewer_keywords:
- CA1415
- DeclarePInvokesCorrectly
ms.assetid: 42a90796-0264-4460-bf97-2fb4a093dfdc
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f95c3e68190acbd53c4b75ceb81abf2885d15bce
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49922621"
---
# <a name="ca1415-declare-pinvokes-correctly"></a>CA1415: declarar P/Invokes corretamente

|||
|-|-|
|NomeDoTipo|DeclarePInvokesCorrectly|
|CheckId|CA1415|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Separação de não - se o valor de P/Invoke, que declara o parâmetro não pode ser vista de fora do assembly. Quebrando - se que o P/Invoke que declara o parâmetro pode ser visto de fora do assembly.|

## <a name="cause"></a>Causa
 Uma plataforma de invocação de método é declarado incorretamente.

## <a name="rule-description"></a>Descrição da regra
 Uma plataforma de chamar código não gerenciado do método acessos e é definido usando o `Declare` palavra-chave na [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ou o <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>. No momento, esta regra procura declarações de método que se destinam a funções do Win32 que têm um ponteiro para um parâmetro de estrutura OVERLAPPED de invocação de plataforma e o parâmetro gerenciado correspondente não é um ponteiro para um <xref:System.Threading.NativeOverlapped?displayProperty=fullName> estrutura.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, declarar corretamente a plataforma de invocação de método.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 A exemplo a seguir mostra os métodos que violam a regra e atendem à regra de invocação de plataforma.

 [!code-csharp[FxCop.Interoperability.DeclarePInvokes#1](../code-quality/codesnippet/CSharp/ca1415-declare-p-invokes-correctly_1.cs)]

## <a name="see-also"></a>Consulte também
 [Interoperação com código não gerenciado](/dotnet/framework/interop/index)