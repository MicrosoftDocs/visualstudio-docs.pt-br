---
title: Salvando dados em extensões do sistema de projeto do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
helpviewer_keywords:
- SharePoint project items, saving string data
- project items [SharePoint development in Visual Studio], saving string data
- projects [SharePoint development in Visual Studio], saving string data
- SharePoint projects, saving string data
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 74228b5259b733c91397eb1b40a2485daea8b79e
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118380"
---
# <a name="save-data-in-extensions-of-the-sharepoint-project-system"></a>Salvar os dados nas extensões do sistema de projeto do SharePoint
  Quando você estende o sistema de projeto do SharePoint, você pode salvar os dados de cadeia de caracteres que persiste depois que um projeto do SharePoint é fechado. Os dados são normalmente associados a um item de projeto específico ou com o projeto em si.  
  
 Se você tiver dados que não precisam manter, você pode adicionar dados a qualquer objeto no modelo de objeto de ferramentas do SharePoint que implementa o <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> interface. Para obter mais informações, consulte [extensões de ferramentas associado a dados personalizados com o SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md).  
  
## <a name="save-data-that-is-associated-with-a-project-item"></a>Salvar os dados que está associados um item de projeto
 Quando você tiver dados que está associados um item de projeto do SharePoint específico, como o valor de uma propriedade que você adicionar a um item de projeto, você pode salvar os dados para o *. spdata* arquivo para o item de projeto. Para fazer isso, use o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> objeto. Dados que você adicionar a essa propriedade é salvo na **ExtensionData** elemento o *. spdata* arquivo para o item de projeto. Para obter mais informações, consulte [elemento ExtensionData](../sharepoint/extensiondata-element.md).  
  
 O exemplo de código a seguir demonstra como usar o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> propriedade para salvar o valor de uma propriedade de cadeia de caracteres que é definido em um tipo de item de projeto personalizado do SharePoint. Para ver esse exemplo no contexto de um exemplo maior, consulte [como: adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md).  
  
 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#14](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb#14)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#14](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs#14)]  
  
## <a name="save-data-that-is-associated-with-a-project"></a>Salvar os dados que está associados um projeto
 Quando você tem dados de nível de projeto, como o valor de uma propriedade que você adicionar a projetos do SharePoint, você pode salvar os dados para o arquivo de projeto (o *. csproj* arquivo ou *. vbproj* arquivo) ou a opção de usuário do projeto arquivo (a *. csproj* arquivo ou *. vbproj* arquivo). O arquivo que você optar por salvar os dados em depende de como você deseja que os dados a ser usado:  
  
-   Se você deseja que os dados estejam disponíveis para todos os desenvolvedores que abrir o projeto do SharePoint, salve os dados para o arquivo de projeto. Este arquivo sempre é verificado bancos de dados de controle do código-fonte, para que os dados deste arquivo estão disponíveis para outros desenvolvedores que fazer check-out do projeto.  
  
-   Se você deseja que os dados estejam disponíveis apenas para o desenvolvedor atual que abriu o projeto do SharePoint no Visual Studio, salve os dados para o arquivo de opção de usuário do projeto. Esse arquivo não é normalmente verificado bancos de dados de controle do código-fonte, para que os dados neste arquivo não estão disponíveis para outros desenvolvedores que fazer check-out do projeto.  
  
### <a name="save-data-to-the-project-file"></a>Salvar dados no arquivo de projeto
 Para salvar dados no arquivo de projeto, converter um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> do objeto para um <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> do objeto e, em seguida, use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> método. O exemplo de código a seguir demonstra como usar esse método para salvar o valor de uma propriedade de projeto para o arquivo de projeto. Para ver esse exemplo no contexto de um exemplo maior, consulte [como: adicionar uma propriedade a projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md).  
  
 [!code-vb[SpExt_SPCustomPrjProperty#3](../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb#3)]
 [!code-csharp[SpExt_SPCustomPrjProperty#3](../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs#3)]  
  
 Para obter mais informações sobre como converter <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> objetos em outros tipos no modelo de objeto de automação do Visual Studio ou modelo de objeto de integração, consulte [converter entre tipos de sistema de projeto do SharePoint e outros tipos de projeto do Visual Studio](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md).  
  
### <a name="save-data-to-the-project-user-option-file"></a>Salvar os dados para o arquivo de opção de usuário do projeto
 Para salvar os dados para o arquivo de opção de usuário do projeto, use o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> objeto. O exemplo de código a seguir demonstra como usar essa propriedade para salvar o valor de uma propriedade de projeto para o arquivo de opção de usuário do projeto. Para ver esse exemplo no contexto de um exemplo maior, consulte [como: adicionar uma propriedade a projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md).  
  
 [!code-vb[SpExt_SPCustomPrjProperty#2](../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb#2)]
 [!code-csharp[SpExt_SPCustomPrjProperty#2](../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs#2)]  
  
## <a name="see-also"></a>Consulte também
 [Estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md)   
 [Associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)   
 [Converter entre tipos de sistema de projeto do SharePoint e outros tipos de projeto do Visual Studio](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)  
  
