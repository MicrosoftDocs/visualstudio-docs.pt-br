---
title: 'CA1017: Marcar assemblies com ComVisibleAttribute | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1017
- MarkAssembliesWithComVisible
helpviewer_keywords:
- MarkAssembliesWithComVisible
- CA1017
ms.assetid: 4842cb49-8dd8-4e5d-a2d6-ceeaf6c6cf8e
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 17f0a540a436316d3a4fb3b71a2a51b1c5a90a6d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535064"
---
# <a name="ca1017-mark-assemblies-with-comvisibleattribute"></a>CA1017: Marcar assemblies com ComVisibleAttribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|MarkAssembliesWithComVisible|
|CheckId|CA1017|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um assembly não tem o <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> atributo aplicado a ele.

## <a name="rule-description"></a>Descrição da Regra
 O <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributo determina como os clientes com acessam o código gerenciado. Um bom design determina que os assemblies indiquem explicitamente a visibilidade de COM. A visibilidade COM pode ser definida para um assembly inteiro e, em seguida, substituída para tipos individuais e membros de tipo. Se o atributo não estiver presente, o conteúdo do assembly será visível para clientes COM.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione o atributo ao assembly. Se você não quiser que o assembly fique visível para clientes COM, aplique o atributo e defina seu valor como `false` .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. Se você quiser que o assembly fique visível, aplique o atributo e defina seu valor como `true` .

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um assembly que tem o <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributo aplicado para impedir que ele seja visível para clientes com.

 [!code-cpp[FxCop.Design.AssembliesCom#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCom/cpp/FxCop.Design.AssembliesCom.cpp#1)]
 [!code-csharp[FxCop.Design.AssembliesCom#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCom/cs/FxCop.Design.AssembliesCom.cs#1)]
 [!code-vb[FxCop.Design.AssembliesCom#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCom/vb/FxCop.Design.AssembliesCom.vb#1)]

## <a name="see-also"></a>Consulte Também
 Interoperação com tipos .NET qualificados de [código não gerenciado](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258) [para interoperabilidade](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)
