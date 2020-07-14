---
title: 'CA1721: os nomes de propriedade não devem corresponder aos métodos get | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
helpviewer_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
ms.assetid: 45a0e853-1f06-4688-af1b-cc634409e295
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 77ec48a1164c7065ba5033ef51eb704b8361dc1c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544450"
---
# <a name="ca1721-property-names-should-not-match-get-methods"></a>CA1721: Nomes de propriedades não devem corresponder a métodos get
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|PropertyNamesShouldNotMatchGetMethods|
|CheckId|CA1721|
|Categoria|Microsoft. Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O nome de um membro público ou protegido começa com ' Get ' e, caso contrário, corresponde ao nome de uma propriedade pública ou protegida. Por exemplo, um tipo que contém um método chamado ' GetColor ' e uma propriedade chamada ' color ' viola essa regra.

## <a name="rule-description"></a>Descrição da Regra
 Os métodos get e as propriedades devem ter nomes que distinguem claramente sua função.

 As convenções de nomenclatura fornecem uma aparência comum para as bibliotecas direcionadas ao Common Language Runtime. Isso reduz o tempo necessário para aprender uma nova biblioteca de software e aumenta a confiança do cliente de que a biblioteca foi desenvolvida por alguém que tenha experiência no desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Altere o nome para que ele não corresponda ao nome de um método que tenha o prefixo ' Get '.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

> [!NOTE]
> Esse aviso poderá ser excluído se o método Get for causado pela implementação da interface E IExtenderProviderUnk.

## <a name="example"></a>Exemplo
 O exemplo a seguir contém um método e uma propriedade que violam essa regra.

 [!code-csharp[FxCop.Naming.GetMethod#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.GetMethod/cs/FxCop.Naming.GetMethod.cs#1)]
 [!code-vb[FxCop.Naming.GetMethod#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.GetMethod/vb/FxCop.Naming.GetMethod.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1024: Usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md)
