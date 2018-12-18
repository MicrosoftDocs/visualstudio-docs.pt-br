---
title: Ferramentas F#
description: Saiba quais recursos do Visual Studio são compatíveis com o F#.
ms.date: 07/11/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- F# features [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 4512a6ad5efe519c203a764b18cdfc352ed6e81a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49921425"
---
# <a name="develop-with-visual-f-in-visual-studio"></a>Desenvolver com o Visual F# no Visual Studio

Este artigo inclui informações sobre os recursos do Visual Studio para o desenvolvimento do F#.

## <a name="install-f-support"></a>Instalar o suporte do F#

Para desenvolver com o F# no Visual Studio, primeiro instale a carga de trabalho **desenvolvimento para desktop do .NET**, caso ainda não tenha feito isso. Instale as cargas de trabalho do Visual Studio por meio do Instalador do Visual Studio, que pode ser aberto pela seleção de **Ferramentas** > **Obter Ferramentas e Recursos**.

![Carga de trabalho de desenvolvimento para desktop do .NET no Visual Studio](media/dotnet-desktop-development-workload.png)

## <a name="f-project-features"></a>Recursos de projeto do F#

Vários modelos de projeto e de item estão disponíveis para o F# no Visual Studio. A seguinte imagem mostra alguns dos modelos de projeto do F# para o .NET Core e o .NET Standard:

