---
title: 'Como: usar um arquivo de recurso para especificar nomes, propriedades e permissões localizadas | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
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
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a87cc8a3eb8f98ea19a87e93c37aae5303151ecf
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015396"
---
# <a name="how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions"></a>Como: usar um arquivo de recurso para especificar nomes, propriedades e permissões localizadas
  Usando um arquivo de recurso, você pode fornecer nomes localizados, definir propriedades e aplicar permissões Tor objetos que são definidos em um modelo de BDC (conectividade de dados corporativos). Para especificar essas informações, você adiciona um item de **recurso de conectividade de dados corporativos** a um projeto que contém um item de **modelo de conectividade de dados corporativos** . Em seguida, especifique nomes, propriedades e permissões editando o XML para o arquivo de recurso.

### <a name="to-add-a-bdc-resource-file-to-a-sharepoint-project"></a>Para adicionar um arquivo de recurso do BDC a um projeto do SharePoint

1. Em **Gerenciador de soluções**, expanda a pasta do projeto do SharePoint e escolha a pasta que contém o modelo do BDC.

2. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

3. Expanda o nó do **SharePoint** e escolha o nó **2010** .

4. Na caixa de diálogo **Adicionar novo item** , escolha **item de recurso de conectividade de dados corporativos**.

5. Na caixa **nome** , especifique o nome do arquivo de recurso e, em seguida, escolha o botão **Adicionar** .

     Um arquivo de recurso que tem a extensão. bdcr é adicionado ao projeto e aberto para edição.

6. Adicione XML para definir os nomes, as propriedades e as permissões localizadas que você deseja aplicar ao modelo do BDC.

     Para obter informações sobre como definir esses elementos, consulte [modelo e arquivos de recurso](/previous-versions/office/developer/sharepoint-2010/aa674515(v=office.14)).

## <a name="see-also"></a>Consulte também
- [Como: adicionar um arquivo de modelo BDC existente a um projeto do SharePoint](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md)
- [Como: criar um modelo de BDC](../sharepoint/how-to-create-a-bdc-model.md)
- [Como: incluir um assembly personalizado em um recurso do BDC](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [Integrando dados corporativos ao SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)
