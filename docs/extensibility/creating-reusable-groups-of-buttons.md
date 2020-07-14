---
title: Criando grupos de botões reutilizáveis | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- button groups, creating in VSPackages
- VSPackages, creating reusable button groups
- buttons, creating reusable groups
ms.assetid: 0c561617-fb86-476d-8bd1-c6e5e7464c65
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 477014ed77b60821ad191ba6842999be6f528fee
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903645"
---
# <a name="create-reusable-groups-of-buttons"></a>Criar grupos de botões reutilizáveis
Um grupo de comandos é uma coleção de comandos que sempre aparecem juntos em um menu ou barra de ferramentas. Qualquer grupo de comandos pode ser usado novamente atribuindo-o a diferentes menus pai na seção CommandPlacements do arquivo *. vsct* .

 Os grupos de comandos normalmente contêm botões, mas também podem conter outros menus ou caixas de combinação.

## <a name="to-create-a-reusable-group-of-buttons"></a>Para criar um grupo de botões reutilizáveis

1. Crie um projeto VSIX denominado `ReusableButtons` . Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).

2. Quando o projeto for aberto, adicione um modelo de item de comando personalizado chamado **ReusableCommand**. Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**. Na caixa de diálogo **Adicionar novo item** , vá para extensibilidade do **Visual C#**  >  **Extensibility** e selecione **comando personalizado**. No campo **nome** na parte inferior da janela, altere o nome do arquivo de comando para *ReusableCommand.cs*.

3. No arquivo *. vsct* , vá para a seção símbolos e localize o elemento GuidSymbol que contém grupos e comandos para o projeto. Ele deve ser nomeado guidReusableCommandPackageCmdSet.

4. Adicione um IDSymbol para cada botão que será adicionado ao grupo, como no exemplo a seguir.

    ```xml
    <GuidSymbol name="guidReusableCommandPackageCmdSet" value="{7f383b2a-c6b9-4c1d-b4b8-a26dc5b60ca1}">
        <IDSymbol name="MyMenuGroup" value="0x1020" />
        <IDSymbol name="ReusableCommandId" value="0x0100" />
        <IDSymbol name="SecondReusableCommandId" value="0x0200" />
    </GuidSymbol>
    ```

     Por padrão, o modelo de item de comando cria um grupo chamado **MyMenu** Group e um botão que tem o nome que você forneceu, junto com uma entrada IDSymbol para cada um.

5. Na seção grupos, crie um elemento de grupo que tenha os mesmos atributos GUID e ID que os fornecidos na seção símbolos. Você também pode usar um grupo existente ou usar a entrada fornecida pelo modelo de comando, como no exemplo a seguir. Esse grupo aparece no menu **ferramentas**

    ```xml
    <Groups>
        <Group guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
              <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS"/>
        </Group>
    </Groups>
    ```

## <a name="to-create-a-group-of-buttons-for-reuse"></a>Para criar um grupo de botões para reutilização

1. Você pode colocar um comando ou um menu em um grupo usando o grupo como um pai na definição do comando ou do menu, ou colocando o comando ou o menu no grupo usando a seção CommandPlacements.

     Na seção botões, defina um botão que tenha seu grupo como seu pai ou use o botão que é fornecido pelo modelo de pacote, conforme mostrado no exemplo a seguir.

    ```xml
    <Button guid="guidReusableCommandPackageCmdSet" id="ReusableCommandId" priority="0x0100" type="Button">
        <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ReusableCommand</ButtonText>
        </Strings>
    </Button>
    ```

2. Se um botão precisar aparecer em mais de um grupo, crie uma entrada para ele na seção CommandPlacements, que deve ser colocada após a seção de comandos. Defina os atributos GUID e ID do elemento CommandPlacement para corresponder àqueles do botão que você deseja posicionar e, em seguida, defina o GUID e a ID de seu elemento pai para os do grupo de destino, conforme mostrado no exemplo a seguir.

    ```xml
    <CommandPlacements>
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="SecondReusableCommandId" priority="0x105">
          <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        </CommandPlacement>
    </CommandPlacements>
    ```

    > [!NOTE]
    > O valor do campo prioridade determina a posição do comando no novo grupo de comandos. As prioridades definidas no elemento CommandPlacement substituem aquelas definidas na definição do item. Comandos que têm valores de prioridade mais baixa são exibidos antes dos comandos que têm valores de prioridade mais altos. Valores de prioridade duplicados são permitidos, mas a posição relativa de comandos que têm o mesmo valor de prioridade não pode ser garantida porque a ordem na qual o comando **devenv/setup** cria a interface final do registro pode não ser consistente.

## <a name="to-put-a-reusable-group-of-buttons-on-a-menu"></a>Para colocar um grupo reutilizável de botões em um menu

1. Crie uma entrada na `CommandPlacements` seção. Defina o GUID e a ID do `CommandPlacement` elemento para os do seu grupo e defina o GUID pai e a ID para os do local de destino.

    A seção CommandPlacements deve ser colocada logo após a seção Commands:

   ```xml
   <CommandTable>
   ...
     <Commands>... </Commands>
     <CommandPlacements>... </CommandPlacements>
   ...
   </CommandTable>
   ```

    Um grupo de comandos pode ser incluído em mais de um menu. O menu pai pode ser um que você criou, um que é fornecido pelo [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] (conforme descrito em *ShellCmdDef. vsct* ou *SharedCmdDef. vsct*), ou um que é definido em outro VSPackage. O número de camadas de pai é ilimitado, desde que o menu pai seja eventualmente conectado ao [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ou a um menu de atalho que seja exibido por um VSPackage.

    O exemplo a seguir coloca o grupo na barra de ferramentas **Gerenciador de soluções** , à direita dos outros botões.

   ```xml
   <CommandPlacements>
       <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0xF00">
         <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
       </CommandPlacement>
   </CommandPlacements>
   ```

   ```xml
   <CommandPlacements>
     <CommandPlacement guid="guidButtonGroupCmdSet" id="MyMenuGroup"
         priority="0x605">
       <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS" />
     </CommandPlacement>
   </CommandPlacements>

   ```
