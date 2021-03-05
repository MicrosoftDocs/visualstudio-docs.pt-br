---
description: O Depurador de Instantâneos do Visual Studio agora está conectado ao seu serviço e você pode começar a coletar instantâneos para ajudar na depuração.
title: Página inicial do Depurador de Instantâneos
ms.date: 07/14/2018
robots: noindex, nofollow
ms.topic: reference
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 96e0c6196d99b8a2b7ac9b4187dbd1397111abbd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160336"
---
# <a name="getting-started-with-the-snapshot-debugger"></a>Introdução com o Depurador de Instantâneos

O Depurador de Instantâneos do Visual Studio agora está conectado ao seu serviço e você pode começar a coletar instantâneos para ajudar na depuração.

Para usar o Depurador de Instantâneos, defina alguns snappoints em seu código, clique no botão para começar a coletar instantâneos e, em seguida, execute seu cenário. Quando o código é executado no qual você definiu um snappoint, um instantâneo do seu aplicativo é obtido. Em seguida, abra o instantâneo clicando nele no Visual Studio na janela Ferramentas de Diagnóstico. Agora você pode depurar o instantâneo de seu serviço da mesma forma que era local. Para obter instruções detalhadas, continue lendo.

## <a name="collect-and-view-snapshots"></a>Coletar e exibir instantâneos

O Depurador de Instantâneos coleta instantâneos do seu aplicativo. Os instantâneos são como imagens de seu como em um ponto no tempo. Você informa ao Visual Studio quando e onde coletar um instantâneo definindo um snappoint no código. No snappoint, você define quaisquer condições necessárias para certificar-se de obter um instantâneo do problema que está investigando.

### <a name="set-a-snappoint"></a>Definir um Snappoint

1. No editor de código, clique na medianiz à esquerda ao lado de uma linha de código em que você está interessado para definir um snappoint. Verifique se o código que você sabe que será executado.

    ![Configurando um snappoint no editor](../media/snapshot-startpage-set-snappoint.png)

    Um hexágono roxo aparece onde você clica à esquerda.

2. Clique em **Iniciar Coleção** para ativar o snappoint.

### <a name="open-a-snapshot"></a>Abrir um instantâneo

1. Quando o snappoint é atingido, um instantâneo é exibido na janela de Ferramentas de Diagnóstico à direita. Se a janela não abrir, você poderá abri-la escolhendo **depurar**  >  **janelas**  >  **Mostrar ferramentas de diagnóstico**.

    ![Instantâneo na janela de Ferramentas de Diagnóstico](../media/snapshot-startpage-diagsession-window.png)

2. Clique duas vezes no instantâneo para abri-lo.

### <a name="inspect-snapshot-data"></a>Inspecionar dados de instantâneo

Nessa exibição, você pode passar o mouse sobre as variáveis para exibir DataTips; use as janelas Locais, Inspeções e Pilha de Chamadas e também avalie expressões.

O site em si ainda fica ativo, e os usuários finais não são afetados. Por padrão, apenas um instantâneo é capturado por snappoint. Ou seja, depois que um instantâneo é capturado, o snappoint desliga. Se você quiser capturar outro instantâneo no snappoint, poderá ativar o snappoint novamente clicando em **Atualizar Coleção**.

### <a name="set-a-logpoint"></a>Definir um Logpoint

1. Clique com o botão direito do mouse em um ícone de snappoint (o hexágono roxo) e escolha **configurações**.

2. Na janela **configurações do Snappoint** , selecione **ações**.

    ![Condições de Snappoint](../media/snapshot-startpage-logpoint.png)

3. No campo **mensagem** , insira uma mensagem de log que você deseja registrar. Você também pode avaliar variáveis na sua mensagem de log colocando-as entre chaves.

    Se você escolher **Enviar para janela de saída**, a mensagem aparecerá na janela ferramentas de diagnóstico quando o logpoint for atingido.

    Se você escolher **Enviar para o log do aplicativo**, a mensagem será exibida em qualquer lugar que você possa ver as mensagens do `System.Diagnostics.Trace` (ou `ILogger` no .NET Core), como o app insights, quando o logpoint for atingido.

## <a name="learn-more"></a>Saiba mais

Você pode encontrar mais informações sobre o Depurador de Instantâneos na [página de documentos](../debug-live-azure-applications.md). Saiba mais sobre como definir condições para facilitar a localização de bugs.

## <a name="dont-show-me-this-again"></a>Não mostrar novamente

Para nunca mostrar a depurador de instantâneos página inicial novamente ao conectar o depurador de instantâneos, altere a **página Mostrar ' Introdução ' na** opção de início da sessão em **ferramentas**  >  **Opções**  >  **depurador de instantâneos**.

![Página de opções da ferramenta de Depurador de Instantâneos](../media/snapshot-startpage-tools-options.png)
