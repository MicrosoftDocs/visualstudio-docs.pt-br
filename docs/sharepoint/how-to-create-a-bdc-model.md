---
title: 'Como: criar um modelo BDC | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 139da31ced1d32def450a1dc176ca241b0c4677f
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014541"
---
# <a name="how-to-create-a-bdc-model"></a>Como: criar um modelo de BDC
  Você pode criar um modelo de BDC (conectividade de dados corporativos) usando o modelo para esse tipo de item e, em seguida, adicionando o modelo a qualquer projeto do SharePoint. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md). Para obter mais informações sobre como projetar o modelo, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

### <a name="to-create-a-bdc-project"></a>Para criar um projeto do BDC

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

    > [!NOTE]
    > Se o IDE estiver definido para usar Visual Basic configurações de desenvolvimento, escolha **arquivo**  >  **novo projeto**.

     A caixa de diálogo **Novo Projeto** será aberta.

2. Em **Visual Basic** ou **Visual C#**, escolha **Office/SharePoint**, **soluções do SharePoint**.

3. No painel **modelos** , escolha o item de **projeto do SharePoint 2013-vazio** e, em seguida, escolha o botão **OK** .

     O **Assistente para personalização do SharePoint** é aberto.

4. Na página **especificar o site e o nível de segurança para depuração** , ESPECIFIQUE a URL de um site do SharePoint no computador local, escolha o botão de opção **implantar como solução de farm** e, em seguida, escolha o botão **concluir** .

     Você testará o modelo no site do SharePoint especificado.

    > [!IMPORTANT]
    > Você deve implantar o projeto como uma solução de farm porque os modelos BDC dão suporte apenas a soluções de farm.

     Um projeto do SharePoint vazio é criado.

5. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

6. Na caixa de diálogo **Adicionar novo item** , escolha o nó **Office/SharePoint** .

7. Na lista de modelos do SharePoint, escolha **modelo de conectividade de dados corporativos (somente solução de farm)**.

8. Na caixa **nome** , especifique um nome para o modelo BDC e, em seguida, escolha o botão **Adicionar** .

     Um item de **modelo de conectividade de dados corporativos** é adicionado ao projeto. Por padrão, o modelo aparece no BDC designer. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md).

## <a name="see-also"></a>Consulte também
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md)
- [Como: adicionar um arquivo de modelo BDC existente a um projeto do SharePoint](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [Como: usar um arquivo de recurso para especificar nomes, propriedades e permissões localizadas](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [Como: incluir um assembly personalizado em um recurso do BDC](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [Integrando dados corporativos ao SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)
