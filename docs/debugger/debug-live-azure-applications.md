---
title: Depurar aplicativos do Azure do ASP.NET em tempo real
description: Saiba como configurar o snappoints e exibir instantâneos com o depurador de instantâneo.
ms.custom: mvc
ms.date: 03/16/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- debugger
ms.assetid: adb22512-4d4d-40e5-9564-1af421b7087e
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
- azure
ms.openlocfilehash: b7f98dccebe9db183c63c6f859ceb2234fdb1acf
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53056912"
---
# <a name="debug-live-aspnet-azure-apps-using-the-snapshot-debugger"></a>Depurar aplicativos em tempo real do Azure do ASP.NET usando o depurador de instantâneo

O depurador de instantâneo tira um instantâneo de seus aplicativos em produção, quando o código que você está interessado é executado. Para instruir o depurador a tirar um instantâneo, defina snappoints e logpoints em seu código. O depurador permite ver exatamente o que deu errado sem afetar o tráfego do seu aplicativo de produção. O Depurador de Instantâneo pode ajudar a reduzir drasticamente o tempo que leva para resolver problemas que ocorrem em ambientes de produção.

Snappoints e logpoints são semelhantes aos pontos de interrupção, mas ao contrário de pontos de interrupção, snappoints não interrompem o aplicativo quando atingidos. Normalmente, capturando um instantâneo em um snappoint leva 10 a 20 milissegundos.

Neste tutorial, você irá:

> [!div class="checklist"]
> * Inicie o depurador de instantâneo
> * Defina um snappoint e exibir um instantâneo
> * Defina um logpoint

## <a name="prerequisites"></a>Pré-requisitos

* Depurador de instantâneos só está disponível para o Visual Studio 2017 Enterprise versão 15.5 ou posterior com o **carga de trabalho de desenvolvimento ASP.NET e web**. Para o ASP.NET Core, você também precisa de **desenvolvimento do .NET Core** carga de trabalho instalada.

    Se ainda não estiver instalado, instale [Visual Studio 2017 Enterprise versão 15.5](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) ou posterior. Se você estiver atualizando de uma instalação anterior do Visual Studio 2017, execute o instalador do Visual Studio e verifique o componente do depurador de instantâneos **carga de trabalho de desenvolvimento ASP.NET e web**.

* Plano de serviço de aplicativo do Azure básico ou superior.

* A coleção de instantâneos está disponível para os seguintes aplicativos Web em execução no Serviço de Aplicativo do Azure:

    * Aplicativos ASP.NET em execução no .NET Framework 4.6.1 ou posterior.
    * Aplicativos ASP.NET Core em execução no .NET Core 2.0 ou posterior no Windows.

## <a name="open-your-project-and-start-the-snapshot-debugger"></a>Abra seu projeto e iniciar o depurador de instantâneo

1. Abra o projeto que você gostaria de depuração de instantâneo.

    > [!IMPORTANT]
    > A depuração de instantâneo, você precisará abrir o **mesma versão do código-fonte** que é publicado ao serviço de aplicativo do Azure.

1. No Gerenciador de nuvem (**exibição > Gerenciador de nuvem**), o serviço de aplicativo do Azure seu projeto é implantado com o botão direito e selecione **Anexar depurador de instantâneo**.

   ![Iniciar o depurador de instantâneo](../debugger/media/snapshot-launch.png)

    Na primeira vez que você seleciona **anexar o depurador de instantâneo**, você será solicitado a instalar a extensão de site do depurador de instantâneo em seu serviço de aplicativo do Azure. Esta instalação requer uma reinicialização do serviço de aplicativo do Azure.

   Visual Studio agora está no modo de depuração de instantâneo.

    > [!NOTE]
    > A extensão de site do Application Insights também dá suporte à depuração de instantâneo. Se você encontrar uma mensagem de erro "desatualizados da extensão de site", consulte [solução de problemas e problemas conhecidos para depuração de instantâneo](../debugger/debug-live-azure-apps-troubleshooting.md) para atualizar os detalhes.

   ![Modo de depuração de instantâneo](../debugger/media/snapshot-message.png)

   O **módulos** janela mostra quando todos os módulos de tem carregado para o serviço de aplicativo do Azure (escolher **depurar / Windows / módulos** para abrir essa janela).

   ![Verifique a janela módulos](../debugger/media/snapshot-modules.png)

## <a name="set-a-snappoint"></a>Defina um snappoint

1. No editor de códigos, clique na medianiz esquerda ao lado de uma linha de código que você está interessado para definir um snappoint. Verifique se que ele é o código que você sabe que será executado.

   ![Defina um snappoint](../debugger/media/snapshot-set-snappoint.png)