![Modelos de projeto do F# no Visual Studio](media/fsharp-project-templates.png)

A seguinte imagem mostra alguns dos modelos de item do F#:

![Modelos de item do F# no Visual Studio](media/fsharp-item-templates.png)

Para obter mais informações sobre os modelos de item para acesso a dados, confira [Provedores de tipos F#](/dotnet/fsharp/tutorials/type-providers/index).

A seguinte tabela resume os recursos nas propriedades do projeto para o F#:

|Configuração do projeto|Compatível com o F#?|Observações|
|---------------|----------------|-----|
|Arquivos de recurso|Sim||
|Configurações de build, depuração e referência|Sim||
|Multiplataforma|Sim||
|Ícone e manifesto|Não|Disponível por meio das opções da linha de comando do compilador.|
|Serviços de Cliente ASP.NET|Não||
|ClickOnce|Não|Use um projeto de cliente em outra linguagem do .NET Framework, se aplicável.|
|Nomenclatura forte|Não|Disponível por meio das opções da linha de comando do compilador.|
|Publicação e controle de versão de assembly|Não||
|Análise de código|Não|As ferramentas de análise de código podem ser executadas manualmente ou como parte de um comando pós-build.|
|Segurança (alterar níveis de confiança)|Não||

## <a name="project-designer"></a>Designer de Projeto

O **Designer de Projeto** consiste no agrupamento de várias páginas de propriedades do projeto por funcionalidade relacionada. As páginas disponíveis para projetos do F# são, principalmente, um subconjunto daquelas disponíveis para outras linguagens e são descritas na tabela a seguir. Links são fornecidos para a página correspondente do **Designer de Projeto** do C#.

|Página do Designer de Projeto|Links relacionados|Descrição|
| - |-------------|-----------|
|Aplicativo|[Página Aplicativo, Designer de Projeto](reference/application-page-project-designer-csharp.md)|Permite que você especifique configurações e propriedades no nível do aplicativo, como se estivesse criando uma biblioteca ou um arquivo executável, qual é a versão de destino do .NET Framework para o aplicativo e informações sobre o local de armazenamento dos arquivos de recurso usados pelo aplicativo.|
|Build|[Página de build, Designer de Projeto](reference/build-page-project-designer-csharp.md)|Permite que você controle como o código é compilado.|
|Compilar Eventos|[Página Eventos de Build, Designer de Projeto](reference/build-events-page-project-designer-csharp.md)|Permite que você especifique os comandos a serem executados antes ou depois de uma compilação.|
|Depurar|[Página de Depuração, Designer de Projeto](reference/debug-page-project-designer.md)|Permite que você controle como o aplicativo é executado durante a depuração. Isso inclui os comandos a serem usados e o diretório inicial do aplicativo, bem como os modos de depuração especiais que você deseja habilitar, como o código nativo e o SQL.|
|Pacote (somente SDK do .NET)|N/D|Permite que você defina metadados do Pacote NuGet durante a publicação como um pacote NuGet.|
|Caminhos de referência|[Gerenciar referências em um projeto](managing-references-in-a-project.md)|Permite que você especifique o local em que pesquisar assemblies dos quais o código depende.|
|Recursos (somente SDK do .NET)|N/D|Permite que você gere e gerencie um arquivo de recurso padrão.|

### <a name="f-specific-settings"></a>Configurações específicas do F#

A seguinte tabela resume as configurações específicas do F#:

|Página do Designer de Projeto|Configuração|Descrição|
| - |-------|-----------|
|Build|Gerar chamadas da parte final|Se ela estiver selecionada, habilitará o uso da instrução MSIL (Microsoft Intermediate Language) da parte final. Isso faz com que o registro de ativação seja reutilizado para funções recursivas da parte final. Equivalente à opção do compilador `--tailcalls`.|
|Build|Outros sinalizadores|Permite que você especifique opções adicionais de linha de comando do compilador.|

## <a name="code-and-text-editor-features"></a>Recursos do editor de código e texto

Há suporte para os seguintes recursos dos editores de código e de texto do Visual Studio no F#:

|Recurso|Descrição|Compatível com o F#?|
|-------|-----------|----------------|
|Comentar automaticamente|Permite que você comente ou remova a marca de comentário das seções de código.|Sim|
|Formatar automaticamente|Reformata o código com recuo e estilo padrão.|Não|
|Indicadores|Permite que você salve locais no editor.|Sim|
|Alterar recuo|Recua ou desfaz o recuo das linhas selecionadas.|Sim|
|Recuo inteligente|Recua e desfaz o recuo do cursor automaticamente, de acordo com as regras de escopo do F#.|Sim|
|[Localizar e substituir texto](finding-and-replacing-text.md)|Permite que você faça pesquisas em um arquivo, um projeto ou uma solução e, potencialmente, altere o texto.|Sim|
|Ir para definição de API do .NET Framework|Quando o cursor estiver posicionado em uma API do .NET Framework, essa configuração mostrará o código gerado com base nos metadados do .NET Framework.|Não|
|Ir para definição de API definida pelo usuário|Quando o cursor estiver em uma entidade de programa definida, essa configuração moverá o cursor para o local no código em que a entidade foi definida.|Sim|
|Ir para a linha|Permite que você vá para uma linha específica em um arquivo, por número de linha.|Sim|
|Barras de navegação na parte superior do arquivo|Permite que você vá para locais no código, por exemplo, por nome da função.|Sim|
|Diretrizes de estrutura de bloco|Mostra as diretrizes que indicam os escopos do F#, que podem ser focalizados para obter uma versão prévia.|Sim|
|[Estrutura de tópicos](outlining.md)|Permite que você recolha as seções do código para criar uma exibição mais compacta.|Sim|
|Tabular|Converte espaços em tabulações.|Sim|
|Colorização de tipo|Mostra os nomes de tipo definidos em uma cor especial.|Sim|
|Localização Rápida. Confira Localização Rápida, Janela Localizar e Substituir.|Permite que você faça pesquisas em um arquivo ou um projeto.|Sim|
|**CTRL**+**clique** para Ir para Definição|Permite que você mantenha a tecla **Ctrl** pressionada e clique em um símbolo do F# para invocar a opção Ir para Definição.|Sim|
|Ir para definição de QuickInfo|Símbolos clicáveis dentro das dicas de ferramenta que invocam a opção Ir para Definição.|Sim|
|Ir para Todos|Permite a navegação global de correspondência difusa para todos os constructos do F# por meio de **Ctrl**+**T**.|Sim|
|Renomeação embutida|Renomeia todas as ocorrências de um símbolo embutido.|Sim|
|Localizar todas as Referências|Localiza todas as ocorrências de um símbolo em uma base de código.|Sim|
|Simplificar a correção de código do nome|Remove os qualificadores desnecessários para símbolos do F#.|Sim|
|Remover correção de código de instrução `open` não utilizada|Remove todas as instruções `open` desnecessárias de um documento.|Sim|
|Correção de código do valor não utilizada|Sugere a renomeação de um identificador não utilizado para sublinhado.|Sim|

Para obter informações gerais sobre como editar o código no Visual Studio, bem como os recursos do editor de texto, confira [Escrever o código no editor](writing-code-in-the-code-and-text-editor.md).

## <a name="intellisense-features"></a>Recursos do IntelliSense

A seguinte tabela resume os recursos do IntelliSense compatíveis e não compatíveis com o F#:

|Recurso|Descrição|Compatível com o F#?|
|-------|-----------|----------------|
|Implementar interfaces automaticamente|Gera os stubs de código para os métodos de interface.|Sim|
|Snippets de código|Injeta o código de uma biblioteca de constructos de codificação comuns em tópicos.|Não|
|Completar Palavra|Economiza tempo de digitação preenchendo palavras e nomes conforme você digita.|Sim|
|Conclusão automática|Quando essa opção está habilitada, faz com que o preenchimento de palavras selecione a primeira correspondência conforme você digita, em vez de esperar que você selecione uma opção ou pressione **Ctrl**+**Espaço**.|Sim|
|Oferecer preenchimento para símbolos em namespaces não abertos|Com o preenchimento automático, um símbolo correspondente que reside em um namespace não aberto é sugerido, oferecendo o preenchimento com a instrução `open` correspondente, quando selecionado.|Sim|
|Gerar elementos de código|Permite que você gere o código de stub para uma variedade de constructos.|Não|
|Listar Membros|Quando você digita o operador de acesso de membro (.), essa opção mostra os membros de um tipo.|Sim|
|Organizar usings/open|Organiza os namespaces referenciados por instruções **using** no C# ou diretivas **open** no F#.|Não|
|Informações de Parâmetro|Mostra informações úteis sobre os parâmetros conforme você digita uma chamada de função.|Sim|
|Informação Rápida|Exibe a declaração completa de um identificador no código.|Sim|
|Preenchimento automático de chaves|Preenche automaticamente constructos de sintaxe semelhantes à chave do F# de maneira transacional.|Sim|

Para obter informações gerais sobre o IntelliSense, confira [Usar o IntelliSense](using-intellisense.md).

## <a name="debugging-features"></a>Recursos de depuração

A seguinte tabela resume os recursos disponíveis ao depurar o código F#:

|Recurso|Descrição|Compatível com o F#?|
|-------|-----------|----------------|
|Janela Autos|Mostra variáveis automáticas ou temporárias.|Não|
|Pontos de interrupção|Permite que você pause a execução de código em pontos específicos durante a depuração.|Sim|
|Pontos de interrupção condicionais|Permite pontos de interrupção que testam uma condição que determina se a execução deve ser colocada em pausa.|Sim|
|Editar e continuar|Permite que o código seja modificado e compilado durante a depuração de um programa em execução sem interromper e reiniciar o depurador.|Não|
|Avaliador de expressão|Avalia e executa o código em tempo de execução.|Não, mas o avaliador de expressão C# pode ser usado, embora seja necessário usar a sintaxe C#.|
|Depuração de histórico|Permite que você intervenha no código executado anteriormente.|Sim|
|Janela Locais|Mostra as variáveis e os valores definidos localmente.|Sim|
|Executar até o cursor|Permite que você execute o código até que a linha que contém o cursor seja atingida.|Sim|
|Entrar em|Permite que você avance a execução e passe para qualquer chamada de função.|Sim|
|Depuração Parcial|Permite que você avance a execução no registro de ativação atual e passe por qualquer chamada de função.|Sim|

Para obter informações gerais sobre o depurador do Visual Studio, confira [Depuração no Visual Studio](../debugger/index.md).

## <a name="additional-tools"></a>Ferramentas adicionais

A tabela a seguir resume o suporte para o F# nas ferramentas do Visual Studio.

|Ferramenta|Descrição|Compatível com o F#?|
|----|-----------|----------------|
|Hierarquia de chamadas|Exibe a estrutura aninhada das chamadas de função no código.|Não|
|Métricas de código|Coleta informações sobre o código, como contagens de linha.|Não|
|Exibição de Classe|Fornece uma exibição baseada em tipo do código em um projeto.|Não|
|[Janela Lista de Erros](reference/error-list-window.md)|Mostra uma lista de erros no código.|Sim|
|[F# Interativo](/dotnet/fsharp/tutorials/fsharp-interactive/)|Permite que você digite (ou copie e cole) o código F# e execute-o imediatamente, seja qual for o build do projeto. A janela do F# Interativo é um REPL (Loop Ler, Avaliar, Imprimir).|Sim|
|Pesquisador de Objetos|Permite que você veja os tipos em um assembly.|Os tipos F# exibidos em assemblies compilados não são exibidos exatamente como são criados. Você pode percorrer a representação compilada de tipos F#, mas não pode exibir os tipos como são exibidos no F#.|
|[Janela de Saída](reference/output-window.md)|Exibe a saída de build.|Sim|
|Análise de desempenho|Fornece ferramentas para avaliar o desempenho do código.|Sim|
|Janela de Propriedades|Exibe e permite a edição das propriedades do objeto no ambiente de desenvolvimento que tem o foco.|Sim|
|conexões de servidor|Fornece maneiras de interagir com uma variedade de recursos do servidor.|Sim|
|Gerenciador de Soluções|Permite que você veja e gerencie projetos e arquivos.|Sim|
|Lista de Tarefas|Permite que você gerencie itens de trabalho pertencentes ao código.|Não|
|Projetos de teste|Fornece recursos que ajudam você a testar o código.|Não|
|Caixa de Ferramentas|Exibe as guias que contêm objetos arrastáveis como controles e seções de texto ou de código.|Sim|

## <a name="see-also"></a>Consulte também

- [Guia do F# (.NET Framework)](/dotnet/fsharp/)
- [Introdução ao F# no Visual Studio](/dotnet/fsharp/get-started/get-started-visual-studio)