---
title: 'CA1053: Tipos de suporte estático não devem ter construtores'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- StaticHolderTypesShouldNotHaveConstructors
- CA1053
helpviewer_keywords:
- CA1053
- StaticHolderTypesShouldNotHaveConstructors
ms.assetid: 10302b9a-fa5e-4935-a06a-513d9600f613
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 52f04355a266f87a039b8197675c2f5377b840ee
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388310"
---
# <a name="ca1053-static-holder-types-should-not-have-constructors"></a>CA1053: Tipos de suporte estático não devem ter construtores

|||
|-|-|
|NomeDoTipo|StaticHolderTypesShouldNotHaveConstructors|
|CheckId|CA1053|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou público aninhado declara apenas membros estáticos e tem um construtor padrão público ou protegido.

## <a name="rule-description"></a>Descrição da regra
 O construtor é desnecessário porque chamar membros estáticos não exige uma instância do tipo. Além disso, porque o tipo não tem membros não estáticos, criando uma instância não fornece acesso a qualquer um dos membros do tipo.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, remova o construtor padrão ou torná-la particular.

> [!NOTE]
> Alguns compiladores criar automaticamente um construtor padrão público se o tipo de não definir nenhum construtor. Se esse for o caso com seu tipo, adicione um construtor padrão particular para eliminar a violação.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra. A presença do construtor sugere que o tipo não é um tipo estático.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra. Observe que não há nenhum construtor padrão no código-fonte. Quando esse código é compilado em um assembly, o compilador c# irá inserir um construtor padrão, que irá violar essa regra. Para corrigir isso, declare um construtor particular.

 [!code-csharp[FxCop.Design.StaticTypes#1](../code-quality/codesnippet/CSharp/ca1053-static-holder-types-should-not-have-constructors_1.cs)]