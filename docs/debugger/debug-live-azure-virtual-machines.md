---
title: Depurar máquinas virtuais do Azure ASP.NET e conjuntos de dimensionamento dinâmicos
description: Saiba como configurar o snappoints e exibir instantâneos com o Depurador de Instantâneos.
ms.custom: ''
ms.date: 02/06/2019
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
ms.openlocfilehash: d1e9248d3e70c885fa072e3bd4682a24f0bcfdd6
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350609"
---
# <a name="debug-live-aspnet-apps-on-azure-virtual-machines-and-azure-virtual-machine-scale-sets-using-the-snapshot-debugger"></a>Depurar aplicativos ASP.NET dinâmicos em máquinas virtuais do Azure e conjuntos de dimensionamento de máquinas virtuais do Azure usando o Depurador de Instantâneos

O Depurador de Instantâneos tira um instantâneo de seus aplicativos em produção quando o código no qual você está interessado é executado. Para instruir o depurador a tirar um instantâneo, defina snappoints e logpoints em seu código. O depurador permite ver exatamente o que deu errado sem afetar o tráfego do seu aplicativo de produção. O Depurador de Instantâneo pode ajudar a reduzir drasticamente o tempo que leva para resolver problemas que ocorrem em ambientes de produção.

Snappoints e logpoints são semelhantes aos pontos de interrupção. Porém, ao contrário dos pontos de interrupção, os snappoints não interrompem o aplicativo quando atingidos. Normalmente, a captura de um instantâneo em um snappoint leva 10 a 20 milissegundos.

Neste tutorial, você irá:

> [!div class="checklist"]
> * Iniciar o Depurador de Instantâneos
> * Definir um snappoint e exibir um instantâneo
> * Definir um logpoint

## <a name="prerequisites"></a>Pré-requisitos

