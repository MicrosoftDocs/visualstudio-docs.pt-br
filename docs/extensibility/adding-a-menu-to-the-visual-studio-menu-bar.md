---
title: Adicionando um menu à barra de menus do Visual Studio | Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- menus, creating top level
- top-level menus
ms.assetid: 58fc1a31-2aeb-441c-8e48-c7d5cbcfe501
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 39dee051991efe05b9a661ce1d213e71b456590b
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904257"
---
# <a name="add-a-menu-to-the-visual-studio-menu-bar"></a>Adicionar um menu à barra de menus do Visual Studio

Este tutorial mostra como adicionar um menu à barra de menus do IDE (ambiente de desenvolvimento integrado) do Visual Studio. A barra de menus do IDE contém categorias de menu, como **arquivo**, **Editar**, **Exibir**, **janela**e **ajuda**.

Antes de adicionar um novo menu à barra de menus do Visual Studio, considere se os comandos devem ser colocados em um menu existente. Para obter mais informações sobre o posicionamento do comando, consulte [menus e comandos para o Visual Studio](../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md).

Os menus são declarados no arquivo *. vsct* do projeto. Para obter mais informações sobre menus e arquivos *. vsct* , consulte [comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).

Ao concluir este passo a passos, você pode criar um menu chamado **TestMenu** que contém um comando.

:::moniker range=">=vs-2019"
> [!NOTE]
> A partir do Visual Studio 2019, os menus de nível superior contribuídos por extensões são colocados no menu **extensões** .
:::moniker-end

## <a name="prerequisites"></a>Pré-requisitos

A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-vsix-project-that-has-a-custom-command-item-template"></a>Criar um projeto VSIX que tenha um modelo de item de comando personalizado

1. Crie um projeto VSIX denominado `TopLevelMenu` . Você pode encontrar o modelo de projeto VSIX na caixa de diálogo **novo projeto** pesquisando por "VSIX".  Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

2. Quando o projeto for aberto, adicione um modelo de item de comando personalizado chamado **TestCommand**. Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >   **novo item**. Na caixa de diálogo **Adicionar novo item** , vá para **Visual C#/extensibilidade** e selecione **comando personalizado**. No campo **nome** na parte inferior da janela, altere o nome do arquivo de comando para *TestCommand.cs*.

## <a name="create-a-menu-on-the-ide-menu-bar"></a>Criar um menu na barra de menus do IDE

::: moniker range="vs-2017"

1. Em **Gerenciador de soluções**, abra *TestCommandPackage. vsct*.

    No final do arquivo, há um \<Symbols> nó que contém vários \<GuidSymbol> nós. No nó chamado guidTestCommandPackageCmdSet, adicione um novo símbolo, da seguinte maneira:

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. Crie um \<Menus> nó vazio no \<Commands> nó, logo antes de \<Groups> . No \<Menus> nó, adicione um \<Menu> nó, da seguinte maneira:

   ```xml
   <Menus>
         <Menu guid="guidTestCommandPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
           <Parent guid="guidSHLMainMenu"
                   id="IDG_VS_MM_TOOLSADDINS" />
           <Strings>
             <ButtonText>TestMenu</ButtonText>
             <CommandName>TestMenu</CommandName>
           </Strings>
       </Menu>
   </Menus>
   ```

    Os `guid` `id` valores e do menu especificam o conjunto de comandos e o menu específico no conjunto de comandos.

    Os `guid` `id` valores e do pai posicionam o menu na seção da barra de menus do Visual Studio que contém os menus ferramentas e suplementos.

    O valor da `CommandName` cadeia de caracteres especifica que o texto deve aparecer no item de menu.

3. Na \<Groups> seção, localize \<Group> e altere o \<Parent> elemento para apontar para o menu que acabamos de adicionar:

   ```xml
   <Groups>
       <Group guid="guidTestCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTestCommandPackageCmdSet" id="TopLevelMenu"/>
       </Group>
   </Groups>
   ```

    Isso faz com que o grupo faça parte do novo menu.

::: moniker-end

::: moniker range=">=vs-2019"

1. Em **Gerenciador de soluções**, abra *TopLevelMenuPackage. vsct*.

    No final do arquivo, há um \<Symbols> nó que contém vários \<GuidSymbol> nós. No nó chamado guidTopLevelMenuPackageCmdSet, adicione um novo símbolo, da seguinte maneira:

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. Crie um \<Menus> nó vazio no \<Commands> nó, logo antes de \<Groups> . No \<Menus> nó, adicione um \<Menu> nó, da seguinte maneira:

   ```xml
   <Menus>
         <Menu guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
           <Parent guid="guidSHLMainMenu"
                   id="IDG_VS_MM_TOOLSADDINS" />
           <Strings>
             <ButtonText>TestMenu</ButtonText>
             <CommandName>TestMenu</CommandName>
           </Strings>
       </Menu>
   </Menus>
   ```

    Os `guid` `id` valores e do menu especificam o conjunto de comandos e o menu específico no conjunto de comandos.

    Os `guid` `id` valores e do pai posicionam o menu na seção da barra de menus do Visual Studio que contém os menus ferramentas e suplementos.

    O valor da `CommandName` cadeia de caracteres especifica que o texto deve aparecer no item de menu.

3. Na \<Groups> seção, localize \<Group> e altere o \<Parent> elemento para apontar para o menu que acabamos de adicionar:

   ```xml
   <Groups>
       <Group guid="guidTopLevelMenuPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu"/>
       </Group>
   </Groups>
   ```

    Isso faz com que o grupo faça parte do novo menu.

::: moniker-end

4. Localize a seção `Buttons`. Observe que o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] modelo de pacote gerou um `Button` elemento que tem seu pai definido como `MyMenuGroup` . Como resultado, esse comando aparece no menu.

## <a name="build-and-test-the-extension"></a>Compilar e testar a extensão

1. Compile o projeto e comece a depuração. Uma instância da instância experimental deve aparecer.

::: moniker range="vs-2017"

2. A barra de menus na instância experimental deve conter um menu **TestMenu** .

::: moniker-end

::: moniker range=">=vs-2019"

2. O menu **extensões** na instância experimental deve conter um menu **TestMenu** .

::: moniker-end

3. No menu **TestMenu** , clique em **invocar comando de teste**.

     Uma caixa de mensagem deve aparecer e exibir a mensagem "TestCommand Package in TopLevelMenu. TestCommand. MenuItemCallback ()".

## <a name="see-also"></a>Confira também

- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)
