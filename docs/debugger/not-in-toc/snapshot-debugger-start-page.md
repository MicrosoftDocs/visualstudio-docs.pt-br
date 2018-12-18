---
title: Página inicial para o depurador de instantâneo
ms.date: 07/14/2018
robots: noindex, nofollow
ms.technology: vs-ide-debug
ms.topic: reference
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c7b5b48aeeb0cfcaeed72a06bfb6709892c58de7
ms.sourcegitcommit: e2373d40ca9829cee63519152a97172763471e21
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2018
ms.locfileid: "39310105"
---
# <a name="getting-started-with-the-snapshot-debugger"></a>Guia de Introdução com o depurador de instantâneo

O depurador de instantâneo do Visual Studio agora está conectado ao seu serviço, e você pode iniciar a coleta de instantâneos para ajudar na depuração.

Para usar o depurador de instantâneo, defina algumas snappoints em seu código, clique no botão para começar a coletar instantâneos e, em seguida, execute seu cenário. Quando o código é executado no qual você definiu um snappoint, é tirado um instantâneo do seu aplicativo. Em seguida, abra o instantâneo clicando no Visual Studio na janela ferramentas de diagnóstico. Agora você pode depurar o instantâneo de seu serviço exatamente como se fosse local. Para obter instruções detalhadas, continue lendo.

## <a name="collect-and-view-snapshots"></a>Coletar e exibir instantâneos

O depurador de instantâneo coleta instantâneos do seu aplicativo. Instantâneos são como as imagens do seu aplicativo em um ponto no tempo. Informar ao Visual Studio quando e onde coletar um instantâneo, definindo um snappoint no código. Snappoint, você define as condições que você precisa certificar-se de que você obter um instantâneo do problema que você está investigando.

### <a name="set-a-snappoint"></a>Defina um Snappoint

1. No editor de códigos, clique na medianiz esquerda ao lado de uma linha de código que você está interessado para definir um snappoint. Verifique se que ele é o código que você sabe que será executado. 

    ![Definindo um snappoint no Editor](../media/snapshot-startpage-set-snappoint.png)

    Um hexágono roxo aparece em que você clica no lado esquerdo.

2. Clique em **iniciar coleta** para ativar o snappoint.

### <a name="open-a-snapshot"></a>Abrir um instantâneo

1. Quando o snappoint for atingido, um instantâneo é exibida na janela de ferramentas de diagnóstico à direita. Se não abrir a janela, você pode abri-lo escolhendo **Debug** > **Windows** > **Mostrar ferramentas de diagnóstico**. 

    ![Instantâneo na janela de ferramentas de diagnóstico](../media/snapshot-startpage-diagsession-window.png)

2. Clique duas vezes o instantâneo para abri-lo.

### <a name="inspect-snapshot-data"></a>Inspecione os dados de instantâneo

Nessa exibição, é possível focalizar variáveis exibir DataTips, use os locais, inspeções, e chamar empilhar windows e também avaliar expressões.

O site em si ainda está ao vivo e os usuários finais não são afetados. Por padrão, apenas um instantâneo é capturado por snappoint. Ou seja, depois que um instantâneo é capturado, o snappoint seja desligada. Se você quiser capturar outro instantâneo no snappoint, você pode ativar o snappoint novamente clicando **atualizar coleção**.

### <a name="set-a-logpoint"></a>Defina um Logpoint

1. Um ícone de snappoint (o hexágono roxo) com o botão direito e escolha **configurações**.

2. No **configurações de Snappoint** janela, selecione **ações**.

    ![Condições de Snappoint](../media/snapshot-startpage-logpoint.png)

3. No **mensagem** , insira uma mensagem de log que você deseja registrar. Você também pode avaliar variáveis na sua mensagem de log, colocando-os entre chaves.

    Se você escolher **enviar para a janela de saída**, a mensagem será exibida na janela de ferramentas de diagnóstico quando o logpoint for atingido. 

    Se você escolher **enviar para log de aplicativo**, a mensagem será exibida em qualquer lugar que você pode ver mensagens de `System.Diagnostics.Trace` (ou `ILogger` no .NET Core), como o App Insights, quando o logpoint for atingido.

## <a name="learn-more"></a>Saiba Mais

Você pode encontrar mais informações sobre o depurador de instantâneo na [página de documentos](../debug-live-azure-applications.md). Saiba mais sobre como configurar condições para torná-lo mais fácil de encontrar bugs.

## <a name="dont-show-me-this-again"></a>Não ' Mostrar isso novamente

Para nunca mostrar a página de início de depurador de instantâneo novamente quando você conecta o depurador de instantâneo, alterar o **Mostrar 'Getting Started' página no início da sessão** opção **ferramentas**  >   **As opções** > **depurador de instantâneo**. 

![Página de opção de ferramenta de depurador de instantâneo](../media/snapshot-startpage-tools-options.png)
