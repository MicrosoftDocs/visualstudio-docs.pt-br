---
title: Personalizando campos de texto e imagem
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 29210ec667bffd6b632bcfbee0b87c0cbb2d5f38
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542708"
---
# <a name="customizing-text-and-image-fields"></a>Personalizando campos de texto e imagem
Quando você define um decorador de texto em uma forma, ele é representado por um TextField. Para obter exemplos de inicialização de TextFields e outros ShapeFields, inspecione Dsl\GeneratedCode\Shapes.cs em sua solução de DSL.

 Um TextField é um objeto que gerencia uma área dentro de uma forma, como o espaço atribuído a um rótulo. Uma instância de TextField é compartilhada entre muitas formas da mesma classe. A instância TextField não armazena o texto do rótulo separadamente para cada instância: em vez disso, o `GetDisplayText(ShapeElement)` método usa a forma como um parâmetro e pode pesquisar o texto dependente do estado atual da forma e seu elemento Model.

## <a name="how-the-appearance-of-a-text-field-is-determined"></a>Como a aparência de um campo de texto é determinada
 O `DoPaint()` método é chamado para exibir o campo na tela. Você pode substituir o padrão `DoPaint(),` ou pode substituir alguns dos métodos que ele chama. A seguinte versão simplificada dos métodos padrão pode ajudá-lo a entender como substituir o comportamento padrão:

```csharp
// Simplified version:
public override void DoPaint(DiagramPaintEventArgs e, ShapeElement parentShape)
{
  string text = GetDisplayText(shape);
  StringFormat format = GetStringFormat(parentShape);
  Brush brush = GetTextBrush(e.View, shape);
  using (Font font = GetFont(shape))
  {
    e.Graphics.DrawString(text, font, brush, format);
  }
}
// StringFormat determines whether the string is centered etc.
// To customize statically for all instances of this shape field,
// assign to DefaultStringFormat.
// To customize dynamically or per shape, override this:
public virtual StringFormat GetStringFormat(ShapeElement shape)
{ return DefaultStringFormat; }

// Override to customize the displayed string:
public virtual string GetDisplayText(ShapeElement shape)
{ return this.GetValue(shape).ToString(); }

// Brush determines the text color.
// To change the brush for every field, change the shape's styleset.
// To customize to a brush in the style set, override GetTextBrushId.
// To change the brush to non-standard color, override this.
// Should take account of whether selected.
public virtual Brush GetTextBrush(DiagramClientView view, ShapeElement shape)
{ return shape.StyleSet.GetBrush(this.GetTextBrushId(view, shape)); }

// Brush ID selects a brush from a StyleSet.
// Either return a member of DiagramBrushes
// or add your own brush to the shape or application's styleset.
// Override this to change dynamically or per instance.
// To change statically, just assign to default values.
public virtual StyleSetResourceId GetTextBrushId(DiagramClientView view, ShapeElement shape)
{ return IsSelected(view, shape) ? (view.Focused ? DefaultSelectedTextBrushId
: DefaultInactiveSelectedTextBrushId ) : DefaultTextBrushId ;
}

// Font determines the shape and size of the text.
// To change the font for every field, change the shape's styleset.
// To customize to a font in the style set, override GetFontId.
// To change the font to a non-standard font, override this.
public virtual Font GetFont(ShapeElement shape)
{ return shape.StyleSet.GetFont(GetFontId(shape)); }

// Selects a font from a styleset.
// Either return a member of DiagramFonts or
// add your own font to the shape or application's styleset.
// To change statically for all instances of this field,
// assign to DefaultFontId.
// To change per shape or dynamically, override this.
public virtual StyleSetResourceId GetFontId(ShapeElement parentShape)
{ return DefaultFontId; }
```

 Há vários outros pares de `Get` métodos e `Default` Propriedades, como `DefaultMultipleLine/GetMultipleLine()` . Você pode atribuir um valor à propriedade padrão para alterar o valor de todas as instâncias do campo de forma. Para fazer com que o valor varie de uma instância de forma para outra, ou que dependa do estado da forma ou de seu elemento de modelo, substitua o `Get` método.

## <a name="static-customizations"></a>Personalizações estáticas
 Se você quiser alterar cada instância desse campo de forma, primeiro descubra se você pode definir a propriedade na definição de DSL. Por exemplo, você pode definir o tamanho e o estilo da fonte na janela Propriedades.

 Caso contrário, substitua o `InitializeShapeFields` método da classe Shape e atribua um valor à `Default...` propriedade apropriada do campo de texto.

