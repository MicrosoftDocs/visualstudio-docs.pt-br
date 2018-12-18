---
title: Como exibir tipos existentes (Designer de Classe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.CannotShowBaseType
helpviewer_keywords:
- types [Visual Studio], visualizing
- types [Visual Studio], class diagrams
- class diagrams, types
ms.assetid: de110a4e-5b51-4a40-9dee-615df4d8f999
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6f477f64188c9592db65d0a82c8a1b8b3ec5b776
ms.sourcegitcommit: 4c0db930d9d5d8b857d3baf2530ae89823799612
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "33956647"
---
# <a name="how-to-view-existing-types-in-class-designer"></a>Como exibir tipos existentes no Designer de Classe

Para ver um tipo existente e seus membros, adicione sua forma a um diagrama de classe.

Você pode ver tipos locais e referenciados. Um tipo local existe no projeto atualmente aberto e é leitura/gravação. Um tipo referenciado existe em outro projeto ou em um assembly referenciado e é somente leitura.

Para criar tipos em diagramas de classe, confira [Como criar tipos usando o Designer de Classe](how-to-create-types.md).

## <a name="to-see-types-in-a-project-on-a-class-diagram"></a>Para ver tipos de um projeto em um diagrama de classes

1.  Em um projeto no **Gerenciador de Soluções**, abra um arquivo de diagrama de classe (.cd) existente. Ou, se não houver nenhum diagrama de classes, adicione um novo ao projeto. Consulte [Como adicionar diagramas de classe a projetos](how-to-add-class-diagrams-to-projects.md).

2.  No projeto localizado no **Gerenciador de Soluções**, arraste um arquivo de código-fonte para o diagrama de classe.

    > [!NOTE]
    > Se sua solução tiver um projeto que compartilha código por vários aplicativos, você poderá arrastar arquivos ou código para um diagrama de classe apenas das seguintes fontes:
    >
    > - Do projeto de aplicativo que contém o diagrama
    > - De um projeto compartilhado que foi importado pelo projeto de aplicativo
    > - De um projeto referenciado
    > - De um assembly

    As formas que representam os tipos definidos no arquivo de código-fonte aparecem no diagrama na posição para a qual você arrastou o arquivo.

Também é possível exibir tipos no projeto arrastando um ou mais tipos do nó do projeto no **Modo de Exibição de Classe** para o diagrama de classe.

> [!TIP]
> Se o **Modo de Exibição de Classe** não estiver aberto, abra o **Modo de Exibição de Classe** no menu **Exibir**.

Para exibir tipos em locais padrão no diagrama, selecione um ou mais tipos no **Modo de Exibição de Classe**, clique com o botão direito do mouse nos tipos selecionados e escolha **Exibir Diagrama de Classe**.

> [!NOTE]
> Se um diagrama de classes fechado contendo o tipo já existir no projeto, o diagrama de classes será aberto para exibir a forma do tipo. No entanto, se nenhum diagrama de classe contiver o tipo que existe no projeto, o **Designer de Classe** criará um diagrama de classe no projeto e o abrirá para exibir o tipo.

Quando você exibe um tipo no diagrama pela primeira vez, sua forma aparece recolhida por padrão. É possível expandir a forma para exibir seu conteúdo.

### <a name="to-display-the-contents-of-a-project-in-a-class-diagram"></a>Para exibir o conteúdo de um projeto em um diagrama de classe

No **Gerenciador de Soluções** ou no **Modo de Exibição de Classe**, clique com o botão direito do mouse no projeto e escolha **Exibir** e, em seguida, escolha **Exibir Diagrama de Classe**. Um Diagrama de Classe populado automaticamente é criado.

## <a name="see-also"></a>Consulte também

- [Como exibir herança entre tipos](how-to-view-inheritance-between-types.md)
- [Como personalizar diagramas de classe](how-to-customize-class-diagrams.md)
- [Exibindo tipos e relações](viewing-types-and-relationships.md)