---
title: 'Como: Adicionar e remover pastas mapeadas | Microsoft Docs'
description: Adicionar e remover pastas mapeadas para um projeto no SharePoint.  Alterar o local de implantação de uma pasta mapeada. Renomear ou remover pastas mapeadas.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.Project.MappedFolder
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, mapped folders
- mapped folders [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a9b74ba786c9d1104fd507442d959e75afb17bf2
ms.sourcegitcommit: 1f27f33852112702ee35fbc0c02fba37899e4cf5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2021
ms.locfileid: "112112423"
---
# <a name="how-to-add-and-remove-mapped-folders"></a>Como: Adicionar e remover pastas mapeadas

  Algumas pastas comumente usadas no SharePoint, como imagens e layouts, estão profundamente inseridas na hierarquia de arquivos. Você pode mapear essas pastas em um projeto do SharePoint para acessá-las com mais facilidade. Pastas mapeadas são pastas no projeto do SharePoint que correspondem ao local físico dos arquivos na instalação do SharePoint Server.

 Quando você implanta um aplicativo do SharePoint, o conteúdo da pasta mapeada e de todas as suas subpastas são copiados pelo pacote de solução (. wsp) no servidor que está executando o SharePoint no local especificado na árvore de pastas do SharePoint. Esse local é determinado pela propriedade **local de implantação** que é definida para a pasta mapeada. Todas as subpastas na pasta mapeada são relativas ao **local de implantação** da pasta mapeada. Observe que a propriedade **local de implantação** , não o nome da pasta mapeada, determina onde os itens são implantados.
Você pode adicionar pastas mapeadas a um projeto usando comandos na barra de menus ou no menu de atalho do projeto. Você pode usar a **pasta mapeada "imagens" do SharePoint** e **adicionar comandos de pasta do SharePoint "layouts"** para adicionar as pastas mapeadas que são usadas com mais frequência. Você pode mapear qualquer uma das outras pastas do SharePoint disponíveis para seu projeto usando o comando **Adicionar pasta mapeada do SharePoint** no menu de atalho e, em seguida, especificando as pastas na caixa de diálogo **Adicionar pasta mapeada do SharePoint** .

## <a name="add-mapped-folders-to-a-project"></a>Adicionar pastas mapeadas a um projeto

 O procedimento a seguir descreve como adicionar duas pastas mapeadas a um projeto de Web Part Visual. Para começar, você cria um projeto de Web Part Visual.

## <a name="to-add-mapped-folders-to-a-project"></a>Para adicionar pastas mapeadas a um projeto

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.
::: moniker range="=vs-2017"
2. Na caixa de diálogo **novo projeto** , expanda o nó **Visual Basic** ou **Visual C#** , expanda o nó **Office/SharePoint** e escolha o nó **soluções do SharePoint** .

3. Na lista de modelos de projeto, escolha o modelo de **Web Part Visual do SharePoint 2013** .

4. Na caixa **nome** , digite **TestProject1** e, em seguida, escolha o botão **OK** .
::: moniker-end
::: moniker range=">=vs-2019"
2. Na caixa de diálogo **criar um novo projeto** , selecione a *Web Part Visual do SharePoint** para a versão específica do SharePoint que você instalou. Por exemplo, se você tiver a instalação do SharePoint 2019, selecione o modelo de **Web Part Visual do sharepoint 2019** .
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. Na caixa **nome** , digite **TestProject1**
4. Em seguida, escolha o botão **criar** .
::: moniker-end

5. No **Assistente para personalização do SharePoint**, escolha o botão **concluir** para manter as configurações padrão.

6. Em **Gerenciador de soluções**, escolha o nó do projeto e, na barra de menus, escolha **projeto**  >  **Adicionar SharePoint "imagens" pasta mapeada**.

     Uma pasta denominada **imagens** aparece em seu projeto e contém uma subpasta denominada TestProject1. Essa pasta mapeada conterá imagens para o projeto de Web Part Visual.

7. Em **Gerenciador de soluções**, escolha o nó do projeto e, na barra de menus, escolha **projeto**  >  **Adicionar pasta mapeada do SharePoint** para exibir a caixa de diálogo **Adicionar pasta mapeada do SharePoint** .

8. No modo de exibição de árvore das pastas que estão disponíveis para mapeamento, escolha a pasta **recursos** e, em seguida, escolha o botão **OK** .

     Uma pasta denominada **recursos** é exibida em seu projeto. Essa pasta pode armazenar itens como arquivos de recurso de cadeia de caracteres. As subpastas podem ser úteis para organizar o conteúdo de uma pasta mapeada, mas elas não são criadas automaticamente quando você adiciona uma pasta mapeada usando o comando **Adicionar pasta mapeada do SharePoint** . Para adicionar uma subpasta, escolha a pasta **recursos** e, na barra de menus, escolha **projeto**  >  **nova pasta**.

## <a name="change-the-deployment-location-of-a-mapped-folder"></a>Alterar o local de implantação de uma pasta mapeada

 Por padrão, as pastas mapeadas são adicionadas a locais específicos relativos ao caminho de instalação raiz do SharePoint, que o token \<SharePointRoot> denota. No entanto, você pode alterar esse local alterando a propriedade **local de implantação** da pasta mapeada. Cada pasta mapeada tem sua própria propriedade de **local de implantação** .

### <a name="to-change-the-deployment-location-of-a-mapped-folder"></a>Para alterar o local de implantação de uma pasta mapeada

1. No projeto que você criou anteriormente, escolha uma pasta mapeada.

2. Na janela **Propriedades** , escolha o botão de reticências (![elipse do ASP.NET Mobile Designer](../sharepoint/media/mwellipsis.gif "Elipse do designer móvel ASP.NET")) na propriedade **local da implantação** .

3. Na caixa de diálogo **Adicionar pasta mapeada do SharePoint** , navegue até a pasta na qual você deseja que a pasta mapeada aponte.

4. Escolha o nó e, em seguida, escolha o botão **OK** .

## <a name="rename-or-remove-mapped-folders"></a>Renomear ou remover pastas mapeadas

### <a name="to-rename-or-remove-a-mapped-folder"></a>Para renomear ou remover uma pasta mapeada

1. No projeto que você criou anteriormente, escolha uma pasta mapeada.

2. Para renomear a pasta mapeada, abra o menu de atalho, escolha **renomear**, insira o novo nome e, em seguida, escolha a tecla Enter.

     Como alternativa, você pode escolher a pasta mapeada que deseja renomear, abrir a janela **Propriedades** e, em seguida, definir o valor da propriedade **nome da pasta** como o novo nome.

3. Para remover uma pasta mapeada do projeto, abra o menu de atalho, escolha **excluir** e, em seguida, escolha o botão **OK** na caixa de diálogo para confirmar a remoção.

## <a name="see-also"></a>Confira também

- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
