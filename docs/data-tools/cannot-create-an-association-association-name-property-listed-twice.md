---
title: Não é possível criar uma associação - propriedade listada duas vezes
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 3ced8bda-210e-4caf-9d8f-96cdbba19251
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: d508cc407087e481ff77e29956db7511bba81165
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31916823"
---
# <a name="cannot-create-an-association-ltassociation-namegt---property-listed-twice"></a>Não é possível criar uma associação &lt;nome da associação&gt; -propriedade listada duas vezes

Não é possível criar uma associação \<nome da associação >. A mesma propriedade está listada mais de uma vez: \<nome da propriedade >.

Associações definidas pelo selecionado **propriedades de associação** no **Editor de associação** caixa de diálogo. As propriedades podem ser listadas apenas uma vez para cada classe na associação.

A propriedade na mensagem aparece mais de uma vez da classe pai ou filho **propriedades de associação**.

## <a name="to-resolve-this-condition"></a>Para resolver essa condição

- Examine a mensagem e observe a propriedade especificada na mensagem.

- Clique em **Okey** para fechar a caixa de mensagem.

- Inspecione o **propriedades de associação** e remova as entradas duplicadas.

- Clique em **OK**.

## <a name="see-also"></a>Consulte também

- [Mensagens do O/R Designer](../data-tools/o-r-designer-messages.md)
- [LINQ to SQL tools no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Como: criar uma associação entre classes LINQ to SQL (Object Relational Designer)](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md)