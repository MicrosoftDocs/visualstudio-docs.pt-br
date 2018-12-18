---
title: Como criar tipos usando Designer de Classe
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.Clr.ClrAttributesDialog
helpviewer_keywords:
- custom attributes, applying
- class diagrams, creating types
- classes [Visual Studio], creating with Class Designer
- Class Designer [Visual Studio], creating classes
- types [Visual Studio], class diagrams
- attributes [Visual Studio], applying custom
ms.assetid: 94458c31-28bc-40e2-9737-85868788a0e5
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 769bcfa202961c5a492e4fcb5af8e522b9052059
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49842255"
---
# <a name="how-to-create-types-by-using-class-designer"></a>Como criar tipos usando o Designer de Classe

Para criar novos tipos para projetos em C# e Visual Basic, você precisa criá-los em um diagrama de classe. Para ver os tipos existentes, consulte [Como exibir tipos existentes](how-to-view-existing-types.md).

##  <a name="CreateType"></a> Criar um novo tipo

1.  Na **Caixa de Ferramentas**, no **Designer de Classe**, arraste um dos itens abaixo para um diagrama de classe:

    -   **Classe** ou **Classe Abstrata**

    -   **Enum**

    -   **Interface**

    -   **Estrutura** (VB) ou **Struct** (C#)

    -   **Delegado**

    -   **Módulo** (apenas VB)

2.  Dê um nome ao tipo. Selecione o nível de acesso.

3.  Selecione o arquivo em que deseja adicionar o código inicial para o tipo:

    -   Para criar um novo arquivo e adicioná-lo ao projeto atual, selecione **Criar novo arquivo** e dê um nome ao arquivo.

    -   Para adicionar código a um arquivo existente, selecione **Adicionar a arquivo existente**.

         Se sua solução tiver um projeto que compartilha código entre vários aplicativos, você poderá adicionar um novo tipo a um diagrama de classes no projeto do aplicativo, mas somente se o arquivo de classe correspondente estiver no mesmo projeto de aplicativo ou no projeto compartilhado.

4.  Agora adicione outros itens para definir o tipo:

    |||
    |-|-|
    |**Para**|**Adicionar**|
    |Classes, classes abstratas, estruturas ou structs|Métodos, propriedades, campos, eventos, construtores (método), destruidores (método) e constantes que definem o tipo|
    |Enums|Valores de campo que compõem a enumeração|
    |Interfaces|Métodos, propriedades e eventos que compõem a interface|
    |delegado|Parâmetros que definem o representante|
    |Módulo|Métodos, propriedades, campos, eventos, construtores (método) e constantes que definem o módulo|

     Consulte [Criando membros](creating-and-configuring-type-members.md#create-members).

##  <a name="CustAttributeType"></a> Aplicar um atributo personalizado a um tipo

1. Clique na forma do tipo em um diagrama de classes.

2. Na janela **Propriedades**, ao lado da propriedade **Atributos Personalizados** do tipo, clique no botão de reticências (…).

3. Adicione um ou mais atributos personalizados, um por linha. Não os coloque entre colchetes.

   Os atributos personalizados são aplicados ao tipo.

##  <a name="CustAttributeMember"></a> Aplicar um atributo personalizado a um membro de tipo

1. Clique no nome do membro na forma de seu tipo em um diagrama de classes ou em sua linha na janela Detalhes da Classe.

2. Na janela **Propriedades**, localize a propriedade **Atributos Personalizados** do membro.

3. Adicione um ou mais atributos personalizados, um por linha. Não os coloque entre colchetes.

   Os atributos personalizados são aplicados ao tipo.

## <a name="see-also"></a>Consulte também

- [Como criar herança entre tipos](how-to-create-inheritance-between-types.md)
- [Como criar associações entre tipos](how-to-create-associations-between-types.md)
- [Criando e configurando membros de tipo](creating-and-configuring-type-members.md)
- [Trabalhando com diagramas de classe](working-with-class-diagrams.md)
- [Projetando classes e tipos](designing-and-viewing-classes-and-types.md)
