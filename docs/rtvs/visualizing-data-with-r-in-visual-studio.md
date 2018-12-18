---
title: Visualizando dados com R
description: Como plotar dados em programas de R no Visual Studio, usando janelas de plotagem.
ms.date: 06/29/2017
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: f44ba213defef153acd2f5d1ef247bb093448263
ms.sourcegitcommit: f685fa5e2df9dc307bf1230dd9dc3288aaa408b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36235182"
---
# <a name="create-visual-data-plots-with-r"></a>Criar gráficos de dados visuais com R

Criar gráficos é uma parte fundamental do fluxo de trabalho de um cientista de dados. Nas RTVS (Ferramentas do R para Visual Studio), todas as atividades de criação de gráficos giram em torno de uma ou mais janelas de gráficos, que são projetadas para melhorar a produtividade nesta importante atividade.

![Imagem hero de criação de gráficos](media/plotting-hero-image.png)

|   |   |
|---|---|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo (youtube.com)](https://www.youtube.com/watch?v=ZTbKmz5RSgY) sobre como plotar com o R (2m 02s). |

## <a name="the-plot-window"></a>A janela de gráficos

Uma janela de gráficos contém uma série de gráficos, em que cada gráfico é gerado por um comando `plot`. Por exemplo, usar `plot(1:100)` cria uma nova janela de gráficos se já não houver alguma disponível:

![Gráfico linear de 1 a 100](media/plotting-1-to-100.png)

Tecnicamente falando, os comandos R `plot` renderizam a saída para um dispositivo de gráficos do R. Uma janela de gráficos renderiza o conteúdo de um dispositivo de gráficos do R, por isso, cada janela de gráficos recebe um número de dispositivo.

As janelas de gráficos são independentes dos projetos do Visual Studio e permanecem abertas ao carregar e fechar projetos.

A geração de um gráfico usará a janela de gráficos “ativa”, salvando todos os gráficos anteriores no histórico de gráficos (consulte [Histórico de gráficos](#plot-history)). Por exemplo, digite `plot(100:1)` e o primeiro gráfico é substituído por uma linha para baixo.

Como todas as outras janelas do Visual Studio. a janela de gráficos dá suporte a layouts personalizados (consulte [Personalização de layouts de janela no Visual Studio](../ide/customizing-window-layouts-in-visual-studio.md). As janelas de gráficos podem ser encaixadas em diferentes locais dentro do quadro do Visual Studio, redimensionadas dentro desse quadro ou retiradas inteiramente do quadro para um redimensionamento independente. 

Redimensionar uma janela de gráficos sempre renderiza o gráfico novamente para fornecer a melhor qualidade de imagem. Geralmente, é importante redimensionar o gráfico antes de exportá-lo para um arquivo ou para a área de transferência usando os comandos descritos na próxima seção.

## <a name="plot-window-commands"></a>Comandos da janela de gráficos

A barra de ferramentas da janela de gráficos contém comandos aplicáveis e a maioria deles também está disponível por meio do menu **Ferramentas do R** > **Gráficos**.

| Botão | Comando | Descrição | 
| --- | --- | --- |
| ![Botão Nova janela de gráficos](media/plotting-toolbar-01-new-plot-window.png) | Nova janela de gráficos | Cria uma janela de gráficos separada com seu próprio histórico. Consulte [Várias janelas de gráficos](#multiple-plot-windows). |
| ![Botão Ativar janela de gráficos](media/plotting-toolbar-02-activate-plot-window.png) | Ativar a janela de gráficos | Define a janela de gráficos atual como a janela ativa, de modo que os próximos comandos `plot` sejam renderizados para essa janela. Consulte [Várias janelas de gráficos](#multiple-plot-windows). Consulte [Várias janelas de gráficos](#multiple-plot-windows). |
| ![Botão Janela de histórico de gráficos](media/plotting-toolbar-03-plot-history.png) | Janela de histórico de gráficos | Abre uma janela com todos os gráficos no histórico mostrados como miniaturas. Consulte [Histórico de gráficos](#plot-history). |
| ![Botões Histórico de gráficos](media/plotting-toolbar-04-plot-history-arrows.png) | Gráfico anterior/seguinte |  Navega para gráfico anterior ou seguinte no histórico. Você também pode navegar no histórico com Ctrl + Alt + F11 (anterior) e Ctrl + Alt + F12 (seguinte). Consulte [Histórico de gráficos](#plot-history). |
| ![Botão Salvar como imagem](media/plotting-toolbar-05-save-as-image.png)| Salvar como imagem | Solicita um nome de arquivo e salva o gráfico atual (o conteúdo da janela, no tamanho da janela) em um arquivo de imagem. Os formatos disponíveis são `.png`, `.jpg`, `.bmp` e `.tif`. |
| ![Botão Salvar como PDF](media/plotting-toolbar-06-save-as-pdf.png)| Salvar como PDF | Salva o gráfico atual em um arquivo PDF, usando o tamanho da janela atual. O gráfico será renderizado novamente se o PDF for dimensionado. |
| ![Botão Copiar como bitmap](media/plotting-toolbar-07-copy-as-bitmap.png)| Copiar como bitmap | Copia o gráfico na área de transferência como um bitmap de varredura, usando o tamanho da janela atual. | 
| ![Botão Copiar como metarquivo](media/plotting-toolbar-08-copy-as-metafile.png)| Copiar como metarquivo | Copia o gráfico na área de transferência como um [metarquivo do Windows](https://en.wikipedia.org/wiki/Windows_Metafile) (Wikipédia). | 
| ![Botão Remover gráfico](media/plotting-toolbar-09-remove-plot.png)| Remover gráfico | Remove o gráfico atual do histórico. |
| ![Botão Limpar todos os gráficos](media/plotting-toolbar-10-clear-all-plots.png) | Limpar todos os gráficos | Remove todos os gráficos do histórico (solicita confirmação). |

## <a name="multiple-plot-windows"></a>Várias janelas de gráficos

Como os cientistas de dados geralmente trabalham com muitos gráficos de vários conjuntos de dados diferentes, as RTVS permitem criar quantas janelas de gráficos independentes forem necessárias. Em seguida, você pode organizar essas janelas da forma que desejar no quadro do Visual Studio ou completamente fora desse quadro. (Consulte [Personalização de layouts de janela no Visual Studio](../ide/customizing-window-layouts-in-visual-studio.md) para obter informações gerais sobre encaixe e redimensionando de janelas.)

É possível criar uma nova janela de gráficos usando o botão de barra de ferramentas ou **Ferramentas do R** > **Gráficos** > **Nova Janela de Gráficos**. A nova janela de gráficos se torna a janela *ativa*, que é onde os novos gráficos são renderizados. Para alterar a janela ativa, mude para ela e selecione o botão de barra de ferramentas **Ativar Janela de Gráficos** ou **Ferramentas do R** > **Gráficos** > **Ativar Janela de Gráficos**.

Os gráficos também são objetos independentes, o que significa que você pode copiá-los ou movê-los entre as janelas de gráficos usando o recurso do tipo “arrastar e soltar” com o mouse ou usando os comandos **Copiar**, **Recortar** e **Colar** no menu de contexto acionado com um clique do botão direito do mouse ou no menu **Editar**.

O comportamento padrão para ações do tipo "arrastar e soltar" é copiar. Para mover, arraste e solte mantendo pressionada a tecla **Shift**.

## <a name="plot-history"></a>Histórico de gráficos

Os comandos de gráficos são mantidos em um histórico de gráficos de cada janela, garantindo que todos os gráficos dentro de uma sessão sejam preservados. Para navegar no histórico, use os botões de seta na barra de ferramentas da janela de gráficos ou **Ctrl**+**Alt**+**F11** e **Ctrl**+**Alt**+**F12**. Você também pode remover gráficos individuais ou limpar todos os gráficos da janela, novamente usando os botões de barra de ferramentas ou os comandos de menu **Ferramentas do R** > **Gráficos**.

Para ver a coleção de gráficos inteira, abra a janela de histórico de gráficos usando o botão de barra de ferramentas ou **Ferramentas do R** > **Gráficos** > **Janela de Histórico de Gráficos**.
O histórico fornece uma lista de miniaturas dos gráficos que foram exibidos nessa janela, agrupadas por diferentes janelas de gráficos (ou dispositivos). Usar os botões de zoom na barra de ferramentas altera o tamanho das miniaturas.

![Janela de histórico de gráficos](media/plotting-plot-history-window.png)

Para abrir um gráfico em sua janela associada, clique duas vezes no gráfico e, em seguida, selecione o botão de barra de ferramentas **Mostrar gráfico** ou clique com o botão direito do mouse e selecione **Mostrar Gráfico**. Você também pode selecionar um gráfico individual e copiar, recortar ou excluir usando o menu de contexto acionado com um clique do botão direito do mouse ou o menu **Editar**.

O tempo de vida de seu histórico de gráficos em todas as janelas está vinculado ao tempo de vida da sessão interativa do R. Se você redefinir a sessão do R ou sair e reiniciar o Visual Studio, o histórico de gráficos será redefinido.

## <a name="programmatically-manipulate-plot-windows"></a>Manipular programaticamente janelas de gráficos

Você pode manipular as janelas de gráficos do código R de forma programática, usando números de dispositivo para identificar janelas de gráficos específicas. 

- `dev.list()`: listar todos os dispositivos de gráficos na sessão atual do R.
- `dev.new()`: criar um novo dispositivo de gráficos (uma nova janela de gráficos).
- `dev.set(<device number>)`: definir o dispositivo de gráficos ativo.
- `dev.off()`: excluir o dispositivo ativo.
