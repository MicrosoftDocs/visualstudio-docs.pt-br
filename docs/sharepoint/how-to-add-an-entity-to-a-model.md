---
title: 'Como: adicionar uma entidade a um modelo | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- EntityTool
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], entity
- Business Data Connectivity service [SharePoint development in Visual Studio], adding an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], entity
- BDC [SharePoint development in Visual Studio], adding an entity
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b80f39494b98014a75d4265f228906be2ff45188
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016671"
---
# <a name="how-to-add-an-entity-to-a-model"></a>Como: adicionar uma entidade a um modelo
  Para criar uma entidade, adicione um controle de entidade da caixa de **ferramentas** do Visual Studio ao designer do BDC (conectividade de dados corporativos).

### <a name="to-add-an-entity-to-the-model"></a>Para adicionar uma entidade ao modelo

1. Crie um projeto do BDC ou abra um projeto do BDC existente. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md).

2. Na **caixa de ferramentas**, no grupo **BusinessDataCatalog** , adicione um controle de **entidade** no designer.

     A nova entidade aparece no designer. O Visual Studio adiciona um `<Entity>` elemento ao XML do arquivo de modelo do BDC em seu projeto. Para obter mais informações sobre os atributos de um elemento de entidade, consulte [Entity](/previous-versions/office/developer/sharepoint-2010/ee558325(v=office.14)).

3. No designer, abra o menu de atalho da entidade, escolha **Adicionar**e, em seguida, escolha **identificador**.

     Um novo identificador é exibido na entidade.

    > [!NOTE]
    > Você pode alterar o nome da entidade e o identificador na janela **Propriedades** .

4. Defina os campos da entidade em uma classe. Você pode adicionar uma nova classe ao projeto ou usar uma classe existente criada usando outras ferramentas, como o Object Relational Designer (O/R Designer). O exemplo a seguir mostra uma classe de entidade chamada Contact.

     [!code-csharp[SP_BDC_Entity_Data_Class#1](../sharepoint/codesnippet/CSharp/sp_bdc_entity_data_class/bdcmodel1/contact.cs#1)]
     [!code-vb[SP_BDC_Entity_Data_Class#1](../sharepoint/codesnippet/VisualBasic/sp_bdc_entity_data_class/bdcmodel1/contact.vb#1)]

## <a name="see-also"></a>Consulte também
- [Como: adicionar um método de criador](../sharepoint/how-to-add-a-creator-method.md)
- [Como adicionar um método excluidor](../sharepoint/how-to-add-a-deleter-method.md)
- [Como adicionar um método de atualizador](../sharepoint/how-to-add-an-updater-method.md)
- [Como adicionar um método localizador](../sharepoint/how-to-add-a-finder-method.md)
- [Como adicionar um método localizador específico](../sharepoint/how-to-add-a-specific-finder-method.md)
