---
title: Como especificar comandos pré e pós-instrumento | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.property.instrument
helpviewer_keywords:
- profiling tools, pre-instrument events
- events [Visual Studio], pre-instrument
- pre-instrument events, performance tools
ms.assetid: 6a8d5340-1d1b-4d81-88dd-8e1f435eb828
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: ba91e04342b9b78e3c6acae5296857a6f00f2aba
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329000"
---
# <a name="how-to-specify-pre--and-post-instrument-commands"></a>Como especificar comandos de pré e pós-instrumentação

Você pode especificar comandos que são executados antes ou depois que os binários em uma sessão de desempenho são instrumentados. Qualquer comando que pode ser emitido na linha de comando pode ser especificado como um evento pré-instrumento ou pós-instrumento. Por exemplo, é possível especificar comandos que automatizam a desistência de um assembly com uma chave de nome forte em um arquivo de lote que é executado depois que os binários são instrumentados.

Você pode especificar comandos para todos os binários instrumentados na execução da criação de perfil ou para binários individuais. No entanto, você pode especificar apenas um comando pré-instrumento para ser executado antes e apenas um comando pós-instrumento para ser executado após o processo de instrumentação. Não é possível especificar comandos para todos os binários e para binários individuais ao mesmo tempo. Ao especificar comandos para todos os binários, os comandos são executados antes ou depois da instrumentação de cada binário na sessão.

O diretório de trabalho no qual os comandos são executados depende do sistema operacional em que você está executando o [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] e da plataforma de destino do aplicativo analisado.

Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).

## <a name="to-specify-pre-instrument-commands"></a>Para especificar comandos pré-instrumentos

1. Execute uma das seguintes etapas:

    - Para especificar comandos pré-instrumentos para todos os binários em uma sessão de desempenho, selecione o nó da sessão de desempenho no **Gerenciador de Desempenho** e, em seguida, clique com botão direito do mouse e selecione **Propriedades**.

    - Para especificar comandos pré-instrumentos para um binário específico, clique com o botão direito do mouse no nome do binário na lista de **Destinos** da sessão de desempenho e, em seguida, selecione **Propriedades**.

2. Nas **Páginas de Propriedades**, clique em **Instrumentação**.

3. Digite o comando na caixa de texto **Linha de comando** em **Eventos Pré-Instrumento**.

    > [!NOTE]
    > Você pode clicar no botão de reticências **(...)** que está adjacente à caixa de **linha de comando** para procurar e selecionar o arquivo. exe,. cmd ou. bat apropriado.

4. Clique em **OK**.

     Para desabilitar a execução do comando sem removê-lo, selecione a caixa de seleção **Excluir da instrumentação**. Para modificar as configurações do vinculador ou do compilador, use as páginas de propriedades do projeto.

## <a name="to-specify-post-instrument-commands"></a>Para especificar comandos pós-instrumentos

1. Execute uma das seguintes etapas:

    - Para especificar comandos pós-instrumentos para todos os binários em uma sessão de desempenho, selecione o nó da sessão de desempenho no **Gerenciador de Desempenho** e, em seguida, clique com botão direito do mouse e selecione **Propriedades**.

    - Para especificar comandos pós-instrumentos para um binário específico, clique com o botão direito do mouse no nome do binário na lista de **Destinos** da sessão de desempenho e, em seguida, selecione **Propriedades**.

2. Nas **Páginas de Propriedades**, clique em **Instrumentação**.

3. Digite o comando na caixa de texto **Linha de comando** em **Eventos Pós-Instrumento**.

    > [!NOTE]
    > Você pode clicar no botão de reticências **(...)** que está adjacente à caixa de **linha de comando** para procurar e selecionar o arquivo. exe,. cmd ou. bat apropriado.

4. Clique em **OK**.

     Para desabilitar a execução do comando sem removê-lo, selecione a caixa de seleção **Excluir da instrumentação**. Para modificar as configurações do vinculador ou do compilador, use as páginas de propriedades do projeto.

## <a name="see-also"></a>Veja também

[Configurar sessões de desempenho](../profiling/configuring-performance-sessions.md)
