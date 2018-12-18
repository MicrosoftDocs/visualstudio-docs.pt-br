---
title: 'Como: importar uma página mestra ou tema | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- importing items [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 116ab878d8591fb15bfbb319b2c1d79952fbd0e7
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118540"
---
# <a name="how-to-import-a-master-page-or-theme"></a>Como: importar uma página mestra ou tema
  Você pode dar o páginas no site do SharePoint uma aparência consistente, criando e usando páginas mestras e temas. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] não fornece modelos para esses elementos, mas você pode criá-los no SharePoint Designer e, em seguida, importá-los para [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Para obter mais informações, consulte [bloco de construção: páginas e a Interface do usuário](http://go.microsoft.com/fwlink/?LinkID=182095) no site da Microsoft.  
  
### <a name="to-import-a-master-page-or-theme"></a>Para importar uma página mestra ou tema  
  
1.  No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], crie ou abra um projeto do SharePoint.  
  
     Para obter informações sobre como criar um projeto do SharePoint, consulte [SharePoint modelos de item de projeto e projeto](../sharepoint/sharepoint-project-and-project-item-templates.md).  
  
2.  Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.  
  
3.  No **Adicionar Novo Item** diálogo caixa, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
4.  Na lista de modelos do SharePoint, escolha o **módulo** modelo e, em seguida, especifique um nome para o módulo.  
  
     Um módulo contém arquivos (por exemplo, página mestra ou arquivos de tema) para implantação em um local que você especifica no SharePoint.  
  
5.  No módulo, exclua o arquivo padrão, que é chamado *txt*.  
  
6.  Escolha o nó do módulo.  
  
7.  Na barra de menus, escolha **Project** > **Add Existing Item**e, em seguida, escolha o arquivo de tema ou página mestra.  
  
     Arquivos de página mestra tem uma extensão. master e arquivos de tema têm uma extensão. thmx.  
  
8.  Se você tiver adicionado uma página mestra, altere sua **resolução de conflitos de implantação** definir como **automático** nas propriedades do módulo.  
  
    > [!NOTE]  
    >  Podem ocorrer erros se o nome da página mestra for igual ao nome de uma página mestra existente que está marcado como página padrão do mestre ou página mestra personalizada. Para obter informações sobre como resolver esse problema, consulte [instruções passo a passo: importar uma página mestra personalizada e a página do site com uma imagem](../sharepoint/walkthrough-import-a-custom-master-page-and-site-page-with-an-image.md).  
  
9. O módulo, abra *Elements. XML*.  
  
     Você deve atualizar o *Elements. XML* arquivo para fazer referência a página mestra ou tema que você adicionou.  
  
10. Para uma página mestra, substitua a marcação de módulo existente com a marcação a seguir.  
  
    ```xml  
    <Module Name="[Module Name]" Url="_catalogs/masterpage">  
        <File Path="[Module Name]\[Master Page Name].master"   
          Url="[Master Page Name].master" Type="GhostableInLibrary" />  
    </Module>  
    ```  
  
     Para um tema, substitua a marcação de módulo existente com a marcação a seguir.  
  
    ```xml  
    <Module Name="[Module Name]" Url="_catalogs/theme"   
        <File Path="[Module Name]\[Theme Name].thmx" Url="[Theme     
          Name].thmx" Type="GhostableInLibrary" />  
    </Module>  
    ```  
  
     Certifique-se de substituir os valores de espaço reservado com os nomes reais do módulo e a página mestra ou tema.  
  
     O atributo `Type="GhostableInLibrary"` indica que o item é adicionado para o banco de dados de conteúdo e o `Url` atributo do módulo Especifica onde armazenar o arquivo do banco de dados de conteúdo do SharePoint.  
  
11. Para alterar o escopo da implantação para uma página mestra, na **Gerenciador de soluções**, abra o arquivo de recurso no Designer de recurso e, em seguida, escolha um novo escopo de implantação dos **escopo** lista.  
  
     Um valor de **Web** significa que a página mestra se aplica somente ao site que é especificado no momento no projeto. Um valor de **Site** significa que a página mestra se aplica à coleção de site atual, que inclui todos os subsites e web raiz. Não se aplicam os outros valores.  
  
    > [!NOTE]  
    >  Como os temas se aplicam somente ao nível de coleção de sites, é recomendável que você não definir o escopo de um tema para qualquer coisa diferente de **Site**. Podem ocorrer erros se um tema é usado em um subsite.  
  
12. Na barra de menus, escolha **construir** > **implantar solução**.  
  
13. Para verificar se os arquivos foram implantados corretamente, abra o site do SharePoint, escolha o **ações do Site** menu, escolha o **configurações de Site** de comando e, em seguida, escolha o **páginas mestras**  link ou o **temas** link.  
  
     A lista de páginas mestras ou temas aparece e contém a página mestra ou tema que você importou.  
  
## <a name="see-also"></a>Consulte também
 [Páginas mestras](http://go.microsoft.com/fwlink/?LinkId=184955)   
 [Importando itens de um site do SharePoint existente](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)   
 [Criar páginas do SharePoint](../sharepoint/creating-pages-for-sharepoint.md)   
 [Usar módulos para incluir arquivos na solução](../sharepoint/using-modules-to-include-files-in-the-solution.md)  
  
