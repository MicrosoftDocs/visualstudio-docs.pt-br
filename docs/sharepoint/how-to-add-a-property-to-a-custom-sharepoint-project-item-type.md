---
title: Adicionar Propriedade ao tipo de item de projeto personalizado do SharePoint
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 54765b9b6b82214a7deccaee4f9ee671a72dd40d
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015997"
---
# <a name="how-to-add-a-property-to-a-custom-sharepoint-project-item-type"></a>Como: adicionar uma propriedade a um tipo de item de projeto personalizado do SharePoint
  Ao definir um tipo de item de projeto personalizado do SharePoint, você pode adicionar uma propriedade ao item de projeto. A propriedade aparece na janela **Propriedades** quando o item de projeto é selecionado em **Gerenciador de soluções**.

 As etapas a seguir pressupõem que você já definiu seu próprio tipo de item de projeto do SharePoint. Para obter mais informações, consulte [como: definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md).

### <a name="to-add-a-property-to-a-definition-of-a-project-item-type"></a>Para adicionar uma propriedade a uma definição de um tipo de item de projeto

1. Defina uma classe com uma propriedade pública que represente a propriedade que você está adicionando ao tipo de item de projeto personalizado. Se você quiser adicionar várias propriedades a um tipo de item de projeto personalizado, poderá definir todas as propriedades na mesma classe ou em classes diferentes.

2. No <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> método de sua <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> implementação, manipule o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> evento do parâmetro *projectItemTypeDefinition* .

3. No manipulador de eventos para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> evento, adicione uma instância de sua classe de propriedades personalizadas à <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A> coleção do parâmetro de argumentos de evento.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como adicionar uma propriedade denominada de propriedade de **exemplo** a um tipo de item de projeto personalizado.

 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#11](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb#11)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#11](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs#11)]

### <a name="understand-the-code"></a>Compreender o código
 Para garantir que a mesma instância da `CustomProperties` classe seja usada cada vez que o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> evento ocorrer, o exemplo de código salva o objeto de propriedades na <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> Propriedade do item do projeto na primeira vez em que esse evento ocorre. O código recupera esse objeto sempre que esse evento ocorrer novamente. Para obter mais informações sobre como usar a <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade para salvar dados com itens de projeto, consulte [associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md).

 Para manter as alterações no valor da propriedade, o acessador **set** para `ExampleProperty` salva o novo valor na <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> Propriedade do <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> objeto ao qual a propriedade está associada. Para obter mais informações sobre como usar a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> propriedade para manter dados com itens de projeto, consulte [salvar dados em extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md).

### <a name="specify-the-behavior-of-custom-properties"></a>Especificar o comportamento das propriedades personalizadas
 Você pode definir como uma propriedade personalizada aparece e se comporta na janela **Propriedades** aplicando atributos do <xref:System.ComponentModel> namespace à definição de propriedade. Os seguintes atributos são úteis em muitos cenários:

- <xref:System.ComponentModel.DisplayNameAttribute>: Especifica o nome da propriedade que aparece na janela **Propriedades** .

- <xref:System.ComponentModel.DescriptionAttribute>: Especifica a cadeia de caracteres de descrição que aparece na parte inferior da janela **Propriedades** quando a propriedade é selecionada.

- <xref:System.ComponentModel.DefaultValueAttribute>: Especifica o valor padrão da propriedade.

- <xref:System.ComponentModel.TypeConverterAttribute>: Especifica uma conversão personalizada entre a cadeia de caracteres que é exibida na janela **Propriedades** e um valor de propriedade que não é de cadeia de caracteres.

- <xref:System.ComponentModel.EditorAttribute>: Especifica um editor personalizado a ser usado para modificar a propriedade.

## <a name="compile-the-code"></a>Compilar o código
 Esses exemplos de código exigem um projeto de biblioteca de classes com referências para os seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

## <a name="deploy-the-project-item"></a>Implantar o item de projeto
 Para permitir que outros desenvolvedores usem seu item de projeto, crie um modelo de projeto ou um modelo de item de projeto. Para obter mais informações, consulte [criar modelos de item e modelos de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md).

 Para implantar o item de projeto, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly, o modelo e outros arquivos que você deseja distribuir com o item de projeto. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Como definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [Como: adicionar um item de menu de atalho a um tipo personalizado de item de projeto do SharePoint](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [Definindo tipos de item de projeto personalizados do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)