> [!WARNING]
> Para substituir `InitializeShapeFields()` , você deve definir a propriedade **derivada dupla** da classe Shape como `true` na definição de DSL.

 Neste exemplo, uma forma tem um campo de texto que será usado para comentários do usuário. Queremos usar a fonte de comentários padrão. Como se trata de uma fonte padrão do conjunto de estilos, podemos definir a ID da fonte padrão:

```csharp

 partial class ExampleShape
{   protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);
      // Find and update comment field:
      TextField commentField = ShapeElement.FindShapeField(shapeFields, "CommentDecorator") as TextField;
      // Use the standard font for comments:
      commentField.DefaultFontId = DiagramFonts.CommentText;
```

## <a name="dynamic-customizations"></a>Personalizações dinâmicas
 Para fazer com que a aparência varie de acordo com o estado de uma forma ou de seu elemento Model, derive sua própria subclasse de `TextField` e substitua um ou mais `Get...` métodos. Você também deve substituir o método InitializeShapeFields da forma e substituir a instância do TextField por uma instância de sua própria classe.

 O exemplo a seguir torna a fonte de um campo de texto dependente do estado de uma propriedade de domínio booliana do elemento de modelo da forma.

 Para executar este código de exemplo, crie uma nova solução DSL usando o modelo de linguagem mínimo. Adicione uma propriedade de domínio booliano `AlternateState` à classe de domínio exampleelement. Adicione um decorador de ícone à classe ExampleShape e defina sua imagem como um arquivo de bitmap. Clique em **transformar todos os modelos**. Adicione um novo arquivo de código no projeto DSL e insira o código a seguir.

 Para testar o código, pressione F5 e, na solução de depuração, abra um diagrama de exemplo. O estado padrão do ícone deve aparecer. Selecione a forma e, na janela Propriedades, altere o valor da propriedade **alternatestate** . A fonte do nome do elemento deve ser alterada.

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
...

  partial class ExampleShape
  {
    /// <summary>
    /// Compose a list of the fields in this shape.
    /// Called once for each shape class.
    /// </summary>
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);
      // Replace the text field for NameDecorator:
      TextField oldField = ShapeElement.FindShapeField(shapeFields, "NameDecorator") as TextField;
      shapeFields.Remove(oldField);
      // Replace with my text field based on DSL Definition values:
      MyTextField newField = new MyTextField(oldField);
      shapeFields.Add(newField);
    }
  }
  /// <summary>
  /// Dynamic font depends on state of model element.
  /// </summary>
  public class MyTextField : TextField
  {
    public MyTextField(TextField prototype)
      : base(prototype.Name)
    {
      DefaultText = prototype.DefaultText;
      DefaultFocusable = prototype.DefaultFocusable;
      DefaultAutoSize = prototype.DefaultAutoSize;
      AnchoringBehavior.MinimumHeightInLines = prototype.AnchoringBehavior.MinimumHeightInLines;
      AnchoringBehavior.MinimumWidthInCharacters = prototype.AnchoringBehavior.MinimumWidthInCharacters;
      DefaultAccessibleState = prototype.DefaultAccessibleState;
    }

    public override System.Drawing.Font GetFont(ShapeElement parentShape)
    {
      // Access the Boolean domain property of the model element:
      if ((parentShape.ModelElement as ExampleElement).AlternateState)
        return new System.Drawing.Font("Callisto", 14.0f,
               System.Drawing.FontStyle.Italic |
               System.Drawing.FontStyle.Bold);
      else
        return base.GetFont(parentShape);
    }

  }
