---
title: Salvando dados em extensões do sistema de projeto do SharePoint | Microsoft Docs
titleSuffix: ''
description: Saiba como salvar os dados de cadeia de caracteres que persistem após o fechamento de um projeto do SharePoint que contém uma extensão.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
helpviewer_keywords:
- SharePoint project items, saving string data
- project items [SharePoint development in Visual Studio], saving string data
- projects [SharePoint development in Visual Studio], saving string data
- SharePoint projects, saving string data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 87e05ba763095a818cc5db6f92828e6259d30e73
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217431"
---
# <a name="save-data-in-extensions-of-the-sharepoint-project-system"></a>Salvar dados em extensões do sistema de projeto do SharePoint
  Ao estender o sistema de projeto do SharePoint, você pode salvar dados de cadeia de caracteres que persistem depois que um projeto do SharePoint é fechado. Os dados normalmente são associados a um item de projeto específico ou ao próprio projeto.

 Se você tiver dados que não precisam persistir, você pode adicionar os dados a qualquer objeto no modelo de objeto de ferramentas do SharePoint que implementa a <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> interface. Para obter mais informações, consulte [associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md).

## <a name="save-data-that-is-associated-with-a-project-item"></a>Salvar dados associados a um item de projeto
 Quando você tem dados associados a um item de projeto do SharePoint específico, como o valor de uma propriedade que você adiciona a um item de projeto, você pode salvar os dados no arquivo *. COMDATA* do item de projeto. Para fazer isso, use a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> objeto. Os dados adicionados a essa propriedade são salvos no elemento **ExtensionData** no arquivo *. COMDATA* do item de projeto. Para obter mais informações, consulte [elemento ExtensionData](../sharepoint/extensiondata-element.md).

 O exemplo de código a seguir demonstra como usar a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> propriedade para salvar o valor de uma propriedade de cadeia de caracteres que é definida em um tipo de item de projeto do SharePoint personalizado. Para ver esse exemplo no contexto de um exemplo maior, consulte [como adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md).

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb" id="Snippet14":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs" id="Snippet14":::

## <a name="save-data-that-is-associated-with-a-project"></a>Salvar dados associados a um projeto
 Quando você tem dados de nível de projeto, como o valor de uma propriedade que você adiciona aos projetos do SharePoint, você pode salvar os dados no arquivo de projeto (o arquivo *. csproj* ou *. vbproj* ) ou o arquivo de opção de usuário do projeto (o arquivo *. csproj. User* ou *. vbproj. User* ). O arquivo no qual você escolhe salvar os dados depende de como você deseja que os dados sejam usados:

- Se você quiser que os dados estejam disponíveis para todos os desenvolvedores que abrem o projeto do SharePoint, salve os dados no arquivo de projeto. Esse arquivo sempre é verificado nos bancos de dados de controle do código-fonte, portanto, os dados nesse arquivo estão disponíveis para outros desenvolvedores que confiram o projeto.

- Se você quiser que os dados estejam disponíveis somente para o desenvolvedor atual que tem o projeto do SharePoint aberto no Visual Studio, salve os dados no arquivo de opção de usuário do projeto. Normalmente, esse arquivo não é verificado nos bancos de dados de controle do código-fonte, portanto, os dados nesse arquivo não estão disponíveis para outros desenvolvedores que confiram o projeto.

### <a name="save-data-to-the-project-file"></a>Salvar dados no arquivo de projeto
 Para salvar dados no arquivo de projeto, converta um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> objeto em um <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> objeto e, em seguida, use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> método. O exemplo de código a seguir demonstra como usar esse método para salvar o valor de uma propriedade de projeto no arquivo de projeto. Para ver esse exemplo no contexto de um exemplo maior, consulte [como: adicionar uma propriedade aos projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md).

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb" id="Snippet3":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs" id="Snippet3":::

 Para obter mais informações sobre como converter <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> objetos em outros tipos no modelo de objeto de automação do Visual Studio ou no modelo de objeto de integração, consulte [converter entre tipos de sistema de projeto do SharePoint e outros tipos de projeto do Visual Studio](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md).

### <a name="save-data-to-the-project-user-option-file"></a>Salvar dados no arquivo de opção de usuário do projeto
 Para salvar dados no arquivo de opção de usuário do projeto, use a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> objeto. O exemplo de código a seguir demonstra como usar essa propriedade para salvar o valor de uma propriedade de projeto no arquivo de opção de usuário do projeto. Para ver esse exemplo no contexto de um exemplo maior, consulte [como: adicionar uma propriedade aos projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md).

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb" id="Snippet2":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs" id="Snippet2":::

## <a name="see-also"></a>Confira também
- [Estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md)
- [Associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [Converter entre os tipos do sistema de projeto do SharePoint e outros tipos de projeto do Visual Studio](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
