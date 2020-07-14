---
title: 'Como: adicionar um arquivo de modelo BDC existente a um projeto do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.BDC.ImportDialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], import a model
- Business Data Connectivity service [SharePoint development in Visual Studio], reuse a model
- BDC [SharePoint development in Visual Studio], import a model
- BDC [SharePoint development in Visual Studio], remove a model
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 92063b5aeaf4f86919b9eabf783b102a9f5b8f34
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016519"
---
# <a name="how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project"></a>Como: adicionar um arquivo de modelo BDC existente a um projeto do SharePoint
  Você pode personalizar, empacotar e reimplantar um modelo de BDC (conectividade de dados corporativos) usando o Visual Studio para adicionar o arquivo de modelo (*. bdcm*) a qualquer projeto de farm do SharePoint. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md).

### <a name="to-add-a-bdc-model-file-to-a-sharepoint-project"></a>Para adicionar um arquivo de modelo do BDC a um projeto do SharePoint

1. Em **Gerenciador de soluções**, escolha a pasta para um projeto do SharePoint.

2. Na barra de menus, escolha **projeto**  >  **Adicionar item existente**.

3. Na caixa de diálogo **Adicionar item existente** , navegue até o local do arquivo de definição de modelo que você deseja adicionar ao seu projeto, escolha o arquivo e, em seguida, escolha o botão **Adicionar** .

    Se o modelo não definir um *sistema de linha de negócios (LOB) do tipo assembly .net*, a caixa de diálogo **Add .NET assembly LobSystem** será aberta.

4. Se a caixa de diálogo for exibida, execute uma das seguintes etapas:

   - Se você quiser escrever código personalizado e usar um designer para definir os metadados para o modelo importado, escolha o botão **Sim** , nomeie o sistema e, em seguida, escolha o botão **OK** .

   - Caso contrário, escolha o botão **não** e, em seguida, escolha o botão **OK** .

     O item de **modelo de conectividade de dados corporativos** é adicionado ao projeto.

## <a name="see-also"></a>Consulte também
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md)
- [Como: criar um modelo de BDC](../sharepoint/how-to-create-a-bdc-model.md)
- [Como: usar um arquivo de recurso para especificar nomes, propriedades e permissões localizadas](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [Como: incluir um assembly personalizado em um recurso do BDC](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [Integrando dados corporativos ao SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)