* Os Depurador de Instantâneos para VMs (máquinas virtuais) do Azure e conjuntos de dimensionamento de máquinas virtuais do Azure só estão disponíveis para o Visual Studio 2019 Enterprise ou superior com a **carga de trabalho de desenvolvimento do Azure**. (Na guia **Componentes individuais**,é possível encontrá-lo em **Depuração e testes** > **Depurador de instantâneos**).

    Se ele ainda não estiver instalado, instale o [Visual Studio 2019 Enterprise](https://visualstudio.microsoft.com/vs/).

* A coleta de instantâneos está disponível para os seguintes aplicativos Web de conjuntos de dimensionamento de máquinas virtuais Machines\Virtual do Azure:
  * Aplicativos ASP.NET em execução no .NET Framework 4.6.1 ou posterior.
  * Aplicativos ASP.NET Core em execução no .NET Core 2.0 ou posterior no Windows.

  > [!NOTE]
  >  Visual Studio Enterprise em execução no Windows de 32 bits não poderá exibir instantâneos.

## <a name="open-your-project-and-start-the-snapshot-debugger"></a>Abra seu projeto e iniciar o Depurador de Instantâneos

1. Abra o projeto em que você gostaria de fazer a depuração de instantâneos.

    > [!IMPORTANT]
    > Para depurar o instantâneo, você precisa abrir a *mesma versão do código-fonte* que é publicado no serviço de conjunto de dimensionamento de máquinas virtuais Machine\Virtual do Azure.

1. Escolha **depurar > anexar depurador de instantâneos...**. Selecione o conjunto de dimensionamento da máquina Machine\Virtual virtual do Azure em que seu aplicativo Web está implantado e uma conta de armazenamento do Azure e clique em **anexar**. Depurador de Instantâneos também dá suporte ao [serviço kubernetes do Azure](debug-live-azure-kubernetes.md) e ao [serviço de Azure app](debug-live-azure-applications.md).

    ![Iniciar o depurador de instantâneos no menu Depurar](../debugger/media/snapshot-debug-menu-attach.png)

    ![Selecionar recurso do Azure](../debugger/media/snapshot-select-azure-resource-vm.png)

    > [!IMPORTANT]
    > Na primeira vez que você selecionar **Anexar Depurador de Instantâneos** para sua VM, o IIS será reiniciado automaticamente.
    > Na primeira vez que você selecionar **anexar depurador de instantâneos** para os conjuntos de dimensionamento de máquinas virtuais, o exigirá a atualização manual de cada instância dos conjuntos de dimensionamento de máquinas virtuais.

    > [!NOTE]
    > (Visual Studio 2019 versão 16,2 e superior) O Depurador de Instantâneos habilitou o suporte à nuvem do Azure. Verifique se o recurso do Azure e a conta de armazenamento do Azure selecionados são da mesma nuvem. Entre em contato com o administrador do Azure se você tiver dúvidas sobre as configurações de [conformidade do Azure](https://azure.microsoft.com/overview/trusted-cloud/) da sua empresa.

    Os metadados para os **módulos** não serão ativados inicialmente, navegue até o aplicativo Web e o botão **Iniciar coleção** ficará ativo. O Visual Studio agora está no modo de depuração de instantâneos.

    ![Modo de depuração de instantâneos](../debugger/media/snapshot-message.png)

    > [!NOTE]
    > Para VMSS, o usuário é solicitado a atualizar manualmente as instâncias em seus conjuntos de dimensionamento de máquinas virtuais depois de anexar o Depurador de Instantâneos pela primeira vez.

    A janela **módulos** mostra quando todos os módulos foram carregados para o conjunto de dimensionamento de máquinas virtuais Machine\Virtual do Azure (escolha **depurar > módulos do Windows >** para abrir esta janela).

    ![Verificar a janela Módulos](../debugger/media/snapshot-modules.png)

## <a name="set-a-snappoint"></a>Definir um snappoint

1. No editor de código, clique na medianiz à esquerda ao lado de uma linha de código em que você está interessado para definir um snappoint. Verifique se o código que você sabe que será executado.

    ![Definir um snappoint](../debugger/media/snapshot-set-snappoint.png)

1. Clique em **Iniciar Coleção** para ativar o snappoint.

    ![Ativar o snappoint](../debugger/media/snapshot-start-collection.png)

    > [!TIP]
    > Não é possível depurar ao exibir um instantâneo, mas você pode colocar vários snappoints em seu código para seguir a execução em diferentes linhas de código. Se você tiver vários snappoints em seu código, o Depurador de Instantâneos garantirá que os instantâneos correspondentes sejam da mesma sessão do usuário final. O Depurador de Instantâneos fará isso mesmo se houver muitos usuários acessando seu aplicativo.

## <a name="take-a-snapshot"></a>Tirar um instantâneo

Quando um snappoint é definido, você pode gerar manualmente um instantâneo acessando a exibição do navegador do seu site e executando a linha de código marcada ou aguardando que os usuários gerem um a partir de seu uso do site.

## <a name="inspect-snapshot-data"></a>Inspecionar dados de instantâneo

1. Quando o snappoint for atingido, um instantâneo será exibido na janela de Ferramentas de Diagnóstico. Para abrir essa janela, escolha **Depurar > Janelas > Mostrar Ferramentas de Diagnóstico**.

    ![Abrir um snappoint](../debugger/media/snapshot-diagsession-window.png)

1. Clique duas vezes o snappoint para abrir o instantâneo no editor de códigos.

    ![Inspecionar dados de instantâneo](../debugger/media/snapshot-inspect-data.png)

    Nessa exibição, você pode passar o mouse sobre as variáveis para exibir DataTips; use as janelas **Locais**, **Inspeções** e **Pilha de Chamadas** e também avalie expressões.

    O próprio site ainda é ao vivo e os usuários finais não são afetados. Apenas um instantâneo é capturado por snappoint por padrão: após a captura de um instantâneo, o snappoint é desativado. Se você quiser capturar outro instantâneo no snappoint, poderá ativar o snappoint novamente clicando em **Atualizar Coleção**.

Você também pode adicionar mais snappoints ao seu aplicativo e ativá-los com o botão **Atualizar Coleção**.

**Precisa de ajuda?** Consulte as páginas [Solução de problemas e problemas conhecidos](../debugger/debug-live-azure-apps-troubleshooting.md) e [Perguntas frequentes sobre depuração de instantâneo](../debugger/debug-live-azure-apps-faq.md).

## <a name="set-a-conditional-snappoint"></a>Definir um snappoint condicional

Se for difícil recriar um estado específico em seu aplicativo, considere usar um snappoint condicional. O snappoints condicional ajuda você a controlar quando obter um instantâneo, como quando uma variável contém um valor específico que você deseja inspecionar. É possível definir condições usando expressões, filtros ou contagens de ocorrências.

#### <a name="to-create-a-conditional-snappoint"></a>Para criar um snappoint condicional

1. Clique com o botão direito do mouse em um ícone de snappoint (a bola vazada) e escolha **Configurações**.

   ![Escolha Configurações](../debugger/media/snapshot-snappoint-settings.png)

1. Na janela de configurações de snappoint, digite uma expressão.

   ![Digitar uma expressão](../debugger/media/snapshot-snappoint-conditions.png)

   Na ilustração anterior, o instantâneo é criado para o snappoint somente quando `visitor.FirstName == "Dan"`.

## <a name="set-a-logpoint"></a>Definir um logpoint

Além de tirar um instantâneo quando um snappoint é atingido, também é possível configurar um snappoint para registrar uma mensagem em log (ou seja, criar um logpoint). Você pode definir logpoints sem a necessidade de reimplantar o aplicativo. Logpoints são executados virtualmente e não causam impacto ou efeitos colaterais ao seu aplicativo em execução.

#### <a name="to-create-a-logpoint"></a>Para criar um logpoint

1. Clique com o botão direito em um ícone de snappoint (o hexágono azul) e escolha **Configurações**.

1. Na janela de configurações de snappoint, selecione **Ações**.

    ![Criar um logpoint](../debugger/media/snapshot-logpoint.png)

1. No campo **Mensagem**, você pode inserir a nova mensagem de log para registrar em log. Você também pode avaliar variáveis na sua mensagem de log colocando-as entre chaves.

    Se você escolher **Enviar para a Janela de Saída**, quando o logpoint for atingido, a mensagem será exibida na janela de Ferramentas de Diagnóstico.

    ![Dados de logpoint na janela Ferramentas de Diagnóstico](../debugger/media/snapshot-logpoint-output.png)

    Se você escolher **Enviar para log do aplicativo**, quando o logpoint for atingido, a mensagem será exibida em qualquer lugar em que você possa ver mensagens de `System.Diagnostics.Trace` (ou `ILogger` no .NET Core), como [App Insights](/azure/application-insights/app-insights-asp-net-trace-logs).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como usar o Depurador de Instantâneos para Máquinas Virtuais e Conjuntos de Dimensionamento de Máquinas Virtuais do Azure. Talvez você queira ler mais detalhes sobre esse recurso.

> [!div class="nextstepaction"]
> [Perguntas frequentes sobre depuração de instantâneo](../debugger/debug-live-azure-apps-faq.md)
