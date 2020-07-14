---
title: 'CA1802: usar literais quando apropriado | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseLiteralsWhereAppropriate
- CA1802
helpviewer_keywords:
- UseLiteralsWhereAppropriate
- CA1802
ms.assetid: 2515e4cd-9e61-486d-b067-58ba1a743ce4
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dc8019c97d3c561000f1c6a8d083bee6253face3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544398"
---
# <a name="ca1802-use-literals-where-appropriate"></a>CA1802: Usar literais quando apropriado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|UseLiteralsWhereAppropriate|
|CheckId|CA1802|
|Categoria|Microsoft. performance|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um campo é declarado `static` e `readonly` ( `Shared` e `ReadOnly` em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ) e é inicializado com um valor que é computáveis no momento da compilação.

## <a name="rule-description"></a>Descrição da Regra
 O valor de um `static``readonly` campo é calculado em tempo de execução quando o construtor estático para o tipo declarativo é chamado. Se o `static``readonly` campo for inicializado quando for declarado e um construtor estático não for declarado explicitamente, o compilador emitirá um construtor estático para inicializar o campo.

 O valor de um `const` campo é calculado no momento da compilação e armazenado nos metadados, o que aumenta o desempenho do tempo de execução quando ele é comparado a um `static``readonly` campo.

 Como o valor atribuído ao campo de destino é computáveis em tempo de compilação, altere a declaração para um `const` campo para que o valor seja calculado no momento da compilação em vez de em tempo de execução.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, substitua os `static` `readonly` modificadores e pelo `const` modificador.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra ou desabilitar a regra, se o desempenho não for preocupante.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo, `UseReadOnly` , que viola a regra e um tipo, `UseConstant` , que satisfazem a regra.

 [!code-csharp[FxCop.Performance.UseLiterals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.UseLiterals/cs/FxCop.Performance.UseLiterals.cs#1)]
 [!code-vb[FxCop.Performance.UseLiterals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.UseLiterals/vb/FxCop.Performance.UseLiterals.vb#1)]
