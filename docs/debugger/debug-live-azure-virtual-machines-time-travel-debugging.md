---
title: Depuração de viagem no tempo ASP.NET em tempo real na VM do Azure
description: Saiba como registrar e repetir aplicativos ASP.NET em máquinas virtuais do Azure usando o Depurador de Instantâneos.
ms.custom: SEO-VS-2020
ms.date: 04/11/2019
ms.topic: how-to
helpviewer_keywords:
- debugger
author: poppastring
ms.author: madownie
manager: andster
monikerRange: '>= vs-2019'
ms.workload:
- aspnet
- azure
ms.openlocfilehash: f8aabb109de02a1beec326407472a841fe16425a
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798447"
---
# <a name="record-and-replay-live-aspnet-apps-on-azure-virtual-machines-using-the-snapshot-debugger"></a>Registrar e repetir aplicativos ASP.NET em máquinas virtuais do Azure usando o Depurador de Instantâneos

A versão prévia da TTD (Depuração de Viagem no Tempo) no Visual Studio Enterprise fornece a capacidade de registrar um aplicativo Web em execução em uma VM (Máquina Virtual) do Azure e, em seguida, reconstruir e repetir com precisão o caminho de execução. O TTD se integra ao Depurador de Instantâneos e permite que você rewind e replay cada linha de código quantas vezes você quiser, ajudando você a isolar e identificar problemas que podem ocorrer apenas em ambientes de produção.

Capturar uma gravação TTD não interromperá o aplicativo. No entanto, a gravação de TDD adiciona sobrecarga significativa ao seu processo de execução, retardando-o com base em fatores que incluem o tamanho do processo e o número de threads ativos.

Esse recurso está em versão prévia para o lançamento do Visual Studio 2019 com uma licença go live.

Neste tutorial, você irá:

> [!div class="checklist"]
> * Iniciar o Depurador de Instantâneos com a Depuração de Viagem no Tempo habilitada
> * Definir um snappoint e coletar uma gravação de viagem no tempo
> * Iniciar a depuração de uma gravação de viagem no tempo

## <a name="prerequisites"></a>Pré-requisitos

