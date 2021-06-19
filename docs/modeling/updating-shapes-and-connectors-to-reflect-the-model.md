---
title: Atualizando formas e conectores para refletir o modelo
description: Saiba que, em um idioma específico do domínio Visual Studio, você pode fazer com que a aparência de uma forma reflita o estado do modelo subjacente.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6439a01de2a02361914ce227c43d903f1b24b405
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388562"
---
# <a name="update-shapes-and-connectors-to-reflect-the-model"></a>Atualizar formas e conectores para refletir o modelo

Em um idioma específico do domínio Visual Studio, você pode fazer com que a aparência de uma forma reflita o estado do modelo subjacente.

Os exemplos de código neste tópico devem ser adicionados a um `.cs` arquivo em seu `Dsl` projeto. Você precisa dessas diretivas em cada arquivo:

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
```

## <a name="set-shape-map-properties-to-control-the-visibility-of-a-decorator"></a>Definir propriedades do Mapa de Formas para controlar a visibilidade de um decorador

Você pode controlar a visibilidade de um decorador sem escrever o código do programa configurando o mapeamento entre a forma e a classe de domínio na Definição de DSL. Para obter mais informações, [consulte How to Define a Domain-Specific Language](../modeling/how-to-define-a-domain-specific-language.md).

## <a name="expose-the-color-and-style-of-a-shape-as-properties"></a>Expor a cor e o estilo de uma forma como propriedades

Na Definição de DSL, clique com o botão direito do mouse na classe de forma, aponte para Adicionar Exposto e clique em um dos itens, como **Cor de Preenchimento.**

A forma agora tem uma propriedade de domínio que você pode definir no código do programa ou como um usuário. Por exemplo, para defini-lo no código do programa de um comando ou regra, você pode escrever:

`shape.FillColor = System.Drawing.Color.Red;`

Se você quiser tornar a variável de propriedade somente sob o controle de  programa e não pelo usuário, selecione a nova propriedade de domínio, como Cor de Preenchimento no diagrama de Definição de DSL. Em seguida, no janela Propriedades, de conjunto **É Navegar** como ou definir `false` Is **UI Readonly** como `true` .

## <a name="define-change-rules-to-make-color-style-or-location-depend-on-model-element-properties"></a>Definir Regras de Alteração para fazer com que a cor, o estilo ou o local dependam das propriedades do elemento de modelo
 Você pode definir regras que atualizem a aparência da forma dependente de outras partes do modelo. Por exemplo, você pode definir uma Regra de Alteração em um elemento de modelo que atualiza a cor de sua forma dependendo das propriedades do elemento de modelo. Para obter mais informações sobre regras de alteração, consulte [Regras propagam alterações dentro do modelo](../modeling/rules-propagate-changes-within-the-model.md).

 Você deve usar regras somente para atualizar as propriedades mantidas no Store, porque as regras não são invocadas quando o comando Desfazer é executado. Isso não inclui alguns recursos gráficos, como o tamanho e a visibilidade de uma forma. Para atualizar esses recursos de uma forma, consulte [Atualizando recursos gráficos que não são da loja.](#OnAssociatedProperty)

 O exemplo a seguir presume que você tenha exposto `FillColor` como uma propriedade de domínio, conforme descrito na seção anterior.

```csharp
[RuleOn(typeof(ExampleElement))]
  class ExampleElementPropertyRule : ChangeRule
  {
    public override void ElementPropertyChanged(ElementPropertyChangedEventArgs e)
    {
      base.ElementPropertyChanged(e);
      ExampleElement element = e.ModelElement as ExampleElement;
      // The rule is called for every property that is updated.
      // Therefore, verify which property changed:
      if (e.DomainProperty.Id == ExampleElement.NameDomainPropertyId)
      {
        // There is usually only one shape:
        foreach (PresentationElement pel in PresentationViewsSubject.GetPresentation(element))
        {
          ExampleShape shape = pel as ExampleShape;
          // Replace this with a useful condition:
          shape.FillColor = element.Name.EndsWith("3")
                     ? System.Drawing.Color.Red : System.Drawing.Color.Green;
        }
      }
    }
  }
  // The rule must be registered:
  public partial class OnAssociatedPropertyExptDomainModel
  {
    protected override Type[] GetCustomDomainModelTypes()
    {
      List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
      types.Add(typeof(ExampleElementPropertyRule));
      // If you add more rules, list them here.
      return types.ToArray();
    }
  }
