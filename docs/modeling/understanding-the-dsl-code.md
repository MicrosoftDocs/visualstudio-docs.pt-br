---
title: Noções básicas do código de DSL
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, generated code
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 490c9c3fe5724373072b2857eb0ce3da7905b172
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49813309"
---
# <a name="understanding-the-dsl-code"></a>Noções básicas do código de DSL
Uma solução de linguagem específica do domínio (DSL) gera uma API que você pode usar para ler e atualizar instâncias da DSL no Visual Studio. Essa API é definida no código que é gerado na definição da DSL. Este tópico descreve a API gerada.

## <a name="the-example-solution-component-diagrams"></a>A solução do exemplo: Diagramas de Componente
 Para criar a solução que é a origem da maioria dos exemplos neste tópico, crie uma DLs a partir de **modelos do componente** modelo de solução. Esse é um dos modelos padrão que são exibidos ao criar uma nova solução DSL.

> [!NOTE]
>  O modelo DSL de diagramas de componente não está relacionado aos diagramas de componente UML que você pode criar usando o menu de arquitetura no Visual Studio. No **novo projeto** diálogo caixa, expanda **outros tipos/extensibilidades do projeto** e, em seguida, clique em **Designer de linguagem específica do domínio**.

 Pressione F5 e experimente, se ainda não estiver familiarizado com esse modelo de solução. Observe especificamente que é possível criar portas arrastando uma ferramenta de porta para um componente e que é possível conectar portas.

 ![Componentes e portas interconectadas](../modeling/media/componentsample.png)

## <a name="the-structure-of-the-dsl-solution"></a>A Estrutura da Solução DSL
 O **Dsl** projeto define a API da DSL. O **DslPackage** projeto define como ele se integra com o Visual Studio. Também é possível adicionar seus próprios projetos, que também podem conter código gerado a partir do modelo.

### <a name="the-code-directories"></a>Os diretórios do código
 A maioria do código em cada um desses projetos é gerada a partir **Dsl\DslDefinition.dsl**. O código gerado está no **código gerado pelo** pasta. Para ver um arquivo gerado, clique em **[+]** ao lado de geração **. TT** arquivo.

 É recomendável inspecionar o código gerado para ajudar a entender a DSL. Para visualizar os arquivos gerados, expanda os arquivos *.tt no Gerenciador de Soluções.

 O \*arquivos. TT contêm muito pouco código de geração. Ao invés, eles usam diretrizes `<#include>` para incluir arquivos de modelo compartilhados. Os arquivos compartilhados podem ser encontrados no **\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft\DSL SDK\DSL Designer\11.0\TextTemplates**

 Ao adicionar seu próprio código do programa à solução DSL, adicione-o em um arquivo separado, fora da pasta do Código Gerado. Você talvez queira criar uma **código personalizado** pasta. (Ao adicionar um novo arquivo de código a uma pasta personalizada, lembre-se de corrigir o namespace no esqueleto inicial do código.)

 É altamente recomendável não editar o código gerado diretamente, pois, as edições serão perdidas ao recompilar a solução. Ao invés, para personalizar a DSL:

-   Ajuste os diversos parâmetros na Definição da DSL.

-   Grave classes parciais em arquivos de código separados, para substituir métodos que são definidos nas ou herdado pelas classes geradas. Em alguns casos, você deve definir a **gera derivado duplo** opção de uma classe na definição de DSL, para poder substituir um método gerado.

-   Definir opções na definição de DSL que fazem com que o código gerado forneça 'ganchos' para seu próprio código.

     Por exemplo, se você definir a **possui construtor personalizado** opção de uma classe de domínio e, em seguida, compile a solução, você verá mensagens de erro. Ao clicar duas vezes em uma dessas mensagens de erro, serão exibidos comentários sobre o código gerado que explicam o que o código personalizado deveria fornecer.

-   Grave seus próprios modelos de texto para gerar código específico para o aplicativo. Você pode usar arquivos de inclusão para compartilhar partes dos modelos que são comuns a muitos projetos, e você pode criar modelos de projeto do Visual Studio para configurar projetos que são inicializados com sua própria estrutura de arquivos.

