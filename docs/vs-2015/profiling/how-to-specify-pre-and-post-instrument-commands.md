---
title: Como especificar comandos pré e pós-instrumento | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.performance.property.instrument
helpviewer_keywords:
- profiling tools, pre-instrument events
- events [Visual Studio], pre-instrument
- pre-instrument events, performance tools
ms.assetid: 6a8d5340-1d1b-4d81-88dd-8e1f435eb828
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b88d49be8ee4651d82135b3e8d27bef8218ffd43
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51772216"
---
# <a name="how-to-specify-pre--and-post-instrument-commands"></a>Como especificar comandos pré e pós-instrumento
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode especificar comandos que são executados antes ou depois que os binários em uma sessão de desempenho são instrumentados. Qualquer comando que pode ser emitido na linha de comando pode ser especificado como um evento pré-instrumento ou pós-instrumento. Por exemplo, é possível especificar comandos que automatizam a desistência de um assembly com uma chave de nome forte em um arquivo de lote que é executado depois que os binários são instrumentados.  
  
 Você pode especificar comandos para todos os binários instrumentados na execução da criação de perfil ou para binários individuais. No entanto, você pode especificar apenas um comando pré-instrumento para ser executado antes e apenas um comando pós-instrumento para ser executado após o processo de instrumentação. Não é possível especificar comandos para todos os binários e para binários individuais ao mesmo tempo. Ao especificar comandos para todos os binários, os comandos são executados antes ou depois da instrumentação de cada binário na sessão.  
  
 **Requisitos**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  O diretório de trabalho no qual os comandos são executados depende do sistema operacional em que você está executando o [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] e da plataforma de destino do aplicativo analisado.  
  
  **Computadores de 32 bits**  
  
  Em computadores de 32 bits, o diretório das ferramentas de criação de perfil padrão é Drive\Program Files\Microsoft Visual Studio 10.0\Team Tools\Performance Tools.  
  
  **Computadores de 64 bits**  
  
  Em computadores de 64 bits, especifique o caminho de acordo com a plataforma de destino do aplicativo analisado:  
  
- No caso de aplicativos de 32 bits, o diretório padrão das ferramentas de criação de perfil é:  
  
   *Unidade*\Arquivos de Programas (x86)\Microsoft Visual Studio 10.0\Team Tools\Performance Tools  
  
- No caso de aplicativos de 64 bits, o diretório padrão das ferramentas de criação de perfil é:  
  
   *Unidade*\Arquivos de Programas (x86)\Microsoft Visual Studio 10.0\Team Tools\Performance Tools\x64  
  
### <a name="to-specify-pre-instrument-commands"></a>Para especificar comandos pré-instrumentos  
  
1.  Execute uma das seguintes etapas:  
  
    -   Para especificar comandos pré-instrumentos para todos os binários em uma sessão de desempenho, selecione o nó da sessão de desempenho no **Gerenciador de Desempenho** e, em seguida, clique com botão direito do mouse e selecione **Propriedades**.  
  
    -   Para especificar comandos pré-instrumentos para um binário específico, clique com o botão direito do mouse no nome do binário na lista de **Destinos** da sessão de desempenho e, em seguida, selecione **Propriedades**.  
  
2.  Nas **Páginas de Propriedades**, clique em **Instrumentação**.  
  
3.  Digite o comando na caixa de texto **Linha de comando** em **Eventos Pré-Instrumento**.  
  
    > [!NOTE]
    >  Você pode clicar no botão de reticências **(...)** ao lado da caixa **Linha de comando** para navegar até o arquivo apropriado .exe, .cmd ou .bat e selecioná-lo.  
  
4.  Clique em **OK**.  
  
     Para desabilitar a execução do comando sem removê-lo, selecione a caixa de seleção **Excluir da instrumentação**. Para modificar as configurações do vinculador ou do compilador, use as páginas de propriedades do projeto.  
  
### <a name="to-specify-post-instrument-commands"></a>Para especificar comandos pós-instrumentos  
  
1.  Execute uma das seguintes etapas:  
  
    -   Para especificar comandos pós-instrumentos para todos os binários em uma sessão de desempenho, selecione o nó da sessão de desempenho no **Gerenciador de Desempenho** e, em seguida, clique com botão direito do mouse e selecione **Propriedades**.  
  
    -   Para especificar comandos pós-instrumentos para um binário específico, clique com o botão direito do mouse no nome do binário na lista de **Destinos** da sessão de desempenho e, em seguida, selecione **Propriedades**.  
  
2.  Nas **Páginas de Propriedades**, clique em **Instrumentação**.  
  
3.  Digite o comando na caixa de texto **Linha de comando** em **Eventos Pós-Instrumento**.  
  
    > [!NOTE]
    >  Você pode clicar no botão de reticências **(...)** ao lado da caixa **Linha de comando** para navegar até o arquivo apropriado .exe, .cmd ou .bat e selecioná-lo.  
  
4.  Clique em **OK**.  
  
     Para desabilitar a execução do comando sem removê-lo, selecione a caixa de seleção **Excluir da instrumentação**. Para modificar as configurações do vinculador ou do compilador, use as páginas de propriedades do projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Configurando sessões de desempenho](../profiling/configuring-performance-sessions.md)



