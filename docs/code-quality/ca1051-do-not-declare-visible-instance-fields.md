---
title: 'CA1051: não declarar campos de instância visíveis'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1051
- DoNotDeclareVisibleInstanceFields
helpviewer_keywords:
- CA1051
- DoNotDeclareVisibleInstanceFields
ms.assetid: 2805376c-824c-462c-81d1-c51aaf7cabe7
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f907b1d8626e8babc88137ed70cf6330386ab92a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49832193"
---
# <a name="ca1051-do-not-declare-visible-instance-fields"></a>CA1051: não declarar campos de instância visíveis

|||
|-|-|
|NomeDoTipo|DoNotDeclareVisibleInstanceFields|
|CheckId|CA1051|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo visível externamente tem um campo de instância visíveis externamente.

## <a name="rule-description"></a>Descrição da regra
 O principal uso de um campo deve ser um como um detalhe da implementação. Os campos devem ser `private` ou `internal` e devem ser expostos por meio de propriedades. Ele é tão fácil acessar uma propriedade que ela acessar um campo, e o código nos acessadores de uma propriedade pode alterar como os recursos do tipo expandem sem introduzir alterações significativas. Propriedades que retornam apenas o valor de um campo privado ou interno são otimizadas para executar no mesmo nível de acesso a um campo; muito pouco ganho de desempenho está associado com o uso de campos visíveis externamente em Propriedades.

 Refere-se visível externamente ao `public`, `protected`, e `protected internal` (`Public`, `Protected`, e `Protected Friend` no Visual Basic) níveis de acessibilidade.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, tornar o campo `private` ou `internal` e expô-lo por meio de uma propriedade visível externamente.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra. Campos visíveis externamente não fornecem todos os benefícios que não estão disponíveis para as propriedades. Além disso, os campos públicos não podem ser protegidos por [demandas de Link](/dotnet/framework/misc/link-demands). Ver [CA2112: tipos seguros não devem expor campos](../code-quality/ca2112-secured-types-should-not-expose-fields.md).

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo (`BadPublicInstanceFields`) que viola essa regra. `GoodPublicInstanceFields` mostra o código corrigido.

 [!code-csharp[FxCop.Design.TypesPublicInstanceFields#1](../code-quality/codesnippet/CSharp/ca1051-do-not-declare-visible-instance-fields_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2112: os tipos seguros não devem expor campos](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

## <a name="see-also"></a>Consulte também
 [Demandas de link](/dotnet/framework/misc/link-demands)