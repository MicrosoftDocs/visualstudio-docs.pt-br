---
title: MenuCommands Vs. OleMenuCommands | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, creating in VSPackages
- command buttons, creating and placing
- menus, creating commands
ms.assetid: 553d5e07-3e19-4aba-b490-6c7dd05fd82e
manager: douge
ms.openlocfilehash: 0fbe8ea2a78eae02cb7e0d390da49eafe55e75ee
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49888951"
---
# <a name="menucommands-vs-olemenucommands"></a>MenuCommands Vs. OleMenuCommands
Você pode criar comandos de menu, derivando de <xref:System.ComponentModel.Design.MenuCommand> ou de <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> do objeto e a implementação de manipuladores de eventos apropriados. Na maioria dos casos, você pode usar <xref:System.ComponentModel.Design.MenuCommand>, como o modelo de projeto de VSPackage faz, mas, ocasionalmente, talvez você precise usar <xref:Microsoft.VisualStudio.Shell.OleMenuCommand>.  
  
 Os comandos que um VSPackage disponibiliza para o IDE deve ser visível e habilitado antes que um usuário podem usá-los. Quando os comandos são criados em uma *VSCT* arquivo usando o modelo de projeto do Visual Studio Package, eles são visíveis e habilitados por padrão. Definir alguns sinalizadores de comando, como `DynamicItemStart`, pode alterar o comportamento padrão. A visibilidade, status habilitado e outras propriedades de um comando também podem ser alteradas no código em tempo de execução acessando o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> objeto que está associado com o comando.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
## <a name="template-locations-for-the-visual-studio-package-template"></a>Locais de modelo para o modelo de pacote do Visual Studio  
 Você pode encontrar o modelo de pacote do Visual Studio na **novo projeto** diálogo sob **Visual Basic** > **extensibilidade**  >  **C#** > **extensibilidade**, ou **outros tipos de projeto** > **extensibilidade**.  
  
## <a name="create-a-command"></a>Criar um comando  
 Todos os comandos, grupos de comando, menus, barras de ferramentas e janelas de ferramentas são definidas na *VSCT* arquivo. Para obter mais informações, consulte [arquivos de tabela (. VSCT) de comando do Visual Studio](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).  
  
 Se você estiver criando um VSPackage usando o modelo de pacote, selecione **comando de Menu** para criar um *VSCT* de arquivo e definir um comando de menu padrão. Para obter mais informações, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
### <a name="to-add-a-command-to-the-ide"></a>Para adicionar um comando ao IDE  
  
1. Abra o *VSCT* arquivo.  
  
2. No `Symbols` seção, localize o [GuidSymbol](../extensibility/guidsymbol-element.md) elemento que contém os grupos e comandos.  
  