```

## <a name="use-onchildconfigured-to-initialize-a-shapes-properties"></a>Usar OnChildConfigured para inicializar as propriedades de uma forma

Para definir as propriedades de uma forma quando ela é criada pela primeira vez, a substituição `OnChildConfigured()` em uma definição parcial da classe de diagrama. A classe de diagrama é especificada em sua Definição de DSL e o código gerado está em **Dsl\Generated Code\Diagram.cs**. Por exemplo:

```csharp
partial class MyLanguageDiagram
{
  protected override void OnChildConfigured(ShapeElement child, bool childWasPlaced, bool createdDuringViewFixup)
  {
    base.OnChildConfigured(child, childWasPlaced, createdDuringViewFixup);
    ExampleShape shape = child as ExampleShape;
    if (shape != null)
    {
      if (!createdDuringViewFixup) return; // Ignore load from file.
      ExampleElement element = shape.ModelElement as ExampleElement;
      // Replace with a useful condition:
      shape.FillColor = element.Name.EndsWith("3")
          ? System.Drawing.Color.Red : System.Drawing.Color.Green;
    }
    // else deal with other types of shapes and connectors.
  }
}
```

Esse método pode ser usado para propriedades de domínio e recursos que não são de armazenamento, como o tamanho da forma.

## <a name="use-associatevaluewith-to-update-other-features-of-a-shape"></a><a name="OnAssociatedProperty"></a> Usar AssociateValueWith() para atualizar outros recursos de uma forma

Para alguns recursos de uma forma, como se ela tem uma sombra ou o estilo de seta de um conector, não há nenhum método integrado de expor o recurso como uma propriedade de domínio.  As alterações nesses recursos não estão sob o controle do sistema de transações. Portanto, não é apropriado atualizá-las usando regras, pois as regras não são invocadas quando o usuário executa o comando Desfazer.

Em vez disso, você pode atualizar esses recursos usando <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnAssociatedPropertyChanged%2A> . No exemplo a seguir, o estilo de seta de um conector é controlado por um valor de uma propriedade de domínio na relação que o conector exibe:

```csharp
public partial class ArrowConnector // My connector class.
{
    /// <summary>
    /// Called whenever a registered property changes in the associated model element.
    /// </summary>
    /// <param name="e"></param>
    protected override void OnAssociatedPropertyChanged(VisualStudio.Modeling.Diagrams.PropertyChangedEventArgs e)
    {
      base.OnAssociatedPropertyChanged(e);
      // Can be called for any property change. Therefore,
      // Verify that this is the property we're interested in:
      if ("IsDirected".Equals(e.PropertyName))
      {
        if (e.NewValue.Equals(true))
        { // Update the shape's built-in Decorator feature:
          this.DecoratorTo = LinkDecorator.DecoratorEmptyArrow;
        }
        else
        {
          this.DecoratorTo = null; // No arrowhead.
        }
      }
    }

    // OnAssociatedPropertyChanged is called only for properties
    // that have been registered using AssociateValueWith().
    // InitializeResources is a convenient place to call this.
    // This method is invoked only once per class, even though
    // it is an instance method.
    protected override void InitializeResources(StyleSet classStyleSet)
    {
      base.InitializeResources(classStyleSet);
      AssociateValueWith(this.Store, Wire.IsDirectedDomainPropertyId);
      // Add other properties here.
    }
}
```

`AssociateValueWith()` deve ser chamado uma vez para cada propriedade de domínio que você deseja registrar. Depois de ser chamado, todas as alterações na propriedade especificada chamarão em qualquer forma que apresente o `OnAssociatedPropertyChanged()` elemento de modelo da propriedade.

Não é necessário chamar para `AssociateValueWith()` cada instância. Embora InitializeResources seja um método de instância, ele é invocado apenas uma vez para cada classe de forma.
