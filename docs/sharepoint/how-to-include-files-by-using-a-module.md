---
title: 'Como: incluir arquivos usando um módulo | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, modules
- modules [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5c5152221e5e58504ba84e0ad0f31511b4d93aa0
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118342"
---
# <a name="how-to-include-files-by-using-a-module"></a>Como: incluir arquivos usando um módulo
  *Módulos* (não deve ser confundido com [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] módulos) são contêineres que permitem que você implante imagens, arquivos de texto ou arquivos como páginas mestras do ASPX no SharePoint.  
  
 Você pode optar por implantar um arquivo em uma biblioteca de documentos ou como um arquivo normal (por exemplo, default. aspx) fora de uma biblioteca de documentos. Para adicionar um arquivo a uma biblioteca de documentos, especifique `Type="GhostableInLibrary"` como um atributo na **arquivo** elemento. Esta configuração instrui o SharePoint para criar um item de lista para ir com o arquivo quando ele é adicionado à biblioteca. Para implantar um arquivo fora de uma biblioteca de documentos, especifique `Type="Ghostable"` ou apenas omita a **tipo** atributo.  
  
## <a name="add-a-module-to-a-sharepoint-solution"></a>Adicionar um módulo a uma solução do SharePoint  
  
#### <a name="to-add-a-module"></a>Para adicionar um módulo  
  
1.  No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], abra ou crie um projeto do SharePoint.  
  
     Para obter mais informações, consulte [SharePoint modelos de item de projeto e projeto](../sharepoint/sharepoint-project-and-project-item-templates.md).  
  
2.  Na **Gerenciador de soluções**, escolha o nó do projeto e, em seguida, na barra de menus, escolha **Project** > **Add New Item**.  
  
     A caixa de diálogo **Adicionar Novo Item** é aberta.  
  
3.  Na lista de modelos do SharePoint, escolha o **módulo** modelo e, em seguida, escolha o **Add** botão.  
  
     Esta etapa cria um nó do projeto chamado Module1.  
  
4.  Em Module1, exclua o *txt* arquivo.  
  
     Txt está incluído em todos os novos módulos fins por exemplo e não é necessária. (Observe que excluir o arquivo também remove sua entrada do módulo *Elements. XML* arquivo.)  
  
5.  Se você quiser que seus arquivos para implantar em uma estrutura de pasta específica no SharePoint, criar essas pastas em Module1 na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] escolhendo o nó Module1 e, em seguida, na barra de menus, escolhendo **Project**, **novo Pasta**.  
  
6.  Escolha a pasta na qual você deseja adicionar o arquivo e, em seguida, na barra de menus, escolha **Project**, **Add Existing Item**.  
  
7.  Escolha um ou mais arquivos que você deseja implantar no SharePoint e, em seguida, escolha o **adicionar** botão.  
  
     Quando você adiciona um arquivo ao projeto, uma entrada para que ele é automaticamente adicionada ao arquivo Elements XML do módulo. Quando o projeto é implantado, os arquivos são copiados para o servidor do SharePoint, relativo ao diretório raiz do projeto, que é especificado pela **arquivo** do elemento **Url** atributo, como `Url="Module1/New Folder/SomeFile.doc`. Se você quiser alterar o local de implantação para um arquivo, mova-lo para outra pasta **Gerenciador de soluções** ou altere seu **Url** configuração.  
  
8.  Para todos os arquivos que você deseja que apareça em uma biblioteca de documentos, acrescente a `Type="GhostableInLibrary"` atributo de entrada na *Elements. XML*. Por exemplo,  
  
    ```xml  
    <File Path="Module1\Some Folder\SomePage.aspx" Url="Module1/Some Folder/SomePage.aspx" Type="GhostableInLibrary" />  
    ```  
  
9. Implante o projeto.  
  
     Copie os arquivos para os locais especificados no SharePoint.  
  
## <a name="see-also"></a>Consulte também
 [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)   
 [Desenvolvendo soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)  
  