2. Clique em **iniciar coleta** para ativar o snappoint.

   ![Ativar o snappoint](../debugger/media/snapshot-start-collection.png)

    > [!TIP]
    > Você não pode depurar ao exibir um instantâneo, mas você pode colocar vários snappoints em seu código a seguir execução em diferentes linhas de código. Se você tiver vários snappoints em seu código, o depurador de instantâneo garante que os instantâneos correspondentes são da mesma sessão do usuário final. O depurador de instantâneo faz isso, mesmo se houver muitos usuários acessando seu aplicativo.

## <a name="take-a-snapshot"></a>Tirar um instantâneo

Quando um snappoint for ativado, ele irá capturar um instantâneo sempre que executa a linha de código em que o snappoint é colocado. Essa execução pode ser causada por uma solicitação real em seu servidor. Para forçar o snappoint participar, vá para a exibição de navegador do seu site e executar quaisquer ações necessárias que fazem com que seu snappoint seja atingido.

## <a name="inspect-snapshot-data"></a>Inspecione os dados de instantâneo

1. Quando o snappoint for atingido, um instantâneo é exibida na janela de ferramentas de diagnóstico. Para abrir essa janela, escolha **depurar / Windows / Mostrar ferramentas de diagnóstico**.

   ![Abra um snappoint](../debugger/media/snapshot-diagsession-window.png)

1. Clique duas vezes o snappoint para abrir o instantâneo no editor de códigos.

   ![Inspecione os dados de instantâneo](../debugger/media/snapshot-inspect-data.png)

   Nessa exibição, você pode passar o mouse sobre as variáveis para exibir os DataTips, use o **Locals**, **inspeções**, e **pilha de chamadas** windows e também avaliar expressões.

    O site em si ainda está ao vivo e os usuários finais não são afetados. Apenas um instantâneo é capturado por snappoint por padrão: após um instantâneo captura o snappoint seja desligada. Se você quiser capturar outro instantâneo no snappoint, você pode ativar o snappoint novamente clicando **atualizar coleção**.

Você também pode adicionar mais snappoints ao seu aplicativo e ligá-los com o **atualizar coleção** botão.

**Precisa de ajuda?** Consulte a [problemas conhecidos e solução de problemas](../debugger/debug-live-azure-apps-troubleshooting.md) e [perguntas frequentes sobre depuração de instantâneo](../debugger/debug-live-azure-apps-faq.md) páginas.

## <a name="set-a-conditional-snappoint"></a>Defina um snappoint condicional

Se você tiver dificuldades recriar um estado específico em seu aplicativo, considere se o uso de um snappoint condicional pode ajudar. Snappoints condicional ajuda a que evitar tirar um instantâneo, até que o aplicativo entra em um estado desejado, como quando uma variável tem um valor específico que você deseja inspecionar. Você pode definir condições de uso de expressões, filtros, ou contagens de ocorrências.

#### <a name="to-create-a-conditional-snappoint"></a>Para criar um snappoint condicional

1. Um ícone de snappoint (a bola vazado) com o botão direito e escolha **configurações**.

   ![Escolha Configurações](../debugger/media/snapshot-snappoint-settings.png)

1. Na janela de configurações de snappoint, digite uma expressão.

   ![Digite uma expressão](../debugger/media/snapshot-snappoint-conditions.png)

   Na ilustração anterior, o instantâneo é criado somente para o snappoint quando `visitor.FirstName == "Dan"`.

## <a name="set-a-logpoint"></a>Defina um logpoint

Além de gerar um instantâneo quando um snappoint for atingido, você também pode configurar um snappoint para registrar em log uma mensagem (ou seja, criar um logpoint). Você pode definir logpoints sem a necessidade de reimplantar o aplicativo. Logpoints são executados virtualmente e fazer com que nenhum impacto ou efeitos colaterais para seu aplicativo em execução.

#### <a name="to-create-a-logpoint"></a>Para criar um logpoint

1. Um ícone de snappoint (o azul hexágono) com o botão direito e escolha **configurações**.

1. Na janela de configurações de snappoint, selecione **ações**.

    ![Criar um logpoint](../debugger/media/snapshot-logpoint.png)

1. No campo de mensagem, você pode inserir a nova mensagem de log para registrar em log. Você também pode avaliar variáveis na sua mensagem de log, colocando-os entre chaves.

    Se você escolher **enviar para a janela de saída**, quando o logpoint for atingido, a mensagem será exibida na janela de ferramentas de diagnóstico.

    ![Logpoint dados na janela diagsession](../debugger/media/snapshot-logpoint-output.png)

    Se você escolher **enviar para log de aplicativo**, quando o logpoint for atingido, a mensagem será exibida em qualquer lugar que você pode ver mensagens de `System.Diagnostics.Trace` (ou `ILogger` no .NET Core), como [App Insights](/azure/application-insights/app-insights-asp-net-trace-logs).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como usar o depurador de instantâneo. Você talvez queira ler mais detalhes sobre esse recurso.

> [!div class="nextstepaction"]
> [Perguntas frequentes sobre depuração de instantâneos](../debugger/debug-live-azure-apps-faq.md)
