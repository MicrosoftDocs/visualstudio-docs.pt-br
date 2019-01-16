---
title: O que há de novo no depurador no Visual Studio 2017 | Microsoft Docs
ms.date: 01/22/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, what's new
- what's new [debugger]
- debugging [Visual Studio], what's new
- what's new [Visual Studio], debugging
ms.assetid: 2aed9caa-2384-4e49-8595-82d8b06cf271
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fbc48fdc93feebf2f78b6d11ae2b7cc744c46f98
ms.sourcegitcommit: 38db86369af19e174b0aba59ba1918a5c4fe4a61
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54269729"
---
# <a name="whats-new-for-the-debugger-in-includevsdev15miscincludesvsdev15mdmd"></a>O que há de novo no depurador no [!include[vs_dev15](../misc/includes/vs_dev15_md.md)]

O depurador inclui esses novos recursos:

- Uma novidade na versão 15.5, o **Depurador de Instantâneos** tira um instantâneo de seus aplicativos em produção quando o código no qual você está interessado é executado. Para instruir o depurador a tirar um instantâneo, defina snappoints e logpoints em seu código. O depurador permite ver exatamente o que deu errado sem afetar o tráfego do seu aplicativo de produção. O Depurador de Instantâneo pode ajudar a reduzir drasticamente o tempo que leva para resolver problemas que ocorrem em ambientes de produção.

    A coleção de instantâneos está disponível para os seguintes aplicativos Web em execução no Serviço de Aplicativo do Azure:

  * Aplicativos ASP.NET em execução no .NET Framework 4.6.1 ou posterior.
  * Aplicativos ASP.NET Core em execução no .NET Core 2.0 ou posterior no Windows.

    Para obter mais informações, confira [Depurar aplicativos ASP.NET dinâmicos usando o Depurador de Instantâneos](../debugger/debug-live-azure-applications.md).

- Novidade na versão 15.5, apenas, no Visual Studio Enterprise **retrocesso do IntelliTrace** tira um instantâneo do seu aplicativo em cada ponto de interrupção e o depurador automaticamente a eventos de etapa. Os instantâneos registrados permitem retornar aos pontos de interrupção ou às etapas anteriores e exibir o estado do aplicativo como ele era no passado. O retrocesso do IntelliTrace poderá poupar seu tempo quando você desejar ver o estado do aplicativo anterior, mas não desejar reiniciar a depuração nem recriar o estado do aplicativo desejado.

    É possível navegar e exibir instantâneos usando os botões **Voltar** e **Avançar** na barra de ferramentas Depurar. Esses botões navegam pelos eventos exibidos na guia **Eventos** na janela **Ferramentas de Diagnóstico**.

    ![Botões Voltar e Avançar Etapa](../debugger/media/intellitrace-step-back-icons-description.png  "Botões Voltar e Avançar Etapa")

    Para obter mais informações, confira a página [Inspecionar estados anteriores do aplicativo usando o IntelliTrace](../debugger/view-historical-application-state.md).

- O **auxiliar de exceção** substitui o Assistente de exceção e aparece em uma caixa de diálogo não modal onde ocorreu o erro. O **auxiliar de exceção** fornece um acesso mais rápido para quaisquer exceções internas, análises adicionais pelo depurador (se disponível) e ter acesso imediato à **configurações de exceção** da exceção. O auxiliar de exceção também podem ser arrastado para um modo de exibição flutuante se ele está bloqueando algo que você precisa ver.

    Por exemplo, uma **NullReferenceException** agora mostra a variável que tem a referência nula (informações extras).

    ![Auxiliar de exceção do depurador](../debugger/media/dbg-exception-helper.png "DbgExceptionHelper")

    Para obter mais informações, consulte a postagem de blog [Usando o novo Auxiliar de Exceção no Visual Studio](https://blogs.msdn.microsoft.com/visualstudioalm/2016/03/31/using-the-new-exception-helper-in-visual-studio-15-preview/).

- Agora você pode executar para uma linha de código enquanto está em pausa no depurador, selecionando o **executar para este lugar** ícone de seta verde (você verá o ícone ao passar o mouse sobre uma linha de código). Isso elimina a necessidade de definir pontos de interrupção temporários.

    ![Depurador do executar com um clique](../debugger/media/dbg-run-to-click.png "DbgRunToClick")

- Você pode definir condições de exceções na **configurações de exceção** caixa de diálogo (você pode fazer isso usando o **Editar condição** ícone na caixa de diálogo Configurações de exceção ou por meio do menu do botão direito do mouse no exceção). Condições com suporte no momento incluem os nomes de módulo para incluir ou excluir da exceção.

    ![Condições em uma exceção](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

- Anexe ao processo, caixa de diálogo inclui um novo recurso de pesquisa que pode ajudá-lo mais rapidamente identificar o que você precisa anexar ao processo.

    ![Pesquisar em Anexar ao processo](../debugger/media/dbg-attach-to-process-search.png "DbgAttachToProcessSearch")

Para obter mais informações sobre esses novos recursos, consulte a [notas de versão do [!include[vs_dev15](../misc/includes/vs_dev15_md.md)] ](/visualstudio/releasenotes/vs2017-relnotes#debuggingdiag).

## <a name="see-also"></a>Consulte também

- [Depurando no Visual Studio](../debugger/index.md)
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)