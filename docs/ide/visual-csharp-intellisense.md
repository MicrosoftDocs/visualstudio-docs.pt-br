---
title: C# IntelliSense
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- C#, IntelliSense
- IntelliSense [C#]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 882e9471646d83434c18f18811f9f6f693d2e551
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39513394"
---
# <a name="c-intellisense"></a>C# IntelliSense

O C# IntelliSense fica disponível durante a codificação no editor e durante a depuração na janela Comando do [Modo imediato](../ide/reference/immediate-window.md).

## <a name="completion-lists"></a>Listas de conclusão

As listas de preenchimento do IntelliSense no C# contêm tokens de Listar Membros, Completar Palavra e muito mais. Ele fornece acesso rápido a:

- Membros de um tipo ou namespace

- Variáveis, comandos e nomes de funções

- Trechos de código

- Palavras-chave de linguagem

- Métodos de extensão

A lista de conclusão no C# também é inteligente o suficiente para filtrar tokens irrelevantes e pré-selecionar um token com base no contexto. Para obter mais informações, consulte [Listas de conclusão filtradas](#filtered-completion-lists).

### <a name="code-snippets-in-completion-lists"></a>Trechos de código em listas de conclusão

No C#, a lista de preenchimento inclui trechos de código para ajudá-lo a inserir com facilidade corpos de código predefinidos no programa. Os trechos de código são exibidos na lista de conclusão como [texto de atalho](../ide/code-snippets-schema-reference.md#shortcut-element) do trecho. Para obter mais informações sobre os trechos de código disponíveis no C# por padrão, consulte [Trechos de código do C#](../ide/visual-csharp-code-snippets.md).

### <a name="language-keywords-in-completion-lists"></a>Palavras-chave de linguagem em listas de conclusão

No C#, a lista de preenchimento também inclui palavras-chave. Para obter mais informações sobre palavras-chave da linguagem C#, consulte [Palavras-chave do C#](/dotnet/csharp/language-reference/keywords/index).

### <a name="extension-methods-in-completion-lists"></a>Métodos de extensão em listas de conclusão

No C#, a lista de conclusão inclui métodos de extensão que estão no escopo.

> [!NOTE]
> A lista de conclusão não exibe todos os métodos de extensão para objetos <xref:System.String>.

Os métodos de extensão usam um ícone diferente dos métodos de instância. Para obter um guia de referência dos ícones de lista, confira [Modo de Exibição de Classe e ícones do Pesquisador de Objetos](../ide/class-view-and-object-browser-icons.md). Quando um método de instância e um método de extensão com o mesmo nome estão no escopo, a lista de preenchimento exibe o ícone do método de extensão.

### <a name="filtered-completion-lists"></a>Listas de preenchimento filtradas

O IntelliSense remove membros desnecessários da lista de preenchimento usando filtros. O C# filtra as listas de preenchimento exibidas para estes itens:

- **Interfaces e classes base**: o IntelliSense remove automaticamente itens das listas de conclusão de interface e de classe base, tanto nas listas de interface quanto nas listas de restrição de base de declaração de classe. Por exemplo, enumerações não aparecem na lista de preenchimento nas classes base, pois enumerações não podem ser usadas para as classes base. A lista de preenchimento de classes base contém apenas interfaces e namespaces. Se você selecionar um item na lista e, em seguida, digitar uma vírgula, o IntelliSense removerá as classes base da lista de preenchimento, pois o C# não dá suporte à herança múltipla. O mesmo comportamento também ocorre em cláusulas de restrição.

- **Atributos**: ao aplicar um atributo a um tipo, a lista de conclusão é filtrada para que ela tenha somente os tipos que descendem dos namespaces que contêm esses tipos, como <xref:System.Attribute>.

- **Cláusulas Catch**

- **Inicializadores de objeto**: somente os membros que podem ser inicializados serão exibidos na lista de conclusão.

- **Palavra-chave new**: ao digitar `new` e, em seguida, pressionar o **Espaço**, uma lista de conclusão é exibida. Um item é selecionado na lista automaticamente, de acordo com o contexto no código. Por exemplo, os itens são selecionados automaticamente na lista de preenchimento em busca de declarações e instruções de retorno nos métodos.

- **Palavra-chave enum**: ao pressionar o **Espaço** após um sinal de igual para uma atribuição de enum, uma lista de conclusão será exibida. Um item é selecionado na lista automaticamente, de acordo com o contexto no código. Por exemplo, os itens serão selecionados automaticamente na lista de conclusão depois que você digitar a palavra-chave retorno e quando fizer uma declaração.

- **Operadores as e is**: uma lista de conclusão filtrada é exibida automaticamente ao pressionar o **Espaço** depois de digitar a palavra-chave `as` ou `is`.

- **Eventos**: ao digitar a palavra-chave `event`, a lista de conclusão conterá apenas os tipos de delegado.

- A **ajuda do parâmetro** classifica automaticamente para a primeira sobrecarga de método que corresponde aos parâmetros, conforme eles são inseridos. Se houver várias sobrecargas de método disponíveis, será possível usar as setas para cima e para baixo para navegar para a próxima sobrecarga possível na lista.

### <a name="most-recently-used-members"></a>Membros usados mais recentemente

O IntelliSense lembra os membros selecionados recentemente na caixa pop-up [Listar Membros](../ide/using-intellisense.md) quanto à conclusão automática de nome de objeto. Na próxima vez que você usar a **Lista de Membros**, os membros usados mais recentemente serão mostrados na parte superior. O histórico dos membros mais usados recentemente é limpo entre cada sessão do Visual Studio.

### <a name="override"></a>override

Ao digitar [override](/dotnet/csharp/language-reference/keywords/override) e, em seguida, pressionar **Espaço**, o IntelliSense exibe todos os membros da classe base válidos que podem ser substituídos em uma caixa de listagem pop-up. Digitar o tipo de retorno do método após `override` solicitará que o IntelliSense mostre apenas os métodos que retornam o mesmo tipo. Quando o IntelliSense não conseguir encontrar nenhuma correspondência, ele exibirá todos os membros da classe base.

### <a name="ai-enhanced-intellisense"></a>IntelliSense aprimorado com a inteligência artificial

Você pode instalar uma [extensão do IntelliCode](/visualstudio/intellicode/intellicode-visual-studio) experimental para Visual Studio, a qual fornece listas de conclusão do IntelliSense aprimoradas com a inteligência artificial. Essa extensão prevê a API mais provavelmente correta a ser usada, em vez de apenas apresentar uma lista de membros em ordem alfabética. Ele usa os seus padrões e contexto de código atuais para fornecer a lista dinâmica.

## <a name="automatic-code-generation"></a>Geração automática de código

### <a name="add-using"></a>Adicionar usando

A operação **Adicionar usando** do IntelliSense adiciona automaticamente a diretiva `using` necessária em seu arquivo de código. Esse recurso permite que você mantenha o foco no código que está sendo escrito, em vez de precisar mudar o foco para outra parte do código.

Para iniciar a operação **Adicionar usando**, posicione o cursor em uma referência de tipo que não pode ser resolvida. Por exemplo, quando você cria um aplicativo de console e, em seguida, adiciona `XmlTextReader` ao corpo do método `Main`, um rabisco vermelho aparece nessa linha de código, porque a referência de tipo não pode ser resolvida. Em seguida, você pode invocar a operação **Adicionar usando** por meio da **Ação Rápida**. A **Ação Rápida** fica visível apenas quando o cursor está posicionado no tipo não associado.

![Adicionar usando, imagem expandida da ação rápida](../ide/media/addusing-quickaction.png)

Clique no ícone de lâmpada e, em seguida, escolha **using System.Xml;** para adicionar automaticamente a diretiva using.

### <a name="remove-and-sort-usings"></a>Remover e classificar usos

A opção **Remover e Classificar Usos** classifica e remove as declarações `using` e `extern` sem alterar o comportamento do código-fonte. Ao longo do tempo, os arquivos de origem poderão ficar sobrecarregados e ser difíceis de serem lidos devido a diretivas `using` desnecessárias e desorganizadas. A opção **Remover e Classificar Usos** compacta o código-fonte ao remover as diretivas `using` não utilizadas e melhora a legibilidade com sua classificação. No menu **Editar**, selecione **IntelliSense** e, depois, selecione **Organizar Usos**.

### <a name="implement-interface"></a>Implementar interface

O IntelliSense fornece uma opção para ajudá-lo a implementar uma [interface](/dotnet/csharp/language-reference/keywords/interface) enquanto estiver trabalhando no editor de códigos. Normalmente, para implementar uma interface corretamente, é necessário criar uma declaração de método para cada membro da interface na classe. Usando o IntelliSense, depois de digitar o nome de uma interface em uma declaração de classe, uma lâmpada de **Ações Rápidas** é exibida. A lâmpada oferece a opção de implementar a interface automaticamente, usando a nomenclatura explícita ou implícita. Na nomenclatura explícita, as declarações de método levam o nome da interface. Na nomenclatura implícita, as declarações de método não indicam a interface à qual pertencem. Um método de interface explicitamente nomeado só pode ser acessado por meio de uma instância de interface, e não por meio de uma instância de classe. Para obter mais informações, consulte [Implementação explícita da interface](/dotnet/csharp/programming-guide/interfaces/explicit-interface-implementation).

A implementação da interface gera o número mínimo de stubs de método necessários para atender à interface. Se uma classe base implementar partes da interface, os stubs não serão regenerados.

### <a name="implement-abstract-base-class"></a>Implementar classe base abstrata

O IntelliSense fornece uma opção para ajudá-lo a implementar membros de uma classe base abstrata automaticamente enquanto estiver trabalhando no editor de códigos. Normalmente, para implementar membros de uma classe base abstrata, é necessário criar uma nova definição de método para cada método da classe base abstrata na classe derivada. Usando o IntelliSense, depois de digitar o nome de uma classe base abstrata em uma declaração de classe, uma lâmpada **Ações Rápidas** é exibida. A lâmpada oferece a opção de implementar os métodos de classe base automaticamente.

Os stubs de método gerados pelo recurso **Implementar Classe Base Abstrata** são modelados pelo trecho de código definido no arquivo *MethodStub.snippet*. Os trechos de código são modificáveis. Para obter mais informações, consulte [Passo a passo: Criar um trecho de código](../ide/walkthrough-creating-a-code-snippet.md).

### <a name="generate-from-usage"></a>Gerar com base no uso

O recurso **Gerar com Base no Uso** permite usar classes e membros antes de defini-los. É possível gerar um stub para qualquer classe, construtor, método, propriedade, campo ou enumeração que você deseja usar, mas que ainda não foi definido. É possível gerar novos tipos e membros sem sair do local atual no código. Isso minimiza a interrupção do fluxo de trabalho.

Um sublinhado vermelho ondulado é exibido em cada identificador indefinido. Ao posicionar o ponteiro do mouse sobre o identificador, uma mensagem de erro é exibida em uma dica de ferramenta. Para exibir as opções apropriadas, é possível usar um dos seguintes procedimentos:

- Clique no identificador indefinido. Uma lâmpada de **Ações Rápidas** é exibida abaixo do identificador. Clique na lâmpada.

- Clique no identificador indefinido e, em seguida, pressione **Ctrl**+**.** (**Ctrl** + ponto).

- Clique com o botão direito do mouse no identificador indefinido e, em seguida, clique em **Ações Rápidas e Refatorações**.

As opções exibidas podem incluir as seguintes:

- **Gerar propriedade**

- **Gerar campo**

- **Gerar método**

- **Gerar classe**

- **Gerar novo tipo** (para uma classe, um struct, uma interface ou enumeração)

## <a name="generate-event-handlers"></a>Gerar manipuladores de eventos

No editor de códigos, o IntelliSense pode ajudá-lo a vincular métodos (manipuladores de eventos) a campos de evento.

Ao digitar o operador `+=` após um campo de evento em um arquivo *.cs*, o IntelliSense mostra a opção de pressionar a tecla **Tab**. Isso insere uma nova instância de um delegado que aponta para o método que manipula o evento.

![Botão Vínculo Automático](../ide/media/vxautohookup.gif)

Se você pressionar a tecla **Tab**, o IntelliSense concluirá a instrução para você automaticamente e exibirá a referência do manipulador de eventos como um texto selecionado no editor de códigos. Para concluir o vínculo automático de evento, o IntelliSense solicita que você pressione a tecla **Guia** novamente para criar um stub vazio para o manipulador de eventos.

![Gerar manipulador de eventos](../ide/media/vxgenerateeventhandler.gif)

> [!NOTE]
> Se um novo delegado criado pelo IntelliSense referenciar um manipulador de eventos existente, o IntelliSense comunicará essas informações na dica de ferramenta. Em seguida, você pode modificar essa referência; o texto já está selecionado no editor de códigos. Caso contrário, o vínculo automático de evento será concluído nesse ponto.

Se você pressionar a **Guia**, o IntelliSense criará um stub de um método com a assinatura correta e colocará o cursor no corpo do manipulador de eventos.

> [!NOTE]
> Use o comando **Navegação Regressiva** no menu **Exibir** (**Ctrl**+**-**) para retornar à declaração de vínculo de evento.

## <a name="see-also"></a>Consulte também

- [Usar o IntelliSense](../ide/using-intellisense.md)
- [Visual Studio IDE](../ide/visual-studio-ide.md)