---
title: 'Como: adicionar um parâmetro a um método | Microsoft Docs'
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
- Business Data Connectivity service [SharePoint development in Visual Studio], adding a method to a parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], parameter
- BDC [SharePoint development in Visual Studio], adding a method to a parameter
- BDC [SharePoint development in Visual Studio], parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], method parameters
- BDC [SharePoint development in Visual Studio], method parameters
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 196ac37cc9bc4f53cfa886b92c62c7a301c3451a
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36756305"
---
# <a name="how-to-add-a-parameter-to-a-method"></a>Como: adicionar um parâmetro a um método
  Use um parâmetro para passar informações para o método ou para retornar informações de um método. Todos os métodos devem ter pelo menos um parâmetro. Para obter mais informações sobre como criar um parâmetro para dar suporte o tipo de método que você deseja criar, consulte [criando um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).  
  
 Quando você adiciona um parâmetro para um método, o Visual Studio adiciona o elemento de parâmetro para o XML do arquivo de modelo em seu projeto. Para obter mais informações sobre os atributos de um elemento de parâmetro, consulte [parâmetro](http://go.microsoft.com/fwlink/?LinkId=169284).  
  
### <a name="to-add-a-parameter-to-a-method"></a>Para adicionar um parâmetro a um método  
  
1.  Adicione um método a uma entidade.  
  
2.  Na barra de menus, escolha **modo de exibição** > **Other Windows** > **detalhes do método BDC**.  
  
     O **detalhes do método BDC** janela é aberta. Para obter mais informações, consulte [visão geral de ferramentas de Design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md).  
  
3.  No **detalhes do método BDC** , expanda o nó do método e, em seguida, expanda o **parâmetros** nó.  
  
4.  No **adicionar um parâmetro** , escolha **criar parâmetro**.  
  
     Um novo parâmetro aparece sob o **parâmetros** nó.  
  
5.  Na barra de menus, escolha **modo de exibição** > **janela propriedades**.  
  
6.  No **propriedades** janela, defina as **nome** propriedade para qualquer nome que faça sentido. Por exemplo, se o método retornará os clientes, você pode nomear o método **GetCustomers**.  
  
7.  No **detalhes do método BDC** janela, abra a lista que aparece para a direção do parâmetro e, em seguida, escolha **na**, **InOut**, **Out**, ou **retornar**.  
  
     Para obter mais informações sobre a direção de escolha para o método de tipo que você está criando, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).  
  
8.  Modificar o descritor de tipo do parâmetro. Para obter mais informações, consulte [como: definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md).  
  
## <a name="see-also"></a>Consulte também
 [Visão geral de ferramentas de design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md)   
 [Como: adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md)   
 [Como: definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)   
 [Como: definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)   
 [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)  
  
