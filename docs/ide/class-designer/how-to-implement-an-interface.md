---
title: Como implementar uma interface (Designer de Classe)
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interfaces [Visual Studio], implementing
- interfaces [Visual Studio]
ms.assetid: 81d2cf46-7f60-448c-83e3-1d16bb88ca36
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bf03046abcf79933044cfb01bf079aee64d09077
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72647710"
---
# <a name="how-to-implement-an-interface-in-class-designer"></a>Como implementar uma interface no Designer de Classe

No **Designer de Classe**, você pode implementar uma interface no diagrama de classe conectando-a a uma classe que forneça código para os métodos da interface. O **Designer de Classe** gera uma implementação da interface e exibe a relação entre a interface e a classe como uma relação de herança. É possível implementar uma interface desenhando uma linha de herança entre a interface e a classe ou arrastando a interface do Modo de Exibição de Classe.

> [!TIP]
> Você pode criar interfaces da mesma maneira como cria outros tipos. Se a interface existir, mas não aparecer no diagrama de classe, exiba-a primeiro. Para obter mais informações, confira [Como criar tipos usando o Designer de Classe](how-to-create-types.md) e [Como exibir tipos existentes](how-to-view-existing-types.md).

## <a name="to-implement-an-interface-by-drawing-an-inheritance-line"></a>Para implementar uma interface desenhando uma linha de herança

1. No diagrama de classe, exiba a interface e a classe que a implementará.

2. Desenhe uma linha de herança da classe e da interface.

     Um pirulito aparece anexado à classe, e um rótulo com o nome da interface identifica a relação de herança. O Visual Studio gera stubs para todos os membros da interface.

Para obter mais informações, confira [Como criar herança entre tipos](how-to-create-inheritance-between-types.md).

## <a name="to-implement-an-interface-from-the-class-view-window"></a>Para implementar uma interface da janela do Modo de Exibição de Classe

1. No diagrama de classe, exiba a classe cuja interface você deseja implementar.

2. Abra o **Modo de Exibição de Classe** e localize a interface.

    > [!TIP]
    > Se o **Modo de Exibição de Classe** não estiver aberto, abra o **Modo de Exibição de Classe** no menu **Exibir** ou pressione **Ctrl**+**Shift**+**C**.

3. Arraste o nó da interface para a forma de classe no diagrama.

     Um pirulito aparece anexado à classe, e um rótulo com o nome da interface identifica a relação de herança. O Visual Studio gera stubs para todos os membros da interface. Neste ponto, a interface é implementada.

## <a name="see-also"></a>Consulte também

- [Como criar tipos usando o Designer de Classe](how-to-create-types.md)
- [Como exibir tipos existentes](how-to-view-existing-types.md)
- [Como criar herança entre tipos](how-to-create-inheritance-between-types.md)
- [Refatorando classes e tipos](refactoring-classes-and-types.md)