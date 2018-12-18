---
title: 'CA2201: não acionar tipos de exceção reservados'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotRaiseReservedExceptionTypes
- CA2201
helpviewer_keywords:
- CA2201
- DoNotRaiseReservedExceptionTypes
ms.assetid: dd14ef5c-80e6-41a5-834e-eba8e2eae75e
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 763c8656507f8a1d9c1f59bd548469c338aeb012
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547507"
---
# <a name="ca2201-do-not-raise-reserved-exception-types"></a>CA2201: não acionar tipos de exceção reservados

|||
|-|-|
|NomeDoTipo|DoNotRaiseReservedExceptionTypes|
|CheckId|CA2201|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Um método gera um tipo de exceção que é muito geral ou que está reservado pelo tempo de execução.

## <a name="rule-description"></a>Descrição da regra

Os seguintes tipos de exceção são muito gerais para fornecer informações suficientes para o usuário:

- <xref:System.Exception?displayProperty=fullName>

- <xref:System.ApplicationException?displayProperty=fullName>

- <xref:System.SystemException?displayProperty=fullName>

Os seguintes tipos de exceção são reservados e devem ser gerados apenas pelo common language runtime:

- <xref:System.ExecutionEngineException?displayProperty=fullName>

- <xref:System.IndexOutOfRangeException?displayProperty=fullName>

- <xref:System.NullReferenceException?displayProperty=fullName>

- <xref:System.OutOfMemoryException?displayProperty=fullName>

**Não lance exceções gerais**

Se você lança um tipo de exceção geral, como <xref:System.Exception> ou <xref:System.SystemException> em uma biblioteca ou estrutura, ele força os consumidores a capturar todas as exceções, incluindo exceções desconhecidas que eles não saibam como manipular.

Em vez disso, lançar um tipo mais derivado que já existe no framework, ou criar seu próprio tipo que deriva de <xref:System.Exception>.

**Lançar exceções específicas**

A tabela a seguir mostra os parâmetros e quais exceções a ser gerada quando você valida o parâmetro, incluindo o parâmetro de valor no acessador set de uma propriedade:

|Descrição do parâmetro|Exceção|
|---------------------------|---------------|
|`null` Referência|<xref:System.ArgumentNullException?displayProperty=fullName>|
|Fora do intervalo permitido de valores (como um índice para uma coleção ou lista)|<xref:System.ArgumentOutOfRangeException?displayProperty=fullName>|
|Inválido `enum` valor|<xref:System.ComponentModel.InvalidEnumArgumentException?displayProperty=fullName>|
|Contém um formato que atende às especificações de parâmetro de um método (como a cadeia de caracteres de formato para `ToString(String)`)|<xref:System.FormatException?displayProperty=fullName>|
|Caso contrário inválido|<xref:System.ArgumentException?displayProperty=fullName>|

Quando uma operação é inválida para o estado atual de um objeto throw <xref:System.InvalidOperationException?displayProperty=fullName>

Quando uma operação é executada em um objeto que foi descartado throw <xref:System.ObjectDisposedException?displayProperty=fullName>

Quando não há suporte para uma operação (como em um substituída **Stream.Write** em um Stream aberto para leitura) throw <xref:System.NotSupportedException?displayProperty=fullName>

Quando uma conversão resultar em um estouro (como em uma sobrecarga de operador de conversão explícita) acionar <xref:System.OverflowException?displayProperty=fullName>

Em outras situações, considere a criação de seu próprio tipo que deriva de <xref:System.Exception> e lançar que.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, altere o tipo da exceção lançada para um tipo específico que não é um dos tipos reservados.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Não suprima um aviso nessa regra.

## <a name="related-rules"></a>Regras relacionadas

- [CA1031: não capturar tipos de exceção gerais](../code-quality/ca1031-do-not-catch-general-exception-types.md)