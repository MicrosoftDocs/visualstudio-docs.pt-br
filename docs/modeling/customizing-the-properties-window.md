---
title: Personalizando a janela de propriedades
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Domain-Specific Language, Properties window
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4dac40177c3df2a346039a08cf557b6083ed9fc2
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548272"
---
# <a name="customize-the-properties-window"></a>Personalizar o janela Propriedades

Você pode personalizar a aparência e o comportamento da janela Propriedades em sua DSL (linguagem específica do domínio) no Visual Studio. Na definição de DSL, você define as propriedades de domínio em cada classe de domínio. Por padrão, quando você seleciona uma instância da classe, seja em um diagrama ou no Gerenciador de modelos, cada propriedade de domínio é listada na janela Propriedades. Isso permite que você veja e edite os valores das propriedades de domínio, mesmo que você não os tenha mapeado para campos de forma no diagrama.

## <a name="names-descriptions-and-categories"></a>Nomes, descrições e categorias

**Nome e nome para exibição**. Na definição de uma propriedade de domínio, o nome de exibição da propriedade é o nome que aparece em tempo de execução na janela Propriedades. Por outro lado, o nome é usado quando você escreve o código do programa para atualizar a propriedade. O nome deve ser um nome alfanumérico CLR correto, mas o nome de exibição pode conter espaços.

Quando você define o nome de uma propriedade na definição de DSL, seu nome de exibição é definido automaticamente como uma cópia do nome. Se você escrever um nome do Pascal case como "FuelGauge", o nome de exibição conterá automaticamente um espaço: "medidor de combustível". No entanto, você pode definir o nome de exibição explicitamente para outro valor.

**Descrição**. A descrição de uma propriedade de domínio aparece em dois locais:

- Na parte inferior da janela Propriedades quando o usuário seleciona a propriedade. Você pode usá-lo para explicar ao usuário o que a propriedade representa.

- No código do programa gerado. Se você usar os recursos de documentação para extrair a documentação da API, ela será exibida como a descrição dessa propriedade na API.

**Categoria**. Uma categoria é um título na janela Propriedades.

## <a name="expose-style-features"></a>Expor recursos de estilo

Alguns dos recursos dinâmicos de elementos gráficos podem ser representados ou *expostos* como propriedades de domínio. Um recurso que foi exposto dessa maneira pode ser atualizado pelo usuário e pode ser atualizado com mais facilidade pelo código do programa.

Clique com o botão direito do mouse em uma classe Shape na definição de DSL, aponte para **Adicionar exposto**e escolha um recurso.

Em formas, você pode expor as propriedades **FillColor**, **OutlineColor**, **TextColor**, **OutlineDashStyle**, **OutlineThickness** e **FillGradientMode** . Em conectores, você pode expor as propriedades **Color** `,` **TextColor**, **DashStyle**e **espessura** . Em diagramas, você pode expor as propriedades **FillColor** e **TextColor** .

## <a name="forwarding-display-properties-of-related-elements"></a>Encaminhamento: Exibir Propriedades de elementos relacionados

Quando o usuário de sua DSL seleciona um elemento em um modelo, as propriedades desse elemento são exibidas na janela Propriedades. No entanto, você também pode exibir as propriedades de elementos relacionados especificados. Isso será útil se você tiver definido um grupo de elementos que funciona em conjunto. Por exemplo, você pode definir um elemento principal e um elemento de plug-in opcional. Se o elemento principal for mapeado para uma forma e o outro não for, será útil ver todas as suas propriedades como se estivessem em um elemento.

Esse efeito é chamado de *encaminhamento de propriedade*e acontece automaticamente em vários casos. Em outros casos, você pode obter o encaminhamento de propriedade definindo um descritor de tipo de domínio.

### <a name="default-property-forwarding-cases"></a>Casos de encaminhamento de propriedades padrão

Quando o usuário seleciona uma forma ou um conector, ou um elemento no Explorer, as seguintes propriedades são exibidas no janela Propriedades:

- As propriedades de domínio que são definidas na classe de domínio do elemento de modelo, incluindo aquelas definidas em classes base. Uma exceção é que as propriedades de domínio para as quais você definiu **são navegáveis** `False` .

- Os nomes dos elementos que são vinculados por meio de relações que têm uma multiplicidade de 0.. 1. Isso fornece um método conveniente para ver elementos vinculados opcionalmente, mesmo que você não tenha definido um mapeamento de conector para a relação.

