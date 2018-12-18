---
title: A propriedade não pode ser excluída.
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 55873f74-7834-4ec1-8815-eeeb65618d87
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 7e85860de7494ae7d93ad37bd0a115fa786f0a87
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174007"
---
# <a name="the-property-property-name-cannot-be-deleted"></a>A propriedade \<nome da propriedade > não pode ser excluído

A propriedade \<nome da propriedade > não pode ser excluído porque ele está definido como o **propriedade discriminatória** para herança entre \<nome da classe > e \<nome de classe >

A propriedade selecionada é definida como o **propriedade discriminatória** para herança entre as classes mencionadas na mensagem de erro. Propriedades não podem ser excluídas estão participando na configuração de herança entre classes de dados.

Defina as **propriedade discriminatória** a uma propriedade diferente da classe de dados para permitir a exclusão de bem-sucedida da propriedade desejada.

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. No **Relational Designer**, selecione a linha de herança que conecta as classes de dados indicada na mensagem de erro.

2. Defina as **discriminador** propriedade a uma propriedade diferente.

3. Tente excluir novamente a propriedade.

## <a name="see-also"></a>Consulte também

- [Mensagens do O/R Designer](../data-tools/o-r-designer-messages.md)
- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)