---
title: 'Como: adicionar uma propriedade aos projetos do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eb72b0546b504e2df1a7e93ea9d4def350143d1d
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015918"
---
# <a name="how-to-add-a-property-to-sharepoint-projects"></a>Como: adicionar uma propriedade a projetos do SharePoint
  Você pode usar uma extensão de projeto para adicionar uma propriedade a qualquer projeto do SharePoint. A propriedade aparece na janela **Propriedades** quando o projeto é selecionado em **Gerenciador de soluções**.

 As etapas a seguir pressupõem que você já criou uma extensão de projeto. Para obter mais informações, consulte [como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md).

### <a name="to-add-a-property-to-a-sharepoint-project"></a>Para adicionar uma propriedade a um projeto do SharePoint

1. Defina uma classe com uma propriedade pública que represente a propriedade que você está adicionando aos projetos do SharePoint. Se você quiser adicionar várias propriedades, poderá definir todas as propriedades na mesma classe ou em classes diferentes.

2. No <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> método de sua <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> implementação, manipule o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> evento do parâmetro *ProjectService* .

3. No manipulador de eventos para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> evento, adicione uma instância da classe Properties à <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectPropertiesRequestedEventArgs.PropertySources%2A> coleção do parâmetro arguments do evento.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como adicionar duas propriedades a projetos do SharePoint. Uma propriedade persiste seus dados no arquivo de opção de usuário do projeto (o arquivo *. csproj. User* ou *. vbproj. User* ). A outra propriedade persiste seus dados no arquivo de projeto (arquivo *. csproj* ou arquivo *. vbproj* ).

 [!code-vb[SpExt_SPCustomPrjProperty#1](../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb#1)]
 [!code-csharp[SpExt_SPCustomPrjProperty#1](../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs#1)]

### <a name="understand-the-code"></a>Compreender o código
 Para garantir que a mesma instância da `CustomProjectProperties` classe seja usada cada vez que o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> evento ocorrer, o exemplo de código adiciona o objeto de propriedades à <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> Propriedade do projeto na primeira vez em que esse evento ocorrer. O código recupera esse objeto sempre que esse evento ocorrer novamente. Para obter mais informações sobre como usar a <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade para associar dados a projetos, consulte [associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md).

 Para manter as alterações nos valores de propriedade, os acessadores **definidos** das propriedades usam as seguintes APIs:

- `CustomUserFileProperty`usa a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> propriedade para salvar seu valor no arquivo de opção de usuário do projeto.

- `CustomProjectFileProperty`usa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> método para salvar seu valor no arquivo de projeto.

  Para obter mais informações sobre como manter os dados nesses arquivos, consulte [salvar dados em extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md).

### <a name="specify-the-behavior-of-custom-properties"></a>Especificar o comportamento das propriedades personalizadas
 Você pode definir como uma propriedade personalizada aparece e se comporta na janela **Propriedades** aplicando atributos do <xref:System.ComponentModel> namespace à definição de propriedade. Os seguintes atributos são úteis em muitos cenários:

- <xref:System.ComponentModel.DisplayNameAttribute>: Especifica o nome da propriedade que aparece na janela **Propriedades** .

- <xref:System.ComponentModel.DescriptionAttribute>: Especifica a cadeia de caracteres de descrição que aparece na parte inferior da janela **Propriedades** quando a propriedade é selecionada.

- <xref:System.ComponentModel.DefaultValueAttribute>: Especifica o valor padrão da propriedade.

- <xref:System.ComponentModel.TypeConverterAttribute>: Especifica uma conversão personalizada entre a cadeia de caracteres que é exibida na janela **Propriedades** e um valor de propriedade que não é de cadeia de caracteres.

- <xref:System.ComponentModel.EditorAttribute>: Especifica um editor personalizado a ser usado para modificar a propriedade.

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer referências aos seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- Microsoft. VisualStudio. Shell

- Microsoft. VisualStudio. Shell. Interop

- Microsoft. VisualStudio. Shell. Interop. 8.0

- System. ComponentModel. composição

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Estender projetos do SharePoint](../sharepoint/extending-sharepoint-projects.md)
- [Como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [Como: adicionar um item de menu de atalho a projetos do SharePoint](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [Estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md)