3. Criar uma [IDSymbol](../extensibility/idsymbol-element.md) elemento para cada menu, grupo ou comando que você deseja adicionar, conforme mostrado no exemplo a seguir.  
  
    <!--FIXME [!CODE [ButtonGroup#01](../CodeSnippet/VS_Snippets_VSSDK/buttongroup#01)]  -->
   ```xaml  
   <GuidSymbol name="guidButtonGroupCmdSet" value="{f69209e9-975a-4543-821d-1f4a2c52d737}">
     <IDSymbol name="MyMenuGroup" value="0x1020" />
     <IDSymbol name="cmdidMyCommand" value="0x0100" />
   </GuidSymbol>
   ```  
  
   O `name` atributos do `GuidSymbol` e `IDSymbol` elementos fornecem o par de GUID:ID para cada novo menu, um grupo ou um comando. O `guid` representa um conjunto de comandos que está definido para o VSPackage. Você pode definir vários conjuntos de comandos. Cada par de GUID:ID deve ser exclusivo.  
  
4. No [botões](../extensibility/buttons-element.md) seção, crie um [botão](../extensibility/button-element.md) elemento para definir o comando, conforme mostrado no exemplo a seguir.  
  
    <!--FIXME [!CODE [ButtonGroup#03](../CodeSnippet/VS_Snippets_VSSDK/buttongroup#03)]  -->
   ```xaml  
   <Button guid="guidButtonGroupCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
     <Parent guid="guidButtonGroupCmdSet" id="MyMenuGroup" />
     <Icon guid="guidImages" id="bmpPic1" />
     <Strings>
       <CommandName>cmdidMyCommand</CommandName>
       <ButtonText>My Command name</ButtonText>
     </Strings>
   </Button>
   ```  
  
   1.  Defina as `guid` e `id` campos a serem associados a GUID:ID do novo comando.  
  
   2.  Defina o `priority` atributo.  
  
        O `priority` atributo é usado pela. VSCT para determinar o local do botão entre os outros objetos no respectivo grupo pai.  
  
        Comandos que têm valores de prioridade mais baixos são exibidos acima ou à esquerda de comandos que têm valores de prioridade mais alta. Os valores de prioridade duplicados são permitidos, mas a posição relativa dos comandos que têm a mesma prioridade é determinada pela ordem na qual os VSPackages são processados em tempo de execução e, nessa ordem não pode ser predeterminada.  
  
        Omitindo o `priority` atributo define seu valor como 0.  
  
   3.  Defina o `type` atributo. Na maioria dos casos, seu valor será `"Button"`. Para obter descrições dos outros tipos de botões válidos, consulte [elemento Button](../extensibility/button-element.md).  
  
5. Na definição do botão, crie uma [cadeias de caracteres](../extensibility/strings-element.md) elemento que contém uma [ButtonText](../extensibility/buttontext-element.md) elemento para conter o nome do menu, como ele aparece no IDE e uma [CommandName](../extensibility/commandname-element.md) elemento para conter o nome do comando que é usado para acessar o menu na **comando** janela.  
  
    Se a cadeia de caracteres de texto do botão inclui o caractere '&', o usuário pode abrir o menu pressionando **Alt** além do caractere que segue imediatamente o '&'.  
  
    Adicionando um `Tooltip` elemento fará com que o texto contido seja exibido quando um usuário posiciona o ponteiro sobre o botão.  
  
6. Adicionar um [ícone](../extensibility/icon-element.md) elemento para especificar o ícone, se houver, para ser exibido com o comando. Os ícones são necessários para botões em barras de ferramentas, mas não para itens de menu. O `guid` e `id` da `Icon` elemento deve corresponder aos de uma [Bitmap](../extensibility/bitmap-element.md) elemento definido no `Bitmaps` seção.  
  
7. Adicione sinalizadores de comando, conforme apropriado, para alterar a aparência e comportamento do botão. Para fazer isso, adicione uma [CommandFlag](../extensibility/command-flag-element.md) elemento na definição de menu.  
  
8. Defina o grupo pai do comando. O grupo pai pode ser um grupo que você cria, um grupo de outro pacote ou um grupo a partir do IDE. Por exemplo, para adicionar o comando à barra de ferramentas de edição da Visual Studio, ao lado de **comentário** e **Remover comentário** botões, definir o pai para guidStdEditor:IDG_VS_EDITTOOLBAR_COMMENT. Se o pai for um grupo definido pelo usuário, ele deve ser o filho de um menu, barra de ferramentas ou janela de ferramenta que aparece no IDE.  
  
    Você pode fazer isso de duas maneiras, dependendo do seu projeto:  
  
   - No `Button` elemento, criar um [pai](../extensibility/parent-element.md) elemento e o conjunto de seus `guid` e `id` campos para o Guid e ID do grupo que irá hospedar o comando, também conhecido como o *grupo pai primário*.  
  
      O exemplo a seguir define um comando que será exibido em um menu definido pelo usuário.  
  
      <!--FIXME [!CODE [TopLevelMenu#03](../CodeSnippet/VS_Snippets_VSSDK/toplevelmenu#03)]  -->
     ```xaml  
     <Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
       <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
       <Icon guid="guidImages" id="bmpPic1" />
       <Strings>
         <CommandName>cmdidTestCommand</CommandName>
         <ButtonText>Test Command</ButtonText>
       </Strings>
     </Button>
     ```  
  
   - Você pode omitir o `Parent` elemento se o comando é posicionado por meio de posicionamento do comando. Criar uma [CommandPlacements](../extensibility/commandplacements-element.md) elemento antes do `Symbols` seção e, em seguida, adicione um [CommandPlacement](../extensibility/commandplacement-element.md) elemento que tem o `guid` e `id` do comando, um `priority`e um pai, conforme mostrado no exemplo a seguir.  
  
      <!-- FIXME [!CODE [ButtonGroup#04](../CodeSnippet/VS_Snippets_VSSDK/buttongroup#04)] -->  
     ```xaml  
     <CommandPlacements>
       <CommandPlacement guid="guidButtonGroupCmdSet" id="cmdidMyCommand" priority="0x105">
         <Parent guid="guidButtonGroupCmdSet" id="MyMenuGroup" />
       </CommandPlacement>
     </CommandPlacements>
     ```  
  
      Criar vários posicionamentos de comandos que têm o mesmo GUID:ID e tem pais diferentes faz com que um menu apareça em vários locais. Para obter mais informações, consulte [CommandPlacements](../extensibility/commandplacements-element.md) elemento.  
  
     Para obter mais informações sobre grupos de comando e gerenciamento do domínio pai, consulte [criar grupos reutilizáveis de botões](../extensibility/creating-reusable-groups-of-buttons.md).  
  
   Neste ponto, o comando estará visível no IDE, mas não terá nenhuma funcionalidade. Se o comando foi criado pelo modelo de pacote, ele terá um manipulador de clique que exibe uma mensagem por padrão.  
  
## <a name="handle-the-new-command"></a>Lidar com o novo comando  
 A maioria dos comandos em código gerenciado podem ser tratadas por estrutura de pacote gerenciado (MPF) por meio da associação de comando com um <xref:System.ComponentModel.Design.MenuCommand> objeto ou <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> objeto e implementar seus manipuladores de eventos.  
  
 Para o código que usa o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface diretamente para a manipulação de comando, você deve implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> e seus métodos. Os dois métodos mais importantes são <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> e <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>.  
  
1.  Obter o <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> da instância, conforme mostrado no exemplo a seguir.  
  
     [!code-csharp[ButtonGroup#21](../extensibility/codesnippet/CSharp/menucommands-vs-olemenucommands_5.cs)]  
  
2.  Criar um <xref:System.ComponentModel.Design.CommandID> objeto que tem como seus parâmetros o GUID e ID do comando para manipular, conforme mostrado no exemplo a seguir.  
  
     [!code-csharp[ButtonGroup#22](../extensibility/codesnippet/CSharp/menucommands-vs-olemenucommands_6.cs)]  
  
     O modelo de pacote do Visual Studio fornece duas coleções, `GuidList` e `PkgCmdIDList`, para manter os GUIDs e IDs de comandos. Eles são preenchidos automaticamente para os comandos que são adicionados pelo modelo, mas para os comandos que você adicionar manualmente, você também deve adicionar a entrada de ID para o `PkgCmdIdList` classe.  
  
     Como alternativa, você pode preencher o <xref:System.ComponentModel.Design.CommandID> objeto usando o valor de cadeia de caracteres bruta do GUID e o valor de inteiro da ID.  
  
3.  Criar uma instância de qualquer um uma <xref:System.ComponentModel.Design.MenuCommand> ou <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> objeto que especifica o método que manipula o comando junto com o <xref:System.ComponentModel.Design.CommandID>, conforme mostrado no exemplo a seguir.  
  
     [!code-csharp[ButtonGroup#23](../extensibility/codesnippet/CSharp/menucommands-vs-olemenucommands_7.cs)]  
  
     O <xref:System.ComponentModel.Design.MenuCommand> é apropriado para comandos estáticos. Exibe de item de menu dinâmico exige QueryStatus manipuladores de eventos. O <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> adiciona o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> evento que ocorre quando o menu de host do comando é abertas e algumas outras propriedades, tais como <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.Text%2A>.  
  
     Os comandos criados pelo modelo de pacote são passados por padrão para um <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> do objeto no `Initialize()` método da classe de pacote.  
  
4.  O <xref:System.ComponentModel.Design.MenuCommand> é apropriado para comandos estáticos. Exibe de item de menu dinâmico exige QueryStatus manipuladores de eventos. O <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> adiciona o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> evento que ocorre quando o menu de host do comando é abertas e algumas outras propriedades, tais como <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.Text%2A>.  
  
     Os comandos criados pelo modelo de pacote são passados por padrão para um <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> do objeto no `Initialize()` método da classe de pacote. O Assistente do Visual Studio implementa o `Initialize` método usando `MenuCommand`. Para exibições de item de menu dinâmico, você deve alterar isso para `OleMenuCommand`, conforme é mostrado na próxima etapa. Além disso, para alterar o texto do item de menu, você deve adicionar um sinalizador de comando textoAltera para o botão de comando de menu no arquivo. VSCT, conforme mostrado no exemplo a seguir  
  
     <!--FIXME [!CODE [MenuText#02](../CodeSnippet/VS_Snippets_VSSDK/menutext#02)]-->  
    ```xaml  
    <Button guid="guidMenuTextCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
      <Parent guid="guidMenuTextCmdSet" id="MyMenuGroup" />
      <Icon guid="guidImages" id="bmpPic1" />
      <CommandFlag>TextChanges</CommandFlag>
      <Strings>
        <CommandName>cmdidMyCommand</CommandName>
        <ButtonText>My Command name</ButtonText>
      </Strings>
    </Button>
    ```
  
5.  Passe o novo comando de menu para o <xref:System.ComponentModel.Design.IMenuCommandService.AddCommand%2A> método no <xref:System.ComponentModel.Design.IMenuCommandService> interface. Isso é feito por padrão para comandos criados pelo modelo de pacote, conforme mostrado no exemplo a seguir  
  
     [!code-csharp[ButtonGroup#24](../extensibility/codesnippet/CSharp/menucommands-vs-olemenucommands_9.cs)]  
  
6.  Implemente o método que manipula o comando.  
  
### <a name="to-implement-querystatus"></a>Para implementar QueryStatus  
  
1. O evento QueryStatus ocorre antes que um comando é exibido. Isso permite que as propriedades desse comando para ser definida no evento manipulador antes de atingir o usuário. Somente os comandos que são adicionados como <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> objetos podem acessar esse método.  
  
    Adicionar um `EventHandler` do objeto para o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> evento na <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> objeto que é criado para lidar com o comando, conforme mostrado no exemplo a seguir (`menuItem` é o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> instância).  
  
    [!code-csharp[MenuText#14](../extensibility/codesnippet/CSharp/menucommands-vs-olemenucommands_10.cs)]
    [!code-vb[MenuText#14](../extensibility/codesnippet/VisualBasic/menucommands-vs-olemenucommands_10.vb)]  
  
    O `EventHandler` objeto recebe o nome de um método que é chamado quando o status do comando de menu é consultado.  
  
2. Implemente o método de manipulador de status de consulta para o comando. O `object` `sender` parâmetro pode ser convertido em um <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> objeto, que é usado para definir os vários atributos do comando de menu, incluindo o texto. A tabela a seguir mostra as propriedades na <xref:System.ComponentModel.Design.MenuCommand> classe (que a classe MPF <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> deriva) que correspondem ao <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> sinalizadores.  
  
   |Propriedade MenuCommand|Sinalizador OLECMDF|  
   |--------------------------|------------------|  
   |<xref:System.ComponentModel.Design.MenuCommand.Checked%2A> = `true`|OLECMDF_LATCHED|  
   |<xref:System.ComponentModel.Design.MenuCommand.Visible%2A> = `false`|OLECMDF_INVISIBLE|  
   |<xref:System.ComponentModel.Design.MenuCommand.Enabled%2A> = `true`|OLECMDF_ENABLED|  
  
    Para alterar o texto de um comando de menu, use o <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.Text%2A> propriedade no <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> do objeto, conforme mostrado no exemplo a seguir.  
  
    [!code-csharp[MenuText#11](../extensibility/codesnippet/CSharp/menucommands-vs-olemenucommands_11.cs)]
    [!code-vb[MenuText#11](../extensibility/codesnippet/VisualBasic/menucommands-vs-olemenucommands_11.vb)]  
  
   MPF controla automaticamente o caso dos grupos sem suporte ou desconhecidos. A menos que um comando foi adicionado para o <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> usando o <xref:System.ComponentModel.Design.IMenuCommandService.AddCommand%2A> não há suporte para o método, o comando.  
  
### <a name="handle-commands-by-using-the-iolecommandtarget-interface"></a>Comandos de identificador por meio da interface IOleCommandTarget  
 Para o código que usa o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> diretamente a interface, o VSPackage deve implementar ambas as <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> e <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> métodos do <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface. Se o VSPackage implementa uma hierarquia do projeto, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> métodos do <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface deve ser implementada em vez disso.  
  
 Tanto a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> e <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> métodos destinam-se para receber um conjunto único comando `GUID` e uma matriz de IDs de comando como entrada. É recomendável que os VSPackages dão suporte total a esse conceito de várias IDs em uma chamada. No entanto, desde que um VSPackage não é chamado de outros VSPackages, você pode supor que a matriz de comando contém apenas uma ID de comando porque o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> e <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> métodos são executados em uma ordem bem definida. Para obter mais informações sobre roteamento, consulte [roteamento de comando em VSPackages](../extensibility/internals/command-routing-in-vspackages.md).  
  
 Para o código que usa o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface diretamente para a manipulação de comando, você deve implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método em um VSPackage da seguinte maneira para lidar com comandos.  
  
#### <a name="to-implement-the-querystatus-method"></a>Para implementar o método QueryStatus  
  
1. Retornar <xref:Microsoft.VisualStudio.VSConstants.S_OK> para comandos válidos.  
  
2. Defina as `cmdf` elemento do `prgCmds` parâmetro.  
  
    O valor da `cmdf` elemento é a união lógica dos valores da <xref:Microsoft.VisualStudio.OLE.Interop.OLECMDF> enumeração, combinada com o OR lógico (`|`) operador.  
  
    Use a enumeração apropriada, com base no status do comando:  
  
   - Se houver suporte para o comando:  
  
      `prgCmds[0].cmdf = OLECMDF_SUPPORTED;`  
  
   - Se o comando deve ser invisível no momento:  
  
      `prgCmds[0].cmdf |= OLECMDF_INVISIBLE;`  
  
   - Se o comando é ativado e parece ter sido clicado:  
  
      `prgCmds[0].cmdf |= OLECMDF_LATCHED;`  
  
      No caso do processamento de comandos que são hospedados em um menu do tipo `MenuControllerLatched`, o primeiro comando que está marcado com o `OLECMDF_LATCHED` sinalizador é o comando de padrão que é exibido pelo menu na inicialização. Para obter mais informações sobre `MenuController` tipos de menu, consulte [elemento Menu](../extensibility/menu-element.md).  
  
   - Se o comando é habilitado no momento:  
  
      `prgCmds[0].cmdf |= OLECMDF_ENABLED;`  
  
   - Se o comando é parte de um menu de atalho e fica oculta por padrão:  
  
      `prgCmds[0] cmdf |= OLECMDF_DEFHIDEONCTXTMENU`  
  
   - Se o comando usa o `TEXTCHANGES` sinalizador, defina a `rgwz` elemento da `pCmdText` parâmetro para o novo texto do comando e definido o `cwActual` elemento do `pCmdText` parâmetro para o tamanho da cadeia de caracteres de comando.  
  
     Para condições de erro, o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método deve manipular casos de erro a seguir:  
  
   - Se o GUID é desconhecido ou não tem suporte, retorne `OLECMDERR_E_UNKNOWNGROUP`.  
  
   - Se o GUID é conhecido, mas a ID de comando é desconhecido ou não tem suporte, retorne `OLECMDERR_E_NOTSUPPORTED`.  
  
   A implementação de VSPackage do <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> método também deve retornar códigos de erro específicos, dependendo se o comando tem suporte e se o comando foi tratado com êxito.  
  
#### <a name="to-implement-the-exec-method"></a>Para implementar o método Exec  
  
-   Se o comando `GUID` for desconhecido, retornar `OLECMDERR_E_UNKNOWNGROUP`.  
  
-   Se o `GUID` é conhecido, mas o comando ID for desconhecido, retorne `OLECMDERR_E_NOTSUPPORTED`.  
  
-   Se o `GUID` e ID de comando corresponder o par de GUID:ID que é usado pelo comando na *VSCT* de arquivos, execute o código que está associado com o comando e o retorno <xref:Microsoft.VisualStudio.VSConstants.S_OK>.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema XML do VSCT](../extensibility/vsct-xml-schema-reference.md)   
 [Ampliar menus e comandos](../extensibility/extending-menus-and-commands.md)