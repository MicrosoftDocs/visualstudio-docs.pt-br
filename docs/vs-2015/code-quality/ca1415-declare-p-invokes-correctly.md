---
title: 'CA1415: declarar P-Invokes corretamente | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1415
- DeclarePInvokesCorrectly
helpviewer_keywords:
- CA1415
- DeclarePInvokesCorrectly
ms.assetid: 42a90796-0264-4460-bf97-2fb4a093dfdc
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b9931d29c818d95785146558637c32237e2c5276
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547843"
---
# <a name="ca1415-declare-pinvokes-correctly"></a>CA1415: declarar P/Invokes corretamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DeclarePInvokesCorrectly|
|CheckId|CA1415|
|Categoria|Microsoft. Interoperability|
|Alteração Significativa|Não separável – se o P/Invoke que declara o parâmetro não puder ser visto fora do assembly. Quebra-se o P/Invoke que declara o parâmetro pode ser visto fora do assembly.|

## <a name="cause"></a>Causa
 Um método de invocação de plataforma está declarado incorretamente.

## <a name="rule-description"></a>Descrição da Regra
 Um método de invocação de plataforma acessa código não gerenciado e é definido usando a `Declare` palavra-chave no [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ou no <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> . Atualmente, essa regra procura declarações de método de invocação de plataforma que se destinam a funções Win32 que têm um ponteiro para um parâmetro de estrutura Sobreposto e o parâmetro gerenciado correspondente não é um ponteiro para uma <xref:System.Threading.NativeOverlapped?displayProperty=fullName> estrutura.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, declare corretamente o método Invoke da plataforma.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra os métodos de invocação de plataforma que violam a regra e satisfazem a regra.

 [!code-csharp[FxCop.Interoperability.DeclarePInvokes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.DeclarePInvokes/cs/FxCop.Interoperability.DeclarePInvokes.cs#1)]

## <a name="see-also"></a>Consulte Também
 [Interoperação com código não gerenciado](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
