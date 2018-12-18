---
title: Editando o código do Python
description: A edição de Python no Visual Studio fornece recursos de IntelliSense, snippets de código e navegação, juntamente com formatação, lint e refatoração.
ms.date: 11/19/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: b8d92f16f869de400d0d66ff44c1848abffde67f
ms.sourcegitcommit: f61ad0e8babec8810295f039e67629f4bdebeef0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "52001263"
---
# <a name="edit-python-code"></a>Editar código do Python

Como você passa muito tempo dedicado ao desenvolvimento no editor de códigos, o [Suporte para Python no Visual Studio](installing-python-support-in-visual-studio.md) fornece funcionalidade para ajudá-lo a ser mais produtivo. Os recursos incluem o realce de sintaxe do IntelliSense, o preenchimento automático, a ajuda da assinatura, as substituições de método, a pesquisa e a navegação.

O editor também é integrado à janela **Interativa** no Visual Studio, facilitando a troca do código entre as duas. Confira [Etapa 3 do tutorial: Usar a janela do REPL Interativo](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md) e [Usar a janela Interativa – comando Enviar para Interativa](python-interactive-repl-in-visual-studio.md#send-to-interactive-command) para obter detalhes.

|   |   |
|---|---|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo (Microsoft Virtual Academy)](https://mva.microsoft.com/en-US/training-courses-embed/python-tools-for-visual-studio-2017-18121/Video-Editing-Python-Code-r2iQH5LWE_4605918567) para uma demonstração da edição do código Python (2min30s).|

Para obter uma documentação geral sobre edição do código no Visual Studio, confira [Recursos do editor de código](../ide/writing-code-in-the-code-and-text-editor.md). Confira também [Estrutura de tópicos](../ide/outlining.md), que ajuda você a manter o foco em seções específicas do código.

Use também o **Pesquisador de Objetos** do Visual Studio (**Exibir** > **Outras Janelas** > **Pesquisador de Objetos** ou **Ctrl**+**W** > **J**) para inspecionar as classes Python definidas em cada módulo e as funções definidas nessas classes.

## <a name="intellisense"></a>IntelliSense

O IntelliSense fornece [preenchimentos](#completions), [ajuda da assinatura](#signature-help), [informações rápidas](#quick-info) e [coloração de código](#code-coloring). O Visual Studio 2017 versão 15.7 e posteriores também dão suporte a [dicas de tipo](#type-hints).

Para melhorar o desempenho, o IntelliSense no **Visual Studio 2017 versão 15.5** e anteriores depende do banco de dados de preenchimento que é gerado para cada ambiente do Python no projeto. Os bancos de dados podem precisar de atualização se você adicionar, remover ou atualizar os pacotes. O status do banco de dados é mostrado na janela **Ambientes do Python** (um irmão do **Gerenciador de Soluções**) na guia **IntelliSense** (confira [Referência da janela Ambientes](python-environments-window-tab-reference.md#intellisense-tab)).

O **Visual Studio 2017 versão 15.6** e posterior usa um modo diferente para fornecer as conclusões de IntelliSense que não são dependentes do banco de dados.

### <a name="completions"></a>Preenchimentos

Preenchimentos aparecem como instruções, identificadores e outras palavras que podem ser inseridas adequadamente na localização atual no editor. O que é mostrado na lista baseia-se no contexto e é filtrado para omitir opções incorretas ou que desviam a atenção. Em geral, os preenchimentos são disparados com a digitação de diferentes instruções (como `import`) e operadores (incluindo um ponto final), mas é possível fazer com que eles apareçam a qualquer momento digitando **Ctrl**+**J** > **Espaço**.

![Preenchimento de membro](media/code-editing-completions-simple.png)

Quando uma lista de preenchimento é aberta, é possível pesquisar o preenchimento que você deseja usando as teclas de direção, o mouse ou continuando a digitação. Conforme você digita mais letras, a lista é filtrada ainda mais para mostrar os prováveis preenchimentos. Você também pode usar atalhos, como:

- Digitar letras que não estão no início do nome, como “parse” para encontrar “argparse”
- Digitar apenas letras que estão no início de palavras, como “abc” para encontrar “AbstractBaseClass” ou “air” para encontrar “as_integer_ratio”
- Ignorar letras, como “b64” para encontrar “base64”

Alguns exemplos:

![Preenchimento de membro com filtragem](media/code-editing-completion-filtering.png)

Os preenchimentos de membro aparecem automaticamente quando você digita um ponto final depois de uma variável ou um valor, juntamente com os métodos e os atributos dos tipos possíveis. Se uma variável puder ser de mais de um tipo, a lista incluirá todas as possibilidades de todos os tipos, com informações extras para indicar quais tipos dão suporte a cada preenchimento. Quando um preenchimento tem o suporte de todos os tipos possíveis, ele é mostrado sem anotação.

![Preenchimento de membro em vários tipos](media/code-editing-completion-types.png)

Por padrão, os membros “dunder” (membros que começam e terminam com um sublinhado duplo) não são mostrados. Em geral, esses membros não devem ser acessados diretamente. Se você precisar de um, no entanto, digitar o sublinhado duplo à esquerda adiciona esses preenchimentos à lista:

![Preenchimento de membro privado](media/code-editing-completion-dunder.png)

As instruções `import` e `from ... import` exibem uma lista de módulos que podem ser importados. Com `from ... import`, a lista inclui os membros que podem ser importados do módulo especificado.

![Preenchimento de importação](media/code-editing-completion-import.png)

As instruções `raise` e `except` exibem listas de classes que provavelmente são tipos de erros. A lista pode não incluir todas as exceções definidas pelo usuário, mas ajuda você a encontrar as exceções internas adequadas rapidamente:

![Preenchimento de exceção](media/code-editing-completion-exception.png)

Digitar @ inicia um decorador e mostra os decoradores possíveis. Muitos desses itens não podem ser usados como decoradores, verifique a documentação da biblioteca para determinar qual deles usar.

![Preenchimento de decorador](media/code-editing-completion-decorator.png)

> [!Tip]
> Configure o comportamento de preenchimentos por meio de **Ferramentas** > **Opções** > **Editor de Texto** > **Python** > **Avançado**. Dentre eles, a opção **Filtrar lista com base na cadeia de caracteres de pesquisa** aplica a filtragem de sugestões de preenchimento enquanto você digita (o padrão é marcado) e a opção **O preenchimento de membro exibe a interseção dos membros** mostra apenas os preenchimentos compatíveis com todos os tipos possíveis (o padrão é desmarcado). Consulte [Opções – Resultados de Conclusão](python-support-options-and-settings-in-visual-studio.md#completion-results).

### <a name="type-hints"></a>Dicas de tipo

*Visual Studio 2017 versão 15.7 e posteriores.*

As "dicas de tipo" no Python 3.5+ ([PEP 484](https://www.python.org/dev/peps/pep-0484/)) (python.org) são uma sintaxe de anotação para funções e classes que indicam os tipos de argumentos, valores de retorno e atributos de classe. O IntelliSense exibe dicas de tipo quando você focaliza argumentos, variáveis e chamadas de função que contêm essas anotações.

No exemplo a seguir, a classe `Vector` é declarada como `List[float]` e a função `scale` contém dicas de tipo para seus argumentos e o valor retornado. Passar o mouse sobre uma chamada da função mostra as dicas de tipo:

![Passar o mouse sobre uma chamada de função para revelar dicas de tipo](media/code-editing-type-hints1.png)

No exemplo a seguir, você pode ver como os atributos anotados da classe `Employee` aparecem no pop-up de conclusão de IntelliSense para um atributo:

![Conclusão do IntelliSense exibindo dicas de tipo](media/code-editing-type-hints2.png)

Também é útil validar as dicas de tipo em todo o seu projeto, pois erros normalmente não aparecerão até o tempo de execução. Para isso, o Visual Studio integra a ferramenta padrão da indústria MyPy usando o comando de menu de contexto **Python** > **Executar MyPy** no **Gerenciador de Soluções**:

![Execute o comando de menu de contexto MyPy no Gerenciador de Soluções](media/code-editing-type-hints-run-mypy.png)

A execução do comando solicitará que você instale o pacote do MyPy, se necessário. Em seguida, o Visual Studio executará o MyPy para validar as dicas de tipo em todos os arquivos Python do projeto. Os erros aparecem na janela **Lista de Erros** do Visual Studio. Selecionar um item na janela navega para a linha apropriada no seu código.

Como um exemplo simples, a definição de função a seguir contém uma dica de tipo que indica que o argumento `input` é do tipo `str`, enquanto a chamada para essa função tenta passar um número inteiro:

```python
def commas_to_colons(input: str):
    items = input.split(',')
    items = [x.strip() for x in items]
    return ':'.join(items)

commas_to_colons(1)
```

Usar o comando **Execute Mypy** neste código gera o seguinte erro:

![Exemplo de resultado de MyPy validando dicas de tipo](media/code-editing-type-hints-validation-error.png)

> [!Tip]
> Para as versões do Python anteriores à 3.5, o Visual Studio também exibe dicas de tipo fornecidas por meio de *arquivos stub* (*.pyi*). Você pode usar arquivos stub sempre que não quiser incluir dicas de tipo diretamente no código, ou quando quiser criar dicas de tipo para uma biblioteca que não as usa diretamente. Para obter mais informações, confira [Criar stubs para módulos do Python](https://github.com/python/mypy/wiki/Creating-Stubs-For-Python-Modules) no wiki de projeto do MyPy.
>
> No momento, o Visual Studio não dá suporte a dicas de tipo nos comentários.

### <a name="signature-help"></a>Ajuda da assinatura

Ao escrever o código que chama uma função, a ajuda da assinatura é exibida quando você digita o `(` de abertura e exibe as informações de parâmetro e documentação disponíveis. Exiba-a também com **Ctrl**+**Shift**+**Espaço** dentro de uma chamada de função. As informações exibidas dependem das cadeias de caracteres de documentação no código-fonte da função, mas incluem os valores padrão.

![Ajuda da assinatura](media/code-editing-signature-help.png)

> [!Tip]
> Para desabilitar a ajuda da assinatura, acesse **Ferramentas** > **Opções** > **Editor de Texto** > **Python** > **Geral** e desmarque a opção **Preenchimento de declaração** > **Informações de parâmetro**.

### <a name="quick-info"></a>Informações rápidas

Focalizar o ponteiro do mouse em um identificador exibe uma dica de ferramenta Informações Rápidas. Dependendo do identificador, as Informações Rápidas poderão exibir os possíveis valores ou tipos, toda a documentação disponível, os tipos de retorno e os locais de definição:

![Informação Rápida](media/code-editing-quick-info.png)

### <a name="code-coloring"></a>Coloração de código

A coloração de código usa informações da análise de código para colorir variáveis, instruções e outras partes do código. Por exemplo, as variáveis que se referem a módulos ou classes podem ser exibidas em uma cor diferente da de funções ou outros valores e os nomes de parâmetro são exibidos em uma cor diferente da que variáveis locais ou globais. (Por padrão, as funções não são exibidas em negrito):

![Coloração de código](media/code-editing-code-coloring.png)

Para personalizar as cores, acesse **Ferramentas** > **Opções** > **Ambiente** > **Fontes e Cores** e modifique as entradas do **Python** na lista **Exibir itens**:

![Opções de Fontes e Cores](media/code-editing-customize-colors.png)

> [!Tip]
> Para desabilitar a coloração de código, acesse **Ferramentas** > **Opções** > **Editor de Texto** > **Python** > **Avançado** e desmarque **Opções Diversas** > **Colorir nomes com base no tipo**. Consulte [Opções – Opções diversas](python-support-options-and-settings-in-visual-studio.md#miscellaneous-options).

## <a name="code-snippets"></a>Snippets de código

Snippets de código são fragmentos de código que podem ser inseridos nos arquivos digitando um atalho e pressionando **Tab** ou usando os comandos **Editar** > **IntelliSense** > **Inserir Snippet de Código** e **Envolver Com**, selecionando **Python** e, em seguida, selecionando o snippet desejado.

Por exemplo, `class` é um atalho para um snippet de código que insere uma definição de classe. Você vê o snippet aparecer na lista de conclusão automática ao digitar `class`:

![Snippet de código para o atalho de classe](media/code-editing-code-snippet-class.png)

Pressionar **Tab** gera o restante da classe. Em seguida, digite sobre o nome e a lista de bases, movendo entre os campos realçados com **Tab** e pressionando **Enter** para começar a digitar o corpo.

![Destaques em áreas de um snippet de código para você preencher](media/code-editing-code-snippets.png)

### <a name="menu-commands"></a>Comandos de menu

Ao usar o comando de menu **Editar** > **IntelliSense** > **Inserir Snippet de Código**, primeiro selecione **Python** e, em seguida, um snippet de código:

![Como selecionar um snippet de código por meio do comando Inserir Snippet de Código](media/code-editing-code-snippet-insert.png)

Da mesma forma, o comando **Editar** > **IntelliSense** > **Envolver com** coloca a seleção atual no editor de texto dentro de um elemento estrutural escolhido. Por exemplo, suponha que você tivesse um trecho de código semelhante ao seguinte:

```python
sum = 0
for x in range(1, 100):
    sum = sum + x
```

Selecionar esse código e escolher o comando **Envolver com** exibe uma lista de snippets de código disponíveis. A escolha de **def** na lista coloca o código selecionado em uma definição de função, e você pode usar a tecla **Tab** para navegar entre os argumentos e o nome de função realçados:

![Usando o comando Envolver com para snippets de código](media/code-editing-code-snippet-surround-with.png)

### <a name="examine-available-snippets"></a>Examinar snippets disponíveis

Veja os snippets de código disponíveis no **Gerenciador de Snippets de Código**, abertos usando o comando de menu **Ferramentas** > **Gerenciador de Snippets de Código** e selecionando **Python** como a linguagem:

![Gerenciador de Snippets de Código](media/code-editing-code-snippets-manager.png)

Para criar seus próprios snippets de código, confira [Passo a passo: Criar um snippet de código](../ide/walkthrough-creating-a-code-snippet.md).

Se você escrever um ótimo snippet de código que gostaria de compartilhar, fique à vontade para postá-lo em linhas gerais e [contar para nós](https://github.com/Microsoft/PTVS/issues). Talvez possamos incluí-lo em uma versão futura do Visual Studio.

## <a name="navigate-your-code"></a>Navegar pelo seu código

O suporte do Python no Visual Studio fornece vários meios para navegar rapidamente pelo código, incluindo bibliotecas para as quais o código-fonte está disponível: a [barra de navegação](#navigation-bar), [**Ir para definição**](#go-to-definition), [**Navegar Para**](#navigate-to) e [**Localizar Todas as Referências**](#find-all-references). Use também o [**Pesquisador de Objetos**](../ide/viewing-the-structure-of-code.md#BKMK_ObjectBrowser) do Visual Studio.

### <a name="navigation-bar"></a>Barra de navegação

A barra de navegação é exibida na parte superior de cada janela do editor e inclui uma lista de dois níveis de definições. A lista suspensa à esquerda contém definições de nível superior de classe e função no arquivo atual; a lista suspensa à direita exibe uma lista de definições dentro do escopo mostrado à esquerda. Conforme você usa o editor, as listas são atualizadas para mostrar o contexto atual e você também pode selecionar uma entrada dessas listas para ir diretamente para ela.

![Barra de navegação](media/code-editing-navigation-bar.png)

> [!Tip]
> Para ocultar a barra de navegação, acesse **Ferramentas** > **Opções** > **Editor de Texto** > **Python** > **Gerais** e desmarque **Configurações** > **Barra de navegação**.

### <a name="go-to-definition"></a>Ir para definição

O comando **Ir Para Definição** vai rapidamente do uso de um identificador (como um nome de função, classe ou variável) para o código-fonte em que ele está definido. Invoque-o clicando com o botão direito do mouse em um identificador e selecionando **Ir para definição** ou colocando o cursor no identificador e pressionando **F12**. Ele funciona em todo o código e nas bibliotecas externas, desde que o código-fonte esteja disponível. Se o código-fonte da biblioteca não estiver disponível, o comando **Ir para definição** irá para a instrução `import` relevante de uma referência de módulo ou exibirá um erro.

![Ir para definição](media/code-editing-go-to-definition.png)

### <a name="navigate-to"></a>Navegar para

O comando **Editar** > **Navegar Para** (**Ctrl**+**,**) exibe uma caixa de pesquisa no editor em que é possível digitar qualquer cadeia de caracteres e ver as possíveis correspondências no código que definem uma função, uma classe ou uma variável que contém a cadeia de caracteres. Esse recurso fornece uma funcionalidade semelhante a **Ir Para Definição**, mas sem a necessidade de localizar um uso de um identificador.

Clicar duas vezes em um nome ou selecioná-lo com teclas de direção e **Enter** levará você para a definição desse identificador.

![Navegar para](media/code-editing-navigate-to.png)

### <a name="find-all-references"></a>Localizar Todas as Referências

O comando **Localizar Todas as Referências** é uma maneira útil de descobrir o local em que um identificador específico é definido e usado, incluindo importações e atribuições. Invoque-o clicando com o botão direito do mouse em um identificador e selecionando **Localizar Todas as Referências** ou colocando o cursor no identificador e pressionando **Shift**+**F12**. Clicar duas vezes em um item da lista navegará para sua localização.

![Resultados de Localizar Todas as Referências](media/code-editing-find-all-references.png)

## <a name="see-also"></a>Consulte também

- [Formatação](formatting-python-code.md)
- [Refatoração](refactoring-python-code.md)
- [Usar um linter](linting-python-code.md)
