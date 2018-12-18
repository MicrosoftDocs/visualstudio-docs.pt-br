---
title: 'Como: adicionar uma entidade a um modelo | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- EntityTool
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], entity
- Business Data Connectivity service [SharePoint development in Visual Studio], adding an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], entity
- BDC [SharePoint development in Visual Studio], adding an entity
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 72dbebd8ff9b2e7bf7b001d540158656271c0556
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36757695"
---
# <a name="how-to-add-an-entity-to-a-model"></a>Como: adicionar uma entidade a um modelo
  Para criar uma entidade, adicione um controle de entidade do Visual Studio **caixa de ferramentas** para o designer de conectividade de dados comerciais (BDC).  
  
### <a name="to-add-an-entity-to-the-model"></a>Para adicionar uma entidade no modelo  
  
1.  Criar um projeto BDC ou abrir um projeto existente do BDC. Para obter mais informações, consulte [criar um modelo de conectividade de dados de negócios](../sharepoint/creating-a-business-data-connectivity-model.md).  
  
2.  No **caixa de ferramentas**, da **BusinessDataCatalog** de grupo, adicione um **entidade** controle para o designer.  
  
     A nova entidade é exibida no designer. O Visual Studio adiciona um `<Entity>` elemento ao XML do arquivo de modelo BDC em seu projeto. Para obter mais informações sobre os atributos de um elemento de entidade, consulte [entidade](http://go.microsoft.com/fwlink/?LinkId=169296).  
  
3.  No designer, abra o menu de atalho para a entidade, escolha **Add**e, em seguida, escolha **identificador**.  
  
     Um novo identificador aparece na entidade.  
  
    > [!NOTE]  
    >  Você pode alterar o nome da entidade e o identificador na **propriedades** janela.  
  
4.  Defina os campos da entidade em uma classe. Você pode adicionar uma nova classe ao projeto ou usar uma classe existente criada usando outras ferramentas, como o Object Relational Designer (O/R Designer). O exemplo a seguir mostra uma classe de entidade chamada contato.  
  
     [!code-csharp[SP_BDC_Entity_Data_Class#1](../sharepoint/codesnippet/CSharp/sp_bdc_entity_data_class/bdcmodel1/contact.cs#1)]
     [!code-vb[SP_BDC_Entity_Data_Class#1](../sharepoint/codesnippet/VisualBasic/sp_bdc_entity_data_class/bdcmodel1/contact.vb#1)]  
  
## <a name="see-also"></a>Consulte também
 [Como: adicionar um método Creator](../sharepoint/how-to-add-a-creator-method.md)   
 [Como: adicionar um método Deleter](../sharepoint/how-to-add-a-deleter-method.md)   
 [Como: adicionar um método Updater](../sharepoint/how-to-add-an-updater-method.md)   
 [Como: adicionar um método Finder](../sharepoint/how-to-add-a-finder-method.md)   
 [Como: adicionar um método Finder específico](../sharepoint/how-to-add-a-specific-finder-method.md)  
  
 
