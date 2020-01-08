---
title: Estendendo o Visual Studio para Mac
description: Os recursos do Visual Studio para Mac podem ser estendido com módulos chamados de pacotes de extensão. A primeira parte deste guia cria um pacote de extensão simples do Visual Studio para Mac para inserir a data e a hora em um documento. A segunda parte deste guia apresenta os conceitos básicos do sistema de pacote de extensão e algumas das principais APIs que formam a base do Visual Studio para Mac.
author: heiligerdankgesang
ms.author: dominicn
ms.date: 12/20/2019
ms.technology: vs-ide-sdk
ms.assetid: D5245AB0-8404-426B-B538-F49125E672B2
ms.openlocfilehash: dcfbee59abeea9b6575470ef313a5ead5b03f9a9
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75398098"
---
# <a name="extending-visual-studio-for-mac"></a>Estendendo o Visual Studio para Mac

O Visual Studio para Mac consiste em um conjunto de módulos chamado *Pacotes de Extensão*. Você pode usar pacotes de extensão para introduzir novos recursos ao Visual Studio para Mac, tal como suporte a um idioma adicional ou um novo modelo de projeto.

Pacotes de extensão são baseados nos pontos de *extensão* de outros pacotes de extensão. Pontos de extensão são espaços reservados para as áreas que podem ser expandidas, como um menu ou a lista de comandos do IDE. Um pacote de extensão pode ser baseado em um ponto de extensão com o registro de um nó de dados estruturados chamados de extensão, como um novo item de menu ou um novo comando. Cada ponto de extensão aceita certos tipos de extensões, como um *Comando*, *Painel* ou *FileTemplate*. Um módulo que contém pontos de extensão é chamado de *host de suplemento*, pois ele pode ser estendido por outros pacotes de extensão.

Para personalizar o Visual Studio para Mac, você pode criar um pacote de extensão baseado em pontos de extensão contidos em hosts de suplementos dentro de bibliotecas pré-existentes no Visual Studio para Mac, conforme ilustrado pelo diagrama a seguir:

![Arquitetura de suplemento](media/extending-visual-studio-mac-addin1.png)

Para que um pacote de extensão se baseie no Visual Studio para Mac, ele deve ter extensões baseadas em pontos de extensão pré-existentes dentro do IDE do Visual Studio para Mac. Quando um pacote de extensão depende de um ponto de extensão definido em um host de suplemento, ele deve ter uma _dependência_ no pacote de extensão em questão.

A vantagem desse design modular é que o Visual Studio para Mac é extensível – há muitos pontos de extensão que podem servir de base com pacotes de extensão personalizados. Exemplos de pacotes de extensão atuais incluem suporte para C# e F#, ferramentas de depuração e modelos de projeto.

