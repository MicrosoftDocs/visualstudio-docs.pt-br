---
title: 'CA1725: Nomes de parâmetro devem corresponder à declaração base | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ParameterNamesShouldMatchBaseDeclaration
- CA1725
helpviewer_keywords:
- CA1725
- ParameterNamesShouldMatchBaseDeclaration
ms.assetid: 9b657ab0-fe81-4f4c-9481-ba746988c922
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: e97431b46640fb8241d6bde80d09d38084650be8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68143167"
---
# <a name="ca1725-parameter-names-should-match-base-declaration"></a>CA1725: Nomes de parâmetros devem corresponder à declaração base
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ParameterNamesShouldMatchBaseDeclaration|
|CheckId|CA1725|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O nome de um parâmetro em uma substituição do método visível externamente não coincide com o nome do parâmetro em que a declaração do método de base ou o nome do parâmetro na declaração de interface do método.

## <a name="rule-description"></a>Descrição da Regra
 A nomenclatura consistente dos parâmetros em uma hierarquia de substituição aumenta a usabilidade das substituições de método. Um nome de parâmetro em um método derivado diferente do nome na declaração de base pode causar confusão em relação à possibilidade do método ser uma substituição do método de base ou de uma nova sobrecarga do método.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, renomeie o parâmetro para corresponder à declaração base. A correção é uma alteração significativa para os métodos visíveis.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra, exceto para os métodos visíveis nas bibliotecas que foram enviados anteriormente.