* A Depuração de Viagem no Tempo para VMs (Máquinas Virtuais) do Azure só está disponível para o Visual Studio 2019 Enterprise ou superior com a carga de trabalho **de desenvolvimento do Azure**. (Na guia **Componentes individuais**,é possível encontrá-lo em **Depuração e testes** > **Depurador de instantâneos**).

    Se ele ainda não estiver instalado, instale o [Visual Studio 2019 Enterprise.](https://visualstudio.microsoft.com/vs/)

* A Depuração de Viagem no Tempo está disponível para os seguintes aplicativos Web de VM do Azure:
  * ASP.NET aplicativos (AMD64) em execução .NET Framework 4.8 ou posterior.

## <a name="start-the-snapshot-debugger-with-time-travel-debugging-enabled"></a>Iniciar o Depurador de Instantâneos com a Depuração de Viagem no Tempo habilitada

1. Abra o projeto para o qual você gostaria de coletar uma gravação de viagem no tempo.

    > [!IMPORTANT]
    > Para iniciar o TTD, você precisa abrir *a* mesma versão do código-fonte publicada no serviço de VM do Azure.

1. Escolha **Depurar > Anexar Depurador de Instantâneos...**. Selecione a VM do Azure em que seu aplicativo Web está implantado e uma conta de armazenamento do Azure. Selecione a opção **habilitar visualização de viagem de tempo de depuração** e clique em **anexar**.

      ![Selecionar recurso do Azure](../debugger/media/time-travel-debugging-select-azure-resource-vm.png)

    > [!IMPORTANT]
    > Na primeira vez que você selecionar **Anexar Depurador de Instantâneos** para sua VM, o IIS será reiniciado automaticamente.

    Os metadados dos **módulos** não são ativados inicialmente. Navegue até o aplicativo Web e o botão **Iniciar coleção** é ativado. O Visual Studio agora está no modo de depuração de instantâneos.

   ![Modo de depuração de instantâneos](../debugger/media/snapshot-message.png)

    > [!NOTE]
    > A extensão de site do Application Insights também dá suporte à depuração de instantâneos. Se você encontrar uma mensagem de erro "extensão de site desatualizada", veja [dicas de solução de problemas e problemas conhecidos da depuração de instantâneos](../debugger/debug-live-azure-apps-troubleshooting.md) para atualizar os detalhes.

   A janela **módulos** mostra quando todos os módulos são carregados para a VM do Azure (escolha **depurar > módulos do Windows >** para abrir esta janela).

   ![Verificar a janela Módulos](../debugger/media/snapshot-modules.png)

## <a name="set-a-snappoint-and-collect-a-time-travel-recording"></a>Definir um snappoint e coletar um horário de gravação de viagem

1. No editor de código, clique na medianiz à esquerda em um método em que você esteja interessado para definir um snappoint. Verifique se esse é o código que você sabe que será executado.

   ![Definir um snappoint](../debugger/media/time-travel-debugging-set-snappoint-settings.png)

1. Clique com o botão direito do mouse no ícone de snappoint (a bola vazia) e escolha **ações**. Na janela **configurações de instantâneo** , clique na caixa de seleção **ação** . Em seguida, clique na caixa de seleção **coletar um rastreamento de viagem de tempo até o final deste método** .

   ![Coletar um rastreamento de viagem de tempo até o final do método](../debugger/media/time-travel-debugging-set-snappoint-action.png)

1. Clique em **Iniciar Coleção** para ativar o snappoint.

   ![Ativar o snappoint](../debugger/media/snapshot-start-collection.png)

## <a name="take-a-snapshot"></a>Tirar um instantâneo

Quando um snappoint é ativado, ele captura um instantâneo sempre que a linha de código em que o snappoint é colocado é executado. Essa execução pode ser causada por uma solicitação real no servidor. Para forçar o snappoint a ser atingido, vá para a exibição de navegador do seu site e realize as ações necessárias que fazem com que o snappoint seja atingido.

## <a name="start-debugging-a-time-travel-recording"></a>Começar a depurar uma gravação de viagem de tempo

1. Quando o snappoint for atingido, um instantâneo será exibido na janela de Ferramentas de Diagnóstico. Para abrir essa janela, escolha **Depurar > Janelas > Mostrar Ferramentas de Diagnóstico**.

   ![Abrir um snappoint](../debugger/media/snapshot-diagsession-window.png)

1. Clique no link exibir instantâneo para abrir a hora de gravação de viagem no editor de códigos.
  
   Você pode executar cada linha de código registrada pelo TTD usando os botões **continue** e **Reverse continue** . Além disso, a barra de ferramentas de **depuração** pode ser usada para **mostrar a próxima instrução** **, entrar, passar** **por** etapas, **sair**, voltar para, voltar **para** **trás,** **voltar.**

   ![Iniciar Depuração](../debugger/media/time-travel-debugging-step-commands.png)

   Você também pode usar as janelas **locais**, **inspeções** e **pilha de chamadas** e também avaliar expressões.

   ![Inspecionar dados de instantâneo](../debugger/media/time-travel-debugging-start-debugging.png)

    O próprio site ainda é dinâmico e os usuários finais não são afetados por nenhuma atividade TTD subsequente. Apenas um instantâneo é capturado por snappoint por padrão: após a captura de um instantâneo, o snappoint é desativado. Se você quiser capturar outro instantâneo no snappoint, poderá ativar o snappoint novamente clicando em **Atualizar Coleção**.

**Precisa de ajuda?** Consulte as páginas [Solução de problemas e problemas conhecidos](../debugger/debug-live-azure-apps-troubleshooting.md) e [Perguntas frequentes sobre depuração de instantâneo](../debugger/debug-live-azure-apps-faq.yml).

## <a name="set-a-conditional-snappoint"></a>Definir um snappoint condicional

Se você tiver dificuldades para recriar um estado específico em seu aplicativo, considere se o uso de um snappoint condicional pode ajudar. O snappoints condicional ajuda a evitar a coleta de um tempo de gravação de viagem até que o aplicativo Insira um estado desejado, como quando uma variável tem um valor específico que você deseja inspecionar. [Você pode definir condições usando expressões, filtros ou contagens de acertos](../debugger/debug-live-azure-apps-troubleshooting.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a coletar uma gravação de viagem no tempo para Máquinas Virtuais do Azure. Talvez você queira ler mais detalhes sobre Depurador de Instantâneos.

> [!div class="nextstepaction"]
> [Perguntas frequentes sobre depuração de instantâneo](../debugger/debug-live-azure-apps-faq.yml)