---
title: 'CA2230: Usar parâmetros para argumentos variáveis | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- UseParamsForVariableArguments
- CA2230
helpviewer_keywords:
- CA2230
- UseParamsForVariableArguments
ms.assetid: bf98b733-4855-4110-9f16-eba5a9e79421
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ad0f43ac18c39d1dfdf6464e5cd260b669e1a0da
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49892721"
---
# <a name="ca2230-use-params-for-variable-arguments"></a>CA2230: usar parâmetros para argumentos variáveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|UseParamsForVariableArguments|
|CheckId|CA2230|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido contém um método público ou protegido que usa o `VarArgs` convenção de chamada.

## <a name="rule-description"></a>Descrição da Regra
 O `VarArgs` convenção de chamada é usada com determinadas definições de método que levam a um número variável de parâmetros. Um método usando o `VarArgs` convenção de chamada não é Common Language Specification (CLS) em conformidade e pode não estar acessível em linguagens de programação.

 No c#, o `VarArgs` convenção de chamada é usada quando a lista de parâmetros do método termina com o `__arglist` palavra-chave. Visual Basic não oferece suporte a `VarArgs` convenção de chamada e Visual C++ permite que seu uso apenas em código não gerenciado que usa a elipse `...` notação.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra no c#, use o [params](http://msdn.microsoft.com/library/1690815e-b52b-4967-8380-5780aff08012) palavra-chave, em vez de `__arglist`.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra dois métodos, um que viola a regra e um que satisfaz a regra.

 [!code-csharp[FxCop.Usage.UseParams#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.UseParams/cs/FxCop.Usage.UseParams.cs#1)]

## <a name="see-also"></a>Consulte também
 <xref:System.Reflection.CallingConventions?displayProperty=fullName> [Independência de linguagem e componentes independentes de linguagem](http://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)



