---
title: 'CA1044: As propriedades não devem ser somente gravação | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- PropertiesShouldNotBeWriteOnly
- CA1044
helpviewer_keywords:
- CA1044
- PropertiesShouldNotBeWriteOnly
ms.assetid: 8386bf3a-b161-4841-bf8b-92591595aea9
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 4b6d0d37d68951d556cdb575897178bd07a55a6e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49860832"
---
# <a name="ca1044-properties-should-not-be-write-only"></a>CA1044: as propriedades não devem ser somente leitura
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|PropertiesShouldNotBeWriteOnly|
|CheckId|CA1044|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 A propriedade pública ou protegida tem um acessador set, mas não tem um acessador get.

## <a name="rule-description"></a>Descrição da Regra
 Obtenha acessadores fornecem acesso de leitura a uma propriedade e acessadores set fornecem acesso de gravação. Embora seja aceitável e normalmente necessário ter uma propriedade somente leitura, as diretrizes de design proíbem o uso de propriedades somente gravação. Isso ocorre porque, permitindo que um usuário defina um valor e, em seguida, impedindo que o usuário visualizando o valor não oferece nenhuma segurança. Além disso, sem acesso de leitura, o estado de objetos compartilhados não pode ser exibido, o que limita sua utilidade.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione um acessador get para a propriedade. Como alternativa, se o comportamento de uma propriedade somente gravação for necessário, considere converter essa propriedade para um método.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É altamente recomendável que você não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 No exemplo a seguir, `BadClassWithWriteOnlyProperty` é um tipo com uma propriedade somente gravação. `GoodClassWithReadWriteProperty` contém o código corrigido.

 [!code-csharp[FxCop.Design.PropertiesNotWriteOnly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.PropertiesNotWriteOnly/cs/FxCop.Design.PropertiesNotWriteOnly.cs#1)]
 [!code-vb[FxCop.Design.PropertiesNotWriteOnly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.PropertiesNotWriteOnly/vb/PropertiesNotWriteOnly.vb#1)]



