---
title: Adicionar um Menu a barra de menus do Visual Studio | Microsoft Docs
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- menus, creating top level
- top-level menus
ms.assetid: 58fc1a31-2aeb-441c-8e48-c7d5cbcfe501
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c7ce5ab06eb641e94d6f972b888882ac1e53e2ee
ms.sourcegitcommit: 4d9c54f689416bf1dc4ace058919592482d02e36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2019
ms.locfileid: "58195041"
---
# <a name="add-a-menu-to-the-visual-studio-menu-bar"></a>Adicionar um menu a barra de menus do Visual Studio

Este passo a passo mostra como adicionar um menu a barra de menus do ambiente de desenvolvimento integrado (IDE) do Visual Studio. A barra de menus do IDE contém categorias de menu, como **arquivo**, **editar**, **exibição**, **janela**, e **ajuda** .

Antes de adicionar um novo menu à barra de menus do Visual Studio, considere se os comandos devem ser colocados dentro de um menu existente. Para obter mais informações sobre o posicionamento de comando, consulte [Menus e comandos para o Visual Studio](../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md).

Menus são declarados na *VSCT* arquivo do projeto. Para obter mais informações sobre menus e *VSCT* arquivos, consulte [comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).

Ao concluir este passo a passo, você pode criar um menu denominado **TestMenu** que contém um comando.

> [!NOTE]
> No VS 2019, menus de nível superior contribuídas por extensões são colocadas sob o **extensões** menu.

## <a name="prerequisites"></a>Pré-requisitos

A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-vsix-project-that-has-a-custom-command-item-template"></a>Crie um projeto VSIX que tem um modelo de item de comando personalizado

1. Crie um projeto do VSIX chamado `TopLevelMenu`. Você pode encontrar o modelo de projeto VSIX na **novo projeto** diálogo pesquisando por "vsix".  Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

2. Quando o projeto aberto, adicione um modelo de item de comando personalizado chamado **TestCommand**. No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add** >  **Novo Item**. No **Adicionar Novo Item** caixa de diálogo, vá para **Visual c# / extensibilidade** e selecione **comando personalizado**. No **nome** campo na parte inferior da janela, altere o nome do arquivo de comando para *TestCommand.cs*.

## <a name="create-a-menu-on-the-ide-menu-bar"></a>Criar um menu na barra de menus do IDE

::: moniker range="vs-2017"

1. Na **Gerenciador de soluções**, abra *TestCommandPackage.vsct*.

    No final do arquivo, há uma \<símbolos > nó que contém vários \<GuidSymbol > nós. No nó chamado guidTestCommandPackageCmdSet, adicione um novo símbolo, da seguinte maneira:

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. Criar vazio \<Menus > nó o \<comandos > nó, logo antes \<grupos >. No \<Menus > nó, adicione um \<Menu > nó, da seguinte maneira:

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

    O `guid` e `id` valores do menu de especificam o conjunto de comandos e menu específico no conjunto de comando.

    O `guid` e `id` valores do pai posicione o menu na seção da barra de menus do Visual Studio que contém os menus de ferramentas e suplementos.

    O valor da `CommandName` cadeia de caracteres que especifica que o texto deve aparecer no item de menu.

3. No \<grupos > seção, localize o \<grupo > e altere o \<pai > elemento para apontar para o menu que acabamos de adicionar:

   ```csharp
   <Groups>
         <Group guid="guidTestCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTestCommandPackageCmdSet" id="TopLevelMenu"/>
         </Group>
       </Groups>
   ```

    Isso torna a parte do grupo do novo menu.

::: moniker-end

::: moniker range=">=vs-2019"

1. Na **Gerenciador de soluções**, abra *TopLevelMenuPackage.vsct*.

    No final do arquivo, há uma \<símbolos > nó que contém vários \<GuidSymbol > nós. No nó chamado guidTopLevelMenuPackageCmdSet, adicione um novo símbolo, da seguinte maneira:

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. Criar vazio \<Menus > nó o \<comandos > nó, logo antes \<grupos >. No \<Menus > nó, adicione um \<Menu > nó, da seguinte maneira:

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

    O `guid` e `id` valores do menu de especificam o conjunto de comandos e menu específico no conjunto de comando.

    O `guid` e `id` valores do pai posicione o menu na seção da barra de menus do Visual Studio que contém os menus de ferramentas e suplementos.

    O valor da `CommandName` cadeia de caracteres que especifica que o texto deve aparecer no item de menu.

3. No \<grupos > seção, localize o \<grupo > e altere o \<pai > elemento para apontar para o menu que acabamos de adicionar:

   ```csharp
   <Groups>
         <Group guid="guidTopLevelMenuPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu"/>
         </Group>
       </Groups>
   ```

    Isso torna a parte do grupo do novo menu.

::: moniker-end

4. Encontre o `Buttons` seção. Observe que o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] modelo de pacote gerou uma `Button` elemento que tem um pai definido como `MyMenuGroup`. Como resultado, esse comando aparece no menu.

## <a name="build-and-test-the-extension"></a>Compilar e testar a extensão

1. Compile o projeto e comece a depuração. Uma instância da instância experimental deve aparecer.

::: moniker range="vs-2017"

2. Barra de menus na instância experimental deve conter um **TestMenu** menu.

::: moniker-end

::: moniker range=">=vs-2019"

2. O **extensões** menu na instância experimental deve conter um **TestMenu** menu.

::: moniker-end

3. Sobre o **TestMenu** menu, clique em **invocar o comando de teste**.

     Uma caixa de mensagem deve aparecer e exibir a mensagem "TestCommand pacote dentro TopLevelMenu.TestCommand.MenuItemCallback()".

## <a name="see-also"></a>Consulte também

- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)