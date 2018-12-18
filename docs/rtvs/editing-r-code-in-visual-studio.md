---
title: Editar o código R
description: O Visual Studio fornece uma experiência de edição personalizada para R, mantendo todos os recursos e a capacidade de usar extensões.
ms.date: 11/05/2018
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: c1d44e6d316db2ddce799784169a11a06578fe7f
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220873"
---
# <a name="edit-r-code-in-visual-studio"></a>Editar o código R no Visual Studio

As RTVS (Ferramentas do R para Visual Studio) personalizam a experiência de edição do Visual Studio especificamente para R, mantendo todos os recursos e a capacidade de usar extensões. (Por exemplo, se preferir associações de teclas VIM, será possível instalar a [extensão VsVim](https://marketplace.visualstudio.com/items?itemName=JaredParMSFT.VsVim) gratuita do Visual Studio Marketplace.)

Além dos recursos neste artigo, veja também [IntelliSense](r-intellisense.md), [lint](linting-r-code.md), [snippets de código](code-snippets-for-r.md), e [R Markdown](rmarkdown-with-r-in-visual-studio.md).

## <a name="syntax-highlighting"></a>Realce de sintaxe

Além de colorir diferentes partes do código, como cadeias de caracteres, comentários e palavras-chave, as RTVS também realçam e habilitam links em comentários:

![Coloração de sintaxe para código R](media/editing-syntax-colors.png)

Para personalizar as fontes e determinadas cores de realce, selecione o comando **Ferramentas** > **Opções**, navegue até **Ambiente** > **Fontes e Cores** e, em seguida, altere as configurações de itens relacionados ao R na caixa **Itens de exibição**:

![Opções de fontes e cores para código R](media/editing-syntax-colors-options.png)

O Visual Studio também sublinha erros de sintaxe no editor:

![Realce de erro de sintaxe no código R](media/editing-syntax-error.png)

Para alterar esse comportamento, confira a configuração **Avançado** > **Verificação de sintaxe** em [opções do editor](#editor-options).

## <a name="edit-and-organize-code"></a>Editar e organizar o código

Conforme você digita o código, as RTVS fornecem preenchimento automático, conforme descrito na página [IntelliSense](r-intellisense.md). Ele também faz a formatação automática, como o fechamento de chaves e parênteses: 

![Animação de formatação embutida](media/editing-inline-formatting.gif)

Ao digitar chamadas de funções que têm muitos parâmetros, muitas vezes você deseja alinhar os parâmetros para deixar o código mais fácil de ler. As RTVS lembram do recuo que você definiu para os parâmetros e aplica esse recuo automaticamente às linhas subsequentes:

![Animação de recuo automático](media/editing-auto-indentation.gif)

Para alterar esse comportamento, consulte [opções do editor](#editor-options) e veja o grupo **Guias**.

As regiões de código recolhíveis permitem ocultar parte do código temporariamente no editor. O Visual Studio cria várias regiões automaticamente, como para instruções multilinhas, a menos que a opção **Avançado** > **Estrutura de Tópicos** > **Estrutura de Tópicos de código** esteja definida como Desabilitada.

Para criar uma região sua, coloque o código desejado entre comentários que terminam com `---`. Os controles pequenos +/- à esquerda do código permitem que você expanda e recolha regiões:

![Criando uma região recolhível com comentários](media/editing-collapsible-regions.gif)

Por padrão, o Visual Studio insere espaços quando você pressiona a tecla **Tab**. Novamente você pode alterar esse comportamento, conforme descrito em [Opções, Editor de Texto, Guias](../ide/reference/options-text-editor-all-languages.md).

## <a name="code-navigation"></a>Navegação de código

A navegação de código fornece acesso rápido ao código-fonte do seu programa do R e de suas bibliotecas. Esses recursos mantêm você no fluxo do seu trabalho em vez de precisar pesquisar manualmente o código.

**Ir para definição** rapidamente salta para uma definição de função ou um minieditor pop-up embutido para ler o código-fonte de uma função de biblioteca. Basta clicar com o botão direito do mouse na função de interesse e selecionar **Ir para Definição** ou colocar o cursor na função e pressionar **F12**.

Este comando abre uma nova janela do editor que contém o código-fonte para a função. O cursor é convenientemente posicionado no início da definição de função.

**Espiar definição**, invocado do menu acionado com o botão direito do mouse ou pressionando **Alt**+**F12**, insere uma região rolável somente leitura, que contém o código-fonte da função abaixo da chamada de função:

![Animação para definição de espiada](media/editing-peek-definition.gif)

## <a name="send-code-to-the-interactive-window"></a>Enviar código para a janela interativa

Muitos desenvolvedores gostam escrever código no editor e, em seguida, enviá-lo para a [janela interativa](interactive-repl-for-r-in-visual-studio.md) para teste imediato [também conhecido como REPL (Read-Evaluate-Print-Loop)]. Pressionar **Ctrl**+**Enter** no editor R envia a linha de código atual para a janela interativa e, em seguida, coloca o cursor na linha seguinte. Em seguida, com **Ctrl**+**Enter**, você pode percorrer o código efetivamente no editor.

Você também pode selecionar o código e pressionar **Ctrl**+**Enter** para aplicar essa seleção inteira. Como alternativa, clique com o botão direito do mouse na seleção e selecione **Executar em Interativo**.

## <a name="format-code"></a>Código de formatação

A formatação automática do Visual Studio mantém o código que você escreve, bem como o código que você cola no editor, formatados conforme definido por suas preferências. Você também pode fazer uma seleção, clicar com o botão direito do mouse e selecionar **Formatar Seleção** (**Ctrl**+**K**,**F**) para aplicar essas preferências. Por exemplo, se você tiver uma definição de função inteira em uma única linha:

```R
f<-function  (a){  return(a + 1) }
```

A aplicação da formatação a limpará deixando assim:

```R
f <- function(a) { return(a + 1) }
```

Para reformatar o arquivo de código inteira, selecione **Editar** > **Avançado** > **Formatar Documento** (**Ctrl**+**E**,**D**).

A formatação automática é uma operação separada que pode ser desfeita. Por exemplo, se você colar o código no editor e a formatação for aplicada, selecionar **Editar** > **Desfazer** ou pressionar **Ctrl**+**Z** uma única vez reverterá a formatação. Um segundo **Desfazer** reverterá a própria colagem.

As opções de formatação (incluindo desabilitar a formatação) são definidas por meio de **Ferramentas** > **Opções** na guia **Editor de Texto** > **R** > **Avançado**. Você pode acessar essa página diretamente usando o comando **Ferramentas do R** > **Opções do editor** ou clicando com o botão direito do mouse no editor e selecionando **Opções de formatação**. Consulte a seção de [opções do editor](#editor-options) para obter detalhes.

## <a name="inserting-roxygen-comments"></a>Inserindo comentários Roxygen

As RTVS fornecem um atalho para a geração de comentários [Roxygen](http://roxygen.org/) usando os nomes de parâmetro de uma função. Basta digitar `###` em uma linha em branco acima da definição de função:

![Animação da inserção de um comentário Roxygen](media/editing-roxygen-comments.gif)

## <a name="editor-options"></a>Opções do editor

As Opções específicas do editor são definidas pelo comando **Ferramentas** > **Opções**, navegando até **Editor de Texto** > **R** ou usando o comando de atalho **Ferramentas do R** > **Opções do Editor**.

As opções nas guias **Geral**, **Barras de rolagem** e **Guias** não são específicas para R, mas são configurações gerais do Visual Studio disponíveis para todas as linguagens, mas são aplicadas de acordo com cada linguagem. Para obter detalhes, veja os seguintes artigos:

- [Opções, Editor de Texto, Todas as Linguagens](../ide/reference/options-text-editor-all-languages.md)
- [Rastrear o código personalizando a barra de rolagem](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md)
- [Opções, editor de texto, guias](../ide/reference/options-text-editor-all-languages-tabs.md)

As opções na guia **R** > **Avançado** são específicas das RTVS:

| Grupo | Opção | Padrão | Descrição |
| --- | --- | --- | --- |
| Formatação | Formatação automática | On | Reformata o código enquanto você digita. Não afeta os comandos **Formatar Seleção** ou **Formatar Documento**. |
| | Chaves expandidas | Off | Coloca uma { aberta em uma nova linha. |
| | Formatar ao colar | On | Aplica a formatação ao colar. |
| | Formatar escopo em } | On | Formata o escopo depois de digitar uma } de fechamento. |
| | Espaço após a vírgula | On | Coloca um espaço depois de vírgulas. |
| | Espaço após a palavra-chave | On | Coloca um espaço depois de palavras-chave como `if`, `while` e `repeat`. |
| | Espaço antes de { | On | Coloca um espaço antes de uma { de abertura. |
| | Espaços antes e depois de = | On | Insere espaços antes e depois de um sinal de igual. |
| IntelliSense | Confirmar com a tecla Enter | Off | Confirma a seleção de preenchimento automático quando **Enter** é pressionado. |
| | Confirmar com a tecla Espaço | Off | Confirma a seleção de preenchimento automático quando **Espaço** é pressionado.|
| | Lista de conclusão no primeiro caractere | On | Mostra a lista de conclusão nos primeiros tipos de caracteres. Quando desabilitada, uma lista de conclusão é exibida com **Editar** > **IntelliSense** > **Listar Membros** (**Ctrl**+**J**). |
| | Lista de conclusão com a tecla **Tab** | Off | Invoca uma lista de conclusão digitando um ou mais caracteres e pressionando **Tab**. |
| | Corresponder parcialmente ao digitar nomes de argumento | Off | Ao digitar os nomes de argumento em uma chamada de função, a ajuda de assinatura mostra uma descrição do argumento que é a melhor correspondência. |
| Janela Interativa | Verificação de sintaxe no console do R | Off | Aplica a verificação na janela interativa de sintaxe. A verificação de sintaxe pode não funcionar corretamente com instruções de várias linhas. | 
| Estrutura de tópicos | Estrutura de tópicos de código | On | Cria regiões recolhíveis automaticamente para áreas como instruções de várias linhas. |
| Verificação de sintaxe | Mostrar erros de sintaxe | On | Habilita a verificação de sintaxe automática do código. |
