---
title: Adicionando um comando à barra de ferramentas Gerenciador de Soluções | Microsoft Docs
description: Saiba como adicionar um botão que executa um comando à barra de ferramentas Gerenciador de Soluções no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: cf6ffcded95d142578ed118ab26b57914eb36c37
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060075"
---
# <a name="add-a-command-to-the-solution-explorer-toolbar"></a>Adicionar um comando à barra de ferramentas Gerenciador de Soluções
Este tutorial mostra como adicionar um botão à barra de ferramentas **Gerenciador de soluções** .

 Qualquer comando em uma barra de ferramentas ou menu é chamado de botão no Visual Studio. Quando o botão é clicado, o código no manipulador de comandos é executado. Normalmente, os comandos relacionados são agrupados em conjunto para formar um grupo. Menus ou barras de ferramentas atuam como contêineres para grupos. A prioridade determina a ordem na qual os comandos individuais em um grupo aparecem no menu ou na barra de ferramentas. Você pode impedir que um botão seja exibido na barra de ferramentas ou no menu controlando sua visibilidade. Um comando que está listado em uma `<VisibilityConstraints>` seção do arquivo *. vsct* aparece apenas no contexto associado. A visibilidade não pode ser aplicada a grupos.

 Para obter mais informações sobre menus, comandos de barra de ferramentas e arquivos *. vsct* , consulte [comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).

> [!NOTE]
> Use arquivos de tabela de comando XML (*. vsct*) em vez de arquivos de configuração de tabela de comando (*. CTC*) para definir como os menus e comandos aparecem em seu VSPackages. Para obter mais informações, consulte [tabela de comandos do Visual Studio (. Vsct) arquivos](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-an-extension-with-a-menu-command"></a>Criar uma extensão com um comando de menu
 Crie um projeto VSIX denominado `SolutionToolbar` . Adicione um modelo de item de comando de menu chamado **ToolbarButton**. Para obter informações sobre como fazer isso, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

## <a name="add-a-button-to-the-solution-explorer-toolbar"></a>Adicionar um botão à barra de ferramentas Gerenciador de Soluções
 Esta seção do passo a passos mostra como adicionar um botão à barra de ferramentas **Gerenciador de soluções** . Quando o botão é clicado, o código no método de retorno de chamada é executado.

1. No arquivo *ToolbarButtonPackage. vsct* , vá para a  `<Symbols>` seção. O `<GuidSymbol>`  nó contém o grupo de menus e o comando que foi gerado pelo modelo de pacote. Adicione um `<IDSymbol>` elemento a este nó para declarar o grupo que irá conter o comando.

    ```xml
    <IDSymbol name="SolutionToolbarGroup" value="0x0190"/>
    ```

2. Na `<Groups>` seção, após a entrada de grupo existente, defina o novo grupo declarado na etapa anterior.

    ```xml
    <Group guid="guidToolbarButtonPackageCmdSet"
           id="SolutionToolbarGroup" priority="0xF000">
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
          </Group>
    ```

     Definir o par pai GUID: ID como `guidSHLMainMenu` e `IDM_VS_TOOL_PROJWIN` coloca esse grupo na barra de ferramentas **Gerenciador de soluções** e definir um valor de alta prioridade o coloca após os outros grupos de comandos.

3. Na `<Buttons>` seção, altere a ID do pai da entrada gerada `<Button>` para refletir o grupo que você definiu na etapa anterior. O `<Button>` elemento Modified deve ter a seguinte aparência:

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

     A barra de ferramentas **Gerenciador de soluções** deve exibir o novo botão de comando à direita dos botões existentes. O ícone do botão é tachado.

5. Clique no botão novo.

     Uma caixa de diálogo com a mensagem **ToolbarButtonPackage dentro de SolutionToolbar. ToolbarButton. MenuItemCallback ()** deve ser exibida.

## <a name="control-the-visibility-of-a-button"></a>Controlar a visibilidade de um botão
 Esta seção do passo a passos mostra como controlar a visibilidade de um botão em uma barra de ferramentas. Ao definir um contexto para um ou mais projetos na `<VisibilityConstraints>` seção do arquivo *SolutionToolbar. vsct* , você restringe um botão para que ele apareça somente quando um projeto ou projetos estiverem abertos.

### <a name="to-display-a-button-when-one-or-more-projects-are-open"></a>Para exibir um botão quando um ou mais projetos estão abertos

1. Na `<Buttons>` seção de *ToolbarButtonPackage. vsct*, adicione dois sinalizadores de comando ao elemento existente `<Button>` , entre as `<Strings>` marcas e `<Icons>` .

   ```xml
   <CommandFlag>DefaultInvisible</CommandFlag>
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

    Os `DefaultInvisible` `DynamicVisibility` sinalizadores e devem ser definidos para que as entradas na `<VisibilityConstraints>` seção possam entrar em vigor.

2. Crie uma `<VisibilityConstraints>` seção que tenha duas `<VisibilityItem>` entradas. Coloque a nova seção logo após a marca de fechamento `</Commands>` .

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

    A barra de ferramentas **Gerenciador de soluções** não contém o botão tachado.

4. Abra qualquer solução que contenha um projeto.

    O botão tachado aparece na barra de ferramentas à direita dos botões existentes.

5. No menu **Arquivo** , clique em **Fechar Solução**. O botão desaparece da barra de ferramentas.

   A visibilidade do botão é controlada pelo [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] até que o VSPackage seja carregado. Depois que o VSPackage é carregado, a visibilidade do botão é controlada pelo VSPackage.  Para obter mais informações, consulte [MenuCommands vs. OleMenuCommands](/previous-versions/visualstudio/visual-studio-2015/misc/menucommands-vs-olemenucommands?preserve-view=true&view=vs-2015).

## <a name="see-also"></a>Confira também
- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)