---
title: 'CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldDifferByMoreThanCase
- CA1708
helpviewer_keywords:
- CA1708
- IdentifiersShouldDifferByMoreThanCase
ms.assetid: dac0f01d-dd21-484d-add1-c8cd2bf6969f
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b2bda5a9f5d569057455af9e31fb5d6852c9881e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49815488"
---
# <a name="ca1708-identifiers-should-differ-by-more-than-case"></a>CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas

|||
|-|-|
|NomeDoTipo|IdentifiersShouldDifferByMoreThanCase|
|CheckId|CA1708|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Os nomes dos dois tipos, membros, parâmetros ou espaços para nomes totalmente qualificados são idênticos quando eles são convertidos em minúsculas.

## <a name="rule-description"></a>Descrição da regra
 Os identificadores de namespaces, tipos, membros e parâmetros não podem se diferenciar apenas por maiúsculas porque linguagens com o Common Language Runtime como destino não precisam diferenciar maiúsculas e minúsculas. Por exemplo, [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] é uma linguagem diferencia maiusculas de minúsculas amplamente utilizada.

 Essa regra é acionada em apenas a membros publicamente visível.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Selecione um nome exclusivo quando comparado a outros identificadores no diferenciando maiusculas de minúsculas.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra. A biblioteca não pode ser utilizada em todos os idiomas disponíveis no .NET Framework.

## <a name="example-of-a-violation"></a>Exemplo de uma violação
 O exemplo a seguir demonstra uma violação dessa regra.

 [!code-csharp[FxCop.Naming.IdentifiersShouldDifferByMoreThanCase#1](../code-quality/codesnippet/CSharp/ca1708-identifiers-should-differ-by-more-than-case_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1709: os identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)