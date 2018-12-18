---
title: 'Como: adicionar comandos aos menus de atalho'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office menus, creating
- Office development in Visual Studio, context menus
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9accca69c5d56461f07d21d25821c0f4181c8fbd
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670051"
---
# <a name="how-to-add-commands-to-shortcut-menus"></a>Como: adicionar comandos aos menus de atalho
  Este tópico demonstra como adicionar comandos ao menu de atalho em um aplicativo do Office usando um suplemento do VSTO.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
### <a name="to-add-commands-to-shortcut-menus-in-office"></a>Para adicionar comandos a menus de atalho no Office  
  
1.  Adicionar um **XML da faixa de opções** item a um nível de documento ou projeto do suplemento do VSTO. Para obter mais informações, consulte [como: Introdução à personalização da faixa de opções](../vsto/how-to-get-started-customizing-the-ribbon.md). No  
  
2.  **Gerenciador de soluções**, selecione **ThisAddin.cs** ou **ThisAddIn. vb**.  
  
3.  Na barra de menus, escolha **Exibir** > **Código**.  
  
     O **ThisAddin** arquivo de classe é aberto no Editor de códigos.  
  
4.  Adicione o seguinte código para o **ThisAddin** classe. Esse código substitui o `CreateRibbonExtensibilityObject` método e retorna o XML da faixa de opções de classe para o aplicativo do Office.  
  
     [!code-csharp[Trin_WordAddIn_Menus#1](../vsto/codesnippet/CSharp/trin_wordaddin_menus.cs/thisaddin.cs#1)]
     [!code-vb[Trin_WordAddIn_Menus#1](../vsto/codesnippet/VisualBasic/trin_wordaddin_menus.vb/thisaddin.vb#1)]  
  
5.  Na **Gerenciador de soluções**, selecione o arquivo XML de faixa de opções. Por padrão, o arquivo XML de faixa de opções é denominado *Ribbon1.xml*.  
  
6.  Na barra de menus, escolha **Exibir** > **Código**.  
  
     O arquivo xml de faixa de opções é aberto no Editor de códigos.  
  
7.  No Editor de códigos, adicione o XML que descreve o menu de atalho e o controle que você deseja adicionar ao menu de atalho.  
  
     O exemplo a seguir adiciona um botão, um menu e um controle da Galeria para o menu de atalho para um documento do word. A ID do controle desse menu de atalho é ContextMenuText. Para obter uma lista completa de controle de atalho do Office 2010 IDs, consulte [arquivos de Ajuda do Office 2010: identificadores de controle de interface de usuário fluent do Office](http://go.microsoft.com/fwlink/?LinkID=181052).  
  
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>  
    <customUI xmlns="http://schemas.microsoft.com/office/2009/07/customui">  
      <contextMenus>  
        <contextMenu idMso="ContextMenuText">  
          <button id="MyButton" label="My Button" insertBeforeMso="HyperlinkInsert" onAction="GetButtonID" />  
          <menu id="MySubMenu" label="My Submenu" >  
            <button id="MyButton2" label="Button on submenu" />  
          </menu>  
          <gallery id="galleryOne" label="My Gallery">  
            <item id="item1" imageMso="HappyFace" />  
            <item id="item2" imageMso="HappyFace" />  
            <item id="item3" imageMso="HappyFace" />  
            <item id="item4" imageMso="HappyFace" />  
          </gallery>  
        </contextMenu>  
      </contextMenus>  
    </customUI>  
    ```  
  
8.  Na **Gerenciador de soluções**, escolha **MyRibbon.cs** ou **Myribbon**.  
  
9. Adicione um método de retorno de chamada para o `Ribbon1` classe para cada controle que você deseja manipular.  
  
     Os seguintes identificadores de método de retorno de chamada a **My Button** botão. Este código adiciona uma cadeia de caracteres para o documento ativo no local atual do cursor.  
  
     [!code-vb[Trin_WordAddIn_Menus#2](../vsto/codesnippet/VisualBasic/trin_wordaddin_menus.vb/ribbon1.vb#2)]
     [!code-csharp[Trin_WordAddIn_Menus#2](../vsto/codesnippet/CSharp/trin_wordaddin_menus.cs/ribbon1.cs#2)]  
  
## <a name="see-also"></a>Consulte também  
 [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)   
 [Passo a passo: Criar menus de atalho para indicadores](../vsto/walkthrough-creating-shortcut-menus-for-bookmarks.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)   
 [Personalizar menus de contexto no Office 2010](http://go.microsoft.com/fwlink/?LinkId=182186)  
  