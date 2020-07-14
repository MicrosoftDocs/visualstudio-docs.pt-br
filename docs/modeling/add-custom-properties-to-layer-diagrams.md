---
title: Adicionar propriedades personalizadas a diagramas de dependência
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- dependency diagrams, adding custom properties
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3c68d8a75ca8203a790684506ffd44b3d890648a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546907"
---
# <a name="add-custom-properties-to-dependency-diagrams"></a>Adicionar propriedades personalizadas a diagramas de dependência

Ao escrever o código de extensão para diagramas de dependência, você pode armazenar valores com qualquer elemento em um diagrama de dependência. Os valores serão persistidos quando o diagrama for salvo e aberto novamente. Você também pode ter essas propriedades exibidas na janela **Propriedades** para que os usuários possam vê-las e editá-las. Por exemplo, você pode permitir que os usuários especifiquem uma expressão regular para cada camada e escrevam o código de validação para verificar se os nomes das classes em cada camada estão em conformidade com o padrão especificado pelo usuário.

## <a name="non-visible-properties"></a>Propriedades não visíveis

Se você quiser apenas que seu código anexe valores a qualquer elemento em um diagrama de dependência, não precisará definir um componente MEF. Há um dicionário chamado `Properties` em [ILayerElement](/previous-versions/ff644511(v=vs.140)). Basta adicionar valores de marshaling ao dicionário de qualquer elemento de camada. Eles serão salvos como parte do diagrama de dependência.

## <a name="editable-properties"></a>Propriedades editáveis

**Preparação inicial**

> [!IMPORTANT]
> Para exibir as propriedades, faça a seguinte alteração em cada computador em que você deseja que as propriedades da camada fiquem visíveis:
>
> 1. Execute o bloco de notas usando **Executar como administrador**. Abra *%ProgramFiles%\Microsoft Visual Studio [Version] \Common7\IDE\Extensions\Microsoft\Architecture Tools\ExtensibilityRuntime\extension.vsixmanifest*.
> 2. Dentro do elemento **Content** , adicione:
>
>     ```xml
>     <MefComponent>Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.Provider.dll</MefComponent>
>     ```
>
> 3. Na seção **Ferramentas do Visual Studio** do menu Iniciar do aplicativo do Visual Studio, abra **prompt de comando do desenvolvedor**. Insira:
>
>      `devenv /rootSuffix /updateConfiguration`
>
>      `devenv /rootSuffix Exp /updateConfiguration`
> 4. Reinicie o Visual Studio.

**Verifique se o código está em um projeto VSIX**

Se sua propriedade fizer parte de um comando, um gesto ou um projeto de validação, você não precisará adicionar nada. O código para sua propriedade personalizada deve ser definido em um projeto de extensibilidade do Visual Studio definido como um componente MEF. Para obter mais informações, consulte [adicionar comandos e gestos a diagramas de dependência](../modeling/add-commands-and-gestures-to-layer-diagrams.md) ou [Adicionar validação de arquitetura personalizada a diagramas de dependência](../modeling/add-custom-architecture-validation-to-layer-diagrams.md).

**Definir a propriedade personalizada**

Para criar uma propriedade personalizada, defina uma classe como esta:

```csharp
[Export(typeof(IPropertyExtension))]
public class MyProperty : PropertyExtension<ILayerElement>
{
  // Implement the interface.
}
```

Você pode definir propriedades em [ILayerElement](/previous-versions/ff644511(v=vs.140)) ou em qualquer uma de suas classes derivadas, que incluem:

- `ILayerModel`-o modelo

- `ILayer`-cada camada

- `ILayerDependencyLink`-os links entre camadas

- `ILayerComment`

- `ILayerCommentLink`

## <a name="example"></a>Exemplo

O código a seguir é um descritor de propriedade personalizada típico. Ele define uma propriedade booliana no modelo de camada ( `ILayerModel` ) que permite que o usuário forneça valores para um método de validação personalizado.

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

## <a name="see-also"></a>Confira também

- [Estender diagramas de dependência](../modeling/extend-layer-diagrams.md)
