---
title: Publicar um serviço de nuvem do Azure
description: Saiba como definir as diversas configurações no Assistente Publicar Aplicativo do Azure do Visual Studio
author: ghogen
manager: jillfra
assetId: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 03/21/2017
ms.author: ghogen
ms.openlocfilehash: 477b7860c320730d6362cdb7e0fcb46ad3bc7d17
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85280525"
---
# <a name="using-the-visual-studio-publish-azure-application-wizard"></a>Uso do Assistente Publicar Aplicativo do Azure do Visual Studio

Depois de desenvolver um aplicativo Web no Visual Studio, você poderá publicá-lo em um serviço de nuvem do Azure usando o assistente **Publicar Aplicativo do Azure**.

> [!Note]
> Este artigo trata da implantação em serviços de nuvem, não em sites. Para obter informações sobre a implantação de sites, consulte [Como implantar um site da Web do Azure](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).

## <a name="accessing-the-publish-azure-application-wizard"></a>Acesso ao assistente Publicar Aplicativo do Azure

É possível acessar o assistente Publicar Aplicativo do Azure de duas maneiras, que varia de acordo com o tipo de projeto do Visual Studio que você tem.

**Se você tiver um projeto de serviço de nuvem do Azure:**

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e, no menu de contexto, selecione **Publicar**.

**Se você tiver um projeto de aplicativo Web que não está habilitado para o Azure:**

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse e, no menu de contexto, selecione **Converter** > **Converter em Projeto de Serviço de Nuvem do Azure**.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto do Azure recentemente criado e, no menu de contexto, selecione **Publicar**.

## <a name="sign-in-page"></a>Página de entrada