- Propriedades de domínio da relação de incorporação que tem como destino o elemento. Como as relações de incorporação geralmente não são exibidas explicitamente, isso permite que o usuário veja suas propriedades.

- Propriedades de domínio que são definidas na forma ou no conector selecionado.

### <a name="add-property-forwarding"></a>Adicionar encaminhamento de propriedade

Para encaminhar uma propriedade, você define um descritor de tipo de domínio. Se você tiver uma relação de domínio entre duas classes de domínio, poderá usar um descritor de tipo de domínio para definir uma propriedade de domínio na primeira classe como o valor de uma propriedade de domínio na segunda classe de domínio. Por exemplo, se você tiver uma relação entre uma classe de domínio de **livro** e uma classe de domínio de **autor** , poderá usar um descritor de tipo de domínio para fazer com que a propriedade **Name** do **autor** de um livro seja exibida na janela Propriedades quando o usuário selecionar o livro.

> [!NOTE]
> O encaminhamento de propriedade afeta somente a janela Propriedades quando o usuário está editando um modelo. Ele não define uma propriedade de domínio na classe de recebimento. Se você quiser acessar a propriedade de domínio encaminhada em outras partes da definição de DSL ou no código do programa, deverá acessar o elemento de encaminhamento.

O procedimento a seguir pressupõe que você tenha criado uma DSL. As primeiras etapas resumem os pré-requisitos.

#### <a name="forward-a-property-from-another-element"></a>Encaminhar uma propriedade de outro elemento

1. Crie uma [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] solução que contenha pelo menos duas classes, que neste exemplo são chamadas de **Book** e **Author**. Deve haver uma relação de qualquer tipo entre o **livro** e o **autor**.

    A multiplicidade da função de origem (a função no lado do **livro** ) deve ser 0.. 1 ou 1.. 1, para que cada **livro** tenha um **autor**.

2. No **Gerenciador de DSL**, clique com o botão direito do mouse na classe de domínio de **livro** e clique em **Adicionar novo o domaintypedescriptor**.

    Um nó chamado **Paths de descritores de propriedade personalizada** aparece sob o nó de **Descrição do tipo personalizado** .

3. Clique com o botão direito do mouse no nó **descritor de tipo personalizado** e clique em **Adicionar novo PropertyPath**.

    Um novo caminho de propriedade aparece sob os **caminhos do nó descritores de propriedade personalizada** .

4. Selecione o novo caminho de propriedade e, na janela **Propriedades** , defina **caminho para Propriedade** como o caminho do elemento de modelo apropriado.

    Você pode editar o caminho em um modo de exibição de árvore clicando na seta para baixo à direita dessa propriedade. Para obter mais informações sobre caminhos de domínio, consulte [sintaxe de caminho de domínio](../modeling/domain-path-syntax.md). Depois de editá-lo, o caminho deve ser semelhante a **BookReferencesAuthor. Author/! Autor**.

5. Defina a **Propriedade** como a propriedade de **nome** de domínio do **autor**.

6. Defina **nome de exibição** como **nome do autor**.

7. Transforme todos os modelos, compile e execute a DSL.

8. Em um diagrama de modelo, crie um livro, um autor e vincule-os usando a relação de referência. Selecione o elemento de livro e, na janela Propriedades você deverá ver o nome do autor além das propriedades do livro. Altere o nome do autor vinculado ou vincule o livro a um autor diferente e observe que o nome do autor do livro é alterado.

## <a name="custom-property-editors"></a>Editores de propriedade personalizada

A janela de propriedades fornece uma experiência de edição padrão apropriada para o tipo de cada propriedade de domínio. Por exemplo, para um tipo enumerado, o usuário vê uma lista suspensa e, para uma propriedade numérica, o usuário pode inserir dígitos. Isso só é verdadeiro para os tipos internos. Se você especificar um tipo externo, o usuário poderá ver os valores da propriedade, mas não editá-lo.

No entanto, você pode especificar os seguintes editores e tipos:

1. Outro editor usado com um tipo padrão. Por exemplo, você pode especificar um editor de caminho de arquivo para uma propriedade de cadeia de caracteres.

2. Um tipo externo para a propriedade de domínio e um editor para ele.

3. Um editor .NET, como o editor de caminho de arquivo, ou você pode criar seu próprio editor de propriedade personalizado.

   Uma conversão entre um tipo externo e um tipo como String, que tem um editor padrão.

   Em uma DSL, um *tipo externo* é qualquer tipo que não seja um dos tipos simples (como booliano ou Int32) ou cadeia de caracteres.

