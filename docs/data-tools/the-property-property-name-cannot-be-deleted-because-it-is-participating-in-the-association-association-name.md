---
title: A propriedade não pode ser excluída porque participa da associação
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 389873cc-92dd-48da-bfca-0f6c8e0ae3c2
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 6ed6b14f64d16d1f18d4b358761169c3d424cee8
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174056"
---
# <a name="the-property-ltproperty-namegt-cannot-be-deleted-because-it-is-participating-in-the-association-ltassociation-namegt"></a>A propriedade &lt;nome da propriedade&gt; não pode ser excluída porque participa da associação &lt;nome da associação&gt;

A propriedade selecionada é definida como o **associação de propriedade** para a associação entre as classes mencionadas na mensagem de erro. Propriedades não podem ser excluídas estão participando em uma associação entre classes de dados.

Defina as **associação de propriedade** a uma propriedade diferente da classe de dados para permitir a exclusão de bem-sucedida da propriedade desejada.

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Selecione a linha de associação sobre o **Relational Designer** que conecta as classes de dados indicadas na mensagem de erro.

2. Clique duas vezes na linha para abrir o **Editor de associação** caixa de diálogo.

3. Remover a propriedade de **propriedades de associação**.

4. Tente excluir novamente a propriedade.

## <a name="see-also"></a>Consulte também

- [Mensagens do O/R Designer](../data-tools/o-r-designer-messages.md)
- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)