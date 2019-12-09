---
title: 'CA2201: não gerar tipos de exceção reservados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotRaiseReservedExceptionTypes
- CA2201
helpviewer_keywords:
- CA2201
- DoNotRaiseReservedExceptionTypes
ms.assetid: dd14ef5c-80e6-41a5-834e-eba8e2eae75e
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a550226a5ea1edb3b30e317be6b5682f4c204d52
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667371"
---
# <a name="ca2201-do-not-raise-reserved-exception-types"></a>CA2201: não acionar tipos de exceção reservados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotRaiseReservedExceptionTypes|
|CheckId|CA2201|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método gera um tipo de exceção que é muito geral ou que é reservado pelo tempo de execução.

## <a name="rule-description"></a>Descrição da Regra
 Os seguintes tipos de exceção são muito gerais para fornecer informações suficientes ao usuário:

- <xref:System.Exception?displayProperty=fullName>

- <xref:System.ApplicationException?displayProperty=fullName>

- <xref:System.SystemException?displayProperty=fullName>

  Os seguintes tipos de exceção são reservados e devem ser lançados somente pelo Common Language Runtime:

- <xref:System.ExecutionEngineException?displayProperty=fullName>

- <xref:System.IndexOutOfRangeException?displayProperty=fullName>

- <xref:System.NullReferenceException?displayProperty=fullName>

- <xref:System.OutOfMemoryException?displayProperty=fullName>

  **Não lançar exceções gerais**

  Se você lançar um tipo de exceção geral, como <xref:System.Exception> ou <xref:System.SystemException> em uma biblioteca ou estrutura, ele forçará os consumidores a capturar todas as exceções, incluindo exceções desconhecidas que eles não sabem como lidar.

  Em vez disso, gere um tipo mais derivado que já existe na estrutura ou crie seu próprio tipo que derive de <xref:System.Exception>.

  **Gerar exceções específicas**

  A tabela a seguir mostra os parâmetros e quais exceções gerar ao validar o parâmetro, incluindo o parâmetro value no acessador set de uma propriedade:

|Descrição do parâmetro|Exceção|
|---------------------------|---------------|
|referência de `null`|<xref:System.ArgumentNullException?displayProperty=fullName>|
|Fora do intervalo de valores permitido (como um índice para uma coleção ou lista)|<xref:System.ArgumentOutOfRangeException?displayProperty=fullName>|
|Valor `enum` inválido|<xref:System.ComponentModel.InvalidEnumArgumentException?displayProperty=fullName>|
|Contém um formato que não atende às especificações de parâmetro de um método (como a cadeia de caracteres de formato para `ToString(String)`)|<xref:System.FormatException?displayProperty=fullName>|
|Caso contrário, inválido|<xref:System.ArgumentException?displayProperty=fullName>|

 Quando uma operação é inválida para o estado atual de um objeto throw <xref:System.InvalidOperationException?displayProperty=fullName>

 Quando uma operação é executada em um objeto que foi descartado throw <xref:System.ObjectDisposedException?displayProperty=fullName>

 Quando uma operação não tem suporte (como em um fluxo substituído **. gravar** em um fluxo aberto para leitura) throw <xref:System.NotSupportedException?displayProperty=fullName>

 Quando uma conversão resultaria em um estouro (como em uma sobrecarga de operador de conversão explícita), throw <xref:System.OverflowException?displayProperty=fullName>

 Para todas as outras situações, considere criar seu próprio tipo que deriva de <xref:System.Exception> e lançar isso.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o tipo da exceção gerada para um tipo específico que não seja um dos tipos reservados.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="related-rules"></a>Regras relacionadas
 [CA1031: não capturar tipos de exceção gerais](../code-quality/ca1031-do-not-catch-general-exception-types.md)
