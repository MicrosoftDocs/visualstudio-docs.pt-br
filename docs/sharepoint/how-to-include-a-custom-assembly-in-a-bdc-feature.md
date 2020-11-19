---
title: 'Como: incluir um assembly personalizado em um recurso do BDC | Microsoft Docs'
description: Inclua assemblies personalizados em um recurso BDC (conectividade de dados corporativos) para que seu projeto possa referenciar assemblies de outros projetos na mesma solução.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.BDC.Add_Assemblies_Dialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], add reference
- Business Data Connectivity service [SharePoint development in Visual Studio], custom assembly
- BDC [SharePoint development in Visual Studio], custom assembly
- BDC [SharePoint development in Visual Studio], add reference
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e7a2a0109faca4da5406b45b4d606ae8a5cd0685
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903462"
---
# <a name="how-to-include-a-custom-assembly-in-a-bdc-feature"></a>Como: incluir um assembly personalizado em um recurso do BDC
  Seu projeto pode referenciar assemblies de outros projetos na mesma solução. No entanto, você deve adicionar esses assemblies ao arquivo de recurso do projeto usando a caixa de diálogo **atribuir assemblies referenciados ao LobSystems** .

### <a name="to-include-a-custom-assembly-in-a-business-data-connectivity-bdc-feature"></a>Para incluir um assembly personalizado em um recurso BDC (conectividade de dados corporativos)

1. Em **Gerenciador de soluções**, escolha a pasta que contém o modelo BDC.

2. No menu **Exibir** , clique em **Janela Propriedades**.

3. Na janela **Propriedades** , escolha a propriedade **assemblies** e, em seguida, o botão de reticências (![ASP.NET Mobile Designer Ellipse](../sharepoint/media/mwellipsis.gif "Elipse do designer móvel ASP.NET")).

     A caixa de diálogo **atribuir assemblies referenciados ao LobSystems** é exibida.

4. Na lista **selecionar um assembly** , escolha o assembly personalizado.

    > [!NOTE]
    > Os assemblies só aparecem na caixa de diálogo **atribuir assemblies referenciados ao LobSystems** se você tiver adicionado uma referência ao projeto que contém o assembly. Para obter mais informações, consulte [como: Adicionar ou remover referências usando a caixa de diálogo Adicionar referência](/previous-versions/wkze6zky(v=vs.140)).

5. No grupo **Propriedades de referência** , abra a lista que aparece para a propriedade **escopo do LobSystem** , escolha o sistema LOB dos métodos que usam o assembly personalizado e escolha o botão **OK** .

    > [!NOTE]
    > Para depurar o código no assembly personalizado, você deve adicionar o assembly ao pacote de solução. Para obter mais informações, consulte [como adicionar e remover assemblies adicionais](../sharepoint/how-to-add-and-remove-additional-assemblies.md).

## <a name="see-also"></a>Confira também
- [Como: usar um arquivo de recurso para especificar nomes, propriedades e permissões localizadas](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [Como: adicionar um arquivo de modelo BDC existente a um projeto do SharePoint](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md)
- [Como: criar um modelo de BDC](../sharepoint/how-to-create-a-bdc-model.md)
- [Integragte dados corporativos no SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)