![Página de entrada](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**Conta** - selecione uma conta ou **Adicionar uma conta** na lista suspensa de contas.

**Escolha sua assinatura** - escolha a assinatura a ser usada na sua implantação.

## <a name="settings-page---common-settings-tab"></a>Página Configurações - guia Configurações Comuns

![Configurações Comuns](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**Serviço de nuvem** - usando a lista suspensa, selecione um serviço de nuvem existente ou selecione **&lt;Criar Novo>** e crie um serviço de nuvem. O datacenter é exibido entre parênteses para cada serviço de nuvem. É aconselhável que o local do datacenter para o serviço de nuvem seja o mesmo local do datacenter para a conta de armazenamento (Configurações Avançadas).

**Ambiente** - selecione **Produção** ou **Preparo**. Escolha o ambiente de preparo se quiser implantar o aplicativo em um ambiente de teste.

**Configuração da compilação** - selecione **Depurar** ou **Liberar**.

**Configuração de serviço** - selecione **Nuvem** ou **Local**.

**Habilitar Área de Trabalho Remota para todas as funções** – marque essa opção se desejar se conectar remotamente ao serviço. Essa opção é usada principalmente para solução de problemas. Para saber mais, veja [Habilitar Conexão de Área de Trabalho Remota para uma função nos Serviços de Nuvem do Azure usando o Visual Studio](/azure/cloud-services/cloud-services-role-enable-remote-desktop-visual-studio).

**Habilitar Implantação da Web para todas as funções web** – marque essa opção para habilitar a implantação da Web para o serviço. Também marque a opção **Habilitar Área de Trabalho Remota para todas as funções** para usar esse recurso. Para obter mais informações, consulte [Publicando um serviço de nuvem com o Visual Studio](vs-azure-tools-publishing-a-cloud-service.md).

## <a name="settings-page---advanced-settings-tab"></a>Página Configurações — guia Configurações Avançadas

![Configurações avançadas](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**Rótulo de implantação**: aceite o nome padrão ou insira um nome de sua escolha. Para anexar a data ao rótulo da implantação, deixe a caixa de seleção marcada.

**Conta de armazenamento**: selecione a conta de armazenamento a ser usada para essa implantação, **&lt;Criar Novo> para criar uma conta de armazenamento. O datacenter é exibido entre parênteses para cada conta de armazenamento. É recomendável que o local de data center da conta de armazenamento seja o mesmo local de data center do serviço de nuvem (Configurações Comuns).

A conta de armazenamento do Azure armazena o pacote para a implantação do aplicativo. Depois que o aplicativo é implantado, o pacote é removido da conta de armazenamento.

**Excluir a implantação em caso de falha**: selecione essa opção para que a implantação seja excluída se algum erro for encontrado durante a publicação. Ela deverá ser desmarcada se você quiser manter um endereço IP virtual constante para o serviço de nuvem.

**Atualização da implantação**: selecione essa opção se quiser implantar apenas componentes atualizados. Esse tipo de implantação pode ser mais rápido do que uma implantação completa. Ela deverá ser marcada se você quiser manter um endereço IP virtual constante para o serviço de nuvem.

**Atualização da implantação — configurações**: essa caixa de diálogo é usada para especificar ainda mais como que você quer que as funções sejam atualizadas. Se você escolher **Atualização incremental**, cada instância do aplicativo será atualizada uma após a outra, de modo que o aplicativo estará sempre disponível. Se você escolher **Atualização simultânea**, todas as instâncias do aplicativo serão atualizadas ao mesmo tempo. A atualização simultânea é mais rápida, mas o serviço pode não estar disponível durante o processo de atualização.

![Configurações da implantação](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**Habilitar o IntelliTrace**: especifique se deseja habilitar o IntelliTrace. Com o IntelliTrace, você pode registrar em log informações extensas de depuração sobre uma instância de função quando ela é executada no Azure. Se precisa encontrar a causa de um problema, você pode usar os logs do IntelliTrace para examinar seu código no Visual Studio como se ele estivesse em execução no Azure. Para saber mais sobre como usar o IntelliTrace, confira [Depuração de um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](./vs-azure-tools-intellitrace-debug-published-cloud-services.md).

**Habilitar criação de perfil**: especifique se deseja habilitar a criação de perfil de desempenho. O criador de perfil do Visual Studio permite obter uma análise detalhada dos aspectos computacionais de como o serviço de nuvem é executado. Para saber mais sobre como usar o criador de perfil do Visual Studio, confira [Teste do desempenho de um serviço de nuvem](./vs-azure-tools-performance-profiling-cloud-services.md).

**Habilitar Depurador Remoto para todas as funções** - especifique se deseja habilitar a depuração remota. Para saber mais sobre como depurar os serviços de nuvem usando o Visual Studio, confira [Depuração de um serviço de nuvem ou máquina virtual do Azure no Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).

## <a name="diagnostics-settings-page"></a>Página Configurações de Diagnóstico

![Configurações de diagnóstico](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

O Diagnóstico permite solucionar problemas de um serviço de nuvem do Azure (ou máquina virtual do Azure). Para saber mais sobre diagnósticos, confira [Configuração do Diagnóstico para os Serviço de Nuvem e as Máquinas Virtuais do Azure](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Para saber mais sobre o Application Insights, confira [O que é o Application Insights?](/azure/application-insights/app-insights-overview).

## <a name="summary-page"></a>Página Resumo

![Resumo](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Perfil de destino** - você pode optar por criar um perfil de publicação usando as configurações que escolheu. Por exemplo, você pode criar um perfil para um ambiente de teste e outro para produção. Para salvar esse perfil, escolha o ícone **Salvar** . O assistente cria o perfil e o salva no projeto do Visual Studio. Para modificar o nome do perfil, abra a lista **Perfil de destino** e, em seguida, escolha **&lt;Gerenciar…&gt;**.

   > [!Note]
   > O perfil de publicação aparece no Gerenciador de Soluções no Visual Studio, e as configurações do perfil são gravadas em um arquivo com a extensão .azurePubxml. As configurações são salvas como atributos de marcas XML.

## <a name="publishing-your-application"></a>Publicação do aplicativo

Depois de definir todas as configurações da implantação do projeto, selecione **Publicar** na parte inferior da caixa de diálogo. Você pode monitorar o status do processo de **Saída** no Visual Studio.

## <a name="next-steps"></a>Próximas etapas

- [Migrar e publicar um aplicativo Web em um serviço de nuvem do Azure usando o Visual Studio](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)

- [Saiba como usar o Visual Studio para publicar um serviço de nuvem do Azure](./vs-azure-tools-publishing-a-cloud-service.md)

- [Depurando um serviço de nuvem do Azure publicado com o Visual Studio e o IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)

- [Testar o desempenho de um serviço de nuvem do Azure](./vs-azure-tools-performance-profiling-cloud-services.md)

- [Configurando o diagnóstico para os serviços de nuvem do Azure e máquinas virtuais](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

- [O que é o Application Insights?](/azure/application-insights/app-insights-overview)