```

## <a name="style-sets"></a>Conjuntos de estilos
 O exemplo anterior mostra como você pode alterar o campo de texto para qualquer fonte que esteja disponível. No entanto, um método preferível é alterá-lo para um de um conjunto de estilos associado à forma ou ao aplicativo. Para fazer isso, você substitui <xref:Microsoft.VisualStudio.Modeling.Diagrams.TextField.GetFontId%2A> ou GetTextBrushId ().

 Como alternativa, considere alterar o conjunto de estilos de sua forma substituindo <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.InitializeResources%2A> . Isso tem o efeito de alterar as fontes e pincéis de todos os campos de forma.

## <a name="customizing-image-fields"></a>Personalizando campos de imagem
 Quando você define um decorador de imagem em uma forma e quando você define uma forma de imagem, a área na qual a forma é exibida é gerenciada por um ImageField. Para obter exemplos de inicialização de ImageFields e outros ShapeFields, inspecione o Dsl\GeneratedCode\Shapes.cs em sua solução de DSL.

 Um ImageField é um objeto que gerencia uma área dentro de uma forma, como o espaço atribuído a um decorador. Uma instância de ImageField é compartilhada entre muitas formas da mesma classe de forma. A instância ImageField não armazena uma imagem separada para cada forma: em vez disso, o `GetDisplayImage(ShapeElement)` método usa a forma como um parâmetro e pode pesquisar a imagem dependente do estado atual da forma e seu elemento de modelo.

 Se você quiser um comportamento especial, como uma imagem variável, poderá criar sua própria classe derivada de ImageField.

#### <a name="to-create-a-subclass-of-imagefield"></a>Para criar uma subclasse de ImageField

1. Defina a propriedade **derivada dupla** da classe Shape pai na sua definição de DSL.

2. Substitua o `InitializeShapeFields` método da sua classe Shape.

    - Crie um novo arquivo de código no projeto DSL e grave uma definição de classe parcial para a classe Shape. Substitua a definição do método por aí.

3. Inspecione o código de `InitializeShapeFields` em DSL\GeneratedCode\Shapes.cs.

     No método override, chame o método base e crie uma instância de sua própria classe de campo de imagem. Use-o para substituir o campo imagem comum na `shapeFields` lista.

## <a name="dynamic-icons"></a>Ícones dinâmicos
 Este exemplo faz com que uma alteração de ícone dependa do estado do elemento Model da forma.

> [!WARNING]
> Este exemplo demonstra como criar um decorador de imagem dinâmica. Mas se você quiser alternar entre uma ou duas imagens dependendo do estado de uma variável de modelo, é mais simples criar vários decoradores de imagem, localizá-los na mesma posição na forma e, em seguida, definir o filtro de visibilidade para depender de valores específicos da variável de modelo. Para definir esse filtro, selecione o mapa de formas na definição de DSL, abra a janela detalhes de DSL e clique na guia decoradores.

 Para executar este código de exemplo, crie uma nova solução DSL usando o modelo de linguagem mínimo. Adicione uma propriedade de domínio booliano `AlternateState` à classe de domínio exampleelement. Adicione um decorador de ícone à classe ExampleShape e defina sua imagem como um arquivo de bitmap. Clique em **transformar todos os modelos**. Adicione um novo arquivo de código no projeto DSL e insira o código a seguir.

 Para testar o código, pressione F5 e, na solução de depuração, abra um diagrama de exemplo. O estado padrão do ícone deve aparecer. Selecione a forma e, na janela Propriedades, altere o valor da propriedade **alternatestate** . O ícone deve aparecer girado até 90 graus, nessa forma.

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
...
partial class ExampleShape
{
    /// <summary>
    /// Compose a list of the fields in this shape.
    /// Called once for each shape class.
    /// </summary>
    /// <param name="shapeFields"></param>
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);

      // Replace the image field:
      ShapeField oldField = ShapeElement.FindShapeField(shapeFields, "IconDecorator");
      shapeFields.Remove(oldField);
      // Must keep the same name:
      MyImageField newField = new MyImageField(oldField.Name);
      shapeFields.Add(newField);
      newField.DefaultImage = (oldField as ImageField).DefaultImage.Clone() as System.Drawing.Image;
    }
  }

  public class MyImageField : ImageField
  {
    public MyImageField(string tag) : base(tag) { }

    /// <summary>
    /// Get the image for this field in the given shape.
    /// </summary>
    public override System.Drawing.Image GetDisplayImage(ShapeElement parentShape)
    {
      ExampleElement element = parentShape.ModelElement as ExampleElement;
      if (element.AlternateState == true)
        return AlternateImage;
      else
        return base.GetDisplayImage(parentShape);
    }

    private System.Drawing.Image alternateImage;
    public System.Drawing.Image AlternateImage
    {
      get
      {
        if (alternateImage == null)
        {
          // Alternate image is a copy of the default, rotated by 90 degrees:
          alternateImage = this.DefaultImage.Clone() as System.Drawing.Image;
          alternateImage.RotateFlip(System.Drawing.RotateFlipType.Rotate90FlipNone);
        }
        return alternateImage;
      }
    }
  }
}
```

## <a name="see-also"></a>Confira também

- [Definindo formas e conectores](../modeling/defining-shapes-and-connectors.md)
- [Definindo uma imagem de plano de fundo em um diagrama](../modeling/setting-a-background-image-on-a-diagram.md)
- [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)