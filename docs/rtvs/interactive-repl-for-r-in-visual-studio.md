---
title: REPL interativo para R
description: Como usar o ambiente REPL interativo para R no Visual Studio, que é integrado às janelas do editor.
ms.date: 06/28/2017
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: a9e475e108fee9134699b0ee80e59fbf3f5eea32
ms.sourcegitcommit: f685fa5e2df9dc307bf1230dd9dc3288aaa408b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36235232"
---
# <a name="work-with-the-r-interactive-window"></a>Trabalhar com a janela R Interativo

As RTVS (Ferramentas do R para Visual Studio) fornecem a janela R Interativo, também conhecida como janela **REPL** (Read-Evaluate-Print-Loop), na qual você pode inserir código R e ver os resultados imediatamente. Todos os módulos, sintaxe e variáveis, bem como o IntelliSense, estão disponíveis na janela interativa.

A janela interativa também está integrada às janelas regulares do editor R. Você pode selecionar o código e pressionar **Ctrl**+**Enter** ou clicar com o botão direito do mouse e selecionar **Executar em Interativo**, e o código será executado linha por linha na janela interativa como se você tivesse digitado diretamente. Quando o cursor está em uma única linha em uma janela do editor **Ctrl**+**Enter** envia essa linha para a janela interativa e, em seguida, move o cursor para a próxima linha. Assim, basta pressionar **Ctrl**+**Enter** repetidamente para percorrer o código.

Para experimentar esses recursos, siga o passo a passo [Introdução ao R](getting-started-with-r.md), bem como as seções neste artigo. Os [Trechos de código](code-snippets-for-r.md) também funcionam na janela interativa como nas janelas do editor de R.

## <a name="overview-of-the-interactive-window"></a>Visão geral da Janela Interativa

Digitar código R válido e pressionar **Enter** no final da linha executa o código nessa linha:

```repl
> 3 + 3
[1] 6
```

Pressionar **Enter** em qualquer lugar em uma entrada de linha única também executa essa linha.

Todas as entradas e saídas anteriores da REPL são somente leitura e não podem ser alteradas. No entanto, você pode selecionar e copiar o texto da janela a qualquer momento e também colá-lo. O código colado é executado como se fosse inserido linha por linha.

Ou seja, quando você começa a digitar uma instrução e pressiona **Enter**, as RTVS sabem quando a instrução precisa ser continuada e entram no modo multilinhas com um prompt + à esquerda e o recuo apropriado. As RTVS também preenchem as chaves, os colchetes e os parênteses:

![Entrada de instrução de várias linhas na janela interativa](media/repl-multiline-entry.png)

No modo multilinhas, a tecla **Enter** executa o bloco de código somente quando posicionada no final do bloco, caso contrário, ela insere uma nova linha. No entanto, você pode pressionar **Ctrl**+**Enter** em qualquer posição para executar esse bloco de código imediatamente.

### <a name="toolbar-commands"></a>Comandos da barra de ferramentas

Aqui está a janela interativa com sua barra de ferramentas:

![Janela interativa com barra de ferramentas](media/repl-window.png)

Os comandos da barra de ferramentas são mostrados a seguir. A maioria deles tem equivalentes de teclado e também está disponível nos menus **Ferramentas do R** > **Sessão** e **Ferramentas do R** > **Diretório de Trabalho** (ou conforme o indicado):