> [!NOTE]
> Se você tiver um projeto do criador de suplementos criado antes do Add-in Maker 1,2, você precisará migrar seu projeto conforme descrito nas etapas [aqui](https://mhut.ch/addinmaker/1.2).

<!---The [Walkthrough](~/extending-visual-studio-mac-walkthrough.md) topic explains how to build an extension package that uses a *Command* to insert the date and time into an open text document.--->

Esta seção examina os diferentes arquivos gerados pelo Criador de Suplementos os dados exigidos por uma extensão de comando.

## <a name="attribute-files"></a>Arquivos de atributo

Pacotes de extensão armazenam metadados sobre seu nome, versão, dependências e outras informações em atributos C#. O Criador de Suplementos cria dois arquivos, `AddinInfo.cs` e `AssemblyInfo.cs`, para armazenar e organizar essas informações. Pacotes de extensão devem ter uma ID exclusiva e o namespace especificado em seus *atributos `Addin`* :

```csharp
[assembly:Addin (
   "DateInserter",
   Namespace = "DateInserter",
   Version = "1.0"
)]
```

Os pacotes de extensão também precisam declarar dependências nos pacotes de extensão que possuem os pontos de extensão aos quais eles se conectam, que são referenciados automaticamente no tempo de compilação.

Além disso, referências adicionais podem ser adicionadas por meio do nó de referência Suplemento no Painel de Soluções do projeto, conforme ilustrado pela imagem a seguir:

![Inserir captura de tela de data](media/extending-visual-studio-mac-addin13.png)

Eles também têm seus atributos `assembly:AddinDependency` correspondentes adicionados no tempo de build. Depois que os metadados e as declarações de dependência estão em vigor, você pode se concentrar nos blocos de construção essenciais do pacote de extensão.

## <a name="extensions-and-extension-points"></a>Extensões e pontos de extensão

Um ponto de extensão é um espaço reservado que define uma estrutura de dados (um tipo), enquanto uma extensão define dados que correspondem a uma estrutura especificada por um determinado ponto de extensão. Os pontos de extensão especificam o tipo de extensão que pode ser aceito em sua declaração. As extensões são declaradas usando nomes de tipos ou caminhos de extensão. Consulte a [Referência de ponto de extensão](https://github.com/mono/mono-addins/wiki/Extension-Points) para ver uma explicação mais aprofundada sobre como criar o ponto de extensão que você precisa.

A arquitetura de extensão/ponto de extensão mantém o desenvolvimento do Visual Studio para Mac modular e rápida.

<!--Since there are a large number of extension types, this article focuses on the ones used in the extension package that was built in the [Walkthrough](~/extending-visual-studio-mac-walkthrough.md).-->

### <a name="command-extensions"></a>Extensões de comando

<!--[Walkthrough](~/extending-visual-studio-mac-walkthrough.md) uses a Command Extension - an extension that points to methods that are called every time it is executed. -->

As Extensões de Comando são extensões que apontam para métodos que são chamados toda vez que eles são executados.

As extensões de comando são definidas ao adicionar entradas ao ponto de extensão `/MonoDevelop/Ide/Commands`. Definimos nossa extensão em `Manifest.addin.xml` com o código a seguir:

 ```xml
<Extension path="/MonoDevelop/Ide/Commands/Edit">
  <Command id="DateInserter.DateInserterCommands.InsertDate"
            _label="Insert Date"
            _description="Insert the current date"
            defaulthandler="DateInserter.InsertDateHandler" />
</Extension>
```

O nó de extensão contém um atributo de caminho que especifica o ponto de extensão de conexão, nesse caso `/MonoDevelop/Ide/Commands/Edit`. Além disso, ele atua como um nó pai para o Comando. O nó Comando tem os seguintes atributos:

* `id` – especifica o identificador para esse Comando. Identificadores de comando devem ser declarados como membros de enumeração e são usados para conectar os Comandos aos CommandItems.
* `_label` – o texto a ser mostrado nos menus.
* `_description` – o texto a ser mostrado como uma dica de ferramenta para os botões da barra de ferramentas.
* `defaultHandler` – especifica a classe `CommandHandler` que habilita o Comando

<!--To invoke the command from the Edit Menu, the walkthrough creates a CommandItem extension that plugs into the `/MonoDevelop/Ide/MainMenu/Edit` extension point:-->

Uma Extensão CommandItem que se conecta ao ponto de extensão `/MonoDevelop/Ide/MainMenu/Edit` é demonstrado no seguinte snippet de código:

```xml
<Extension path="/MonoDevelop/Ide/MainMenu/Edit">
  <CommandItem id="DateInserter.DateInserterCommands.InsertDate" />
</Extension>
```

Um CommandItem posiciona um Comando especificado em seu atributo `id` em um menu. Este CommandItem está estendendo o ponto de extensão `/MonoDevelop/Ide/MainMenu/Edit`, o que faz com que o rótulo do comando apareça no **Menu Editar**. Observe que a ID no CommandItem corresponde à ID do nó do Comando, `InsertDate`. Se você remover o CommandItem, a opção **Inserir Data** desaparecerá do Menu Editar.

### <a name="command-handlers"></a>Manipuladores de comandos

O `InsertDateHandler` é uma extensão da classe `CommandHandler`. Ele substitui dois métodos, `Update` e `Run`. O método `Update` é consultado sempre que um comando é mostrado em um menu ou executado por meio de associações de chave. Alterando o objeto de informações, é possível desabilitar o Comando ou torná-lo invisível, popular comandos de matriz e muito mais. Esse método `Update` desabilita o comando se ele não encontrar um *Documento* ativo com um *TextEditor* para inserção de texto:

```csharp
protected override void Update (CommandInfo info)
{
    info.Enabled = IdeApp.Workbench.ActiveDocument?.Editor != null;
}
```

Será necessário substituir o método `Update` somente se você tiver uma lógica especial para habilitar ou ocultar o Comando. O método `Run` é executado sempre que um usuário executar um Comando, que nesse caso ocorre quando um usuário seleciona o Comando no Menu Editar. Esse método insere a data e a hora na posição do cursor no editor de texto:

```csharp
protected override void Run ()
{
  var editor = IdeApp.Workbench.ActiveDocument.Editor;
  var date = DateTime.Now.ToString ();
  editor.InsertAtCaret (date);
}
```

Declare o tipo de Comando como um membro de enumeração em `DateInserterCommands`:

```csharp
public enum DateInserterCommands
{
  InsertDate,
}
```

Comando e CommandItem agora estão vinculados – o CommandItem chama o Comando quando o CommandItem é selecionado no **Menu Editar**.

## <a name="ide-apis"></a>APIs de IDE

<!--The extension package detailed in the [Walkthrough](~/extending-visual-studio-mac-walkthrough.md) deals with the Text Editor in Visual Studio for Mac, but this is only one of many possible areas for customization. -->

Para ver informações sobre o escopo das áreas que estão disponíveis para o desenvolvimento, consulte a [Referência de árvore de extensões](https://www.monodevelop.com/developers/articles/extension-tree-reference/) e [Visão geral da API](https://www.monodevelop.com/developers/articles/api-overview/). Ao criar pacotes de extensão avançados, consulte também [Artigos do desenvolvedor](https://www.monodevelop.com/developers/articles/). Veja abaixo uma lista parcial das áreas de personalização:

* Painéis
* Esquemas de associação de teclas
* Políticas
* Formatadores de código
* Formatos de arquivo de projeto
* Painéis de preferências
* Painéis de opções
* Protocolos do depurador
* Visualizadores do depurador
* Layouts de workspace
* Nós de árvore do painel de soluções
* Margens do editor de código-fonte
* Mecanismos de teste de unidade
* Geradores de código
* Snippets de código
* Frameworks de destino
* runtime de destino
* Back-ends de VCS
* Refatoração
* Manipuladores de execução
* Realce de sintaxe

## <a name="extending-the-new-editor"></a>Como estender o novo editor

O Visual Studio para Mac [introduz uma nova interface do usuário do editor de texto Cocoa nativo](https://aka.ms/vs/mac/editor/learn-more) criada com base nas mesmas camadas de editor do Visual Studio no Windows.

Um dos muitos benefícios de compartilhar o editor entre o Visual Studio e o Visual Studio para Mac é que o código direcionado ao editor do Visual Studio pode ser adaptado para ser executado no Visual Studio para Mac.

> [!NOTE]
> O novo editor dá suporte apenas a arquivos C# no momento. Outros formatos de arquivo e linguagens serão abertos no editor herdado. No entanto, o editor herdado implementa algumas das APIs do Editor do Visual Studio descritas abaixo.

### <a name="visual-studio-editor-overview"></a>Visão geral do editor do Visual Studio

![Arquitetura do editor do Visual Studio](media/vs-editor-architecture.png)

Antes de entrarmos nos detalhes da extensão específicos do Visual Studio para Mac, é útil entender mais sobre o próprio editor compartilhado. Veja a seguir alguns recursos que podem aprofundar essa compreensão:

* [Managed Extensibility Framework](/dotnet/framework/mef/index)
* [MEF no editor](/visualstudio/extensibility/managed-extensibility-framework-in-the-editor)
* [Dentro do Editor](/visualstudio/extensibility/inside-the-editor)
* [Serviço de linguagem e pontos de extensão do editor](/visualstudio/extensibility/language-service-and-editor-extension-points)
* [Um vídeo de introdução à arquitetura do editor](https://www.youtube.com/watch?v=PkYVztKjO9A)

Com esses recursos em mãos, os principais conceitos com os quais você precisa estar familiarizado são um [`ITextBuffer`](/dotnet/api/microsoft.visualstudio.text.itextbuffer) e um [`ITextView`](/dotnet/api/microsoft.visualstudio.text.editor.itextview):

* Um `ITextBuffer` é uma representação de texto na memória que pode ser alterado ao longo do tempo. A propriedade `CurrentSnapshot` em `ITextBuffer` retorna uma representação *imutável* do conteúdo atual do buffer, uma instância de `ITextSnapshot`. Quando uma edição é feita no buffer, a propriedade CurrentSnapshot é atualizada para a versão mais recente. Os analisadores podem inspecionar o instantâneo de texto em qualquer thread e é certo que seu conteúdo nunca será alterado.

* Um `ITextView` é a representação da interface do usuário de como `ITextBuffer` é renderizado na tela do controle do editor. Ele tem uma referência ao seu buffer de texto, bem como `Caret`, `Selection` e outros conceitos relacionados à interface do usuário.

Para determinado [`MonoDevelop.Ide.Gui.Document`](http://source.monodevelop.com/#MonoDevelop.Ide/MonoDevelop.Ide.Gui/Document.cs,4e960d4735f089b5), você pode recuperar os `ITextBuffer` e `ITextView` subjacentes associados por meio de `Document.GetContent<ITextBuffer>()` e `Document.GetContent<ITextView>()`, respectivamente.

## <a name="additional-information"></a>{1&gt;Informações Adicionais&lt;1}

> [!NOTE]
> Estamos trabalhando para melhorar os cenários de extensibilidade do Visual Studio para Mac. Se você estiver criando extensões e precisa de ajuda ou informações adicionais, ou deseja fornecer comentários, preencha o formulário [Visual Studio for Mac Extension Authoring](https://aka.ms/vsmac-extensions-survey) (Criação de extensão do Visual Studio para Mac).

## <a name="see-also"></a>Veja também

- [Desenvolver extensões do Visual Studio (no Windows)](/visualstudio/extensibility/starting-to-develop-visual-studio-extensions)
