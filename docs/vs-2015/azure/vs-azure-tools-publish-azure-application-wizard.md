---
title: Usando o Visual Studio publica o Assistente de aplicativo do Azure | Microsoft Docs
description: Saiba como configurar as várias configurações no Visual Studio publique Azure Assistente do aplicativo
author: ghogen
manager: douge
assetId: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/21/2017
ms.author: ghogen
ms.openlocfilehash: c9c4104d4d07cab7486038a8787ed0c7759abd60
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001318"
---
# <a name="using-the-visual-studio-publish-azure-application-wizard"></a>Usando o assistente de publicação de aplicativo no Azure do Visual Studio

Depois de desenvolver um aplicativo web no Visual Studio, você pode publicar esse aplicativo em um serviço de nuvem do Azure usando o **publicar aplicativo do Azure** assistente.

> [!Note]
> Este artigo é sobre a implantação de serviços de nuvem, não em sites. Para obter informações sobre a implantação de sites da web, consulte [como implantar um Site do Azure](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).

## <a name="accessing-the-publish-azure-application-wizard"></a>Acessar o assistente Publicar aplicativo do Azure

Você pode acessar o assistente Publicar aplicativo do Azure de duas maneiras, dependendo do tipo de projeto do Visual Studio que você tem.

**Se você tiver um projeto de serviço de nuvem do Azure:**

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Na **Gerenciador de soluções**, clique com botão direito no projeto e, no menu de contexto, selecione **publicar**.

**Se você tiver um projeto de aplicativo web que não está habilitado para o Azure:**

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Na **Gerenciador de soluções**, clique com botão direito no projeto e, no menu de contexto, selecione **converter** > **converter em projeto de serviço de nuvem do Azure**. 

1. Na **Gerenciador de soluções**, o projeto do Azure recentemente criado com o botão direito e, no menu de contexto, selecione **publicar**.

## <a name="sign-in-page"></a>Página de entrada

