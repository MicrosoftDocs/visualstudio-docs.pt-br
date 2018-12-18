---
title: 'CA1700: Não nomeie valores de enumeração &#39;reservado&#39;'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1700
- DoNotNameEnumValuesReserved
helpviewer_keywords:
- DoNotNameEnumValuesReserved
- CA1700
ms.assetid: 7a7e01c3-ae7d-4c82-a646-91b58864a749
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3c5d1cff8f6833696bdb74dbf145b14aaaaaf509
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49883660"
---
# <a name="ca1700-do-not-name-enum-values-39reserved39"></a>CA1700: Não nomeie valores de enumeração &#39;reservado&#39;

|||
|-|-|
|NomeDoTipo|DoNotNameEnumValuesReserved|
|CheckId|CA1700|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

O nome de um membro de enumeração contém a palavra "reservados".

## <a name="rule-description"></a>Descrição da regra

Esta regra pressupõe que um membro da enumeração que tenha um nome que contém "reserved" não é usado atualmente, mas é um espaço reservado a ser renomeado ou removido em uma versão futura. Renomear ou remover um membro é uma alteração drástica. Você não deve esperar que os usuários ignorem um membro apenas porque seu nome contém "reservados", nem você pode contar os usuários leiam ou obedecer a documentação. Além disso, como membros reservados aparecem em ambientes de desenvolvimento integrado inteligente e pesquisadores de objetos, eles podem causar confusão sobre quais membros são realmente sendo usados.

Em vez de usar um membro reservado, adicione um novo membro à enumeração na versão futura. Na maioria dos casos a adição do novo membro não é uma alteração significativa, desde que a adição não faz com que os valores dos membros originais para alterar.

Em um número limitado de casos a adição de um membro é uma alteração significativa, mesmo quando os membros originais retêm seus valores originais. Basicamente, o novo membro não pode ser retornado de caminhos de código existente sem interromper os chamadores que usam um `switch` (`Select` em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) instrução no valor de retorno que abrange a lista inteira de membro e que geram uma exceção caso padrão. Uma preocupação secundária é que o código de cliente talvez não lidar com a alteração no comportamento dos métodos de reflexão, como <xref:System.Enum.IsDefined%2A?displayProperty=fullName>. Da mesma forma, se o novo membro tiver a serem retornados de métodos existentes ou uma incompatibilidade de aplicativos conhecidos ocorre devido ao uso de reflexão ruim, a única solução incondicional é:

1. Adicione uma nova enumeração que contém os membros novos e originais.

2. Marque a enumeração original com o <xref:System.ObsoleteAttribute?displayProperty=fullName> atributo.

   Siga o mesmo procedimento para todos os tipos visíveis externamente ou membros que expõem a enumeração original.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, remova ou renomeie o membro.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso nessa regra para um membro que é usado no momento ou para bibliotecas que foram enviados anteriormente.

## <a name="related-rules"></a>Regras relacionadas

[CA2217: não marcar enums com FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

[CA1712: não usar valores de enum como prefixo com o nome do tipo](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)

[CA1028: o armazenamento de enum deve ser Int32](../code-quality/ca1028-enum-storage-should-be-int32.md)

[CA1008: as enums devem ter valor zero](../code-quality/ca1008-enums-should-have-zero-value.md)

[CA1027: marcar enums com FlagsAttribute](../code-quality/ca1027-mark-enums-with-flagsattribute.md)