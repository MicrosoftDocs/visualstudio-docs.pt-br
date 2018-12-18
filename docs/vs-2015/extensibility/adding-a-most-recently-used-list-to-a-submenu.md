---
title: Adicionando a lista a um Submenu um mais usados recentemente | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MRU lists
- menus, creating MRU list
- most recently used
ms.assetid: 27d4bbcf-99b1-498f-8b66-40002e3db0f8
caps.latest.revision: 47
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 87e9fb6ec0b4d0339427175fd18fdb79f6ef500b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51744350"
---
# <a name="adding-a-most-recently-used-list-to-a-submenu"></a>Adicionando uma lista dos mais usados recentemente a um submenu
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo se baseia no demonstrações [adicionando um Submenu a um Menu](../extensibility/adding-a-submenu-to-a-menu.md)e mostra como adicionar uma lista dinâmica a um submenu. A lista dinâmica constitui a base para a criação de uma lista de usados mais recentemente (MRU).  
  
 Inicia uma lista de menu dinâmico com um espaço reservado em um menu. Sempre que o menu é exibido, o ambiente de desenvolvimento integrado (IDE) do Visual Studio solicita o VSPackage todos os comandos que devem ser mostrados no espaço reservado. Uma lista dinâmica pode ocorrer em qualquer lugar em um menu. No entanto, as listas dinâmicas normalmente serão armazenadas e exibidas por si só, nos submenus ou da parte inferior dos menus. Ao usar esses padrões de design, você deve habilitar a lista dinâmica de comandos para expandir e contrair sem afetar a posição dos outros comandos no menu. Neste passo a passo, a lista MRU dinâmica é exibida na parte inferior de um submenu existente, separado do restante do submenu por uma linha.  
  
 Tecnicamente, uma lista dinâmica também pode ser aplicada a uma barra de ferramentas. No entanto, nós não recomendamos esse uso como uma barra de ferramentas deve permanecer inalterada, a menos que o usuário executa as etapas específicas para alterá-lo.  
  
 Este passo a passo cria uma lista MRU de quatro itens que alterar sua ordem toda vez que uma delas está selecionada (se move o item selecionado na parte superior da lista).  
  
 Para obter mais informações sobre menus e arquivos. VSCT, consulte [comandos, Menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
## <a name="creating-an-extension"></a>Criação de uma extensão  
  
- Siga os procedimentos em [adicionando um Submenu a um Menu](../extensibility/adding-a-submenu-to-a-menu.md) para criar o submenu que é modificado nos procedimentos a seguir.  
  
  Os procedimentos neste passo a passo supõem que o nome do VSPackage é `TopLevelMenu`, que é o nome que é usado no [adicionar um Menu a barra de menus do Visual Studio](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md).  
  
## <a name="creating-a-dynamic-item-list-command"></a>Criar um comando de lista de Item dinâmico  
  
1.  Abra TestCommandPackage.vsct.  
  
2.  No `Symbols` seção, o `GuidSymbol` nó chamado guidTestCommandPackageCmdSet, adicione o símbolo para o `MRUListGroup` grupo e o `cmdidMRUList` comando, da seguinte maneira.  
  
    ```csharp  
    <IDSymbol name="MRUListGroup" value="0x1200"/>  
    <IDSymbol name="cmdidMRUList" value="0x0200"/>  
    ```  
  
3.  No `Groups` seção, adicione o grupo declarado após as entradas existentes do grupo.  
  
    ```cpp  
    <Group guid="guidTestCommandPackageCmdSet" id="MRUListGroup"   
           priority="0x0100">  
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>  
    </Group>  
  
    ```  
  
4.  No `Buttons` seção, adicione um nó para representar o comando recentemente declarado, após as entradas do botão existente.  
  
    ```csharp  
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidMRUList"  
        type="Button" priority="0x0100">  
        <Parent guid="guidTestCommandPackageCmdSet" id="MRUListGroup" />  
        <CommandFlag>DynamicItemStart</CommandFlag>  
        <Strings>  
            <CommandName>cmdidMRUList</CommandName>  
            <ButtonText>MRU Placeholder</ButtonText>  
                </Strings>  
    </Button>  
    ```  
  
     O `DynamicItemStart` sinalizador habilita o comando a ser gerado dinamicamente.  
  
5.  Compile o projeto e iniciar a depuração para testar a exibição do novo comando.  
  
     Sobre o **TestMenu** menu, clique em novo submenu, **submenu**, para exibir o novo comando, **espaço reservado de MRU**. Depois de uma lista dinâmica de MRU de comandos é implementada no próximo procedimento, este rótulo de comando será substituído por essa lista toda vez que o submenu é aberto.  
  
## <a name="filling-the-mru-list"></a>Preencher a lista MRU  
  
1.  No TestCommandPackageGuids.cs, adicione as seguintes linhas após as IDs de comando existente no `TestCommandPackageGuids` definição de classe.  
  
    ```csharp  
    public const string guidTestCommandPackageCmdSet = "00000000-0000-0000-0000-00000000"; // get the GUID from the .vsct file  
    public const uint cmdidMRUList = 0x200;  
    ```  
  
2.  No TestCommand.cs, adicione a seguinte instrução using.  
  
    ```csharp  
    using System.Collections;  
    ```  
  
3.  Adicione o seguinte código no construtor TestCommand após a última chamada AddCommand. O `InitMRUMenu` serão definidos posteriormente  
  
    ```csharp  
    this.InitMRUMenu(commandService);  
    ```  
  
4.  Adicione o seguinte código na classe TestCommand. Esse código inicializa a lista de cadeias de caracteres que representam os itens a serem mostrados na lista MRU.  
  
    ```csharp  
    private int numMRUItems = 4;  
    private int baseMRUID = (int)TestCommandPackageGuids.cmdidMRUList;  
    private ArrayList mruList;  
  
    private void InitializeMRUList()  
    {  
        if (null == this.mruList)  
        {  
            this.mruList = new ArrayList();  
            if (null != this.mruList)  
            {  
                for (int i = 0; i < this.numMRUItems; i++)  
                {  
                    this.mruList.Add(string.Format(CultureInfo.CurrentCulture,  
                        "Item {0}", i + 1));  
                }  
            }  
        }  
    }  
    ```  
  
5.  Após o `InitializeMRUList` método, adicione o `InitMRUMenu` método. Isso inicializa os comandos de menu de lista MRU.  
  
    ```csharp  
    private void InitMRUMenu(OleMenuCommandService mcs)  
    {  
        InitializeMRUList();  
        for (int i = 0; i < this.numMRUItems; i++)  
        {  
            var cmdID = new CommandID(  
                new Guid(TestCommandPackageGuids.guidTestCommandPackageCmdSet), this.baseMRUID + i);  
            var mc = new OleMenuCommand(  
                new EventHandler(OnMRUExec), cmdID);  
            mc.BeforeQueryStatus += new EventHandler(OnMRUQueryStatus);  
            mcs.AddCommand(mc);  
        }  
    }  
    ```  
  
     Você deve criar um objeto de comando de menu para todos os itens possíveis na lista MRU. As chamadas IDE a `OnMRUQueryStatus` método para cada item na lista MRU até que não há mais itens. No código gerenciado, a única maneira de saber que não há mais itens do IDE é primeiro criar todos os itens possíveis. Se você quiser, você pode marcar itens adicionais como não visíveis no primeiro usando `mc.Visible = false;` depois que o comando de menu é criado. Esses itens podem, em seguida, ser tornados visíveis posteriormente usando `mc.Visible = true;` no `OnMRUQueryStatus` método.  
  
6.  Após o `InitMRUMenu` método, adicione o seguinte `OnMRUQueryStatus` método. Esse é o manipulador que define o texto para cada item MRU.  
  
    ```csharp  
    private void OnMRUQueryStatus(object sender, EventArgs e)  
    {  
        OleMenuCommand menuCommand = sender as OleMenuCommand;  
        if (null != menuCommand)  
        {  
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;  
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)  
            {  
                menuCommand.Text = this.mruList[MRUItemIndex] as string;  
            }  
        }  
    }  
    ```  
  
7.  Após o `OnMRUQueryStatus` método, adicione o seguinte `OnMRUExec` método. Esse é o manipulador para a seleção de um item MRU. Esse método Move o item selecionado na parte superior da lista e, em seguida, exibe o item selecionado em uma caixa de mensagem.  
  
    ```csharp  
    private void OnMRUExec(object sender, EventArgs e)  
    {  
        var menuCommand = sender as OleMenuCommand;  
        if (null != menuCommand)  
        {  
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;  
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)  
            {  
                string selection = this.mruList[MRUItemIndex] as string;  
                for (int i = MRUItemIndex; i > 0; i--)  
                {  
                    this.mruList[i] = this.mruList[i - 1];  
                }  
                this.mruList[0] = selection;  
                System.Windows.Forms.MessageBox.Show(  
                    string.Format(CultureInfo.CurrentCulture,  
                                  "Selected {0}", selection));  
            }  
        }  
    }  
  
    ```  
  
## <a name="testing-the-mru-list"></a>Testando a lista MRU  
  
#### <a name="to-test-the-mru-menu-list"></a>Para testar a lista MRU do menu  
  
1.  Compile o projeto e iniciar a depuração  
  
2.  Sobre o **TestMenu** menu, clique em **TestCommand invocar**. Isso exibe uma caixa de mensagem que indica que o comando foi selecionado.  
  
    > [!NOTE]
    >  Essa etapa é necessária para forçar o VSPackage para carregar e exibir corretamente a lista MRU. Se você ignorar essa etapa, a lista MRU não é exibida.  
  
3.  Sobre o **Menu Test** menu, clique em **submenu**. Uma lista de quatro itens é exibida no final do submenu, abaixo de um separador. Quando você clica em **Item 3**, uma caixa de mensagem deve aparecer e exibir o texto, "Selected Item 3". (Se a lista de quatro itens não for exibida, certifique-se de que você seguiu as instruções na etapa anterior.)  
  
4.  Abra o submenu novamente. Observe que **Item 3** agora está na parte superior da lista e os outros itens enviados para uma posição para baixo. Clique em **Item 3** novamente e observe que a caixa de mensagem ainda exibe "Selected Item 3", que indica que o texto corretamente foram movidos para a nova posição junto com o rótulo de comando.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar itens de menu dinamicamente](../extensibility/dynamically-adding-menu-items.md)

