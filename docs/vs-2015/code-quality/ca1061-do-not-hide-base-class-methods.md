---
title: 'CA1061: não ocultar métodos de classe base | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1061
- DoNotHideBaseClassMethods
helpviewer_keywords:
- DoNotHideBaseClassMethods
- CA1061
ms.assetid: 0bda9dc8-87b4-4038-ab9d-563298387466
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c884eb569d5682326d2dc667363f991467171386
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533348"
---
# <a name="ca1061-do-not-hide-base-class-methods"></a>CA1061: Não ocultar métodos de classe base
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotHideBaseClassMethods|
|CheckId|CA1061|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo derivado declara um método com o mesmo nome e com o mesmo número de parâmetros que um de seus métodos base; um ou mais dos parâmetros é um tipo base do parâmetro correspondente no método base; e quaisquer parâmetros restantes têm tipos que são idênticos aos parâmetros correspondentes no método base.

## <a name="rule-description"></a>Descrição da Regra
 Um método em um tipo base é ocultado por um método de nome idêntico em um tipo derivado quando a assinatura de parâmetro do método derivado difere somente por tipos que são mais fracamente derivados do que os tipos correspondentes na assinatura de parâmetro do método de base.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova ou renomeie o método ou altere a assinatura do parâmetro para que o método não oculte o método base.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que viola a regra.

 [!code-csharp[FxCop.Design.HideBaseMethod#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.HideBaseMethod/cs/FxCop.Design.HideBaseMethod.cs#1)]
