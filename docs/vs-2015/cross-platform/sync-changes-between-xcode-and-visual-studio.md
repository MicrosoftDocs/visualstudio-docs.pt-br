---
title: Sincronizar alterações entre o XCode e o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c71a4d7c-120e-4559-a114-3a99c4b860a9
caps.latest.revision: 10
author: corob-msft
ms.author: corob
manager: ghogen
ms.openlocfilehash: 9187d4dcf4a88e672a245e0c589b3d75cf4f696a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51722108"
---
# <a name="sync-changes-between-xcode-and-visual-studio"></a>Sincronizar alterações entre o XCode e o Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O componente Microsoft Visual C++ para Desenvolvimento Móvel inclui funcionalidades remotas para sincronizar seu trabalho entre o computador e o Mac. Quando os computadores do Visual Studio e do Mac são emparelhados, novas opções ficam disponíveis para projetos de Aplicativos do iOS no Visual Studio que podem ser usadas para abrir o projeto no XCode, mover o código entre o XCode e o Visual Studio e limpar o diretório de projeto temporário do XCode.  
  
 Para usar as opções de Computador Remoto, o projeto deve ser um projeto de Aplicativo do iOS e o Visual Studio deve ser emparelhado com o Mac. Para obter pré-requisitos e instruções sobre como emparelhar um Mac, consulte [Instalar e configurar ferramentas para compilar usando o iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md).  
  
## <a name="the-remote-machine-menu"></a>O menu Computador Remoto  
 Em **Gerenciador de Soluções**, clique com o botão direito do mouse em um projeto de Aplicativo do iOS para mostrar o menu de contexto. Selecione o item **Computador Remoto** para mostrar as opções remotas disponíveis.  
  
 ![O item de menu Computador Remoto no Gerenciador de Soluções](../cross-platform/media/cppmdd-u2-remotemachine-menu.jpg "CPPMDD_U2_RemoteMachine_Menu")  
  
 Esses comandos permitem abrir o projeto no XCode, mover alterações locais ou todo o projeto entre o Visual Studio e o XCode e limpar os arquivos temporários no computador remoto.  
  
### <a name="open-in-xcode"></a>Abrir no XCode  
 Para abrir o projeto no XCode por meio do Visual Studio, no submenu **Computador Remoto**, escolha **Abrir no XCode** para abrir o projeto selecionado no computador remoto emparelhado. O servidor vcremote é usado para abrir o XCode no Mac e navegar para um diretório temporário criado no Mac que contém uma cópia do projeto. O Visual Studio exibe uma caixa de diálogo que mostra o diretório temporário usado para o projeto. As ações realizadas no computador remoto também são mostradas na janela **Saída** do Visual Studio. Para vê-las, talvez você precise selecionar **Computador Remoto do Visual C++** na lista suspensa **Mostrar saída de** na parte superior da janela **Saída**.  
  
 ![A janela Saída mostra as ações do computador remoto.](../cross-platform/media/cppmdd-u2-remotemachine-output.png "CPPMDD_U2_RemoteMachine_Output")  
  
 No Mac, é possível usar todas as ferramentas do XCode para editar o código e recursos, storyboards e ações. No Visual Studio, o projeto de Aplicativo do iOS é anotado com “Aberto no XCode” para indicar que podem ser feitas alterações no computador remoto. Depois que as edições forem concluídas, é possível usar os comandos Efetuar Pull de Remoto ou Pull Incremental de Remoto para copiar as alterações de volta para o projeto do Visual Studio.  
  
### <a name="push-to-remote-and-incremental-push-to-remote"></a>Enviar por Push para Remoto e Push Incremental para Remoto  
 Se você tiver feito alterações no projeto de Aplicativo do iOS no Visual Studio, os comandos Enviar por Push para Remoto e Push Incremental para Remoto poderão ser usados para mover os arquivos de projeto alterados para o computador remoto emparelhado. O comando Enviar por Push para Remoto copia todos os arquivos de projeto para o computador remoto. O comando Push Incremental para Remoto copia apenas os arquivos alterados para o computador remoto. Para projetos grandes com pequenas alterações, o comando incremental pode economizar tempo e largura de banda.  
  
 Para copiar os arquivos de projeto para o Mac, no Visual Studio, na janela **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto de Aplicativo do iOS para abrir o menu de contexto. Selecione **Computador Remoto** e escolha **Enviar por Push para Remoto** ou **Push Incremental para Remoto** para copiar os arquivos de projeto do Visual Studio para o Mac.  
  
### <a name="pull-from-remote-and-incremental-pull-from-remote"></a>Efetuar Pull de Remoto e Pull Incremental de Remoto  
 Depois de fazer alterações ao projeto no XCode, mova as alterações de volta para o Visual Studio para manter os projetos em sincronização.  
  
 Para copiar os arquivos de projeto do Mac, no Visual Studio, na janela **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto de Aplicativo do iOS para abrir o menu de contexto. Selecione **Computador Remoto** e escolha **Efetuar Pull de Remoto** ou **Pull Incremental de Remoto** para copiar os arquivos de projeto do Mac para o Visual Studio.  
  
### <a name="clean-remote"></a>Limpar Remoto  
 É possível usar o comando Limpar Remoto para excluir os arquivos no diretório de projeto temporário no computador remoto. O conteúdo do diretório, incluindo arquivos de origem ou produtos de build, é removido do Mac. Verifique se você sincronizou todas as alterações que deseja manter de volta para o Visual Studio usando Efetuar Pull de Remoto ou Pull Incremental de Remoto antes de usar o comando Limpar Remoto.  
  
 Para limpar o diretório de projeto temporário no computador remoto, no Visual Studio, na janela **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto de Aplicativo do iOS para abrir o menu de contexto. Selecione **Computador Remoto** e escolha **Limpar Remoto** para remover os arquivos do diretório de projeto do Mac.

