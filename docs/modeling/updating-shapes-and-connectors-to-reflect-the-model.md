---
title: Atualizando formas e conectores para refletir o modelo
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 5b8b70e1446894d93aa29024dada76af29b818eb
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49889627"
---
# <a name="update-shapes-and-connectors-to-reflect-the-model"></a>Atualizar formas e conectores para refletir o modelo

Em uma linguagem específica de domínio no Visual Studio, você pode fazer com que a aparência de uma forma de refletir o estado do modelo subjacente.

Os exemplos de código neste tópico devem ser adicionados a um `.cs` de arquivo no seu `Dsl` projeto. Você precisa dessas instruções em cada arquivo:

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
```

## <a name="set-shape-map-properties-to-control-the-visibility-of-a-decorator"></a>Definir propriedades de mapa de formas para controlar a visibilidade de um decorador

Você pode controlar a visibilidade de um decorador sem precisar escrever o código do programa, ao configurar o mapeamento entre a forma e a classe de domínio na definição de DSL. Para obter mais informações, consulte [como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md).

## <a name="expose-the-color-and-style-of-a-shape-as-properties"></a>Expor a cor e estilo de uma forma como as propriedades

Na definição de DSL, clique com botão direito na classe de forma, aponte para **adicionar exposto**e, em seguida, clique em um dos itens, como **cor de preenchimento**.

A forma agora tem uma propriedade de domínio que você pode definir no código do programa ou como um usuário. Por exemplo, para defini-lo no código do programa de um comando ou uma regra, você poderia escrever:

`shape.FillColor = System.Drawing.Color.Red;`

Se você quiser tornar a variável de propriedade apenas sob controle do programa e não pelo usuário, selecione a nova propriedade de domínio, como **cor de preenchimento** no diagrama de definição de DSL. Em seguida, na janela Propriedades, defina **é navegável** à `false` ou defina **é somente leitura de interface do usuário** para `true`.

## <a name="define-change-rules-to-make-color-style-or-location-depend-on-model-element-properties"></a>Definir regras de alteração para tornar a cor, estilo ou local dependem das propriedades do elemento de modelo
 Você pode definir regras que atualizam a aparência da forma depende de outras partes do modelo. Por exemplo, você pode definir uma regra de alteração em um elemento de modelo que atualiza a cor da forma dependente nas propriedades do elemento de modelo. Para obter mais informações sobre como alterar as regras, consulte [propagam alterações dentro do modelo de regras](../modeling/rules-propagate-changes-within-the-model.md).

 Você deve usar as regras apenas para atualizar as propriedades que são mantidas dentro de Store, pois as regras não são invocadas quando o comando Desfazer é executado. Isso não inclui alguns recursos gráficos, como o tamanho e a visibilidade de uma forma. Para atualizar esses recursos de uma forma, consulte [atualizando Store não gráfica recursos](#OnAssociatedProperty).

 O exemplo a seguir pressupõe que você expôs `FillColor` como uma propriedade de domínio, conforme descrito na seção anterior.

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

## <a name="use-onchildconfigured-to-initialize-a-shapes-properties"></a>Usar OnChildConfigured para inicializar propriedades de uma forma

Para definir as propriedades de uma forma quando inicialmente criado, a substituição `OnChildConfigured()` em uma definição parcial da sua classe de diagrama. A classe de diagrama é especificada na definição de DSL, e o código gerado está em **Dsl\Generated Code\Diagram.cs**. Por exemplo:

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

Esse método pode ser usado para propriedades de domínio e os recursos de fora da store, como o tamanho da forma.

## <a name="OnAssociatedProperty"></a> Use associatevaluewith () para atualizar outros recursos de uma forma

Para alguns recursos de uma forma, como se ele tem uma sombra, ou o estilo de seta de um conector, não há nenhum método incorporado de expor o recurso como uma propriedade de domínio.  Alterações para esses recursos não estão sob o controle do sistema de transação. Portanto, não é apropriado para atualizá-los usando as regras, pois as regras não são invocadas quando o usuário executa o comando Desfazer.

Em vez disso, você pode atualizar esses recursos usando <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnAssociatedPropertyChanged%2A>. No exemplo a seguir, o estilo de seta de um conector é controlado por um valor de uma propriedade de domínio na relação que exibe o conector:

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

`AssociateValueWith()` deve ser chamado uma vez para cada propriedade de domínio que você deseja registrar. Depois que tiver sido chamado, todas as alterações à propriedade especificada chamará `OnAssociatedPropertyChanged()` em quaisquer formas que apresentam o elemento de modelo da propriedade.

Não é necessário chamar `AssociateValueWith()` para cada instância. Embora InitializeResources é um método de instância, ele é chamado apenas uma vez para cada classe de forma.