| Botão | Comando | Combinação de teclas | Descrição | 
| --- | --- | --- | --- |
| ![Botão Redefinir](media/repl-toolbar-01-reset.png) | Redefinir | **Ctrl**+**Shift**+**F10** | Redefine a sessão de janela interativa, limpando todas as variáveis e o histórico. |
| ![Botão Limpar](media/repl-toolbar-02-clear.png) | Clear | **Ctrl**+**L** | Limpa a saída mostrada na janela interativa. não afeta as variáveis de sessão nem o histórico. |
| ![Botões Histórico](media/repl-toolbar-03-history.png) | Comando Histórico anterior<br/>Comando Próximo histórico | **Para cima**, **Para baixo**<br/>**Alt**+**Para cima**, **Alt**+**Para baixo** | Percorre o histórico, com alguns comportamentos de blocos de código de várias linhas. Consulte [Histórico](#history). |
| ![Botão Carregar espaço de trabalho](media/repl-toolbar-04-load-workspace.png) | Carregar espaço de trabalho | N/D | Carrega um espaço de trabalho anterior salvo (consulte [Espaços de trabalho e sessões](#workspaces-and-sessions). |
| ![Botão Salvar espaço de trabalho como](media/repl-toolbar-05-save-workspace-as.png)| Salvar espaço de trabalho | N/D | Salva o estado atual da sessão como um espaço de trabalho (consulte [Espaços de trabalho e sessões](#workspaces-and-sessions). |
| ![Botão Script R de origem](media/repl-toolbar-06-source-r-script.png) | Script R de origem | **Ctrl**+**Shift**+**S** | Chama `source` com o script R atualmente ativo no editor do Visual Studio, que executa o código.  Esse botão só aparece quando um arquivo R é aberto no editor do Visual Studio. | 
| ![Botão Script R de origem com eco](media/repl-toolbar-07-source-r-script-with-echo.png) | Script R de Origem com Eco | **Ctrl**+**Shift**+**Enter** | Igual ao Script R de Origem, mas exibe o conteúdo do script na janela interativa. |
| ![Botão Interromper R](media/repl-toolbar-08-interrupt-r.png)| Interromper R | **Esc** | Interrompe qualquer código em execução na janela interativa, como o loop `while` na captura de tela mostra no início dessa seção. |
| ![Botão Anexar depurador](media/repl-toolbar-09b-attach-debugger.png)| Anexar depurador | N/D | Também está disponível ao usar o comando **Depurar** > **Anexar a R Interativo**. | 
| ![Botão Definir diretório de trabalho para o local do arquivo de origem](media/repl-toolbar-10-set-working-directory-source.png)| Definir diretório de trabalho para o local do arquivo de origem | **Ctrl**+**Shift**+**E** | Define o diretório de trabalho para o último arquivo de origem carregado na janela interativa (usando `source`). Consulte [Diretório de trabalho](#working-directory). |
| ![Botão Definir diretório de trabalho para o local do projeto](media/repl-toolbar-11-set-working-directory-to-project.png) | Definir diretório de trabalho para o local do projeto | **Ctrl**+**Shift**+**P** | Define o diretório de trabalho para a raiz do projeto carregado atualmente no Visual Studio. Consulte [Diretório de trabalho](#working-directory). |
| (Campo de texto) | Selecionar Diretório de Trabalho | N/D | Campo de entrada direta para o diretório de trabalho. Consulte [Diretório de trabalho](#working-directory). |

## <a name="workspaces-and-sessions"></a>Espaços de trabalho e sessões

Executar o código na janela interativa cria um contexto em sua sessão atual. O contexto é composto de variáveis globais, definições de função, cargas de biblioteca e assim por diante. Esse contexto é chamado coletivamente de *espaço de trabalho* e você pode salvar e carregar espaços de trabalho a qualquer momento. 

Selecionar o botão **Salvar Espaço de Trabalho Como** ou usar os prompts de comando **Ferramentas do R** > **Sessão** > **Salvar Espaço de Trabalho Como** solicitará um local e um nome de arquivo (a extensão padrão é *.RData*).

Para salvar um espaço de trabalho usando um nome de arquivo específico (o padrão é *.RData*), clique no botão **Salvar Espaço de Trabalho** na REPL:

Para recarregar um espaço de trabalho salvo anteriormente, selecione o botão **Carregar Espaço de Trabalho** ou use **Ferramentas do R** > **Sessão** > **Carregar Espaço de Trabalho** e navegue até o arquivo de espaço de trabalho.

O botão **Redefinir** ou **Ferramentas do R** > **Sessão** > **Redefinir** limpa o contexto da sessão. Se você estiver usando uma sessão remota, a redefinição também excluirá o perfil do usuário no computador remoto para limpar todos os arquivos armazenados ali. (Consulte [Espaços de trabalho](r-workspaces-in-visual-studio.md#directories-on-local-and-remote-computers).)

## <a name="working-directory"></a>Diretório de trabalho

Normalmente, os desenvolvedores desejam alterar seu diretório de trabalho enquanto estão em uma sessão interativa. Vários comandos, disponíveis na barra de ferramentas, no menu **Ferramentas do R** > **Diretório de trabalho** e no menu de contexto do projeto, permitem que você configure facilmente um diretório de trabalho como o local de um arquivo de origem, o local do projeto ou qualquer outro local. Isso ajuda a evitar a digitação de nomes de caminho completos ou de nomes de caminho relativos longos ao fazer referência a arquivos.

## <a name="history"></a>Histórico

Cada linha que você insere na janela interativa, incluindo as linhas enviadas de um editor, são mantidas no histórico da REPL. Você pode navegar pelo histórico com as teclas de seta Para Cima e Para Baixo, como provavelmente já está acostumado na linha de comando.

Uma diferença é que, se você começar a digitar na linha atual e pressionar Para Cima, essa linha atual será preservada no histórico, mesmo que ela ainda não tenha sido executada.

O histórico na janela interativa também funciona de forma inteligente com instruções de outro bloco de código que abrangem linhas. Ao percorrer o histórico com as teclas de seta Para Cima e Para Baixo, os blocos de código de várias linhas são recuperados como um todo e mostrados como a entrada atual. Neste ponto, as teclas de seta navegam por esse bloco de código linha por linha, até a parte superior ou inferior seja atingida. Na parte superior do bloco de código, a seta para cima recupera o item anterior no histórico; na linha inferior, a seta para baixo recupera o próximo item.

Esse comportamento acomoda o caso comum de executar novamente o último item no histórico com a combinação de pressionamento de tecla seta para cima e **Enter**, permitindo naturalmente a edição de um bloco de código multilinhas ao pressionar a seta para cima para navegar até ele.

Para evitar a navegação em blocos de código multilinhas, use os botões de barra de ferramentas ou **Alt**+**Para cima** e **Alt**-**Para baixo** para que todos esses blocos sejam tratados como uma única linha.

A maneira mais fácil de experimentar os recursos de histórico é testá-los por contra própria na janela interativa. O código a seguir fornece várias instruções adequadas de linha única e de várias linhas. Use copiar e colar com cada instrução individualmente para criar o histórico apropriado. (Você também pode colar o código em um arquivo de código separado e, em seguida, enviar as linhas para a janela interativa com **Ctrl**+**Enter**.)

```R
3 + 3

4 + 4

5 + 5

add <- function (x, y) {
  return (x + y)
}

sub <- function (x, y) {
  return (x - y)
}
```