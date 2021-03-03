---
title: Adicionar configuração de Azure App usando os serviços conectados | Microsoft Docs
description: Adicionar uma dependência do serviço de configuração do Azure ao seu aplicativo usando os serviços conectados do Visual Studio
author: ghogen
manager: ''
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 12/11/2020
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 250b89c983da039717982b31873a470172bde0f5
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683289"
---
# <a name="adding-azure-app-configuration-by-using-visual-studio-connected-services"></a>Adicionando configuração de Azure App usando os serviços conectados do Visual Studio

Neste tutorial, você aprenderá a adicionar facilmente tudo o que precisa para começar a usar Azure App configuração para gerenciar seus sinalizadores de configuração e recursos para projetos Web no Visual Studio. Usando o recurso serviços conectados no Visual Studio, você pode fazer com que o Visual Studio adicione automaticamente todo o código, os pacotes NuGet e as definições de configuração que você precisa para se conectar ao recurso de configuração de aplicativo no Azure. Para usar esse recurso, você deve usar o Visual Studio 2019 versão 16,9 ou posterior.

Você pode usar o recurso serviços conectados de configuração de aplicativo no ASP.NET Core, no console do .NET Core e em projetos .NET Framework.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Serviços conectados no Visual Studio para Mac](/visualstudio/mac/connected-services).

## <a name="prerequisites"></a>Pré-requisitos

- Visual Studio com a carga de trabalho do Azure instalada.
- Um projeto de um dos tipos com suporte

## <a name="connect-to-azure-app-configuration-using-connected-services"></a>Conectar-se à configuração do Azure App usando os serviços conectados

1. Abra o projeto no Visual Studio.

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó **Serviços conectados** e, no menu de contexto, selecione **Adicionar serviço conectado**.

    ![Adicionar serviço conectado do Azure](./media/vs-azure-tools-connected-services-storage/vs-2019/add-connected-service.png)

1. Na guia **Serviços conectados** , selecione o ícone + para **dependências de serviço**.

    ![Adicionar dependência de serviço](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. Na página **Adicionar dependência** , selecione **configuração de Azure app**.

    ![Adicionar configuração de aplicativo](./media/vs-azure-tools-connected-services-app-configuration/add-azure-app-configuration.png)

    Se você ainda não tiver entrado, entre em sua conta do Azure. Se você não tiver uma conta do Azure, poderá se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/free/dotnet).

1. Na tela **configurar configuração de Azure app** , selecione sua assinatura e um repositório de configuração existente. Em seguida, selecione **Avançar**.

    Se você precisar criar um repositório de configuração de aplicativo, vá para a próxima etapa. Caso contrário, ignore a etapa 6.

    ![Adicionar conta de configuração existente ao projeto](./media/vs-azure-tools-connected-services-app-configuration/select-config-store.png)

1. Para criar um repositório de configurações de aplicativo:

   1. Selecione o ícone + à direita do cabeçalho **repositórios de configuração de aplicativo** . 

   1. Preencha o **Azure app configuração: criar nova** caixa de diálogo e selecione **criar**. Observe que o campo nome do recurso precisa ser exclusivo. 

       ![Novo repositório de configuração de aplicativo do Azure](./media/vs-azure-tools-connected-services-app-configuration/create-new-config-store.png)

   1. Quando a caixa de diálogo **configuração de Azure app** for exibida, o novo repositório de configuração aparecerá na lista. Selecione essa nova loja e, em seguida, selecione **Avançar**.

1. Insira um nome de cadeia de conexão e escolha se deseja que a cadeia de conexão seja armazenada em um arquivo de segredos local ou em [Azure Key Vault](/azure/key-vault).

   ![Especificar cadeia de conexão](./media/vs-azure-tools-connected-services-app-configuration/connection-string-app-config.png)

1. A tela **Resumo das alterações** mostra todas as modificações que serão feitas ao seu projeto se você concluir o processo. Se as alterações parecerem OK, escolha **concluir**.

   ![Resumo das alterações](./media/vs-azure-tools-connected-services-app-configuration/summary-of-changes-app-config.png)

1. Depois que o **processo de configuração de dependência** for concluído, Azure app configuração agora aparecerá no nó **dependências de serviço** do seu projeto.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre a configuração de Azure App em [Azure app documentação de configuração](/azure/azure-app-configuration/overview).

## <a name="see-also"></a>Confira também

- [Tutorial para usar a configuração dinâmica em uma configuração de aplicativo conectada ASP.NET Core aplicativo](/azure/azure-app-configuration/enable-dynamic-configuration-aspnet-core)
- [Serviço conectados (Visual Studio para Mac)](/visualstudio/mac/connected-services)