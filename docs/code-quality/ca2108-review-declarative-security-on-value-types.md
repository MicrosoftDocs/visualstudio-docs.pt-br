---
title: 'CA2108: revisar segurança declarativa em tipos de valor'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
helpviewer_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
ms.assetid: d62bffdd-3826-4d52-a708-1c646c5d48c2
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e2d76a0ecf6a2eeac677475eb25efe495129c213
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45548511"
---
# <a name="ca2108-review-declarative-security-on-value-types"></a>CA2108: revisar segurança declarativa em tipos de valor

|||
|-|-|
|NomeDoTipo|ReviewDeclarativeSecurityOnValueTypes|
|CheckId|CA2108|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Um tipo de valor público ou protegido é protegido por um [dados e modelagem](/dotnet/framework/data/index) ou [demandas de Link](/dotnet/framework/misc/link-demands).

## <a name="rule-description"></a>Descrição da regra

Tipos de valor são alocados e inicializados por seus construtores padrão antes de executar outros construtores. Se um tipo de valor é protegido por um Demand ou LinkDemand e o chamador não tem permissões que satisfazem a verificação de segurança, qualquer construtor diferente do padrão falhará e será gerada uma exceção de segurança. O tipo de valor não é desalocado; ele é deixado no estado definido pelo seu construtor padrão. Não presuma que um chamador que passa uma instância do tipo de valor tem permissão para criar ou acessar a instância.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Você não pode corrigir uma violação dessa regra, a menos que você remover a verificação de segurança do tipo e verificações de segurança de nível de método de uso em seu lugar. Corrigir a violação dessa maneira não impede que os chamadores com permissões inadequadas obtenham as instâncias do tipo de valor. Você deve garantir que uma instância do tipo de valor, em seu estado padrão, não expõe informações confidenciais e não pode ser usada de modo prejudicial.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Você pode suprimir um aviso nessa regra, se qualquer chamador pode obter as instâncias do tipo do valor em seu estado padrão sem apresentando uma ameaça à segurança.

## <a name="example-1"></a>Exemplo 1

O exemplo a seguir mostra uma biblioteca que contém um tipo de valor que viola essa regra. O `StructureManager` tipo pressupõe que um chamador que passa uma instância do tipo de valor tem permissão para criar ou acessar a instância.

[!code-csharp[FxCop.Security.DemandOnValueType#1](../code-quality/codesnippet/CSharp/ca2108-review-declarative-security-on-value-types_1.cs)]

## <a name="example-2"></a>Exemplo 2

O aplicativo a seguir demonstra a desvantagem da biblioteca.

[!code-csharp[FxCop.Security.TestDemandOnValueType#1](../code-quality/codesnippet/CSharp/ca2108-review-declarative-security-on-value-types_2.cs)]

Este exemplo gera a seguinte saída:

```txt
Structure custom constructor: Request failed.
New values SecuredTypeStructure 100 100
New values SecuredTypeStructure 200 200
```

## <a name="see-also"></a>Consulte também

- [Demandas de link](/dotnet/framework/misc/link-demands)
- [Dados e modelagem](/dotnet/framework/data/index)
