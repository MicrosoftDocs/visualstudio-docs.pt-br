---
title: 'CA2220: os finalizadores devem chamar o finalizador de classe base | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2220
- FinalizersShouldCallBaseClassFinalizer
helpviewer_keywords:
- CA2220
- FinalizersShouldCallBaseClassFinalizer
ms.assetid: 48329f42-170d-45ee-a381-e33f55a240c5
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5d9139314d52c4c50de84a45f227e6df5715bf02
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540654"
---
# <a name="ca2220-finalizers-should-call-base-class-finalizer"></a>CA2220: Os finalizadores devem chamar o finalizador de classe base
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|FinalizersShouldCallBaseClassFinalizer|
|CheckId|CA2220|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo que substitui não <xref:System.Object.Finalize%2A?displayProperty=fullName> chama o <xref:System.Object.Finalize%2A> método em sua classe base.

## <a name="rule-description"></a>Descrição da Regra
 A finalização deve ser propagada em toda a hierarquia de herança. Para garantir isso, os tipos devem chamar seu <xref:System.Object.Finalize%2A> método de classe base de dentro de seu próprio <xref:System.Object.Finalize%2A> método. O compilador C# adiciona a chamada ao finalizador de classe base automaticamente.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, chame o método do tipo base <xref:System.Object.Finalize%2A> do seu <xref:System.Object.Finalize%2A> método.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. Alguns compiladores que se destinam ao Common Language Runtime inserir uma chamada para o finalizador do tipo base na MSIL (Microsoft Intermediate Language). Se um aviso dessa regra for relatado, o compilador não inserirá a chamada e você deverá adicioná-la ao seu código.

## <a name="example"></a>Exemplo
 O exemplo a seguir Visual Basic mostra um tipo `TypeB` que chama corretamente o <xref:System.Object.Finalize%2A> método em sua classe base.

 [!code-vb[FxCop.Usage.IDisposableBaseCalled#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposableBaseCalled/vb/FxCop.Usage.IDisposableBaseCalled.vb#1)]

## <a name="see-also"></a>Consulte Também
 [Padrão de descarte](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
