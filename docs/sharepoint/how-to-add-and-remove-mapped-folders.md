---
title: 'Como: adicionar e remover pastas mapeadas | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.MappedFolder
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, mapped folders
- mapped folders [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: fe9868a9909dbb78bf510f18584472520948d6f9
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36757642"
---
# <a name="how-to-add-and-remove-mapped-folders"></a>Como: adicionar e remover pastas mapeadas
  Algumas pastas usadas com frequência no SharePoint, como imagens e Layouts, profundamente inserido na hierarquia de arquivos. Você pode mapear essas pastas em um projeto do SharePoint para acessá-los mais facilmente. Pastas mapeadas são pastas no projeto do SharePoint que correspondem ao local físico dos arquivos na instalação do servidor do SharePoint.  
  
 Quando você implanta um aplicativo do SharePoint, o conteúdo da pasta mapeada e todas as suas subpastas são copiadas pelo pacote de solução (. wsp) para o servidor que está executando o SharePoint no local especificado na árvore de pastas do SharePoint. Esse local é determinado pelo **local de implantação** propriedade é definida para a pasta mapeada. Todas as subpastas na pasta mapeada são relativos **local de implantação** da pasta mapeada. Observe que o **local de implantação** propriedade, não o nome de pasta mapeada, determina quais itens são implantados.  
 Você pode adicionar pastas mapeadas a um projeto usando os comandos na barra de menus ou no menu de atalho para o projeto. Você pode usar o **pasta mapeada de "Imagens" adicionar o SharePoint** e **adicionar o SharePoint "Layouts de" pasta** comandos para adicioná-los mapeado pastas que são usadas com mais frequência. Você pode mapear qualquer uma das outras pastas do SharePoint disponíveis para seu projeto usando o **adicionar pasta mapeada do SharePoint** comando no menu de atalho e, em seguida, especificando as pastas no **adicionar pasta do SharePoint mapeado** caixa de diálogo.  
  
## <a name="add-mapped-folders-to-a-project"></a>Adicionar pastas mapeadas a um projeto  
 O procedimento a seguir descreve como adicionar duas pastas mapeadas para um projeto do visual web part. Para começar, você deve criar um projeto do visual web part.  
  
#### <a name="to-add-mapped-folders-to-a-project"></a>Para adicionar pastas mapeadas a um projeto  
  
1.  Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda o a **Visual Basic** ou **Visual c#** nó, expanda o **Office/SharePoint** nó e, em seguida, Escolha o **soluções do SharePoint** nó.  
  
3.  Na lista de modelos de projeto, escolha o **Visual Web Part do SharePoint 2013** modelo.  
  
4.  No **nome** , digite **TestProject1**e, em seguida, escolha o **Okey** botão.  
  
5.  No **Assistente para personalização do SharePoint**, escolha o **concluir** botão para manter as configurações padrão.  
  
6.  Na **Gerenciador de soluções**, escolha o nó do projeto e, em seguida, na barra de menus, escolha **Project** > **pasta mapeada de "Imagens" adicionar o SharePoint**.  
  
     Uma pasta denominada **imagens** aparece em seu projeto e contém uma subpasta chamada TestProject1. Essa pasta mapeada conterá imagens para o projeto do visual web part.  
  
7.  Na **Gerenciador de soluções**, escolha o nó do projeto e, em seguida, na barra de menus, escolha **Project** > **adicionar pasta mapeada do SharePoint** para exibir o  **Adicionar pasta mapeada do SharePoint** caixa de diálogo.  
  
8.  Na exibição de árvore de pastas que estão disponíveis para mapeamento, escolha o **recursos** pasta e, em seguida, escolha o **Okey** botão.  
  
     Uma pasta denominada **recursos** aparece em seu projeto. Essa pasta pode armazenar itens como arquivos de recurso de cadeia de caracteres. Subpastas podem ser útil para organizar o conteúdo de uma pasta mapeada, mas eles são criados automaticamente quando você adiciona uma pasta mapeada usando o **adicionar pasta mapeada do SharePoint** comando. Para adicionar uma subpasta, escolha o **recursos** pasta e em seguida, na barra de menus, escolha **Project** > **nova pasta**.  
  
## <a name="change-the-deployment-location-of-a-mapped-folder"></a>Alterar o local de implantação de uma pasta mapeada  
 Por padrão, as pastas mapeadas são adicionadas em locais específicos em relação ao caminho de instalação raiz do SharePoint, que o token \<SharePointRoot > denota. No entanto, você pode alterar esse local, alterando a **local de implantação** propriedade da pasta mapeada. Cada pasta mapeada tem seu próprio **local de implantação** propriedade.  
  
#### <a name="to-change-the-deployment-location-of-a-mapped-folder"></a>Para alterar o local de implantação de uma pasta mapeada  
  
1.  No projeto que você criou anteriormente, escolha uma pasta mapeada.  
  
2.  No **propriedades** janela, escolha as reticências (![elipse do Designer de dispositivo móvel do ASP.NET](../sharepoint/media/mwellipsis.gif "elipse do Designer de dispositivo móvel do ASP.NET")) botão o **implantação local** propriedade.  
  
3.  No **adicionar pasta mapeada do SharePoint** caixa de diálogo, navegue até a pasta à qual você deseja que a pasta mapeada para apontar.  
  
4.  Escolha o nó e, em seguida, escolha o **Okey** botão.  
  
## <a name="rename-or-remove-mapped-folders"></a>Renomear ou remover pastas mapeadas  
  
#### <a name="to-rename-or-remove-a-mapped-folder"></a>Para renomear ou remover uma pasta mapeada  
  
1.  No projeto que você criou anteriormente, escolha uma pasta mapeada.  
  
2.  Para renomear a pasta mapeada, abra o menu de atalho, escolha **Renomear**, digite o novo nome e, em seguida, escolha a tecla Enter.  
  
     Como alternativa, você pode escolher a pasta mapeada que você deseja renomear, abra o **propriedades** janela e, em seguida, defina o valor da **nome da pasta** propriedade para o novo nome.  
  
3.  Para remover uma pasta mapeada do projeto, abra o menu de atalho, escolha **exclua**e, em seguida, escolha o **Okey** botão na caixa de diálogo para confirmar a remoção.  
  
## <a name="see-also"></a>Consulte também
 [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)  
  
