---
title: R Markdown
description: Como criar documentos de R Markdown no Visual Studio para produzir painéis, apresentações e relatórios de alta qualidade.
ms.date: 11/16/2017
ms.prod: visual-studio-dev15
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 3a15899d561088ee9911cb08eaa4f5887b996a3e
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55000076"
---
# <a name="create-r-markdown-documents"></a>Criar documentos R Markdown

[R Markdown](https://rmarkdown.rstudio.com/) é um formato de documento que transforma a análise em R em painéis, relatórios, apresentações e documentos de alta qualidade.

As RTVS (Ferramentas do R para Visual Studio) oferecem modelo de item do R Markdown, suporte ao editor (incluindo IntelliSense para código R dentro do editor), funcionalidades de geração de arquivo e versão prévia dinâmica.

## <a name="using-r-markdown"></a>Usando o R Markdown

1. Feche o Visual Studio.
1. (Apenas uma vez) Instalar o `pandoc` do [pandoc.org](http://pandoc.org/installing.html).
1. Reinicie o Visual Studio, que deve captar a instalação do pandoc.
1. Instale os pacotes `knitr` e `rmarkdown`, o que pode ser feito na [janela interativa](interactive-repl-for-r-in-visual-studio.md):

    ```R
    install.packages("knitr")
    install.packages("rmarkdown")

    ```
1. Crie um novo arquivo R Markdown usando o comando de menu **Arquivo** > **Novo** > **Arquivo** e selecionando **R** > **R Markdown** na lista. No contexto de um projeto, clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Adicionar R Markdown** (ou **Adicionar** > **Novo Item** e selecionando **R Markdown** na lista).

1. O conteúdo padrão do novo arquivo é o seguinte:

    ~~~markdown
    ---
    title: "Untitled"
    output: html_document
    ---

    This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and Microsoft Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

    When you click the **R Tools | Publish | Preview** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

    ```{r}
    summary(cars)
    ```

    You can also embed plots, for example:

    ```{r, echo=FALSE}
    plot(cars)
    ```

    Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.

    ~~~

## <a name="previews"></a>Versões prévias

O Visual Studio 2017 versão 15.5 e posterior fornece automaticamente a versão prévia dinâmica para o R Markdown. Para ativar a sincronização automática entre o editor e a versão prévia, selecione **Ferramentas do R** > **Markdown** > **Sincronização Automática** (**CTRL**+**Shift**+**Y**). Se você não estiver usando a sincronização automática, atualize a versão prévia usando **Ferramentas do R** > **Markdown** > **Recarregar Versão Prévia do R Markdown**.

Também é possível visualizar o arquivo nos formatos HTML, PDF e Microsoft Word clicando com o botão direito do mouse no editor e selecionando um dos comandos **Versão prévia**. Os mesmos comandos também estão disponíveis no menu **Ferramentas do R** > **Markdown**. (Em versões anteriores do Visual Studio, esses comandos são encontrados no menu **Ferramentas do R** > **Publicar**.)

![Versão prévia dinâmica do R Markdown e outros comandos de menu de versão prévia](media/rmarkdown-live-preview.png)
