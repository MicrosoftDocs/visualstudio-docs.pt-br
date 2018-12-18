---
title: 'CA2211: os campos não constantes não devem estar visíveis'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2211
- NonConstantFieldsShouldNotBeVisible
helpviewer_keywords:
- NonConstantFieldsShouldNotBeVisible
- CA2211
ms.assetid: e1e42c40-0acd-4312-af29-70133739a304
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 0e40065351342ab49b86b21bb525b45ce78c6028
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45550538"
---
# <a name="ca2211-non-constant-fields-should-not-be-visible"></a>CA2211: os campos não constantes não devem estar visíveis

|||
|-|-|
|NomeDoTipo|NonConstantFieldsShouldNotBeVisible|
|CheckId|CA2211|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um campo estático público ou protegido não é constante nem somente leitura.

## <a name="rule-description"></a>Descrição da regra
 Os campos estáticos que não são constantes nem somente leitura não são thread-safe. O acesso a esse campo deve ser cuidadosamente controlado e exige técnicas de programação avançadas para sincronizar o acesso ao objeto de classe. Como esses são difíceis de habilidades para aprender e mestre e testes de tal objeto apresenta seus próprios desafios, campos estáticos são melhor usados para armazenar dados que não são alterados. Essa regra se aplica às bibliotecas; aplicativos não devem expor todos os campos.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, verifique o campo estático constantes ou somente leitura. Se isso não for possível, recrie o tipo para usar um mecanismo alternativo, como uma propriedade de thread-safe que gerencia o acesso thread-safe para o campo subjacente. Perceba que os problemas, como contenção de bloqueio e deadlocks podem afetar o desempenho e o comportamento da biblioteca.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, se você estiver desenvolvendo um aplicativo e, portanto, têm controle total sobre o acesso ao tipo que contém o campo estático. Designers de bibliotecas não devem suprimir um aviso nessa regra; campos estáticos de não constante pode fazer usando a biblioteca difícil para os desenvolvedores para usar corretamente.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra.

 [!code-vb[FxCop.Usage.AvoidStaticNonConstants#1](../code-quality/codesnippet/VisualBasic/ca2211-non-constant-fields-should-not-be-visible_1.vb)]
 [!code-csharp[FxCop.Usage.AvoidStaticNonConstants#1](../code-quality/codesnippet/CSharp/ca2211-non-constant-fields-should-not-be-visible_1.cs)]