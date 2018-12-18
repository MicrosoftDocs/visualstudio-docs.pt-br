---
title: Personalizando a janela de propriedades
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, Properties window
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 76e7b9433fe76464e7af385081ac3577d53919e1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49813890"
---
# <a name="customizing-the-properties-window"></a>Personalizando a janela de propriedades
Você pode personalizar a aparência e comportamento da janela Propriedades em sua linguagem específica de domínio (DSL) no Visual Studio. Em sua definição de DSL, você pode definir propriedades de domínio em cada classe de domínio. Por padrão, quando você seleciona uma instância da classe, em um diagrama ou no Gerenciador de modelos, todas as propriedades de domínio é listada na janela Propriedades. Isso permite que você consulte e edite os valores das propriedades de domínio, mesmo se você não tiver mapeado-los para os campos de forma no diagrama.

## <a name="names-descriptions-and-categories"></a>Nomes, descrições e categorias
 **Nome e o nome de exibição**. Em sua definição de uma propriedade de domínio, o nome de exibição da propriedade é o nome que aparece em tempo de execução na janela Propriedades. Por outro lado, o nome é usado quando você escreve o código do programa para atualizar a propriedade. O nome deve ser um nome alfanumérico correto do CLR, mas o nome de exibição pode conter espaços.

 Quando você define o nome de uma propriedade na definição de DSL, seu nome de exibição é definido automaticamente para uma cópia do nome. Se você escrever um nome com maiusculas e minúsculas de Pascal, como "FuelGauge", o nome de exibição conterá automaticamente um espaço: "Medidor de combustível". No entanto, você pode definir o nome de exibição explicitamente a outro valor.

 **Descrição**. A descrição de uma propriedade de domínio aparece em dois lugares:

- Na parte inferior da janela Propriedades quando o usuário seleciona a propriedade. Você pode usá-lo para explicar ao usuário o que representa a propriedade.

- No código do programa gerado. Se você usar os recursos de documentação para extrair a documentação da API, ele será exibido como a descrição dessa propriedade na API.

  **Categoria**. Uma categoria é um título na janela Propriedades.

## <a name="exposing-style-features"></a>Expor os recursos de estilo
 Alguns dos recursos dinâmicos de elementos gráficos podem ser representado ou *exposto* como propriedades de domínio. Um recurso que foi exposto dessa maneira pode ser atualizado pelo usuário e muito mais facilidade de atualizar pelo código do programa.

 Clique em uma classe de forma na definição de DSL, aponte para **adicionar exposto**e, em seguida, escolha um recurso.

 Nas formas que você pode expor os **FillColor**, **OutlineColor**, **TextColor**, **OutlineDashStyle**,  **OutlineThickness** e **FillGradientMode** propriedades. Sobre conectores, você pode expor os **cor**`,`**TextColor**, **DashStyle**, e **espessura** propriedades. Em diagramas que você pode expor os **FillColor** e **TextColor** propriedades.

## <a name="forwarding-displaying-properties-of-related-elements"></a>Encaminhamento: Exibe as propriedades de elementos relacionados
 Quando o usuário de sua DSL seleciona um elemento em um modelo, as propriedades desse elemento são exibidas na janela Propriedades. No entanto, você também pode exibir as propriedades de elementos relacionados especificados. Isso é útil se você tiver definido um grupo de elementos que funciona em conjunto. Por exemplo, você pode definir um elemento principal e um elemento de plug-in opcional. Se o principal elemento é mapeado para uma forma e o outro não, é útil ver todas as suas propriedades, como se estivessem em um elemento.

 Esse efeito é denominado *encaminhamento de propriedade*, e isso acontece automaticamente em vários casos. Em outros casos, você pode obter a propriedade de encaminhamento, definindo um descritor de tipo de domínio.

### <a name="default-property-forwarding-cases"></a>Casos de encaminhamento de propriedade padrão
 Quando o usuário seleciona uma forma ou conector ou um elemento no Explorer, as propriedades a seguir são exibidas na janela Propriedades:

-   As propriedades de domínio que são definidas na classe de domínio do elemento de modelo, incluindo aqueles que são definidos nas classes base. Uma exceção é que as propriedades de domínio para o qual você definiu **é navegável** para `False`.

-   Os nomes dos elementos que são vinculados por meio de relações que tenham uma multiplicidade de 0 a 1. Isso fornece um método conveniente de ver opcionalmente vinculado elementos, mesmo se você não definiu um mapeamento de conector para a relação.

-   Propriedades do domínio da relação inserida que tem como alvo o elemento. Porque as relações de incorporação não são geralmente exibidas explicitamente, isso permite que o usuário veja suas propriedades.

-   Propriedades de domínio que são definidas no conector ou forma selecionada.

### <a name="adding-property-forwarding"></a>Adicionando o encaminhamento de propriedade
 Para encaminhar uma propriedade, você deve definir um descritor de tipo de domínio. Se você tiver uma relação de domínio entre duas classes de domínio, você pode usar um descritor de tipo de domínio para definir uma propriedade de domínio na primeira classe para o valor de uma propriedade de domínio na classe de domínio de segundo. Por exemplo, se você tiver uma relação entre um **livro** classe de domínio e um **autor** classe de domínio, você pode usar um descritor de tipo de domínio para fazer o **nome** propriedade de um Do livro **autor** aparecem na janela Propriedades quando o usuário seleciona o livro.

