---
title: Opções de ferramentas R
description: Referência para as opções no Visual Studio para a linguagem R e recursos associados.
ms.date: 12/04/2017
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: reference
f1_keywords:
- vs.toolsoptionspages.text_editor.r.advanced
- vs.toolsoptionspages.r_tools
- vs.toolsoptionspages.r_tools.advanced
- vs.toolsoptionspages.r_tools.#150
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: a40ed2fd72862bde3494edd0c74aebcca6b55711
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37342736"
---
# <a name="r-tools-for-visual-studio-options"></a>Opções das Ferramentas do R para Visual Studio

As configurações são acessadas pelo menu **Ferramentas do R** > **Opções** ou por meio de **Ferramentas** > **Opções** e rolando até as **Ferramentas do R**:

  ![Caixa de diálogo de opções para Ferramentas de R](media/options-dialog.png)

Opções e configurações específicas para o R são acessadas usando os métodos abaixo. É necessário selecionar a caixa **Mostrar todas as configurações** na parte inferior da caixa de diálogo **Opções** para que todas essas seções sejam exibidas.

- Opções de formatação de código (acesse o menu [Opções do Editor](editing-r-code-in-visual-studio.md#editor-options): **Ferramentas** > **Opções** e, em seguida, selecione **Editor de Texto** > **R** > **Formatação**
- Opções de linter (acesse o menu [Linting](linting-r-code.md)): **Ferramentas** > **Opções** e, em seguida, selecione **Editor de Texto** > **R** > **Lint**
- Opções avançadas do editor ([descritas neste artigo](#text-editor--r--advanced-options)): acesse o menu **Ferramentas** > **Opções** e, em seguida, selecione **Editor de Texto** > **R** > **Avançadas**
- Opções comportamentais ([descritas neste artigo](#r-tools--advanced-options)): menu **Ferramentas do R** > **Opções** ou **Ferramentas** > **Opções** e, em seguida, role até **Ferramentas do R**.

O comando **Ferramentas do R** > **Configurações da Ciência de Dados** também afeta inúmeras configurações diferentes no Visual Studio, em geral. Esse comando será descrito na próxima seção.

<a name="data-scientist-layout"></a>

## <a name="r-tools--data-science-settings"></a>Ferramentas do R > Configurações da Ciência de Dados

O item de menu **Ferramentas do R > Configurações da Ciência de Dados** configura o IDE do Visual Studio com um layout otimizado para as necessidades dos cientistas de dados. Especificamente, essa opção abre as janelas [Interativo](interactive-repl-for-r-in-visual-studio.md), [Gerenciador de Variáveis](variable-explorer.md) e [Espaços de trabalho](r-workspaces-in-visual-studio.md):

![Layout da janela do cientista de dados no Visual Studio](media/installation-data-scientist-layout-result.png)

Para reverter posteriormente para outras configurações do Visual Studio, primeiro use o comando **Ferramentas** > **Importar e Exportar Configurações**, selecione **Exportar configurações de ambiente selecionadas** e especifique um nome do arquivo. Para restaurar essas configurações, use o mesmo comando e selecione **Importar configurações de ambiente selecionadas**. Você também poderá usar os mesmos comandos se você alterar o layout do cientista de dados e quiser retornar a ele, em vez de usar o comando **Configurações da ciência de dados** diretamente.

## <a name="text-editor--r--advanced-options"></a>Editor de texto > R > Opções avançadas

Essas opções controlam o comportamento da formatação, do IntelliSense, da estrutura de tópicos, do recuo e da verificação de sintaxe para o R.

![Caixa de diálogo Opções para opções avançadas do editor de texto do R](media/options-dialog-advanced-text-editor.png)

Cada opção é definida como ativada ou desativada para controlar o comportamento em questão. Para obter detalhes sobre o que cada opção afeta, examine o painel de ajuda na parte inferior da caixa de diálogo. Observe que é possível arrastar a parte superior desse painel de ajuda para aumentar o painel.

![Painel de ajuda expandido na caixa de diálogo de opções avançadas do editor de texto do R](media/options-dialog-advanced-text-editor2.png)

## <a name="r-tools--advanced-options"></a>Ferramentas do R > Opções avançadas

O comando de menu **Ferramentas do R** > **Opções** abre a caixa de diálogo **Opções** nas opções do R:

  ![Caixa de diálogo de opções para Ferramentas de R](media/options-dialog.png)

As seções a seguir descrevem as diferentes opções disponíveis nesta página.

### <a name="debugging"></a>Depuração

Essas opções controlam como os valores são manipulados no [Gerenciador de Variáveis](variable-explorer.md) e nas janelas do depurador, como Inspeção e Locais (confira [Depurar código R](debugging-r-in-visual-studio.md)).

| Opção | Valor padrão | Descrição |
| --- | --- | --- |
| Avaliar associações ativas | `True` | Quando é `True`, garante que você sempre veja o valor mais atualizado ao inspecionar variáveis e propriedades. O risco é que avaliar as expressões pode causar efeitos colaterais, dependendo de como elas foram implementados. |
| Mostrar variáveis prefixadas com ponto | `False` | Especifica se as variáveis prefixadas com `.` são mostradas. |

### <a name="grid-view"></a>Exibição em grade

| Opção | Valor padrão | Descrição |
| --- | --- | --- |
| Avaliação dinâmica | `False` | Por padrão, a função `View(<expression>)` tira um instantâneo dos dados como um quadro de dados, que pode consumir memória considerável com grandes conjuntos de dados. Configurar esta opção como `True` significa que a expressão será avaliada quando a grade for atualizada para buscar somente os dados exibidos. No entanto, se a expressão for alterada, os dados também serão, o que pode ser inadequado para expressões dplyr pip. |

### <a name="help"></a>Ajuda

| Opção | Valor padrão | Descrição |
| --- | --- | --- |
| Navegador da Web F1 | `Internal` | Controla como a Ajuda é exibida quando você procura por um termo usando **Ctrl**+**F1**. Quando definido como `Internal`, a ajuda é renderizada dentro de uma janela de ferramentas no Visual Studio. Quando definido como `External`, a ajuda é exibida no navegador da Web padrão. |
| Cadeia de pesquisa da Web F1 | `R site:stackoverflow.com` | Controla como os termos de pesquisa são passados para o mecanismo de pesquisa quando você pressiona **Ctrl**+**F1** em um termo no editor. Por padrão a cadeia de caracteres é `R site:stackoverflow.com`, que acrescenta `R` ao termo de pesquisa. O `site:stackoverflow.com` é uma diretiva que solicita ao mecanismo de pesquisa que as páginas no domínio `stackoverflow.com` sejam incluídas ao escopo da pesquisa. |
| Navegador da Ajuda do R | `Automatic` | Controla como a Ajuda é exibida quando você procura na documentação do R usando **F1**, **?** ou **??**. Quando definido como `Automatic`, a ajuda é renderizada na janela apropriada. Por exemplo, a ajuda em HTML aparece em uma janela de ferramentas do Visual Studio, enquanto PDFs aparecem no programa de PDF padrão. Quando definido como `External`, a ajuda é renderizada no navegador da Web padrão. |

### <a name="history"></a>Histórico

| Opção | Valor padrão | Descrição |
| --- | --- | --- |
| Sempre salvar histórico | `True` | Controla se as RTVS gravam o histórico de comandos em um arquivo *.RHistory* no diretório de trabalho sempre que o projeto é fechado. O salvamento do histórico acontecerá mesmo se você não salvar seu projeto antes de sair. |
| Redefinir filtro de pesquisa | `True` | Determina se a janela Histórico pode filtrar o histórico de comandos para mostrar somente os comandos que correspondem à subcadeia de caracteres em relação ao termo do filtro na caixa de diálogo Histórico do R. Essa configuração determina se o filtro de pesquisa de histórico é redefinido sempre que você executa um novo comando ou alterna para um novo projeto, que dispara o carregamento de um outro arquivo *.RHistory*. A configuração padrão de `True` minimiza a surpresa quando você executa um comando com um conjunto de filtros e percebe que o comando que acabou de ser executado não apareceu no histórico. |
| Usar seleção de várias linhas | `True` | Especifica se é possível selecionar uma instrução de várias linhas no Histórico com um único clique. Também permite a navegação com setas para cima/para baixo nas janelas interativas por instruções e não por linhas. |

### <a name="html"></a>HTML

| Opção | Valor padrão | Descrição |
| --- | --- | --- |
| Navegador de páginas HTML | `External` | Determina onde o conteúdo, como um gráfico `ggvis` ou um aplicativo `shiny`, é renderizado. `Internal` mostra a saída HTML dentro de uma janela de ferramentas no Visual Studio; `External` exibe a saída HTML no navegador padrão. |

### <a name="logging"></a>Registrando em log

| Opção | Valor padrão | Descrição |
| --- | --- | --- |
| Eventos de log | `Normal` | Controla o nível de detalhes do registro em log usado para diagnóstico das RTVS. A configuração padrão de `Normal` cria um arquivo de log em seu diretório `TEMP`. Quando definido como `Traffic`, as RTVS registram todos os comandos e as respostas em sua sessão. Esses arquivos de log nunca saem do computador, mas podem ser úteis para diagnosticar problemas nas RTVS. |

### <a name="markdown"></a>Markdown

| Opção | Valor padrão | Descrição |
| --- | --- | --- |
| Navegador da visualização de markdown | `External` | Determina onde a saída HTML RMarkdown é exibida. `Internal` mostra o documento HTML RMarkdown dentro de uma janela de ferramentas no Visual Studio; `External` exibe o HTML RMarkdown usando o navegador padrão. |

### <a name="r-engine"></a>Mecanismo do R

| Opção | Valor padrão | Descrição |
| --- | --- | --- |
| Página de código | `(OS Default)` | Define a página de código (localidade) para R. Por padrão, ele usa a localidade subjacente do sistema operacional. |
| Espelho CRAN | `(Use .Rprofile)` | Define o espelho CRAN padrão para instalações de pacote. A configuração padrão de `Use .Rprofile` respeita as configurações de Espelho CRAN no arquivo *.RProfile*. |

### <a name="workspace"></a>Espaço de trabalho

| Opção | Valor padrão | Descrição |
| --- | --- | --- |
| Carregar espaço de trabalho quando o projeto é aberto | `No` | Definir como `Yes` permite carregar dados da sessão do arquivo *.RData* no ambiente global quando o projeto é aberto. |
| Prompt para salvar espaço de trabalho ao reiniciar | `Yes` | Definir como `No` desabilita o prompt para salvar o espaço de trabalho ao clicar no botão Redefinir na janela interativa. |
| Salvar espaço de trabalho quando o projeto é fechado | `No` | Definir como `Yes` permite salvar o ambiente global no arquivo *.RData* quando o projeto é fechado. |
| Mostrar caixa de diálogo de confirmação antes de alternar espaços de trabalho | `Yes` | Definir como `No` desabilita o prompt de confirmação do usuário ao alternar entre espaços de trabalho diferentes. Confira [Alternar entre espaços de trabalho](r-workspaces-in-visual-studio.md#switch-between-workspaces) |
| Mostrar indicador de carga do computador | `False` | Controla a visibilidade do indicador de carga CPU/Memória/Rede na barra de status. Como o indicador incorre em tráfego de rede, é útil manter isto `False` em cenários limitados remotos. Alterar essa opção requer a reinicialização do Visual Studio. |
