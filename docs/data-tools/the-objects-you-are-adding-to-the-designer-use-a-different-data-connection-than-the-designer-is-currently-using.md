---
title: Os objetos você estiver adicionando ao uso de designer uma conexão de dados diferente do designer está usando atualmente
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 332ed2f3-3377-4d51-8e3b-fdb98231978e
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: a2fb26fa8960c652feefa157fb04c31b9ed7abb9
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174162"
---
# <a name="the-objects-you-are-adding-to-the-designer-use-a-different-data-connection-than-the-designer"></a>Os objetos que você está adicionando ao designer usam uma conexão de dados diferente que o designer

Os objetos que você está adicionando ao designer usam uma conexão de dados diferente da que o designer está usando no momento. Deseja substituir a conexão usada pelo designer?

Quando você adiciona itens para o **Object Relational Designer** (**Relational Designer**), todos os itens usam uma conexão de dados compartilhada. (A superfície de design representa <xref:System.Data.Linq.DataContext>, que usa uma única conexão para todos os objetos na superfície.) Se você adicionar um objeto para o designer que usa uma conexão de dados que seja diferente de conexão de dados atualmente sendo usada pelo designer, esta mensagem aparece. Para resolver esse erro, você pode escolher para manter a conexão existente. Se você fizer essa opção, o objeto selecionado não será adicionado. Como alternativa, você pode optar por adicionar o objeto e redefinir o <xref:System.Data.Linq.DataContext> conexão para a nova conexão.

> [!NOTE]
> Se você clicar **Sim**, classes de entidade todas na **Relational Designer** são mapeados para a nova conexão.

## <a name="to-replace-the-existing-connection-with-the-connection-used-by-the-selected-object"></a>Para substituir a conexão existente com a conexão usada pelo objeto selecionado

- Clique em **Sim**.

    O objeto selecionado é adicionado para o **Relational Designer**e o *DataContext* é definido como a nova conexão.

## <a name="to-continue-to-use-the-existing-connection-and-cancel-adding-the-selected-object"></a>Para continuar a usar a conexão e cancelar existentes que adicionam o objeto selecionado

- Clique em **Não**.

    A ação é cancelada. O *DataContext* permanecerá definido para a conexão existente.

## <a name="see-also"></a>Consulte também

- [Mensagens do O/R Designer](../data-tools/o-r-designer-messages.md)
- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
