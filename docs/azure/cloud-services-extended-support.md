---
title: Usar serviços de nuvem (suporte estendido)
description: Aprenda agora a criar e implantar serviços de nuvem (suporte estendido) usando o Azure Resource Manager com o Visual Studio
author: ghogen
manager: jmartens
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 01/25/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 289bc88d9aef40fdc260ce84395b1c4b9237c689
ms.sourcegitcommit: 2a50f4c1705baeee5c05580f04e3f468550f44e3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/05/2021
ms.locfileid: "106381589"
---
# <a name="create-and-deploy-to-cloud-services-extended-support-in-visual-studio"></a>Criar e implantar serviços de nuvem (suporte estendido) no Visual Studio

A partir do [Visual Studio 2019 versão 16,9](https://visualstudio.microsoft.com/vs/), você pode trabalhar com os serviços de nuvem usando Azure Resource Manager, o que simplifica bastante e permite a manutenção e o gerenciamento de recursos do Azure. Isso é habilitado por um novo serviço do Azure referido como *serviços de nuvem (suporte estendido)*. Você pode publicar um serviço de nuvem existente nos Serviços de Nuvem (suporte estendido). Para obter informações sobre esse serviço do Azure, confira [Documentação dos Serviços de Nuvem (suporte estendido)](/azure/cloud-services-extended-support/overview).

## <a name="publish-to-cloud-services-extended-support"></a>Publicar em serviços de nuvem (suporte estendido)

Ao publicar seu projeto de serviço de nuvem do Azure existente para serviços de nuvem (suporte estendido), você ainda mantém a capacidade de publicar em um serviço de nuvem do Azure clássico. No Visual Studio 2019 versão 16,9 e posterior, os projetos de serviço de nuvem clássicos têm uma versão especial do comando de **publicação** , **publicação (suporte estendido)**. Esse comando é exibido no menu de atalho no **Gerenciador de soluções**.

Há algumas diferenças quando você publica em serviços de nuvem (suporte estendido). Por exemplo, você não será perguntado se estiver publicando para **preparo** ou **produção**, porque esses slots de implantação não fazem parte do modelo de publicação de suporte estendido. Em vez disso, com os serviços de nuvem (suporte estendido), você pode configurar várias implantações e permutar implantações no portal do Azure. Embora as ferramentas do Visual Studio permitam definir isso em 16,9, o recurso de permuta não será habilitado até uma versão posterior dos serviços de nuvem (suporte estendido) e poderá resultar em uma falha no tempo de implantação durante a versão prévia.

Antes de publicar um serviço de nuvem do Azure clássico para serviços de nuvem (suporte estendido), verifique as contas de armazenamento que seu projeto usa e verifique se elas são contas de armazenamento v1 ou Storage v2. Os tipos de conta de armazenamento clássico falharão com uma mensagem de erro no momento da implantação. Certifique-se de verificar a conta de armazenamento usada pelo diagnóstico. Para verificar a conta de armazenamento de diagnóstico, consulte [Configurar o diagnóstico para os serviços de nuvem do Azure e máquinas virtuais](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Se o serviço usar uma conta de armazenamento clássico, você poderá atualizá-la; consulte [atualizar para uma conta de armazenamento v2 de uso geral](/azure/storage/common/storage-account-upgrade?tabs=azure-portal).  Para obter informações gerais sobre os tipos de contas de armazenamento, consulte [visão geral da conta de armazenamento](/azure/storage/common/storage-account-overview).

### <a name="to-publish-a-classic-azure-cloud-service-project-to-cloud-services-extended-support"></a>Para publicar um projeto de serviço de nuvem do Azure clássico para serviços de nuvem (suporte estendido)

1. Clique com o botão direito do mouse no nó do projeto no projeto do serviço de nuvem do Azure (clássico) e escolha **publicar (suporte estendido)...**. O **Assistente de publicação** é aberto na primeira tela.

   ![Escolha publicar (suporte estendido) no menu](./media/cloud-services-extended-support/publish-commands-on-menu.png)

   O assistente de **publicação** é exibido.

   ![Página de entrada](./media/cloud-services-extended-support/publish-step1.png)

1. **Conta** - selecione uma conta ou **Adicionar uma conta** na lista suspensa de contas.

1. **Escolha sua assinatura** - escolha a assinatura a ser usada na sua implantação.

1. Escolha **Avançar** para passar para a página **Configurações**.

   ![Configurações Comuns](./media/cloud-services-extended-support/publish-settings.png)

1. **Serviço de nuvem (suporte estendido)** -usando a lista suspensa, selecione um serviço de nuvem existente (suporte estendido) ou selecione **criar novo** e crie um. O data center é exibido entre parênteses para cada serviço de nuvem (suporte estendido). É recomendável que o local de data center para o serviço de nuvem (suporte estendido) seja igual ao local de data center para a conta de armazenamento.

   Se você optar por criar um novo serviço, verá a caixa de diálogo **Criar serviço de nuvem (suporte estendido)** . Especifique o local e o grupo de recursos que você deseja usar para o serviço de nuvem (suporte estendido).

   ![Criar um serviço de nuvem (suporte estendido)](./media/cloud-services-extended-support/extended-support-dialog.png)

1. **Configuração da compilação** - selecione **Depurar** ou **Liberar**.

1. **Configuração de serviço** - selecione **Nuvem** ou **Local**.

1. **Conta de armazenamento** – selecione a conta de armazenamento a ser usada para essa implantação ou **Criar** para criar uma conta de armazenamento. A região é exibida entre parênteses para cada conta de armazenamento. É recomendável que o local de data center da conta de armazenamento seja o mesmo local de data center do serviço de nuvem (Configurações Comuns).

   A conta de armazenamento do Azure armazena o pacote para a implantação do aplicativo.

1. **Key Vault** -especifique o cofre de chaves que contém os segredos para esse serviço de nuvem (suporte estendido). Isso será habilitado se a área de trabalho remota estiver habilitada ou se os certificados forem adicionados à configuração.

1. **Habilitar Área de Trabalho Remota para todas as funções** – marque essa opção se desejar se conectar remotamente ao serviço. Você deverá especificar as credenciais.

   ![Configurações da Área de Trabalho Remota](./media/cloud-services-extended-support/remote-desktop-configuration.png)

1. Escolha **Avançar** para passar para a página **Configurações de diagnóstico**.

   ![Configurações de diagnóstico](./media/cloud-services-extended-support/diagnostics-settings.png)

   O diagnóstico permite solucionar problemas de um serviço de nuvem do Azure (suporte estendido). Para saber mais sobre diagnósticos, confira [Configuração do Diagnóstico para os Serviço de Nuvem e as Máquinas Virtuais do Azure](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Para saber mais sobre o Application Insights, confira [O que é o Application Insights?](/azure/application-insights/app-insights-overview).

1. Escolha **Avançar** para passar para a página **Resumo**.

   ![Resumo](./media/cloud-services-extended-support/publish-summary.png)

1. **Perfil de destino** - você pode optar por criar um perfil de publicação usando as configurações que escolheu. Por exemplo, você pode criar um perfil para um ambiente de teste e outro para produção. Para salvar esse perfil, escolha o ícone **Salvar** . O assistente cria o perfil e o salva no projeto do Visual Studio. Para modificar o nome do perfil, abra a lista **Perfil de destino** e, em seguida, escolha **Gerenciar…**.

   > [!Note]
   > O perfil de publicação aparece em Gerenciador de Soluções no Visual Studio, e as configurações de perfil são gravadas em um arquivo com uma extensão *. azurePubxml* . As configurações são salvas como atributos de marcas XML.

1. Depois de definir todas as configurações da implantação do projeto, selecione **Publicar** na parte inferior da caixa de diálogo. Você pode monitorar o status do processo na Janela de Saída do **Log de Atividades do Azure** no Visual Studio. Escolha o link **abrir no portal** para 

Parabéns! Você publicou seu projeto de serviço de nuvem (suporte estendido) no Azure. Para fazer a publicação novamente com as mesmas configurações, você pode reutilizar o perfil de publicação ou repetir essas etapas para criar um. O modelo de Azure Resource Manager (ARM) e os parâmetros que são usados para implantação são salvos na pasta *bin/ \<configuration\> /Publish* .

## <a name="clean-up-azure-resources"></a>Limpar recursos do Azure

Para limpar os recursos do Azure criados seguindo este tutorial, vá para o [portal do Azure](https://portal.azure.com), escolha grupos de **recursos**, localize e abra o grupo de recursos que você usou para criar o serviço de nuvem (suporte estendido) e escolha **excluir grupo de recursos**.

## <a name="next-steps"></a>Próximas etapas

Configure a CI (integração contínua) usando o botão **Configurar** na tela **Publicar**. Para obter mais informações, confira a [documentação do Azure Pipelines](/azure/devops/pipelines/?view=azure-devops&preserve-view=true).