## <a name="generated-files-in-dsl"></a>Arquivos gerados na Dsl
 Os seguintes arquivos gerados são exibidos na **Dsl** projeto.

 *{1&gt;yourdsl&lt;1* `Schema.xsd`

 O esquema dos arquivos que contêm instâncias da DSL. Esse arquivo é copiado para a compilação (**bin**) directory. Quando você instala a DSL, você pode copiar esse arquivo para **\Program Files\Microsoft Visual Studio 11.0\Xml\Schemas** para que os arquivos de modelo podem ser validados. Para obter mais informações, consulte [implantar soluções de linguagem específica do domínio](../modeling/deploying-domain-specific-language-solutions.md).

 Ao personalizar a serialização configurando opções no Gerenciador de DSL, o esquema será alterado de acordo. No entanto, se escrever seu próprio código de serialização, esse arquivo deixará de representar o esquema atual. Para obter mais informações, consulte [Personalizando o armazenamento de arquivos e a serialização XML](../modeling/customizing-file-storage-and-xml-serialization.md).

 `ConnectionBuilders.cs`

 Um compilador de conexão é uma classe que cria relações. É o código por trás de uma ferramenta de conexão. Esse arquivo contém um par de classes para cada ferramenta de conexão. Seus nomes são derivados dos nomes da ferramenta de conexão e de relação do domínio: *relacionamento*Builder, e *ConnectorTool*ConnectAction.

 (No exemplo de solução de componente, um dos compiladores de conexão é chamado ConnectionBuilder, isso é uma coincidência porque o nome da relação do domínio é Connection.)

 A relação é criada na *relacionamento* `Builder.Connect()` método. A versão padrão verifica se os elementos do modelo de origem e de destino são aceitáveis e instancia a relação. Por exemplo:

 `CommentReferencesSubject(sourceAccepted, targetAccepted);`

 Cada classe de construtor é gerada de um nó na **construtores de Conexão** seção no Gerenciador de DSL. Um método `Connect` pode criar relações entre um ou mais pares de classes de domínio. Cada par é definido por uma Diretriz de Conexão de Link, que pode ser encontrada no Gerenciador de DSL sob o nó do compilador.

 Por exemplo, é possível adicionar a um compilador de conexão Diretrizes de Conexão de Link para cada um dos três tipos de relação na DSL de exemplo. Isso forneceria ao usuário uma única ferramenta de conexão. O tipo de relação instanciada dependeria dos tipos dos elementos de origem e de destino selecionados pelo usuário.  Para adicionar Diretrizes de Conexão de Link, clique com o botão direito em um compilador no Gerenciador de DSL.

 Para gravar código personalizado que é executado quando um tipo específico de relação do domínio é criado, selecione a Diretriz de Conexão de Link adequada sob o nó do compilador. Na janela Propriedades, defina **usa conexão personalizada**. Recompile a solução e forneça o código para corrigir os erros resultantes.

 Para escrever código personalizado que é executado sempre que o usuário usa essa ferramenta de conexão, defina as **personalizado é** propriedade do construtor de conexão. É possível fornecer código que decide se um elemento de origem é permitido, se uma combinação específica de origem e destino é permitida e quais atualizações devem ser aplicadas no modelo quando uma conexão é feita. Por exemplo, é possível permitir uma conexão apenas se não criar um loop no diagrama. Ao invés de um único link de relação, é possível instanciar um padrão mais complexo de diversos elementos inter-relacionados entre a origem e o destino.

 `Connectors.cs`

 Contém a classes dos conectores, que são os elementos do diagrama que geralmente representam relações de referência. Cada classe é gerada a partir de um conector na Definição da DSL. Cada classe de conector é derivada de <xref:Microsoft.VisualStudio.Modeling.Diagrams.BinaryLinkShape>

 Para tornar a cor e alguns outros recursos de estilo variáveis em tempo de execução, a classe no diagrama de definição de DSL com o botão direito e aponte para **adicionar exposto**.

 Para tornar recursos de estilo adicionais variáveis em tempo de execução, consulte <xref:Microsoft.VisualStudio.Modeling.Diagrams.TextField> e <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement>, por exemplo.

 `Diagram.cs`

 Contém a classe que define o diagrama. É derivado de <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>.

 Para tornar a cor e alguns outros recursos de estilo variáveis em tempo de execução, a classe no diagrama de definição de DSL com o botão direito e aponte para **adicionar exposto**.

 Além disso, esse arquivo contém a regra `FixupDiagram`, que responde quando um novo elemento é adicionado ao modelo. A regra adiciona um novo formato e vincula o formato ao elemento do modelo.

 `DirectiveProcessor.cs`

 Esse processador de diretriz ajuda os usuários a gravar modelos de texto que fazem a leitura de uma instância da DSL. O processador de diretriz carrega os assemblies (DLLs) da DSL e, efetivamente insere instruções `using` para o namespace. Isso permite ao código nos modelos de texto usar as classes e relações definidas na DSL.

 Para obter mais informações, consulte [código de geração de uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md) e [criando processadores diretiva de modelo de texto do personalizado T4](../modeling/creating-custom-t4-text-template-directive-processors.md).

 `DomainClasses.cs`

 Implementações de classes do domínio que foram definidas, incluindo classes abstratas e a classe raiz do modelo. São derivadas de <xref:Microsoft.VisualStudio.Modeling.ModelElement>.

 Cada classe do domínio contém:

- Uma definição de propriedade e uma classe de manipulador aninhado para cada propriedade do domínio. É possível substituir OnValueChanging() e OnValueChanged(). Para obter mais informações, consulte [manipuladores de alteração de valor de propriedade de domínio](../modeling/domain-property-value-change-handlers.md).

   Na DSL de exemplo, a classe `Comment` contém um `Text` de propriedade e um `TextPropertyHandler` de classe de manipulador.

- Propriedades do acessador das relações das quais essa classe do domínio participa. (Não existe classe aninhada para propriedades de função.)

   Na DSL de exemplo, a classe `Comment` possui acessadores que acessa seu modelo pai através da relação de inserção `ComponentModelHasComments`.

- Construtores. Se você deseja substituí-los, defina **possui construtor personalizado** na classe de domínio.

- Métodos do manipulador Protótipo de Grupo de Elementos (EGP). Eles são necessários se o usuário puder *mesclagem* (Adicionar) outro elemento com instâncias dessa classe. Geralmente, o usuário faz isso arrastando de uma ferramenta de conexão ou outro formato ou colando.

   Na DSL de exemplo, uma Porta de Entrada ou Porta de Saída pode ser mesclada com um Componente. Além disso, Componentes e Comentários podem ser mesclados com o modelo. O

   Os métodos do manipulador EGP na classe Componente permite a um Componente aceitar Portas, porém, não Comentários. O manipulador EGP na classe raiz do modelo aceita Comentários e Componentes, porém, não Portas.

  `DomainModel.cs`

  A classe que representa o modelo do domínio. É derivado de <xref:Microsoft.VisualStudio.Modeling.DomainModel>.

> [!NOTE]
>  Não é a mesma que a classe raiz do modelo.

 Fechamentos de Copiar e Excluir define quais outros elementos devem ser incluídos quando um elemento é copiado ou excluído. Você pode controlar esse comportamento, definindo a **propaga cópia** e **propaga exclusão** propriedades das funções em cada lado de cada relação. Se desejar determinar os valores dinamicamente, é possível gravar código para substituir os métodos das classes de Fechamento.

 `DomainModelResx.resx`

 Isso contém cadeias de caracteres como as descrições de classes e propriedades do domínio, nomes de propriedade, etiquetas de caixa de ferramenta, mensagens de erro padrão e outras cadeias que podem ser exibidas ao usuário. Também contém ícones de ferramentas e imagens dos formatos de imagem.

 Esse arquivo é associado ao assembly de compilação e fornece os valores padrão desses recursos. É possível localizar a DSL criando um assembly satélite que contém uma versão localizada dos recursos. Essa versão será usada quando a DSL for instalada em uma cultura que corresponde aos recursos localizados. Para obter mais informações, consulte [implantar soluções de linguagem específica do domínio](../modeling/deploying-domain-specific-language-solutions.md).

 `DomainRelationships.cs`

 Cada link entre dois elementos em um modelo é representado por uma instância de uma classe de relação do domínio. Todas as classes de relação são derivadas de <xref:Microsoft.VisualStudio.Modeling.ElementLink>, que, por sua vez, é derivado de <xref:Microsoft.VisualStudio.Modeling.ModelElement>. Por ser um ModelElement, uma instância de uma relação pode conter propriedades e pode ser a origem ou o destino de uma relação.

 `HelpKeywordHelper.cs`

 Fornece funções que são usadas quando o usuário pressiona F1.

 `MultiplicityValidation.cs`

 Em funções de relação em que é especificada uma multiplicidade de 1..1 ou 1..*, o usuário deve ser advertido de que será necessária ao menos uma instância da relação. Esse arquivo fornece restrições de validação que implementam essas advertências. O link 1..1 a um pai de inserção não é verificado.

 Essas restrições a serem executadas, você deve ter definido uma da **usa...**  as opções de **Editor \ validação** nó no Gerenciador de DSL. Para obter mais informações, consulte [validação em uma linguagem específica do domínio](../modeling/validation-in-a-domain-specific-language.md).

 `PropertiesGrid.cs`

 Esse arquivo conterá código apenas se houver um Decodificador de Tipo Personalizado anexado a uma propriedade do domínio. Para obter mais informações, consulte [Personalizando a janela propriedades](../modeling/customizing-the-properties-window.md).

 `SerializationHelper.cs`

- Um método de validação para garantir que dois elementos não serão referenciados pelo mesmo moniker. Para obter mais informações, consulte [Personalizando o armazenamento de arquivos e a serialização XML](../modeling/customizing-file-storage-and-xml-serialization.md).

- Classe SerializationHelper, que fornece funções que são usadas em comum pelas classes de serialização.

  `Serializer.cs`

  Uma classe de serializador para cada classe, relação, forma, conector, diagrama e modelo do domínio.

  Muitos dos recursos dessas classes podem ser controlados pelas configurações no Gerenciador de DSL sob **comportamento da serialização Xml**.

  `Shapes.cs`

  Uma classe para cada classe da forma na Definição da DSL. As formas são derivadas de <xref:Microsoft.VisualStudio.Modeling.Diagrams.NodeShape>. Para obter mais informações, consulte [Personalizando o armazenamento de arquivos e a serialização XML](../modeling/customizing-file-storage-and-xml-serialization.md).

  Para substituir os métodos gerados por seus próprios métodos em uma classe parcial, defina **gera derivado duplo** para o conector na definição de DSL. Para substituir um construtor com seu próprio código, defina **possui construtor personalizado**.

  Para tornar a cor e alguns outros recursos de estilo variáveis em tempo de execução, a classe no diagrama de definição de DSL com o botão direito e aponte para **adicionar exposto**.

  Para tornar recursos de estilo adicionais variáveis em tempo de execução, consulte <xref:Microsoft.VisualStudio.Modeling.Diagrams.TextField> e <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement>, por exemplo

  `ToolboxHelper.cs`

  Configura a caixa de ferramentas instalando protótipos de grupo de elementos nas ferramentas do elemento. Cópias desses protótipos são mescladas com os elementos de destino quando o usuário executa a ferramenta.

  É possível substituir `CreateElementPrototype()` para definir um item de caixa de ferramentas que cria um grupo de diversos objetos. Por exemplo, é possível definir um item para representar objetos que possuem subcomponentes. Depois de alterar o código, redefina a instância experimental do Visual Studio para limpar o cache de caixa de ferramentas.

## <a name="generated-files-in-the-dslpackage-project"></a>Arquivos gerados no projeto DslPackage
 DslPackage acopla o modelo DSL ao shell do Visual Studio, gerenciando os comandos de janela, caixa de ferramentas e menus. A maioria das classes são derivadas duplas, de modo que é possível substituir qualquer um de seus métodos.

 `CommandSet.cs`

 Os comandos de menu de contexto que são visíveis no diagrama. É possível adaptar ou adicionar a esse conjunto. Esse arquivo contém o código dos comandos. O local dos comandos nos menus é determinado pelo arquivo Commands.vsct. Para obter mais informações, consulte [comandos de usuário de gravação e ações](../modeling/writing-user-commands-and-actions.md).

 `Constants.cs`

 GUIDs.

 `DocData.cs`

 *{1&gt;yourdsl&lt;1* `DocData` gerencia o carregamento e salvamento de um modelo para o arquivo e cria a instância Store.

 Por exemplo, se desejar salvar a DSL em um banco de dados ao invés de em um arquivo, é possível substituir os métodos `Load` e `Save`.

 `DocView.cs`

 *{1&gt;yourdsl&lt;1* `DocView` gerencia a janela na qual o diagrama é exibido. Por exemplo, é possível inserir o diagrama dentro de um Windows Form:

 Adicionar um arquivo de controle de usuário ao projeto DslPackage. Adicione um Painel no qual o diagrama pode ser exibido. Adicionar botões e outros controles. Na exibição de código do formulário, adicione o seguinte código, ajustando os nomes para sua DSL:

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Drawing;
using System.Data;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Shell;

namespace Company.EmbedInForm
{
  public partial class UserControl1 : UserControl
  {
    public UserControl1()
    {
      InitializeComponent();
    }

    private DiagramDocView docView;

    public UserControl1(DiagramDocView docView, Control content)
      : this()
    {
      this.docView = docView;
      panel1.Controls.Add(content);
    }

    private void button1_Click(object sender, EventArgs e)
    {
      ExampleModel modelRoot = this.docView.CurrentDiagram.ModelElement as ExampleModel;
      foreach (ExampleElement element in modelRoot.Elements)
      {
       listBox1.Items.Add(element.Name);
      }
    }
  }
  internal partial class EmbedInFormDocView
  {

    private ContainerControl container;

    /// <summary>
    /// Return a User Control instead of the DSL window.
    /// The user control will contain the DSL window.
    /// </summary>

    public override System.Windows.Forms.IWin32Window Window
    {
      get
      {
        if (container == null)
        {
          // Put the normal DSL Window inside our control
          container = new UserControl1(this, (Control)base.Window);
        }
        return container;
      }
    }
  }

}
```

 `EditorFactory.cs`

 Instancia `DocData` e `DocView`. Ele atende a uma interface padrão que usa o Visual Studio para abrir um editor quando o pacote DSL é iniciado. É referenciado no atributo `ProvideEditorFactory` em Package.cs

 `GeneratedVSCT.vsct`

 Localiza os comandos de menu padrão em menus, como o menu de contexto do diagrama, o **editar** menu e assim por diante. O código dos comandos está em CommandSet.cs. É possível realocar ou modificar os comandos padrão e adicionar seus próprios comandos. Para obter mais informações, consulte [comandos de usuário de gravação e ações](../modeling/writing-user-commands-and-actions.md).

 `ModelExplorer.cs`

 Define o Gerenciador de Modelos da DSL. Esse é o modo de exibição de árvore do modelo que o usuário vê ao lado do diagrama.

 Por exemplo, é possível substituir `InsertTreeView()` para alterar a ordem na qual elementos são exibidos no Gerenciador de Modelos.

 Se desejar manter a seleção no gerenciador de modelos sincronizada com a seleção do diagrama, é possível usar o seguinte código:

```
protected override void OnSelectionChanged(global::System.EventArgs e)
{
base.OnSelectionChanged(e);
// get the selected element
DslModeling::ModelElement selectedElement =
this.PrimarySelection as DslModeling::ModelElement;
// Select in the model explorer
SelectInModelExplorer<YOURLANGUAGEExplorerToolWindow>(selectedElement);
}
private void SelectInModelExplorer<T>(DslModeling::ModelElement modelElement)
where T : DslShell.ModelExplorerToolWindow
{
DslShell::ModelingPackage package =
this.GetService(typeof(VSShell.Package)) as DslShell::ModelingPackage;

if (package != null)
{
// find the model explorer window
T explorerWindow = package.GetToolWindow(typeof(T), true) as T;
if (explorerWindow != null)
{
// get the tree container
DslShell.ModelExplorerTreeContainer treeContainer =
explorerWindow.TreeContainer;
// find the tree node
DslShell.ExplorerTreeNode treeNode =
treeContainer.FindNodeForElement(modelElement);
// select the node
explorerWindow.TreeContainer.ObjectModelBrowser.SelectedNode = treeNode;
}
}
}
```

 `ModelExplorerToolWindow.cs`

 Define a janela na qual o gerenciador de modelos é exibido. Manipula a seleção de itens no gerenciador.

 `Package.cs`

 Esse arquivo define como a DSL integra no Visual Studio. Atributos na classe do pacote registram a DSL como o manipulador de arquivos que possuem sua extensão de arquivo, define a caixa de ferramentas e define como abrir uma nova janela. O método Initialize () é chamado uma vez quando a primeira DSL é carregada em uma instância do Visual Studio.

 `Source.extension.vsixmanifest`

 Para personalizar esse arquivo, edite o arquivo `.tt`.

> [!WARNING]
>  Ao editar o arquivo .tt para incluir recursos como ícones ou imagens, certifique-se de que o recurso será incluído na compilação VSIX. No Solution Explorer, selecione o arquivo e certifique-se de que o **incluir em VSIX** é de propriedade `True`.

 Esse arquivo controla como a DSL é empacotada em uma Extensão de Integração do Visual Studio (VSIX). Para obter mais informações, consulte [implantar soluções de linguagem específica do domínio](../modeling/deploying-domain-specific-language-solutions.md).

## <a name="see-also"></a>Consulte também

- [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md)
- [Noções básicas sobre modelos, classes e relações](../modeling/understanding-models-classes-and-relationships.md)
- [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md)
- [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)