> [!NOTE]
>  Encaminhamento de propriedade afeta somente a janela de propriedades quando o usuário está editando um modelo. Ele não define uma propriedade de domínio na classe de recebimento. Se você quiser acessar a propriedade de domínio encaminhados em outras partes da definição de DSL ou no código do programa, você deve acessar o elemento de encaminhamento.

 O procedimento a seguir pressupõe que você tenha criado uma DSL. As primeiro algumas etapas resumem os pré-requisitos.

##### <a name="to-forward-a-property-from-another-element"></a>Para encaminhar uma propriedade de outro elemento

1. Criar uma [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] solução que contenha pelo menos duas classes, que, neste exemplo, são chamados **livro** e **autor**. Deve haver uma relação de qualquer um dos tipos entre **livro** e **autor**.

    A multiplicidade da função de origem (a função na **livro** lado) deve ser entre 0 e 1. 1 ou 1, para que cada **livro** tem um **autor**.

2. No **Gerenciador de DSL**, com o botão direito do **livro** classe de domínio e, em seguida, clique **o novo DomainTypeDescriptor adicionar**.

    Um nó chamado **caminhos de descritores de propriedade personalizada** aparece sob o **descritor de tipo personalizado** nó.

3. Com o botão direito do **descritor de tipo personalizado** nó e clique **adicionar novo PropertyPath**.

    Um novo caminho de propriedade aparece sob o **caminhos de descritores de propriedade personalizada** nó.

4. Selecione o novo caminho de propriedade e, na **propriedades** janela, defina **caminho para a propriedade** para o caminho do elemento de modelo apropriado.

    Você pode editar o caminho em uma exibição de árvore clicando na seta para baixo à direita dessa propriedade. Para obter mais informações sobre os caminhos de domínio, consulte [sintaxe de caminho de domínio](../modeling/domain-path-syntax.md). Quando você edita-lo, o caminho deve se parecer com **BookReferencesAuthor.Author/! Autor**.

5. Definir **propriedade** para o **nome** propriedade domain da **autor**.

6. Definir **nome de exibição** à **nome do autor**.

7. Transformar todos os modelos, compile e execute a DSL.

8. Em um diagrama de modelo, crie um livro, um autor e vinculá-los usando a relação de referência. Selecione o elemento de livro e na janela Propriedades, você verá o nome do autor além das propriedades do livro. Altere o nome do autor vinculado, ou vincular o livro a um autor de diferente e observe que o nome do autor do livro é alterado.

## <a name="custom-property-editors"></a>Editores de propriedade personalizada
 A janela de propriedade fornece um padrão apropriado experiência para o tipo de cada propriedade de domínio de edição. Por exemplo, para um tipo enumerado, o usuário vê uma lista suspensa e, para uma propriedade numérica, o usuário pode inserir os dígitos. Isso somente é verdadeiro para os tipos internos. Se você especificar um tipo externo, o usuário será capaz de ver os valores da propriedade, mas não editá-lo.

 No entanto, você pode especificar os editores e os tipos seguintes:

1. Outro editor que é usado com um tipo padrão. Por exemplo, você pode especificar um editor de caminho de arquivo para uma propriedade de cadeia de caracteres.

2. Um tipo externo para a propriedade de domínio e um editor para ele.

3. Um editor do .NET, como o editor de caminho de arquivo, ou você pode criar sua própria propriedade personalizada editor.

    A conversão entre um tipo externo e um tipo como cadeia de caracteres, que tem um editor padrão.

   Em uma DSL, uma *tipo externo* é qualquer tipo que não é um dos tipos simples (como Int32 ou boolianos) ou cadeia de caracteres.

#### <a name="to-define-a-domain-property-that-has-an-external-type"></a>Para definir uma propriedade de domínio que tem um tipo externo

1. No **Gerenciador de soluções**, adicione uma referência ao assembly (DLL) que contém o tipo externo, o **Dsl** projeto.

    O assembly pode ser um assembly .NET ou um assembly fornecido por você.

2. Adicione o tipo para o **tipos de domínio** lista, a menos que você já tiver feito isso.

   1.  Abra o Dsldefinition e, na **Gerenciador de DSL**, clique com botão direito no nó raiz e, em seguida, clique em **adicionar novo tipo externo**.

        Uma nova entrada aparece sob o **tipos de domínio** nó.

       > [!WARNING]
       >  O item de menu não está no nó raiz do DSL, o **tipos de domínio** nó.

   2.  Na janela Propriedades, defina o nome e o namespace do novo tipo.

3. Adicione uma propriedade de domínio a uma classe de domínio da maneira usual.

    Na janela Propriedades, selecione o tipo externo na lista suspensa na **tipo** campo.

   Nesse estágio, os usuários podem exibir os valores da propriedade, mas eles não podem editá-lo. Os valores exibidos são obtidos a `ToString()` função. Você pode escrever o código do programa que define o valor da propriedade, por exemplo, em um comando ou a regra.

