---
title: 'Como: adicionar uma propriedade a projetos do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c956da1df5507d2efecb3ff72f034d54fb377eb5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49898402"
---
# <a name="how-to-add-a-property-to-sharepoint-projects"></a>Como: adicionar uma propriedade a projetos do SharePoint
  Você pode usar uma extensão de projeto para adicionar uma propriedade para qualquer projeto do SharePoint. A propriedade aparece na **propriedades** janela quando o projeto está selecionado no **Gerenciador de soluções**.  
  
 As etapas a seguir pressupõem que você já tenha criado uma extensão de projeto. Para obter mais informações, consulte [como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md).  
  
### <a name="to-add-a-property-to-a-sharepoint-project"></a>Para adicionar uma propriedade para um projeto do SharePoint  
  
1.  Defina uma classe com uma propriedade pública que representa a propriedade que você está adicionando a projetos do SharePoint. Se você quiser adicionar várias propriedades, você pode definir todas as propriedades na mesma classe ou em classes diferentes.  
  
2.  No <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> método de seu <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> implementação, o identificador a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> evento do *projectService* parâmetro.  
  
3.  No manipulador de eventos para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> evento, adicione uma instância de sua classe de propriedades para o <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectPropertiesRequestedEventArgs.PropertySources%2A> coleção do parâmetro de argumentos de evento.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como adicionar duas propriedades a projetos do SharePoint. Uma propriedade persiste seus dados no arquivo de opção de usuário do projeto (o *. csproj* arquivo ou *. vbproj* arquivo). A outra propriedade persiste seus dados no arquivo de projeto (*. csproj* arquivo ou *. vbproj* arquivo).  
  
 [!code-vb[SpExt_SPCustomPrjProperty#1](../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb#1)]
 [!code-csharp[SpExt_SPCustomPrjProperty#1](../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs#1)]  
  
### <a name="understand-the-code"></a>Entender o código  
 Para garantir que a mesma instância das `CustomProjectProperties` classe é usada sempre que o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> evento ocorrer, o exemplo de código adiciona o objeto de propriedades para o <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade do tempo de projeto primeiro esse evento ocorre. O código recupera esse objeto sempre que esse evento ocorre novamente. Para obter mais informações sobre como usar o <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> propriedade para associar dados de projetos, consulte [extensões de ferramentas associado a dados personalizados com o SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md).  
  
 Para manter as alterações feitas aos valores de propriedade, o **definir** acessadores para as propriedades de usam as seguintes APIs:  
  
- `CustomUserFileProperty` usa o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> propriedade para salvar seu valor para o arquivo de opção de usuário do projeto.  
  
- `CustomProjectFileProperty` usa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> método para salvar seu valor para o arquivo de projeto.  
  
  Para obter mais informações sobre como manter os dados nesses arquivos, consulte [salvar os dados nas extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md).  
  
### <a name="specify-the-behavior-of-custom-properties"></a>Especificar o comportamento de propriedades personalizadas  
 Você pode definir como uma propriedade personalizada é exibida e comporta-se a **propriedades** janela aplicando atributos do <xref:System.ComponentModel> namespace à definição da propriedade. Os seguintes atributos são úteis em muitos cenários:  
  
-   <xref:System.ComponentModel.DisplayNameAttribute>: Especifica o nome da propriedade que aparece na **propriedades** janela.  
  
-   <xref:System.ComponentModel.DescriptionAttribute>: Especifica a cadeia de caracteres de descrição que aparece na parte inferior da **propriedades** janela quando a propriedade for selecionada.  
  
-   <xref:System.ComponentModel.DefaultValueAttribute>: Especifica o valor padrão da propriedade.  
  
-   <xref:System.ComponentModel.TypeConverterAttribute>: Especifica uma conversão personalizada entre a cadeia de caracteres que é exibida na **propriedades** janela e um valor da propriedade não cadeia de caracteres.  
  
-   <xref:System.ComponentModel.EditorAttribute>: Especifica um editor personalizado para usar para modificar a propriedade.  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer referências aos assemblies a seguir:  
  
-   Microsoft.VisualStudio.SharePoint
-    
-   Microsoft.VisualStudio.Shell
-     
-   Microsoft.VisualStudio.Shell.Interop
-     
-   Microsoft.VisualStudio.Shell.Interop.8.0
-     
-   System.ComponentModel.Composition  
  
## <a name="deploy-the-extension"></a>Implantar a extensão  
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de extensão (VSIX) para o assembly e outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também
 [Estender projetos do SharePoint](../sharepoint/extending-sharepoint-projects.md)   
 [Como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md)   
 [Como: adicionar um item de menu de atalho a projetos do SharePoint](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)   
 [Estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md)  
  
  
