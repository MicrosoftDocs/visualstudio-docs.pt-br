---
title: 'CA1802: usar literais quando apropriado'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseLiteralsWhereAppropriate
- CA1802
helpviewer_keywords:
- UseLiteralsWhereAppropriate
- CA1802
ms.assetid: 2515e4cd-9e61-486d-b067-58ba1a743ce4
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 13cfc8b090d289173975b0ef2ee55562955de0c8
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45548734"
---
# <a name="ca1802-use-literals-where-appropriate"></a>CA1802: usar literais quando apropriado

|||
|-|-|
|NomeDoTipo|UseLiteralsWhereAppropriate|
|CheckId|CA1802|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um campo é declarado `static` e `readonly` (`Shared` e `ReadOnly` em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) e é inicializada com um valor computável no tempo de compilação.

## <a name="rule-description"></a>Descrição da regra
 O valor de um `static``readonly` campo é calculado em tempo de execução quando o construtor estático para o tipo declarativo é chamado. Se o `static``readonly` campo é inicializado quando ela é declarada e um construtor estático não é declarado explicitamente, o compilador emite um construtor estático para inicializar o campo.

 O valor de uma `const` campo é calculado em tempo de compilação e armazenado nos metadados, o que aumenta o desempenho de tempo de execução quando ele é comparado com um `static``readonly` campo.

 Como o valor atribuído ao campo de destino é computável no tempo de compilação, altere a declaração para um `const` campo para que o valor é calculado em tempo de compilação em vez de em tempo de execução.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, substitua os `static` e `readonly` modificadores com o `const` modificador.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, ou desabilitar a regra, se o desempenho não for uma preocupação.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo `UseReadOnly`, que viola a regra e um tipo, `UseConstant`, que satisfaz a regra.

 [!code-vb[FxCop.Performance.UseLiterals#1](../code-quality/codesnippet/VisualBasic/ca1802-use-literals-where-appropriate_1.vb)]
 [!code-csharp[FxCop.Performance.UseLiterals#1](../code-quality/codesnippet/CSharp/ca1802-use-literals-where-appropriate_1.cs)]