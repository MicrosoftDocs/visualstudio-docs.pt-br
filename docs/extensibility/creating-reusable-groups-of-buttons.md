---
title: Criar grupos reutilizáveis de botões | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- button groups, creating in VSPackages
- VSPackages, creating reusable button groups
- buttons, creating reusable groups
ms.assetid: 0c561617-fb86-476d-8bd1-c6e5e7464c65
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4447ab5e5c0ced7852d0cb7dae3a4c0c7e3b3e68
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49928172"
---
# <a name="create-reusable-groups-of-buttons"></a>Criar grupos reutilizáveis de botões
Um grupo de comandos é uma coleção de comandos que sempre aparecem juntas em um menu ou barra de ferramentas. Qualquer grupo de comando pode ser usado novamente, atribuindo a ela a menus pai diferente na seção CommandPlacements a *VSCT* arquivo.  
  
 Grupos de comando geralmente contêm botões, mas também pode conter outros menus ou caixas de combinação.  
  
## <a name="to-create-a-reusable-group-of-buttons"></a>Para criar um grupo reutilizável de botões  
  
1.  Crie um projeto do VSIX chamado `ReusableButtons`. Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
2.  Quando o projeto aberto, adicione um modelo de item de comando personalizado chamado **ReusableCommand**. No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add** > **Novo Item**. No **Adicionar Novo Item** caixa de diálogo, vá para **Visual c#** > **extensibilidade** e selecione **comando personalizado**. No **nome** campo na parte inferior da janela, altere o nome do arquivo de comando para *ReusableCommand.cs*.  
  
3.  No *VSCT* de arquivos, vá para a seção de símbolos e localizar o elemento GuidSymbol que contém grupos e comandos para o projeto. Ele deve ser chamado guidReusableCommandPackageCmdSet.  
  
4.  Adicione um IDSymbol para cada botão que você irá adicionar ao grupo, como no exemplo a seguir.  
  
    ```xml  
    <GuidSymbol name="guidReusableCommandPackageCmdSet" value="{7f383b2a-c6b9-4c1d-b4b8-a26dc5b60ca1}">  
        <IDSymbol name="MyMenuGroup" value="0x1020" />  
        <IDSymbol name="ReusableCommandId" value="0x0100" />  
        <IDSymbol name="SecondReusableCommandId" value="0x0200" />  
    </GuidSymbol>  
    ```  
  
     Por padrão, o modelo de item de comando cria um grupo chamado **MyMenuGroup** e um botão que tem o nome que você forneceu, junto com uma entrada de IDSymbol para cada um.  
  
5.  Na seção grupos, crie um elemento de grupo que tem os mesmos atributos GUID e ID do que aquelas fornecidas na seção símbolos. Você também pode usar um grupo existente ou usar a entrada que é fornecida pelo modelo de comando, como no exemplo a seguir. Esse grupo apareça na **ferramentas** menu  
  
    ```xml  
    <Groups>  
        <Group guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">  
              <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS"/>  
        </Group>  
    </Groups>  
    ```  
  
## <a name="to-create-a-group-of-buttons-for-reuse"></a>Para criar um grupo de botões para reutilização  
  
1.  Você pode colocar um comando ou um menu em um grupo usando o grupo como um pai na definição de comando ou do menu ou colocando o comando ou o menu do grupo usando a seção CommandPlacements.  
  
     Na seção botões definir um botão que tem o seu grupo como pai, ou use o botão que é fornecido pelo modelo de pacote, conforme mostrado no exemplo a seguir.  
  
    ```xml  
    <Button guid="guidReusableCommandPackageCmdSet" id="ReusableCommandId" priority="0x0100" type="Button">  
        <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />  
        <Icon guid="guidImages" id="bmpPic1" />  
        <Strings>  
            <ButtonText>Invoke ReusableCommand</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
2.  Se um botão deve aparecer em mais de um grupo, crie uma entrada para ele na seção CommandPlacements, que deve ser colocada após a seção de comandos. Defina os atributos GUID e ID do elemento CommandPlacement para corresponder do botão que você deseja posicionar e, em seguida, defina o GUID e a ID do seu elemento pai do grupo de destino, conforme mostrado no exemplo a seguir.  
  
    ```xml  
    <CommandPlacements>  
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="SecondReusableCommandId" priority="0x105">  
          <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />  
        </CommandPlacement>  
    </CommandPlacements>  
    ```  
  
    > [!NOTE]
    >  O valor do campo de prioridade determina a posição do comando no novo grupo de comando. As prioridades de conjunto no CommandPlacement elemento substituem aquelas configuradas na definição de item. Comandos que têm valores de prioridade mais baixos são exibidos antes de comandos que têm valores de prioridade mais alta. Os valores de prioridade duplicados são permitidos, mas a posição relativa de comandos que têm o mesmo valor de prioridade não pode ser garantida, porque a ordem na qual o **devenv /setup** comando cria a interface final do registro pode não ser consistente.  
  
## <a name="to-put-a-reusable-group-of-buttons-on-a-menu"></a>Para colocar um grupo reutilizável de botões em um menu  
  
1. Criar uma entrada no `CommandPlacements` seção. Definir o GUID e ID do `CommandPlacement` elemento do seu grupo e definir o pai GUID e ID do local de destino.  
  
    A seção CommandPlacements deve ser colocada apenas após a seção de comandos:  
  
   ```xml  
   <CommandTable>  
   ...  
     <Commands>... </Commands>  
     <CommandPlacements>... </CommandPlacements>  
   ...   
   </CommandTable>  
   ```  
  
    Um grupo de comando pode ser incluído em mais de um menu. Menu pai pode ser um que você criou, que é fornecido pelo [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] (conforme descrito em *ShellCmdDef.vsct* ou *SharedCmdDef.vsct*), ou que é definido em outro VSPackage. O número de camadas de gerenciamento do domínio pai é ilimitado, desde que o menu pai, eventualmente, está conectado à [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ou a um menu de atalho que é exibido por um VSPackage.  
  
    O exemplo a seguir coloca o grupo **Gerenciador de soluções** barra de ferramentas, à direita dos outros botões.  
  
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