### <a name="define-a-domain-property-that-has-an-external-type"></a>Definir uma propriedade de domínio que tenha um tipo externo

1. No **Gerenciador de soluções**, adicione uma referência ao assembly (DLL) que contém o tipo externo, no projeto **DSL** .

    O assembly pode ser um assembly .NET ou um assembly fornecido por você.

2. Adicione o tipo à lista de **tipos de domínio** , a menos que você já tenha feito isso.

   1. Abra DslDefinition. DSL e, no **Gerenciador de DSL**, clique com o botão direito do mouse no nó raiz e clique em **Adicionar novo tipo externo**.

        Uma nova entrada é exibida sob o nó **tipos de domínio** .

       > [!WARNING]
       > O item de menu está no nó raiz de DSL, não no nó **tipos de domínio** .

   2. Defina o nome e o namespace do novo tipo na janela Propriedades.

3. Adicione uma propriedade de domínio a uma classe de domínio da maneira usual.

    No janela Propriedades, selecione o tipo externo na lista suspensa no campo **tipo** .

   Nesse estágio, os usuários podem exibir os valores da propriedade, mas não podem editá-lo. Os valores exibidos são obtidos da `ToString()` função. Você pode escrever o código do programa que define o valor da propriedade, por exemplo, em um comando ou regra.

### <a name="set-a-property-editor"></a>Definir um editor de propriedade

Adicione um atributo CLR à Propriedade Domain, no seguinte formato:

```csharp
[System.ComponentModel.Editor (
   typeof(AnEditor),
   typeof(System.Drawing.Design.UITypeEditor))]
```

Você pode definir o atributo em uma propriedade usando a entrada de **atributo personalizado** no janela Propriedades.

O tipo de `AnEditor` deve ser derivado do tipo especificado no segundo parâmetro. O segundo parâmetro deve ser <xref:System.Drawing.Design.UITypeEditor> ou <xref:System.ComponentModel.ComponentEditor> . Para obter mais informações, consulte <xref:System.ComponentModel.EditorAttribute>.

Você pode especificar seu próprio editor ou um editor do .NET, como <xref:System.Windows.Forms.Design.FileNameEditor> ou <xref:System.Drawing.Design.ImageEditor> . Por exemplo, use o procedimento a seguir para ter uma propriedade na qual o usuário possa inserir um nome de arquivo.

#### <a name="define-a-file-name-domain-property"></a>Definir uma propriedade de domínio de nome de arquivo

1. Adicione uma propriedade de domínio a uma classe de domínio em sua definição de DSL.

2. Selecione a nova propriedade. No campo **atributo personalizado** na janela Propriedades, insira o atributo a seguir. Para inserir esse atributo, clique nas reticências **[...]** e insira o nome do atributo e os parâmetros separadamente:

    ```csharp
    [System.ComponentModel.Editor (
       typeof(System.Windows.Forms.Design.FileNameEditor)
       , typeof(System.Drawing.Design.UITypeEditor))]

    ```

3. Deixe o tipo da propriedade de domínio em sua configuração padrão de **cadeia de caracteres**.

4. Para testar o editor, verifique se os usuários podem abrir o editor de nome de arquivo para editar sua propriedade de domínio.

    1. Pressione CTRL + F5 ou F5. Na solução de depuração, abra um arquivo de teste. Crie um elemento da classe de domínio e selecione-o.

    2. Na janela Propriedades, selecione a propriedade domínio. O campo valor mostra uma elipse **[...]**.

    3. Clique nas reticências. Uma caixa de diálogo de arquivo é exibida. Selecione um arquivo e feche a caixa de diálogo. O caminho do arquivo agora é o valor da Propriedade Domain.

### <a name="define-your-own-property-editor"></a>Definir seu próprio editor de propriedade

Você pode definir seu próprio editor. Você faria isso para permitir que o usuário edite um tipo que você definiu ou para editar um tipo padrão de forma especial. Por exemplo, você pode permitir que o usuário insira uma cadeia de caracteres que representa uma fórmula.

Você define um editor escrevendo uma classe que é derivada de <xref:System.Drawing.Design.UITypeEditor> . Sua classe deve substituir:

- <xref:System.Drawing.Design.UITypeEditor.EditValue%2A>, para interagir com o usuário e atualizar o valor da propriedade.

- <xref:System.Drawing.Design.UITypeEditor.GetEditStyle%2A>, para especificar se o editor abrirá uma caixa de diálogo ou fornecerá um menu suspenso.