![Página de entrada](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**Conta** - selecione uma conta ou selecione **adicionar uma conta** na lista suspensa de contas.

**Escolha sua assinatura** -escolha a assinatura a ser usado para sua implantação.

## <a name="settings-page---common-settings-tab"></a>Página Configurações - guia Configurações comuns

![Configurações comuns](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**Serviço de nuvem** -usando o menu suspenso, selecione uma nuvem existente do serviço, ou selecione  **&lt;criar novo >** e criar um serviço de nuvem. O data center é exibido entre parênteses para cada serviço de nuvem. É recomendável que o datacenter local para o serviço de nuvem seja o mesmo local do data center da conta de armazenamento (configurações avançadas).

**Ambiente** -selecione a **produção** ou **preparo**. Se você quiser implantar seu aplicativo em um ambiente de teste, escolha o ambiente de preparo. 

**Configuração de Build** -selecione a **Debug** ou **versão**.

**Configuração de serviço** -selecione a **Cloud** ou **Local**.

**Habilitar área de trabalho remota para todas as funções** -Selecione esta opção se você quiser ser capaz de se conectar remotamente ao serviço. Essa opção é usada principalmente para solução de problemas. Para obter mais informações, consulte [habilitar a Conexão de área de trabalho remota para uma função nos serviços de nuvem do Azure usando o Visual Studio](/azure/cloud-services/cloud-services-role-enable-remote-desktop-visual-studio).

**Habilitar implantação da Web para todas as funções web** -Selecione esta opção para habilitar a implantação da web para o serviço. Você também deve selecionar o **habilitar a área de trabalho remota para todas as funções** opção para usar esse recurso. Para obter mais informações, consulte [publicando um serviço de nuvem usando o Visual Studio](vs-azure-tools-publishing-a-cloud-service.md).

## <a name="settings-page---advanced-settings-tab"></a>Página de configurações - guia Configurações avançada

![Configurações avançadas](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**Rótulo de implantação** – aceite o nome padrão ou insira um nome de sua escolha. Para anexar a data para o rótulo de implantação, deixe a caixa de seleção marcada. 

**Conta de armazenamento** -selecione a conta de armazenamento a ser usado para essa implantação, * *&lt;criar novo > para criar uma conta de armazenamento. O data center é exibido entre parênteses para cada conta de armazenamento. É recomendável que o local do Datacenter para a conta de armazenamento é o mesmo local do data center para o serviço de nuvem (configurações comuns).

A conta de armazenamento do Azure armazena o pacote para a implantação do aplicativo. Depois que o aplicativo for implantado, o pacote é removido da conta de armazenamento.

**Excluir implantação em caso de falha** -Selecione esta opção para fazer a implantação seja excluída se houver erros durante a publicação. Isso deve ser desmarcado se você quiser manter um endereço IP virtual constante para seu serviço de nuvem.

**Atualização de implantação** -Selecione esta opção se você quiser implantar apenas componentes atualizados. Esse tipo de implantação pode ser mais rápido do que uma implantação completa. Isso deve ser marcado se você quiser manter um endereço IP virtual constante para seu serviço de nuvem. 

**Atualização da implantação — configurações** -esta caixa de diálogo é usada para especificar como você deseja que as funções sejam atualizadas. Se você escolher **atualização Incremental**, cada instância do seu aplicativo será atualizada uma após a outra, para que o aplicativo estará sempre disponível. Se você escolher **atualização simultânea**, todas as instâncias do seu aplicativo são atualizadas ao mesmo tempo. A atualização simultânea é mais rápida, mas seu serviço pode não estar disponível durante o processo de atualização.

![Configurações de implantação](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**Habilitar o IntelliTrace** -Especifique se deseja habilitar o IntelliTrace. Com o IntelliTrace, você pode registrar informações de depuração abrangentes para uma instância de função quando ele é executado no Azure. Se você precisar descobrir a causa de um problema, você pode usar os logs do IntelliTrace para depurar seu código do Visual Studio como se ele estivesse em execução no Azure. Para obter mais informações sobre como usar o IntelliTrace, consulte [depurando um serviço de nuvem do Azure publicado com o Visual Studio e o IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md).

**Habilitar criação de perfil** -Especifique se deseja habilitar a criação de perfil de desempenho. O criador de perfil do Visual Studio permite que você obtenha uma análise detalhada dos aspectos computacionais de como seu serviço de nuvem é executado. Para obter mais informações sobre como usar o criador de perfil do Visual Studio, consulte [teste o desempenho de um serviço de nuvem](./vs-azure-tools-performance-profiling-cloud-services.md).

**Habilitar depurador remoto para todas as funções** -Especifique se deseja habilitar a depuração remota. Para obter mais informações sobre como depurar serviços de nuvem usando o Visual Studio, consulte [depurando um serviço de nuvem do Azure ou a máquina virtual no Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).

## <a name="diagnostics-settings-page"></a>Página Configurações de diagnóstico

![Configurações de diagnóstico](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

O diagnóstico permite solucionar problemas de um serviço de nuvem do Azure (ou máquina virtual do Azure). Para obter informações sobre o diagnóstico, consulte [Configurando o diagnóstico para serviços de nuvem do Azure e máquinas virtuais](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Para obter informações sobre o Application Insights, consulte [o que é o Application Insights?](/azure/application-insights/app-insights-overview.md).

## <a name="summary-page"></a>Página de resumo

![Resumo](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Perfil de destino** -você pode optar por criar um perfil de publicação das configurações que você escolheu. Por exemplo, você pode criar um perfil para um ambiente de teste e outro para produção. Para salvar esse perfil, escolha o **salvar** ícone. O assistente cria o perfil e salva-o no projeto do Visual Studio. Para modificar o nome do perfil, abra o **perfil de destino** lista e, em seguida, escolha  **&lt;gerenciar... &gt;**.

   > [!Note]
   > O perfil de publicação é exibido no Gerenciador de soluções no Visual Studio, e as configurações de perfil são gravadas em um arquivo com uma extensão. azurePubxml. As configurações são salvas como atributos de marcas XML.

## <a name="publishing-your-application"></a>Publicar um aplicativo

Depois de configurar todas as configurações para a implantação do seu projeto, selecione **publicar** na parte inferior da caixa de diálogo. Você pode monitorar o status do processo do **saída** janela no Visual Studio.

## <a name="next-steps"></a>Próximas etapas

- [Migrar e publicar um aplicativo Web a um serviço de nuvem do Azure do Visual Studio](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)

- [Saiba como usar o Visual Studio para publicar um serviço de nuvem do Azure](./vs-azure-tools-publishing-a-cloud-service.md)

- [Depurando um serviço de nuvem do Azure publicado com o Visual Studio e o IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)

- [Testar o desempenho de um serviço de nuvem do Azure](./vs-azure-tools-performance-profiling-cloud-services.md)

- [Configurando o diagnóstico para serviços de nuvem do Azure e máquinas virtuais](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

- [O que é o Application Insights?](/azure/application-insights/app-insights-overview.md)