### <a name="setting-a-property-editor"></a>Um Editor de propriedade de configuração
 Adicione um atributo CLR para a propriedade de domínio, da seguinte forma:

```csharp
[System.ComponentModel.Editor (
   typeof(AnEditor),
   typeof(System.Drawing.Design.UITypeEditor))]
```

 Você pode definir o atributo em uma propriedade usando o **atributo personalizado** entrada na janela Propriedades.

 O tipo de `AnEditor` deve ser derivado do tipo especificado no segundo parâmetro. O segundo parâmetro deve ser <xref:System.Drawing.Design.UITypeEditor> ou <xref:System.ComponentModel.ComponentEditor>. Para obter mais informações, consulte <xref:System.ComponentModel.EditorAttribute>.

 Você pode especificar seu próprio editor ou um editor fornecido na [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)], como <xref:System.Windows.Forms.Design.FileNameEditor> ou <xref:System.Drawing.Design.ImageEditor>. Por exemplo, use o procedimento a seguir para ter uma propriedade na qual o usuário pode inserir um nome de arquivo.

##### <a name="to-define-a-file-name-domain-property"></a>Para definir uma propriedade de domínio de nome de arquivo

1.  Adicione uma propriedade de domínio a uma classe de domínio em sua definição de DSL.

2.  Selecione a nova propriedade. No **atributo personalizado** na janela Propriedades, insira o seguinte atributo. Para inserir esse atributo, clique no botão de reticências **[...]**  e, em seguida, digite o nome do atributo e os parâmetros separadamente:

    ```csharp
    [System.ComponentModel.Editor (
       typeof(System.Windows.Forms.Design.FileNameEditor)
       , typeof(System.Drawing.Design.UITypeEditor))]

    ```

3.  Deixe o tipo de propriedade de domínio em sua configuração padrão de **cadeia de caracteres**.

4.  Para testar o editor, verifique se que os usuários podem abrir o editor de nome de arquivo para editar a propriedade de domínio.

    1.  Pressione CTRL + F5 ou F5. Na solução de depuração, abra um arquivo de teste. Criar um elemento da classe de domínio e selecioná-lo.

    2.  Na janela Propriedades, selecione a propriedade de domínio. O campo de valor mostra uma elipse **[...]** .

    3.  Clique no botão de reticências. Uma caixa de diálogo é exibida. Selecione um arquivo e feche a caixa de diálogo. O caminho do arquivo agora é o valor da propriedade de domínio.

### <a name="defining-your-own-property-editor"></a>Definindo seu próprio editor de propriedade
 Você pode definir seu próprio editor. Você faria isso para permitir que o usuário para editar um tipo que você tenha definido, ou para editar um tipo padrão de uma maneira especial. Por exemplo, você pode permitir que o usuário insira uma cadeia de caracteres que representa uma fórmula.

 Define um editor, escrevendo uma classe derivada de <xref:System.Drawing.Design.UITypeEditor>. Sua classe deve substituir:

- <xref:System.Drawing.Design.UITypeEditor.EditValue%2A>, para interagir com o usuário e atualizar o valor da propriedade.

- <xref:System.Drawing.Design.UITypeEditor.GetEditStyle%2A>, para especificar se o seu editor de abrir uma caixa de diálogo ou fornecer um menu suspenso.

  Você também pode fornecer uma representação gráfica do valor da propriedade que será exibido na grade de propriedade. Para fazer isso, substitua `GetPaintValueSupported`, e `PaintValue`.  Para obter mais informações, consulte <xref:System.Drawing.Design.UITypeEditor>.

> [!NOTE]
>  Adicione o código em um arquivo de código separado na **Dsl** projeto.

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

 Para usar esse editor, defina as **atributo personalizado** de uma propriedade de domínio para:

```csharp
[System.ComponentModel.Editor (
   typeof(MyNamespace.TextFileNameEditor)
   , typeof(System.Drawing.Design.UITypeEditor))]
```

 Para obter mais informações, consulte <xref:System.Drawing.Design.UITypeEditor>.

## <a name="providing-a-drop-down-list-of-values"></a>Fornecendo uma lista suspensa de valores
 Você pode fornecer uma lista de valores para um usuário à sua escolha.

> [!NOTE]
>  Essa técnica fornece uma lista de valores que podem ser alterados em tempo de execução. Se você quiser fornecer uma lista que não são alterados, em vez disso, considere usar um tipo enumerado como o tipo de sua propriedade de domínio.

 Para definir uma lista de valores padrão, você adicionar à sua propriedade de domínio um atributo CLR que tem a seguinte forma:

```csharp
[System.ComponentModel.TypeConverter
(typeof(MyTypeConverter))]
```

 Defina uma classe derivada de <xref:System.ComponentModel.TypeConverter>. Adicione o código em um arquivo separado na **Dsl** projeto. Por exemplo:

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

## <a name="see-also"></a>Consulte também

- [Navegando por um modelo no código do programa e atualizando-o](../modeling/navigating-and-updating-a-model-in-program-code.md)