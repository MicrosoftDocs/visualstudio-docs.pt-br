---
title: Como alterar entre notação de membro e notação de associação (Designer de Classe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- notation, member
- association notation
- member notation
- notation, association
ms.assetid: 65881c5a-d251-4a36-ad0d-73d088436092
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bdb4f28fc367b309a015a3faa8f749e2512db879
ms.sourcegitcommit: 4c0db930d9d5d8b857d3baf2530ae89823799612
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "33957795"
---
# <a name="how-to-change-between-member-notation-and-association-notation-in-class-designer"></a>Como alterar entre notação de membro e notação de associação no Designer de Classe

No **Designer de Classe**, você pode alterar a maneira que o diagrama de classe representa uma relação de associação entre dois tipos de notação de membro para notação de associação e vice-versa. Membros exibidos como linhas de associação geralmente fornecem uma visualização útil de como os tipos estão relacionados.

> [!NOTE]
> Os relacionamentos de associação podem ser representados como um campo ou uma propriedade de membro. Para alterar notação de membro para notação de associação, um tipo deve ter um membro de outro tipo. Para alterar notação de associação para a notação de membro, os dois tipos devem estar conectados por uma linha de associação. Para obter mais informações, confira [Como criar associações entre tipos](how-to-create-associations-between-types.md). Se o projeto contiver vários diagramas de classe, as alterações feitas na forma como um diagrama exibe os relacionamentos de associação afetarão somente esse diagrama. Para alterar a maneira como outro diagrama exibe os relacionamentos de associação, abra ou exiba esse diagrama e execute estas etapas.

## <a name="to-change-member-notation-to-association-notation"></a>Para alterar de notação de membro para notação de associação

1.  No nó do projeto no Gerenciador de Soluções, abra um arquivo de diagrama de classe (.cd).

2.  Na forma de tipo no diagrama de classe, clique com o botão direito do mouse na propriedade do membro ou no campo que representa a associação e escolha **Mostrar como Associação**.

    > [!TIP]
    > Se não houver campos ou propriedades visíveis na forma de tipo, os compartimentos da forma poderão ser recolhidos. Para expandir a forma do tipo, clique duas vezes no nome do compartimento ou clique com o botão direito do mouse na forma de tipo e escolha **Expandir**.

    O membro desaparece do compartimento na forma de tipo e uma linha de associação é exibida para conectar os dois tipos. A linha de associação é rotulada com o nome da propriedade ou do campo.

## <a name="to-change-association-notation-to-member-notation"></a>Para alterar de notação de associação para notação de membro

No diagrama de classe, clique com o botão direito do mouse na linha de associação e escolha **Mostrar como Propriedade** ou **Mostrar como Campo**, conforme apropriado. A linha de associação desaparece e a propriedade é exibida no compartimento apropriado em sua forma de tipo no diagrama.

## <a name="see-also"></a>Consulte também

- [Como criar herança entre tipos](how-to-create-inheritance-between-types.md)
- [Como exibir herança entre tipos](how-to-view-inheritance-between-types.md)
- [Exibindo tipos e relações](viewing-types-and-relationships.md)
- [Como visualizar uma associação de coleção](how-to-visualize-a-collection-association.md)