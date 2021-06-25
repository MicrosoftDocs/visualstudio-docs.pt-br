---
title: Adicionando um comando à barra de Gerenciador de Soluções de ferramentas | Microsoft Docs
description: Saiba como adicionar um botão que executa um comando à barra de Gerenciador de Soluções de ferramentas no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding buttons
- buttons [Visual Studio], adding to Solution Explorer
- Solution Explorer, adding buttons
ms.assetid: f6411557-2f4b-4e9f-b02e-fce12a6ac7e9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0aa75bd1a229be147e3462845a61266a650e072e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900227"
---
# <a name="add-a-command-to-the-solution-explorer-toolbar"></a>Adicionar um comando à barra de Gerenciador de Soluções de ferramentas
Este passo a passo mostra como adicionar um botão à barra **de Gerenciador de Soluções** ferramentas.

 Qualquer comando em uma barra de ferramentas ou menu é chamado de botão Visual Studio. Quando o botão é clicado, o código no manipulador de comandos é executado. Normalmente, os comandos relacionados são agrupados para formar um grupo. Menus ou barras de ferramentas atuam como contêineres para grupos. A prioridade determina a ordem na qual comandos individuais em um grupo aparecem no menu ou na barra de ferramentas. Você pode impedir que um botão seja exibido na barra de ferramentas ou no menu controlando sua visibilidade. Um comando listado em uma `<VisibilityConstraints>` seção do *arquivo .vsct* aparece apenas no contexto associado. A visibilidade não pode ser aplicada a grupos.

 Para obter mais informações sobre menus, comandos da barra de ferramentas e *arquivos .vsct,* consulte [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).

> [!NOTE]
> Use arquivos de Tabela de Comando XML (*.vsct*) em vez de arquivos de configuração de tabela de comando (*.ctc*) para definir como menus e comandos aparecem em seus VSPackages. Para obter mais informações, [consulte Visual Studio De comando (. Vsct) arquivos](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).

## <a name="prerequisites"></a>Pré-requisitos
 A partir Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele é incluído como um recurso opcional na Visual Studio configuração. Você também pode instalar o SDK do VS posteriormente. Para obter mais informações, [consulte Instalando o SDK Visual Studio .](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-an-extension-with-a-menu-command"></a>Criar uma extensão com um comando de menu
 Crie um projeto VSIX chamado `SolutionToolbar` . Adicione um modelo de item de comando de menu **chamado ToolbarButton**. Para obter informações sobre como fazer isso, consulte [Criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

## <a name="add-a-button-to-the-solution-explorer-toolbar"></a>Adicionar um botão à barra de Gerenciador de Soluções de ferramentas
 Esta seção do passo a passo mostra como adicionar um botão à barra **de Gerenciador de Soluções** ferramentas. Quando o botão é clicado, o código no método de retorno de chamada é executado.

1. No arquivo *ToolbarButtonPackage.vsct,* vá para a  `<Symbols>` seção . O `<GuidSymbol>`  nó contém o grupo de menus e o comando que foi gerado pelo modelo de pacote. Adicione um `<IDSymbol>` elemento a esse nó para declarar o grupo que conterá o comando.

    ```xml
    <IDSymbol name="SolutionToolbarGroup" value="0x0190"/>
    ```

2. Na seção , após a entrada de grupo existente, defina o novo grupo que `<Groups>` você declarou na etapa anterior.

    ```xml
    <Group guid="guidToolbarButtonPackageCmdSet"
           id="SolutionToolbarGroup" priority="0xF000">
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
          </Group>
    ```

     Definir o par PAI GUID:ID como e coloca esse grupo na barra de ferramentas Gerenciador de Soluções e definir um valor de alta prioridade coloca-o após os outros grupos `guidSHLMainMenu` `IDM_VS_TOOL_PROJWIN` de comandos. 

3. Na seção , altere a ID pai da entrada gerada para refletir o `<Buttons>` `<Button>` grupo que você definiu na etapa anterior. O elemento `<Button>` modificado deve ter esta aparência:

    ```xml
    <Button guid="guidToolbarButtonPackageCmdSet" id="ToolbarButtonId" priority="0x0100" type="Button">
        <Parent guid="guidToolbarButtonPackageCmdSet" id="SolutionToolbarGroup" />
        <Icon guid="guidImages" id="bmpPicStrikethrough" />
        <Strings>
            <ButtonText>Invoke ToolbarButton</ButtonText>
        </Strings>
    </Button>
    ```

4. Compile o projeto e comece a depuração. A instância experimental é exibida.

     A **Gerenciador de Soluções** de ferramentas deve exibir o novo botão de comando à direita dos botões existentes. O ícone do botão é o tachado.

5. Clique no botão novo.

     Uma caixa de diálogo que tem a mensagem **ToolbarButtonPackage Inside SolutionToolbar.ToolbarButton.MenuItemCallback()** deve ser exibida.

## <a name="control-the-visibility-of-a-button"></a>Controlar a visibilidade de um botão
 Esta seção do passo a passo mostra como controlar a visibilidade de um botão em uma barra de ferramentas. Ao definir um contexto para um ou mais projetos na seção do arquivo `<VisibilityConstraints>` *SolutionToolbar.vsct,* você restringe um botão a ser exibido somente quando um projeto ou projetos estão abertos.

### <a name="to-display-a-button-when-one-or-more-projects-are-open"></a>Para exibir um botão quando um ou mais projetos estão abertos

1. Na seção `<Buttons>` de *ToolbarButtonPackage.vsct*, adicione dois sinalizadores de comando ao elemento `<Button>` existente, entre as marcas `<Strings>` e `<Icons>` .

   ```xml
   <CommandFlag>DefaultInvisible</CommandFlag>
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

    Os `DefaultInvisible` `DynamicVisibility` sinalizadores e devem ser definidos para que as entradas na `<VisibilityConstraints>` seção possam entrar em vigor.

2. Crie uma `<VisibilityConstraints>` seção que tenha duas `<VisibilityItem>` entradas. Coloque a nova seção logo após a marca de `</Commands>` fechamento.

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidToolbarButtonPackageCmdSet"
             id="ToolbarButtonId"
             context="UICONTEXT_SolutionHasSingleProject" />
       <VisibilityItem guid="guidToolbarButtonPackageCmdSet"
             id="ToolbarButtonId"
             context="UICONTEXT_SolutionHasMultipleProjects" />
   </VisibilityConstraints>
   ```

    Cada item de visibilidade representa uma condição sob a qual o botão especificado é exibido. Para aplicar várias condições, você deve criar várias entradas para o mesmo botão.

3. Compile o projeto e comece a depuração. A instância experimental é exibida.

    A **Gerenciador de Soluções** de ferramentas não contém o botão tachado.

4. Abra qualquer solução que contenha um projeto.

    O botão tachado aparece na barra de ferramentas à direita dos botões existentes.

5. No menu **Arquivo** , clique em **Fechar Solução**. O botão desaparece da barra de ferramentas.

   A visibilidade do botão é controlada por [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] até que o VSPackage seja carregado. Depois que o VSPackage é carregado, a visibilidade do botão é controlada pelo VSPackage.  Para obter mais informações, consulte [MenuCommands vs. OleMenuCommands](/previous-versions/visualstudio/visual-studio-2015/misc/menucommands-vs-olemenucommands?preserve-view=true&view=vs-2015).

## <a name="see-also"></a>Confira também
- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)