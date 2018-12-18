---
title: 'CA1721: os nomes de propriedade não devem corresponder a métodos get'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
helpviewer_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
ms.assetid: 45a0e853-1f06-4688-af1b-cc634409e295
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 26f6e23a340ec018f766477f0bdce089a43ca3e4
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45549671"
---
# <a name="ca1721-property-names-should-not-match-get-methods"></a>CA1721: os nomes de propriedade não devem corresponder a métodos get

|||
|-|-|
|NomeDoTipo|PropertyNamesShouldNotMatchGetMethods|
|CheckId|CA1721|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O nome de um membro público ou protegido começa com 'Get' e, caso contrário, corresponde ao nome de uma propriedade pública ou protegida. Por exemplo, um tipo que contém um método chamado 'GetColor' e uma propriedade chamada 'Color' viola essa regra.

## <a name="rule-description"></a>Descrição da regra
 Os métodos GET e propriedades devem ter nomes que diferenciem claramente a função.

 Convenções de nomenclatura de fornecem uma aparência comum para bibliotecas que direcionam o common language runtime. Essa consistência reduz o tempo necessário para conhecer uma nova biblioteca de software e aumenta a confiança do cliente que a biblioteca foi desenvolvida por alguém que tenha experiência em desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Altere o nome para que ele não coincide com o nome de um método que é prefixado com 'Get'.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

> [!NOTE]
> Esse aviso pode ser excluído se o método Get é causado pela implementação de interface IExtenderProvider.

## <a name="example"></a>Exemplo
 O exemplo a seguir contém um método e propriedade que violam essa regra.

 [!code-csharp[FxCop.Naming.GetMethod#1](../code-quality/codesnippet/CSharp/ca1721-property-names-should-not-match-get-methods_1.cs)]
 [!code-vb[FxCop.Naming.GetMethod#1](../code-quality/codesnippet/VisualBasic/ca1721-property-names-should-not-match-get-methods_1.vb)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1024: usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md)