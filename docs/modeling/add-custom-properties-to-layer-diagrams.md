---
title: Adicionar propriedades personalizadas a diagramas de dependência
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams, adding custom properties
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 368d1a794f51d827aa62cc913039edda59ae7ae6
ms.sourcegitcommit: 33c954fbc8e05f7ba54bfa2c0d1bc1f9bbc68876
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33864184"
---
# <a name="add-custom-properties-to-dependency-diagrams"></a>Adicionar propriedades personalizadas a diagramas de dependência

Quando você escreve o código de extensão para diagramas de dependência, você pode armazenar valores com qualquer elemento em um diagrama de dependência. Os valores serão mantidas quando o diagrama é salvo e aberto novamente. Você também pode ter essas propriedades aparecem no **propriedades** janela para que os usuários podem ver e editá-los. Por exemplo, você pode permitir que os usuários especificar uma expressão regular para cada camada e escrever código de validação para verificar se os nomes das classes em cada camada está de acordo com o padrão especificado pelo usuário.

## <a name="non-visible-properties"></a>Propriedades não visíveis

Se você quiser apenas seu código para anexar os valores para qualquer elemento em um diagrama de dependência, você não precisa definir um componente MEF. Não há um dicionário, chamado `Properties` em <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.ILayerElement>. Basta adicione valores é possível realizar marshaling para o dicionário de qualquer elemento de camada. Elas serão salvas como parte do diagrama de dependência. Para obter mais informações, consulte [navegar e atualizar modelos no código do programa de camada](../modeling/navigate-and-update-layer-models-in-program-code.md).

## <a name="editable-properties"></a>Propriedades editáveis

**Preparação inicial**

> [!IMPORTANT]
> Para exibir propriedades, faça a seguinte alteração em cada computador onde você deseja que as propriedades da camada devem ficar visíveis:
>
> 1. Execute o bloco de notas usando **executar como administrador**. Abra *%ProgramFiles%\Microsoft Visual Studio [version] \Common7\IDE\Extensions\Microsoft\Architecture Tools\ExtensibilityRuntime\extension.vsixmanifest*.
> 2. Dentro de **conteúdo** elemento, adicionar:
>
>     ```xml
>     <MefComponent>Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.Provider.dll</MefComponent>
>     ```
> 3. Sob o **ferramentas do Visual Studio** seção do Visual Studio aplicativo menu Iniciar, abra **Prompt de comando do desenvolvedor**. Digite:
>
>      `devenv /rootSuffix /updateConfiguration`
>
>      `devenv /rootSuffix Exp /updateConfiguration`
> 4. Reinicie o Visual Studio.

**Verifique se que seu código está em um projeto do VSIX**

Se a propriedade for parte de um projeto de validação, um gesto ou um comando, você não precisa adicionar qualquer coisa. O código para a propriedade personalizada deve ser definido em um projeto de extensibilidade do Visual Studio definido como um componente MEF. Para obter mais informações, consulte [adicionar comandos e gestos a diagramas de dependência](../modeling/add-commands-and-gestures-to-layer-diagrams.md) ou [adicionar validação de arquitetura personalizada a diagramas de dependência](../modeling/add-custom-architecture-validation-to-layer-diagrams.md).

**Definir a propriedade personalizada**

Para criar uma propriedade personalizada, defina uma classe como este:

```csharp
[Export(typeof(IPropertyExtension))]
public class MyProperty : PropertyExtension<ILayerElement>
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

O código a seguir é um descritor de propriedade personalizada típico. Define uma propriedade booleana no modelo de camada (`ILayerModel`) que permite que o usuário forneça valores para um método de validação personalizada.

```csharp
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

- [Estender diagramas de dependência](../modeling/extend-layer-diagrams.md)
