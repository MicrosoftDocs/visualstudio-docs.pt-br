---
title: 'Como: adicionar comandos a menus de atalho'
description: Saiba como você pode adicionar comandos a um menu de atalho em um aplicativo do Office usando um suplemento do VSTO.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office menus, creating
- Office development in Visual Studio, context menus
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 276dc7b8094c495a1b3896a4a93a068b1005c8d5
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828443"
---
# <a name="how-to-add-commands-to-shortcut-menus"></a>Como: adicionar comandos a menus de atalho
  Este tópico demonstra como adicionar comandos a um menu de atalho em um aplicativo do Office usando um suplemento do VSTO.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

### <a name="to-add-commands-to-shortcut-menus-in-office"></a>Para adicionar comandos a menus de atalho no Office

1. Adicione um item **XML da faixa** de bits a um projeto de suplemento do VSTO ou no nível do documento. Para obter mais informações, consulte [como: começar a personalizar a faixa de](../vsto/how-to-get-started-customizing-the-ribbon.md)visualização. Em

2. **Gerenciador de soluções**, selecione **ThisAddIn. cs** ou **ThisAddIn. vb**.

3. Na barra de menus, escolha **Exibir**  >  **código**.

     O arquivo de classe **ThisAddIn** é aberto no editor de código.

4. Adicione o código a seguir à classe **ThisAddIn** . Esse código substitui o `CreateRibbonExtensibilityObject` método e retorna a classe XML da faixa de forma para o aplicativo do Office.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_menus.cs/thisaddin.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_menus.vb/thisaddin.vb" id="Snippet1":::

5. Em **Gerenciador de soluções**, selecione o arquivo XML da faixa de opções. Por padrão, o arquivo XML da faixa de faixas é denominado *Ribbon1.xml*.

6. Na barra de menus, escolha **Exibir**  >  **código**.

     O arquivo XML da faixa de faixas é aberto no editor de códigos.

7. No editor de código, adicione XML que descreve o menu de atalho e o controle que você deseja adicionar ao menu de atalho.

     O exemplo a seguir adiciona um botão, um menu e um controle galeria ao menu de atalho para um documento do Word. A ID de controle desse menu de atalho é ContextMenuText. Para obter uma lista completa de IDs de controle de atalho do Office 2010, consulte [arquivos de ajuda do office 2010: identificadores de controle de interface do usuário Fluent do Office](https://www.microsoft.com/download/details.aspx?id=6627).

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

8. Em **Gerenciador de soluções**, escolha **MyRibbon. cs** ou **MyRibbon. vb**.

9. Adicione um método de retorno de chamada à `Ribbon1` classe para cada controle que você deseja manipular.

     O método de retorno de chamada a seguir manipula o botão de **botão My** . Esse código adiciona uma cadeia de caracteres ao documento ativo no local atual do cursor.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_menus.vb/ribbon1.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_menus.cs/ribbon1.cs" id="Snippet2":::

## <a name="see-also"></a>Consulte também
- [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)
- [Walkthrough: criar menus de atalho para indicadores](../vsto/walkthrough-creating-shortcut-menus-for-bookmarks.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
- [Personalizar menus de contexto no Office 2010](/previous-versions/office/developer/office-2010/ee691832(v=office.14))
