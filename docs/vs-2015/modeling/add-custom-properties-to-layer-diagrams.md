---
title: Adicionar propriedades personalizadas a diagramas de camada | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- layer diagrams, adding custom properties
ms.assetid: 52b3ac25-d10b-4507-a1fe-209ccb4d2777
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 9024ccda38e6b261b29d808e6fafb7837776fc8c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51789272"
---
# <a name="add-custom-properties-to-layer-diagrams"></a>Adicionar propriedades personalizadas a diagramas de camada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você escreve o código de extensão para diagramas de camada, você pode armazenar valores com qualquer elemento em um diagrama de camada. Os valores persistirão quando o diagrama é salvo e reaberto. Você também pode ter essas propriedades aparecem na **propriedades** janela para que os usuários podem ver e editá-los. Por exemplo, você pode permitir que usuários especificar uma expressão regular para cada camada e escrever código de validação para verificar se os nomes das classes em cada camada estão em conformidade com o padrão especificado pelo usuário.  
  
## <a name="properties-not-visible-to-the-user"></a>Propriedades não é visíveis para o usuário  
 Se você quiser apenas seu código anexe valores a qualquer elemento em um diagrama de camada, você não precisa definir um componente MEF. Não há um dicionário, chamado `Properties` em <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.ILayerElement>. Adicione valores de marshaling ao dicionário de qualquer elemento de camada. Eles serão salvos como parte do diagrama de camada. Para obter mais informações, consulte [navegar e atualizar modelos no código do programa de camada](../modeling/navigate-and-update-layer-models-in-program-code.md).  
  
## <a name="properties-that-the-user-can-edit"></a>Propriedades que o usuário pode editar  
 **Preparação inicial**  
  
> [!IMPORTANT]
>  Para fazer com que as propriedades aparecerem, você deve fazer a seguinte alteração em cada computador onde você deseja que as propriedades da camada fiquem visíveis.  
> 
> 1. Execute o bloco de notas usando **executar como administrador**. Abrir `%ProgramFiles%\Microsoft Visual Studio [version]\Common7\IDE\Extensions\Microsoft\Architecture Tools\ExtensibilityRuntime\extension.vsixmanifest`  
>    2.  Dentro de `Content` elemento, adicione:  
> 
>    ```xml  
>    <MefComponent>Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.Provider.dll</MefComponent>  
>    ```  
>    3.  Sob o **ferramentas do Visual Studio** seção do Visual Studio aplicativo menu Iniciar, abra **Prompt de comando do desenvolvedor**.  
> 
>    Digite:  
> 
>    `devenv /rootSuffix /updateConfiguration`  
> 
>    `devenv /rootSuffix Exp /updateConfiguration`  
>    4.  Reinicie o Visual Studio.  
  
 **Verifique se que seu código está em um projeto VSIX**  
  
 Se a propriedade for parte de um comando, gesto ou projeto de validação, você não precisará adicionar nada. O código para a propriedade personalizada deve ser definido em um projeto de extensibilidade do Visual Studio definido como um componente de MEF. Para obter mais informações, consulte [adicionar comandos e gestos a diagramas de camada](../modeling/add-commands-and-gestures-to-layer-diagrams.md) ou [adicionar validação de arquitetura personalizada a diagramas de camada](../modeling/add-custom-architecture-validation-to-layer-diagrams.md).  
  
 **Defina a propriedade personalizada**  
  
 Para criar uma propriedade personalizada, defina uma classe como esta:  
  
```  
[Export(typeof(IPropertyExtension))]  
public class MyProperty   
      : PropertyExtension<ILayerElement>  
{  
  // Implement the interface.  
}  
```  
  
 Você pode definir propriedades em <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.ILayerElement> ou qualquer uma de suas classes derivadas, que incluem:  
  
-   `ILayerModel` -o modelo  
  
-   `ILayer` -cada camada  
  
-   `ILayerDependencyLink` -os links entre camadas  
  
-   `ILayerComment`  
  
-   `ILayerCommentLink`  
  
## <a name="example"></a>Exemplo  
 O código a seguir é um descritor de propriedade personalizado típico. Ele define uma propriedade booleana no modelo de camada (`ILayerModel`) que permite ao usuário fornecer valores para um método de validação personalizada.  
  
```  
using System;  
using System.ComponentModel.Composition;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;  
  
namespace MyNamespace  
{  
  /// <summary>  
  /// Custom properties are added to the Layer Designer via a custom  
  /// Property Descriptor. We have to export this Property Descriptor  
  /// using MEF to make it available in the Layer Designer.  
  /// </summary>  
  [Export(typeof(IPropertyExtension))]  
  public class AllTypesMustBeReferencedProperty   
      : PropertyExtension<ILayerModel>  
  {  
    /// <summary>  
    /// Each custom property must have a unique name.   
    /// Usually we use the full name of this class.  
    /// </summary>  
    public static readonly string FullName =  
      typeof(AllTypesMustBeReferencedProperty).FullName;  
  
    /// <summary>  
    /// Construct the property. Notice the use of FullName.  
    /// </summary>  
    public AllTypesMustBeReferencedProperty()  
            : base(FullName)  
    {  }  
  
    /// <summary>  
    /// The display name is shown in the Properties window.  
    /// We therefore use a localizable resource.  
    /// </summary>  
    public override string DisplayName  
    {  
      get { return Strings.AllTypesMustBeReferencedDisplayName; }  
    }  
  
    /// <summary>  
    /// Description shown at the bottom of the Properties window.  
    /// We use a resource string for easier localization.  
    /// </summary>  
    public override string Description  
    {  
      get { return Strings.AllTypesMustBeReferencedDescription; }  
    }  
  
    /// <summary>  
    /// This is called to set a new value for this property. We must  
    /// throw an exception if the value is invalid.  
    /// </summary>  
    /// <param name="component">The target ILayerElement</param>  
    /// <param name="value">The new value</param>  
    public override void SetValue(object component, object value)  
    {  
      ValidateValue(value);  
      base.SetValue(component, value);  
    }  
    /// <summary>  
    /// Helper to validate the value.  
    /// </summary>  
    /// <param name="value">The value to validate</param>  
    private static void ValidateValue(object value)  
    {  }  
  
    public override Type PropertyType  
    { get { return typeof(bool); } }  
  
    /// <summary>  
    /// The segment label of the properties window.  
    /// </summary>  
    public override string Category  
    {   
      get  
      {  
        return Strings.AllTypesMustBeReferencedCategory;  
      }  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Estender diagramas de camada](../modeling/extend-layer-diagrams.md)



