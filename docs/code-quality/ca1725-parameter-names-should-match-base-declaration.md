---
title: 'CA1725: os nomes de parâmetro devem corresponder à declaração base'
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- ParameterNamesShouldMatchBaseDeclaration
- CA1725
helpviewer_keywords:
- CA1725
- ParameterNamesShouldMatchBaseDeclaration
ms.assetid: 9b657ab0-fe81-4f4c-9481-ba746988c922
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 417e03f5d682ad448372d74fa8c9a5c31b798ccc
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72438923"
---
# <a name="ca1725-parameter-names-should-match-base-declaration"></a>CA1725: os nomes de parâmetro devem corresponder à declaração base

|||
|-|-|
|NomeDoTipo|ParameterNamesShouldMatchBaseDeclaration|
|CheckId|CA1725|
|Categoria|Microsoft. Naming|
|Alteração significativa|Quebra|

## <a name="cause"></a>Causa

O nome de um parâmetro em uma substituição de método não corresponde ao nome do parâmetro na declaração base do método ou ao nome do parâmetro na declaração da interface do método.

Por padrão, essa regra só examina os métodos visíveis externamente, mas isso é [configurável](#configurability).

## <a name="rule-description"></a>Descrição da regra

A nomenclatura consistente dos parâmetros em uma hierarquia de substituição aumenta a usabilidade das substituições de método. Um nome de parâmetro em um método derivado diferente do nome na declaração de base pode causar confusão em relação à possibilidade do método ser uma substituição do método de base ou de uma nova sobrecarga do método.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, renomeie o parâmetro para corresponder à declaração base. A correção é uma alteração significativa para métodos visíveis COM.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Não suprimir um aviso dessa regra, exceto para métodos visíveis COM em bibliotecas que foram enviadas anteriormente.

## <a name="configurability"></a>Configurabilidade

Se você estiver executando essa regra por meio de [analisadores do FxCop](install-fxcop-analyzers.md) (e não com a análise herdada), poderá configurar em quais partes de sua base de código executar essa regra, com base em sua acessibilidade. Por exemplo, para especificar que a regra deve ser executada somente na superfície da API não pública, adicione o seguinte par chave-valor a um arquivo. editorconfig em seu projeto:

```ini
dotnet_code_quality.ca1725.api_surface = private, internal
```

Você pode configurar essa opção apenas para essa regra, para todas as regras ou para todas as regras nesta categoria (nomenclatura). Para obter mais informações, consulte [Configurar analisadores de FxCop](configure-fxcop-analyzers.md).
