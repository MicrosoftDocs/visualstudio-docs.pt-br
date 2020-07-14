---
title: A propriedade não pode ser excluída porque participa da associação
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 389873cc-92dd-48da-bfca-0f6c8e0ae3c2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: aab2d2e3151786b45889262680d2f0815f684b6a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535376"
---
# <a name="the-property-ltproperty-namegt-cannot-be-deleted-because-it-is-participating-in-the-association-ltassociation-namegt"></a>A propriedade &lt;nome da propriedade&gt; não pode ser excluída porque está participando da associação &lt;nome da associação&gt;

A propriedade selecionada é definida como **Propriedade de associação** para a associação entre as classes mencionadas na mensagem de erro. Propriedades não podem ser excluídas estão participando em uma associação entre classes de dados.

Defina **Propriedade de Associação** para uma propriedade diferente da classe de dados para permitir que a propriedade desejada seja excluída com êxito.

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Selecione a linha de associação no **Designer de o/R** que conecta as classes de dados indicadas na mensagem de erro.

2. Clique duas vezes na linha para abrir a caixa de diálogo **Editor de Associação**.

3. Remova a propriedade de **Propriedades de Associação**.

4. Tente excluir novamente a propriedade.

## <a name="see-also"></a>Confira também

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)