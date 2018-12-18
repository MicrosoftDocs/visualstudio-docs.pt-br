---
title: 'Como: adicionar uma propriedade a uma extensão de Item de projeto do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 1af848f432183153707b2debfed563f3a00d4156
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36758093"
---
# <a name="how-to-add-a-property-to-a-sharepoint-project-item-extension"></a>Como: adicionar uma propriedade a uma extensão de item de projeto do SharePoint
  Você pode usar uma extensão de item de projeto para adicionar uma propriedade para qualquer item de projeto do SharePoint que já está instalado no Visual Studio. A propriedade aparece na **propriedades** janela quando o item de projeto é selecionado na **Gerenciador de soluções**.  
  
 As etapas a seguir pressupõem que você já tenha criado uma extensão de item de projeto. Para obter mais informações, consulte [como: criar uma extensão de Item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md).  
  
### <a name="to-add-a-property-to-a-project-item-extension"></a>Para adicionar uma propriedade a uma extensão de item de projeto  
  
1.  Defina uma classe com uma propriedade pública que representa a propriedade que você está adicionando a um tipo de item de projeto. Se você quiser adicionar várias propriedades para um tipo de item de projeto, você pode definir todas as propriedades na mesma classe ou em classes diferentes.  
  
2.  No <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> método de seu <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> implementação, o identificador a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> evento do *projectItemType* parâmetro.  
  
3.  No manipulador de eventos para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> evento, adicione uma instância de sua classe de propriedades para o <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A> coleção do parâmetro de argumentos de evento.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como adicionar uma propriedade chamada **exemplo de propriedade** para o item de projeto do receptor de eventos.  
  
 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#8](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionproperty.cs#8)]
 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#8](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionproperty.vb#8)]  
  
### <a name="understand-the-code"></a>Entender o código  
 Para garantir que a mesma instância das `CustomProperties` classe é usada sempre que o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> evento ocorrer, o exemplo de código adiciona o objeto de propriedades para o <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade do tempo de item, o primeiro projeto, esse evento ocorre. O código recupera esse objeto sempre que esse evento ocorre novamente. Para obter mais informações sobre como usar o <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade para associar dados a itens de projeto, consulte [extensões de ferramentas associado a dados personalizados com o SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md).  
  
 Para manter as alterações feitas ao valor da propriedade, o **definir** acessador para `ExampleProperty` salva o novo valor para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> propriedade do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> objeto que a propriedade está associada. Para obter mais informações sobre como usar o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> propriedade para manter os dados com itens de projeto, consulte [salvar os dados nas extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md).  
  
### <a name="specify-the-behavior-of-custom-properties"></a>Especificar o comportamento de propriedades personalizadas  
 Você pode definir como uma propriedade personalizada é exibida e comporta-se a **propriedades** janela aplicando atributos do <xref:System.ComponentModel> namespace à definição da propriedade. Os seguintes atributos são úteis em muitos cenários:  
  
-   <xref:System.ComponentModel.DisplayNameAttribute>: Especifica o nome da propriedade que aparece na **propriedades** janela.  
  
-   <xref:System.ComponentModel.DescriptionAttribute>: Especifica a cadeia de caracteres de descrição que aparece na parte inferior da **propriedades** janela quando a propriedade for selecionada.  
  
-   <xref:System.ComponentModel.DefaultValueAttribute>: Especifica o valor padrão da propriedade.  
  
-   <xref:System.ComponentModel.TypeConverterAttribute>: Especifica uma conversão personalizada entre a cadeia de caracteres que é exibida na **propriedades** janela e um valor da propriedade não cadeia de caracteres.  
  
-   <xref:System.ComponentModel.EditorAttribute>: Especifica um editor personalizado para usar para modificar a propriedade.  
  
## <a name="compile-the-code"></a>Compilar o código  
 Esses exemplos requerem um projeto de biblioteca de classes com as referências aos assemblies a seguir:  
  
-   Microsoft.VisualStudio.SharePoint  
  
-   System.ComponentModel.Composition  
  
## <a name="deploy-the-extension"></a>Implantar a extensão  
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de extensão (VSIX) para o assembly e outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também
 [Como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)   
 [Como: adicionar um item de menu de atalho para uma extensão de item de projeto do SharePoint](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)   
 [Estender os itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md)   
 [Passo a passo: Estender um tipo de item de projeto do SharePoint](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)  
  
  
