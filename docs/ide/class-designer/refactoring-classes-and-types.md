---
title: Renomear e mover classes e tipos no Designer de Classe
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.ClassDesigner.OverrideMembersDialog
helpviewer_keywords:
- members, overriding
- overriding members
- classes [Visual Studio], refactoring
- type members, overriding
- refactoring, types
- types [Visual Studio], refactoring
- Class Designer [Visual Studio], refactoring classes
- refactoring, classes
ms.assetid: dcf07bb4-fa3b-4224-9dec-566fd924a8ce
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: baf0e9d9d0f4bb45ef965f64c256bd9360af112b
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768609"
---
# <a name="refactor-classes-and-types-in-class-designer"></a>Refatorar classes e tipos no Designer de Classe

Quando você refatora o código, ele fica mais fácil de entender, manter e mais eficiente, alterando a estrutura interna e como os seus objetos são criados, não o comportamento externo dele. Use o Designer de Classe e a janela Detalhes da Classe para reduzir o trabalho necessário e a possibilidade de introduzir bugs quando você refatora o código do C#, Visual Basic ou C++ no projeto do Visual Studio.

> [!NOTE]
> Os arquivos de um projeto podem ser somente leitura porque o projeto está sob controle do código-fonte e não foi submetido a check-out, é um projeto referenciado ou os arquivos estão marcados como somente leitura no disco. Ao trabalhar em um projeto em um desses estados, você terá várias maneiras de salvar o trabalho, dependendo do estado do projeto. Isso se aplica ao código de refatoração e também ao código que você altera de outra forma, como editando-o diretamente.

## <a name="common-tasks"></a>Tarefas comuns

|Tarefa|Conteúdo de suporte|
|----------| - |
|**Classes de refatoração:** você pode usar as operações de refatoração para dividir uma classe em classes parciais ou para implementar uma classe base abstrata.|-   [Como dividir uma classe em classes parciais](how-to-split-a-class-into-partial-classes.md)|
|**Trabalho com interfaces:** no Designer de Classe, você pode implementar uma interface no diagrama de classe se ela for conectada a uma classe que fornece o código para os métodos de interface.|-   [Como implementar uma interface](how-to-implement-an-interface.md)|
|**Refatoração de tipos, membros de tipo e parâmetros:** usando o Designer de Classe, você pode renomear tipos, substituir membros de tipo ou movê-los de um tipo para outro. Você também pode criar tipos que permitem valor nulo.|-   [Renomear tipos e membros de tipo](#rename-types-and-type-members)<br />-   [Mover membros de tipo de um tipo para outro](#move-type-members-from-one-type-to-another)<br />-   [Como criar um tipo que permite valor nulo](how-to-create-a-nullable-type.md)|

## <a name="rename-types-and-type-members"></a>Renomear tipos e membros de tipo

No Designer de Classe, é possível renomear um tipo ou membro de um tipo no diagrama de classe ou na janela **Propriedades**. Na janela **Detalhes da Classe**, é possível alterar o nome de um membro, mas não um tipo. A renomeação de um tipo ou membro do tipo propaga para todas as janelas e locais de código onde o nome antigo é exibido.

### <a name="rename-in-the-class-designer"></a>Renomear no Designer de Classe

1. No diagrama de classe, selecione o tipo ou membro e clique no nome.

     O nome do membro se torna editável.

2. Digite o novo nome do tipo ou membro do tipo

### <a name="rename-in-the-class-details-window"></a>Renomear na janela Detalhes da Classe

1. Para exibir a janela **Detalhes da Classe**, clique com o botão direito do mouse no tipo ou membro de tipo e clique em **Detalhes da Classe**.

     A janela **Detalhes da Classe** será exibida.

2. Na coluna **Nome**, altere o nome do membro de tipo

3. Para mover o foco para fora da célula, pressione a tecla **Enter** ou clique fora da célula.

    > [!NOTE]
    > Na janela **Detalhes da Classe**, é possível alterar o nome de um membro, mas não um tipo.

### <a name="rename-in-the-properties-window"></a>Renomear na janela Propriedades

1. No diagrama de classe ou na janela **Detalhes da Classe**, clique com o botão direito do mouse no tipo ou membro e selecione **Propriedades**.

     A janela **Propriedades** aparecerá e exibirá as propriedades do tipo ou membro do tipo.

2. Na propriedade **Nome**, altere o nome do tipo ou do membro de tipo.

     O novo nome propagada para todas as janelas e locais de código no projeto atual em que o nome antigo é exibido.

## <a name="move-type-members-from-one-type-to-another"></a>Mover membros de tipo de um tipo para outro

Com o **Designer de Classe**, é possível mover um membro de tipo de um tipo para outro. Ambos precisam estar visíveis no diagrama de classe atual.

1. Em um tipo visível na área de design, clique com o botão direito do mouse sobre o membro que você deseja mover para o outro tipo e clique em **Recortar**.

2. Clique com o botão direito do mouse no tipo de destino e clique em **Colar**.

     A propriedade é removida do tipo de origem e aparece no tipo de destino.

## <a name="see-also"></a>Confira também

- [Projetando classes e tipos](designing-and-viewing-classes-and-types.md)
