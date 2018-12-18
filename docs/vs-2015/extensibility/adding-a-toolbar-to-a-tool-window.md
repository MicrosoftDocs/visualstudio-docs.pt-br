---
title: Adicionando uma barra de ferramentas para uma janela de ferramentas | Microsoft Docs
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
- tool windows, adding toolbars
- toolbars [Visual Studio], adding to tool windows
ms.assetid: 172f64b3-87f8-4292-9c1c-65bffa2b0970
caps.latest.revision: 49
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 2dfb26dd77a3117f40f82fdb80669a2e849e6c94
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755165"
---
# <a name="adding-a-toolbar-to-a-tool-window"></a>Adicionando uma barra de ferramentas a uma janela de ferramentas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo mostra como adicionar uma barra de ferramentas para uma janela de ferramentas.  
  
 Uma barra de ferramentas é uma faixa horizontal ou vertical que contém os botões associados a comandos. O comprimento de uma barra de ferramentas em uma janela de ferramenta é sempre o mesmo que a largura ou altura da janela de ferramenta, dependendo de onde a barra de ferramentas é encaixada.  
  
 Ao contrário de barras de ferramentas no IDE, uma barra de ferramentas em uma janela de ferramenta deve ser encaixada e não pode ser movida ou personalizada. Se o VSPackage é escrito em código umanaged, a barra de ferramentas pode ser encaixada em qualquer uma das bordas.  
  
 Para obter mais informações sobre como adicionar uma barra de ferramentas, consulte [adicionando uma barra de ferramentas](../extensibility/adding-a-toolbar.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-toolbar-for-a-tool-window"></a>Criando uma barra de ferramentas para uma janela de ferramentas  
  
1.  Crie um projeto do VSIX chamado `TWToolbar` que possui um comando menu denominado **TWTestCommand** e uma janela de ferramenta chamada **TestToolWindow**. Para obter mais informações, consulte [criar uma extensão com um comando de Menu](../extensibility/creating-an-extension-with-a-menu-command.md) e [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md). Você precisará adicionar o modelo de item de comando antes de adicionar o modelo de janela de ferramenta.  
  
2.  No TWTestCommandPackage.vsct, procure a seção de símbolos. No nó do GuidSymbol chamado guidTWTestCommandPackageCmdSet declare uma barra de ferramentas e um grupo de barra de ferramentas, da seguinte maneira.  
  
    ```xml  
    <IDSymbol name="TWToolbar" value="0x1000" />  
    <IDSymbol name="TWToolbarGroup" value="0x1050" />  
    ```  
  
3.  Na parte superior do `Commands` seção, crie um `Menus` seção. Adicionar um `Menu` elemento para definir a barra de ferramentas.  
  
    ```xml  
    <Menus>  
        <Menu guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" type="ToolWindowToolbar">  
            <CommandFlag>DefaultDocked</CommandFlag>  
            <Strings>  
                <ButtonText>Test Toolbar</ButtonText>  
                <CommandName>Test Toolbar</CommandName>  
            </Strings>  
        </Menu>  
    </Menus>  
    ```  
  
     Barras de ferramentas não podem ser aninhadas, como submenus. Portanto, não é necessário atribuir um pai. Além disso, você não precisa definir uma prioridade, porque o usuário pode mover as barras de ferramentas. Normalmente, o posicionamento inicial de uma barra de ferramentas é definido por meio de programação, mas as alterações subsequentes pelo usuário são persistentes.  
  
4.  Na seção grupos, defina um grupo para conter os comandos da barra de ferramentas.  
  
    ```xml  
  
    <Group guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" priority="0x0000">  
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" />  
    </Group>  
    ```  
  
5.  Na seção de botões, altere o pai do elemento de botão existente para o grupo de barra de ferramentas para que a barra de ferramentas será exibida.  
  
    ```xml  
    <Button guid="guidTWTestCommandPackageCmdSet" id="TWTestCommandId" priority="0x0100" type="Button">  
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />  
        <Icon guid="guidImages" id="bmpPic1" />  
        <Strings>  
            <ButtonText>Invoke TWTestCommand</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
     Por padrão, se uma barra de ferramentas não tem nenhum comando, ele não aparece.  
  
     Como a nova barra de ferramentas não é adicionada automaticamente para a janela da ferramenta, a barra de ferramentas deve ser adicionada explicitamente. Isso é abordado na próxima seção.  
  
## <a name="adding-the-toolbar-to-the-tool-window"></a>Adicionar a barra de ferramentas para a janela da ferramenta  
  
1.  No TWTestCommandPackageGuids.cs, adicione as linhas a seguir.  
  
    ```csharp  
    public const string guidTWTestCommandPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file  
    public const int TWToolbar = 0x1000;  
    ```  
  
2.  No TestToolWindow.cs, adicione a seguinte instrução using.  
  
    ```csharp  
    using System.ComponentModel.Design;  
    ```  
  
3.  No construtor TestToolWindow, adicione a seguinte linha.  
  
    ```csharp  
    this.ToolBar = new CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), TWTestCommandPackageGuids.TWToolbar);  
    ```  
  
## <a name="testing-the-toolbar-in-the-tool-window"></a>Teste a barra de ferramentas na janela da ferramenta  
  
1.  Compile o projeto e comece a depuração. A instância experimental do Visual Studio deve aparecer.  
  
2.  No **exibição / Windows outras** menu, clique em **teste ToolWindow** para exibir a janela de ferramenta.  
  
     Você verá uma barra de ferramentas (ele se parece com o ícone padrão) na parte superior esquerda da janela de ferramenta, logo abaixo do título.  
  
3.  Na barra de ferramentas, clique no ícone para exibir a mensagem **TWTestCommandPackage dentro TWToolbar.TWTestCommand.MenuItemCallback()**.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar uma barra de ferramentas](../extensibility/adding-a-toolbar.md)