Você também pode fornecer uma representação gráfica do valor da propriedade que será exibido na grade de propriedades. Para fazer isso, substitua `GetPaintValueSupported` e `PaintValue` .  Para obter mais informações, consulte <xref:System.Drawing.Design.UITypeEditor>.

> [!NOTE]
> Adicione o código em um arquivo de código separado no projeto **DSL** .

Por exemplo:

```csharp
internal class TextFileNameEditor : System.Windows.Forms.Design.FileNameEditor
{
  protected override void InitializeDialog(System.Windows.Forms.OpenFileDialog openFileDialog)
  {
    base.InitializeDialog(openFileDialog);
    openFileDialog.Filter = "Text files(*.txt)|*.txt|All files (*.*)|*.*";
    openFileDialog.Title = "Select a text file";
  }
}
```

Para usar esse editor, defina o **atributo personalizado** de uma propriedade de domínio como:

```csharp
[System.ComponentModel.Editor (
   typeof(MyNamespace.TextFileNameEditor)
   , typeof(System.Drawing.Design.UITypeEditor))]
```

Para obter mais informações, consulte <xref:System.Drawing.Design.UITypeEditor>.

## <a name="provide-a-drop-down-list-of-values"></a>Forneça uma lista suspensa de valores

Você pode fornecer uma lista de valores para que um usuário escolha.

> [!NOTE]
> Essa técnica fornece uma lista de valores que podem ser alterados em tempo de execução. Se você quiser fornecer uma lista que não é alterada, considere usar um tipo enumerado como o tipo de sua propriedade de domínio.

Para definir uma lista de valores padrão, adicione à propriedade de domínio um atributo CLR que tenha o seguinte formato:

```csharp
[System.ComponentModel.TypeConverter
(typeof(MyTypeConverter))]
```

Defina uma classe derivada de <xref:System.ComponentModel.TypeConverter>. Adicione o código em um arquivo separado no projeto **DSL** . Por exemplo:

```csharp
/// <summary>
/// Type converter that provides a list of values
/// to be displayed in the property grid.
/// </summary>
/// <remarks>This type converter returns a list
/// of the names of all "ExampleElements" in the
/// current store.</remarks>
public class MyTypeConverter : System.ComponentModel.TypeConverter
{
  /// <summary>
  /// Return true to indicate that we return a list of values to choose from
  /// </summary>
  /// <param name="context"></param>
  public override bool GetStandardValuesSupported
    (System.ComponentModel.ITypeDescriptorContext context)
  {
    return true;
  }

  /// <summary>
  /// Returns true to indicate that the user has
  /// to select a value from the list
  /// </summary>
  /// <param name="context"></param>
  /// <returns>If we returned false, the user would
  /// be able to either select a value from
  /// the list or type in a value that is not in the list.</returns>
  public override bool GetStandardValuesExclusive
      (System.ComponentModel.ITypeDescriptorContext context)
  {
    return true;
  }

  /// <summary>
  /// Return a list of the values to display in the grid
  /// </summary>
  /// <param name="context"></param>
  /// <returns>A list of values the user can choose from</returns>
  public override StandardValuesCollection GetStandardValues
      (System.ComponentModel.ITypeDescriptorContext context)
  {
    // Try to get a store from the current context
    // "context.Instance"  returns the element(s) that
    // are currently selected i.e. whose values are being
    // shown in the property grid.
    // Note that the user could have selected multiple objects,
    // in which case context.Instance will be an array.
    Store store = GetStore(context.Instance);

    List<string> values = new List<string>();

    if (store != null)
    {
      values.AddRange(store.ElementDirectory
        .FindElements<ExampleElement>()
        .Select<ExampleElement, string>(e =>
      {
        return e.Name;
      }));
    }
    return new StandardValuesCollection(values);
  }

  /// <summary>
  /// Attempts to get to a store from the currently selected object(s)
  /// in the property grid.
  /// </summary>
  private Store GetStore(object gridSelection)
  {
    // We assume that "instance" will either be a single model element, or
    // an array of model elements (if multiple items are selected).

    ModelElement currentElement = null;

    object[] objects = gridSelection as object[];
    if (objects != null && objects.Length > 0)
    {
      currentElement = objects[0] as ModelElement;
    }
    else
    {
        currentElement = gridSelection as ModelElement;
    }

    return (currentElement == null) ? null : currentElement.Store;
  }

}
```

## <a name="see-also"></a>Confira também

- [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)
