---
title: Como definir uma instância de método | Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], method instance
- BDC [SharePoint development in Visual Studio], method instance
- BDC [SharePoint development in Visual Studio], method
- Business Data Connectivity service [SharePoint development in Visual Studio], method
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 170982a5d4abe33ca8cd705a979acc0737185a9c
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016832"
---
# <a name="how-to-define-a-method-instance"></a>Como definir uma instância de método
  Você deve definir pelo menos uma instância de método para cada método em seu modelo.

 Adicione uma instância de método usando a janela **detalhes do método do BDC** . Quando você adiciona a instância do método, o Visual Studio adiciona um `<MethodInstance>` elemento ao XML do arquivo de modelo em seu projeto. Para obter mais informações sobre os atributos de um `<MethodInstance>` elemento, consulte [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14)).

### <a name="to-define-a-method-instance"></a>Para definir uma instância de método

1. Na janela **detalhes do método BDC** , expanda o nó de um método e, em seguida, expanda o nó **instâncias** .

2. Na lista **Adicionar uma instância de método** , escolha **criar instância de localizador**.

     Uma nova instância de método aparece abaixo do nó **instâncias** .

3. Na barra de menus, escolha **Exibir**  >  **janela de propriedades**.

4. Na janela **Propriedades** , defina as propriedades da instância do método. Para obter mais informações sobre cada propriedade, consulte [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14)).

## <a name="see-also"></a>Consulte também
- [Visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md)
- [Como: adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [Como definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
