---
title: Depurando código em R
description: O Visual Studio fornece uma experiência de depuração completa para R, incluindo pontos de interrupção, anexação, pilha de chamadas e inspeção de variáveis.
ms.date: 01/24/2018
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: c89eed2f3e15259489ce43920b912db14ab862a6
ms.sourcegitcommit: f685fa5e2df9dc307bf1230dd9dc3288aaa408b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36235177"
---
# <a name="debug-r-in-visual-studio"></a>Depurar o R no Visual Studio

As RTVS (Ferramentas do R para Visual Studio) se integram à experiência de depuração completa do Visual Studio (consulte [Depurando no Visual Studio](../debugger/debugging-in-visual-studio.md)). Esse suporte inclui pontos de interrupção, a anexação a processos em execução, a inspeção e a observação de varáveis e a inspeção da pilha de chamadas. Portanto, este artigo explora os aspectos de depuração que são exclusivos para R e RTVS.

A inicialização do depurador para o arquivo R de inicialização em um projeto do R é igual a de outros tipos de projeto: use **Depurar** > **Iniciar Depuração**, a tecla **F5** ou o **Arquivo de inicialização de origem** na barra de ferramentas de depuração: 

![Botão Iniciar depurador para R](media/debugger-start-button.png)

Para alterar o arquivo de inicialização, clique com o botão direito do mouse em um arquivo no Gerenciador de Soluções e selecione **Definir Como Script R de Inicialização**.

Em todos os casos, iniciar o depurador "origina" o arquivo na janela interativa, o que significa carregá-lo e executá-lo lá como mostrado na saída da janela interativa:

```output
> rtvs::debug_source("c:/proj/rproject1/rproject1/script.R")
Sourcing: c:\proj\rproject1\rproject1\script.R
Sourcing: c:\proj\rproject1\rproject1\Settings.R
```

Observe que a função `rtvs::debug_source` é usada para o script de origem. Essa função é necessária porque as RTVS precisam modificar o código na preparação para a depuração. Ao usar qualquer comando de fornecimento de RTVS e um depurador estiver anexado, o Visual Studio automaticamente usará `rtvs::debug_source`.

Você também pode anexar manualmente o depurador pela janela interativa diretamente usando o comando **Ferramentas do R** > **Sessão** > **Anexar Depurador**, o comando **Depurar** > **Anexar a R Interativo** ou o comando **Anexar Depurador** na barra de ferramentas da janela interativa. Depois de fazer isso, será sua responsabilidade originar os arquivos que deseja depurar. Se você quiser originar os arquivos manualmente, certifique-se de usar `rtvs::debug_source` e não o comando `source` regular no R.

Essa conexão entre o depurador e a janela interativa facilita ações como chamar (e depurar) uma função com valores de parâmetros diferentes. Por exemplo, suponha que você tenha a seguinte função em um arquivo originado (o que significa que ela foi carregada na sessão):

```R
add <- function(x, y) {
    return(x + y)
}
```

Em seguida você define um ponto de interrupção na instrução `return`. Agora, na janela interativa, inserir `add(4,5)` interrompe o depurador no seu ponto de interrupção.

## <a name="environment-browser-in-the-interactive-window"></a>Navegador de Ambiente na janela interativa

Quando você for interrompido no depurador, você também será interrompido no prompt de Navegador de Ambiente na [janela interativa](interactive-repl-for-r-in-visual-studio.md). O prompt será exibido como `Browse[n]>`, em que n é um número.

O Navegador de Ambiente dá suporte a uma série de comandos especiais:

| Comando | Descrição |
| --- | --- |
| n | próxima: executa a próxima instrução no arquivo de código (o mesmo que avançar). |
| s | intervir: executa a próxima instrução no arquivo de código, executando um escopo de função quando a próxima instrução é uma chamada de função. |
| f | concluir: executa o restante do escopo da função atual e retorna ao chamador (o mesmo que sair). |
| c, cont | continuar: executa o programa até o próximo ponto de interrupção. |
| Q | encerra: termina a sessão de depuração. |
| onde | mostrar pilha: exibe a pilha de chamadas na janela interativa. |
| help | mostrar ajuda: exibe os comandos disponíveis na janela interativa. |
| &lt;expr&gt; | avaliar a expressão em *expr*. |

![Navegador de Ambiente na janela interativa](media/debugger-environment-browser.png)
