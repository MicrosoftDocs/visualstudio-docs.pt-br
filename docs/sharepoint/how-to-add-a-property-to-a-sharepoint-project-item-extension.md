---
title: 'Como: adicionar uma propriedade a uma extensão de item de projeto do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 337536d2219ce8494f96769bc79f10967883e61a
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015981"
---
# <a name="how-to-add-a-property-to-a-sharepoint-project-item-extension"></a>Como: adicionar uma propriedade a uma extensão de item de projeto do SharePoint
  Você pode usar uma extensão de item de projeto para adicionar uma propriedade a qualquer item de projeto do SharePoint que já esteja instalado no Visual Studio. A propriedade aparece na janela **Propriedades** quando o item de projeto é selecionado em **Gerenciador de soluções**.

 As etapas a seguir pressupõem que você já criou uma extensão de item de projeto. Para obter mais informações, consulte [como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md).

### <a name="to-add-a-property-to-a-project-item-extension"></a>Para adicionar uma propriedade a uma extensão de item de projeto

1. Defina uma classe com uma propriedade pública que represente a propriedade que você está adicionando a um tipo de item de projeto. Se você quiser adicionar várias propriedades a um tipo de item de projeto, poderá definir todas as propriedades na mesma classe ou em classes diferentes.

2. No <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> método de sua <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> implementação, manipule o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> evento do parâmetro *projectItemType* .

3. No manipulador de eventos para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> evento, adicione uma instância da classe Properties à <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A> coleção do parâmetro arguments do evento.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como adicionar uma propriedade chamada de propriedade de **exemplo** ao item de projeto receptor de evento.

 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#8](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionproperty.cs#8)]
 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#8](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionproperty.vb#8)]

### <a name="understand-the-code"></a>Compreender o código
 Para garantir que a mesma instância da `CustomProperties` classe seja usada cada vez que o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> evento ocorrer, o exemplo de código adiciona o objeto de propriedades à <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> Propriedade do item do projeto na primeira vez em que esse evento ocorrer. O código recupera esse objeto sempre que esse evento ocorrer novamente. Para obter mais informações sobre como usar a <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade para associar dados a itens de projeto, consulte [associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md).

 Para manter as alterações no valor da propriedade, o acessador **set** para `ExampleProperty` salva o novo valor na <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> Propriedade do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> objeto ao qual a propriedade está associada. Para obter mais informações sobre como usar a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> propriedade para manter dados com itens de projeto, consulte [salvar dados em extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md).

### <a name="specify-the-behavior-of-custom-properties"></a>Especificar o comportamento das propriedades personalizadas
 Você pode definir como uma propriedade personalizada aparece e se comporta na janela **Propriedades** aplicando atributos do <xref:System.ComponentModel> namespace à definição de propriedade. Os seguintes atributos são úteis em muitos cenários:

- <xref:System.ComponentModel.DisplayNameAttribute>: Especifica o nome da propriedade que aparece na janela **Propriedades** .

- <xref:System.ComponentModel.DescriptionAttribute>: Especifica a cadeia de caracteres de descrição que aparece na parte inferior da janela **Propriedades** quando a propriedade é selecionada.

- <xref:System.ComponentModel.DefaultValueAttribute>: Especifica o valor padrão da propriedade.

- <xref:System.ComponentModel.TypeConverterAttribute>: Especifica uma conversão personalizada entre a cadeia de caracteres que é exibida na janela **Propriedades** e um valor de propriedade que não é de cadeia de caracteres.

- <xref:System.ComponentModel.EditorAttribute>: Especifica um editor personalizado a ser usado para modificar a propriedade.

## <a name="compile-the-code"></a>Compilar o código
 Estes exemplos exigem um projeto de biblioteca de classes com referências para os seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [Como: adicionar um item de menu de atalho a uma extensão de item de projeto do SharePoint](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)
- [Estender itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md)
- [Walkthrough: estender um tipo de item de projeto do SharePoint](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
