---
title: A propriedade não pode ser excluída
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 55873f74-7834-4ec1-8815-eeeb65618d87
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 63e99bf7b247856815fd3e8de0f4932fed4881dc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535285"
---
# <a name="the-property-property-name-cannot-be-deleted"></a>A propriedade \<property name> não pode ser excluída

A propriedade \<property name> não pode ser excluída porque está definida como a **Propriedade discriminadora** para a herança entre \<class name> e\<class name>

A propriedade selecionada está definida como a **propriedade discriminatória** para herança entre as classes mencionadas na mensagem de erro. Propriedades não podem ser excluídas estão participando na configuração de herança entre classes de dados.

Defina a **propriedade discriminatória** para uma propriedade diferente da classe de dados para permitir que a propriedade desejada seja excluída com êxito.

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. No o **/R Designer**, selecione a linha de herança que conecta as classes de dados indicadas na mensagem de erro.

2. Defina a propriedade **discriminatória** para uma propriedade diferente.

3. Tente excluir novamente a propriedade.

## <a name="see-also"></a>Confira também

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)