---
title: 'CA1715: Identificadores devem ter um prefixo correto'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- CA1715
- IdentifiersShouldHaveCorrectPrefix
helpviewer_keywords:
- IdentifiersShouldHaveCorrectPrefix
- CA1715
ms.assetid: cf45f8df-6855-4cb6-a4e2-7cfed714cf2f
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 7c7abdaa2356bdf622f0892e9b027047fc021096
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53912919"
---
# <a name="ca1715-identifiers-should-have-correct-prefix"></a>CA1715: Identificadores devem ter um prefixo correto

|||
|-|-|
|NomeDoTipo|IdentifiersShouldHaveCorrectPrefix|
|CheckId|CA1715|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebrando - quando disparado em interfaces.<br /><br /> Sem quebra - quando gerado em parâmetros de tipo genérico.|

## <a name="cause"></a>Causa
 O nome de uma interface visível externamente não começar com letras maiusculas 'I'.

 -ou-

 O nome de um parâmetro de tipo genérico em um tipo visível externamente ou método não começa com uma letra maiuscula ' t '.

## <a name="rule-description"></a>Descrição da regra
 Por convenção, os nomes de determinados elementos de programação começar com um prefixo específico.

 Nomes de interface devem começar com uma letra maiuscula 'I' seguido de outra letra maiuscula. Esta regra relata violações para nomes de interface, como 'MyInterface' e 'IsolatedInterface'.

 Nomes de parâmetro de tipo genérico devem começar com uma letra maiuscula ' t ' e, opcionalmente, pode ser seguido por outra letra maiuscula. Esta regra relata violações para nomes de parâmetro de tipo genérico, como "V" e 'Type'.

 Convenções de nomenclatura de fornecem uma aparência comum para bibliotecas que direcionam o common language runtime. Isso reduz a curva de aprendizado que é necessário para novas bibliotecas de software e aumenta a confiança do cliente que a biblioteca foi desenvolvida por alguém que tenha experiência em desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Renomear o identificador para que ele será prefixado corretamente.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 **O exemplo a seguir mostra uma interface nomeada incorretamente.**

 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_1.cpp)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_1.vb)]
 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_1.cs)]

## <a name="example"></a>Exemplo
 **O exemplo a seguir corrige a violação anterior prefixando a interface com 'I'.**

 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_2.cs)]
 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_2.cpp)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_2.vb)]

## <a name="example"></a>Exemplo
 **O exemplo a seguir mostra um parâmetro de tipo genérico nomeado incorretamente.**

 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_3.cpp)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_3.vb)]
 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_3.cs)]

## <a name="example"></a>Exemplo
 **O exemplo a seguir corrige a violação anterior, prefixando o parâmetro de tipo genérico com T' '.**

 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_4.cpp)]
 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_4.cs)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_4.vb)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1722: Identificadores não devem ter prefixo incorreto](../code-quality/ca1722-identifiers-should-not-have-incorrect-prefix.md)