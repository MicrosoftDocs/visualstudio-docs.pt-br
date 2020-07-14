---
title: Como exibir tipos existentes (Designer de Classe)
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.classdesigner.CannotShowBaseType
helpviewer_keywords:
- types [Visual Studio], visualizing
- types [Visual Studio], class diagrams
- class diagrams, types
ms.assetid: de110a4e-5b51-4a40-9dee-615df4d8f999
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fa27489844bc59bc0d4da32440cc1caa74ecbea6
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770003"
---
# <a name="how-to-view-existing-types-in-class-designer"></a>Como exibir tipos existentes no Designer de Classe

Para ver um tipo existente e seus membros, adicione sua forma a um diagrama de classe.

Você pode ver tipos locais e referenciados. Um tipo local existe no projeto atualmente aberto e é leitura/gravação. Um tipo referenciado existe em outro projeto ou em um assembly referenciado e é somente leitura.

Para criar novos tipos em diagramas de classe, consulte [como: criar tipos usando Designer de classe](how-to-create-types.md).

## <a name="to-see-types-in-a-project-on-a-class-diagram"></a>Para ver tipos de um projeto em um diagrama de classes

1. Em um projeto no **Gerenciador de soluções**, abra um arquivo de diagrama de classe (. CD) existente. Ou, se não houver nenhum diagrama de classes, adicione um novo ao projeto. Consulte [como: Adicionar diagramas de classe a projetos](how-to-add-class-diagrams-to-projects.md).

2. No projeto no **Gerenciador de soluções**, arraste um arquivo de código-fonte para o diagrama de classe.

    > [!NOTE]
    > Se sua solução tiver um projeto que compartilha código por vários aplicativos, você poderá arrastar arquivos ou código para um diagrama de classe apenas das seguintes fontes:
    >
    > - Do projeto de aplicativo que contém o diagrama
    > - De um projeto compartilhado que foi importado pelo projeto de aplicativo
    > - De um projeto referenciado
    > - De um assembly

    As formas que representam os tipos definidos no arquivo de código-fonte aparecem no diagrama na posição para a qual você arrastou o arquivo.

Você também pode exibir tipos no projeto arrastando um ou mais tipos do nó do projeto em **modo de exibição de classe** para o diagrama de classe.

> [!TIP]
> Se **modo de exibição de classe** não estiver aberto, abra **modo de exibição de classe** no menu **Exibir** .

Para exibir tipos em locais padrão no diagrama, selecione um ou mais tipos em **modo de exibição de classe**, clique com o botão direito do mouse nos tipos selecionados e escolha **Exibir diagrama de classe**.

> [!NOTE]
> Se um diagrama de classes fechado contendo o tipo já existir no projeto, o diagrama de classes será aberto para exibir a forma do tipo. No entanto, se nenhum diagrama de classe contendo o tipo existir no projeto, **Designer de classe** criará um novo diagrama de classe no projeto e o abrirá para exibir o tipo.

Quando você exibe um tipo no diagrama pela primeira vez, sua forma aparece recolhida por padrão. É possível expandir a forma para exibir seu conteúdo.

### <a name="to-display-the-contents-of-a-project-in-a-class-diagram"></a>Para exibir o conteúdo de um projeto em um diagrama de classe

Em **Gerenciador de soluções** ou **modo de exibição de classe**, clique com o botão direito do mouse no projeto e escolha **Exibir**e, em seguida, escolha **Exibir diagrama de classe**. Um Diagrama de Classe populado automaticamente é criado.

## <a name="see-also"></a>Confira também

- [Como exibir herança entre tipos](how-to-view-inheritance-between-types.md)
- [Como: Personalizar diagramas de classe](how-to-customize-class-diagrams.md)
- [Exibindo tipos e relações](designing-and-viewing-classes-and-types.md)
