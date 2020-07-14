---
title: 'Como: adicionar um parâmetro a um método | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], adding a method to a parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], parameter
- BDC [SharePoint development in Visual Studio], adding a method to a parameter
- BDC [SharePoint development in Visual Studio], parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], method parameters
- BDC [SharePoint development in Visual Studio], method parameters
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6d0496d0fd6a347683d56630990e50af585520ba
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016711"
---
# <a name="how-to-add-a-parameter-to-a-method"></a>Como: adicionar um parâmetro a um método
  Use um parâmetro para passar informações para o método ou para retornar informações de um método. Todos os métodos devem ter pelo menos um parâmetro. Para obter mais informações sobre como criar um parâmetro para dar suporte ao tipo de método que você deseja criar, consulte [criando um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

 Quando você adiciona um parâmetro a um método, o Visual Studio adiciona o elemento de parâmetro ao XML do arquivo de modelo em seu projeto. Para obter mais informações sobre os atributos de um elemento de parâmetro, consulte [Parameter](/previous-versions/office/developer/sharepoint-2010/ee557705(v=office.14)).

### <a name="to-add-a-parameter-to-a-method"></a>Para adicionar um parâmetro a um método

1. Adicione um método a uma entidade.

2. Na barra de menus, escolha **Exibir**  >  **outros**  >  **detalhes do método**do Windows BDC.

     A janela **detalhes do método BDC** é aberta. Para obter mais informações, consulte [visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md).

3. Na janela **detalhes do método BDC** , expanda o nó do método e expanda o nó **parâmetros** .

4. Na lista **Adicionar um parâmetro** , escolha **criar parâmetro**.

     Um novo parâmetro é exibido abaixo do nó **parâmetros** .

5. Na barra de menus, escolha **Exibir**  >  **janela de propriedades**.

6. Na janela **Propriedades** , defina a propriedade **Name** como qualquer nome que faça sentido. Por exemplo, se o método retornar clientes, você poderá nomear o método **GetCustomers**.

7. Na janela **detalhes do método BDC** , abra a lista que aparece para a direção do parâmetro e, em seguida, escolha **in**, **Inout**, **out**ou **Return**.

     Para obter mais informações sobre qual direção escolher para o método de tipo que você está criando, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

8. Modifique o descritor de tipo do parâmetro. Para obter mais informações, consulte [como: definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md).

## <a name="see-also"></a>Consulte também
- [Visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md)
- [Como: adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [Como definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [Como definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
