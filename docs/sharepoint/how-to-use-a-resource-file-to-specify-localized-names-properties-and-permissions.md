---
title: 'Como: usar um arquivo de recurso para especificar nomes localizados, propriedades e permissões | Microsoft Docs'
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
- Business Data Connectivity service [SharePoint development in Visual Studio], localize strings
- BDC [SharePoint development in Visual Studio], localize strings
- BDC [SharePoint development in Visual Studio], resource file
- Business Data Connectivity service [SharePoint development in Visual Studio], resource strings
- BDC [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], resource file
- BDC [SharePoint development in Visual Studio], resource strings
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c54aa87f09d4821f9fde5cceb95e6ec3a8e089fa
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118358"
---
# <a name="how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions"></a>Como: usar um arquivo de recurso para especificar nomes localizados, propriedades e permissões
  Usando um arquivo de recurso, forneça nomes localizados, defina as propriedades e aplicar permissões tor objetos que são definidos em um modelo de conectividade de dados comerciais (BDC). Para especificar essas informações, você adiciona uma **recurso de conectividade de dados de negócios** item a um projeto que contém uma **modelo de conectividade de dados corporativos** item. Em seguida, especifique nomes, propriedades e permissões, editando o XML para o arquivo de recurso.  
  
### <a name="to-add-a-bdc-resource-file-to-a-sharepoint-project"></a>Para adicionar um arquivo de recurso do BDC a um projeto do SharePoint  
  
1.  Na **Gerenciador de soluções**, expanda a pasta para o projeto do SharePoint e, em seguida, escolha a pasta que contém o modelo BDC.  
  
2.  Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.  
  
3.  Expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
4.  No **Adicionar Novo Item** diálogo caixa, escolha **Item de recurso de conectividade de dados corporativos**.  
  
5.  No **nome** caixa, especifique o nome do arquivo de recurso e, em seguida, escolha o **Add** botão.  
  
     Um arquivo de recurso que tem a extensão de .bdcr é adicionado ao projeto e aberto para edição.  
  
6.  Adicione o XML para definir os nomes localizados, propriedades e permissões que você deseja aplicar o modelo BDC.  
  
     Para obter informações sobre como definir esses elementos, consulte [modelo e arquivos de recurso](http://go.microsoft.com/fwlink/?LinkID=169283).  
  
## <a name="see-also"></a>Consulte também
 [Como: adicionar um arquivo de modelo BDC existente a um projeto do SharePoint](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)   
 [Criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md)   
 [Como: criar um modelo BDC](../sharepoint/how-to-create-a-bdc-model.md)   
 [Como: incluir um assembly personalizado em uma recurso BDC](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)   
 [Integrando dados corporativos ao SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)  
  
