---
title: Como reter um endereço IP virtual constante para um serviço de nuvem do Azure | Microsoft Docs
description: Saiba como assegurar que o endereço IP virtual (VIP) do seu serviço de nuvem do Azure não mude.
author: ghogen
manager: douge
assetId: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/21/2017
ms.author: ghogen
ms.openlocfilehash: e74cc5b9bbbfea92d2dea2c00ee5b0f98dc02f21
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001304"
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>Reter um endereço IP virtual constante para um serviço de nuvem do Azure
Quando você atualiza um serviço de nuvem é hospedado no Azure, você precisa garantir que o endereço IP virtual (VIP) do serviço não mude. Muitos serviços de gerenciamento de domínio usam o sistema de nome de domínio (DNS) para o registro de nomes de domínio. DNS só funciona se o VIP permanece o mesmo. Você pode usar o **Assistente de publicação** nas ferramentas do Azure para garantir que o VIP do serviço de nuvem não seja alterado quando você atualizá-lo. Para obter mais informações sobre como usar o gerenciamento de domínio DNS para serviços de nuvem, consulte [Configurando um nome de domínio personalizado para um serviço de nuvem](/azure/cloud-services/cloud-services-custom-domain-name-portal).

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>Publicar um serviço de nuvem sem alterar seu VIP
O VIP de um serviço de nuvem é alocado quando você primeiro implantá-lo para o Azure em um ambiente específico, como o ambiente de produção. O VIP altera somente se você excluir a implantação explicitamente ou a implantação seja excluída implicitamente pelo processo de atualização de implantação. Para manter o VIP, você não pode excluir sua implantação, e certifique-se de que o Visual Studio não seja excluída automaticamente. 

Você pode especificar configurações de implantação na **Assistente de publicação**, que oferece suporte a várias opções de implantação. Você pode especificar uma nova implantação ou uma implantação de atualização, que pode ser incremental ou simultânea. Os dois tipos de implantação de atualização retêm o VIP. Para obter definições desses tipos diferentes de implantação, consulte [assistente Publicar aplicativo do Azure](vs-azure-tools-publish-azure-application-wizard.md). Além disso, você pode controlar se a implantação anterior de um serviço de nuvem é excluída se ocorrer um erro. Se você não definir essa opção corretamente, o VIP pode mudar inesperadamente.

## <a name="update-a-cloud-service-without-changing-its-vip"></a>Atualizar um serviço de nuvem sem alterar seu VIP
1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio. 

2. Na **Gerenciador de soluções**, clique com botão direito no projeto. No menu de atalho, selecione **publicar**.

    ![Menu Publicar](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. No **publicar aplicativo do Azure** caixa de diálogo, selecione a assinatura do Azure para o qual você deseja implantar. Entre, se necessário e selecione **próxima**.

    ![Publicar página entrar no aplicativo de Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. No **configurações comuns** guia, verifique se o nome da nuvem do serviço no qual você está implantando, o **ambiente**, o **configuração de Build**e o **Configuração do serviço** estão todos corretos.

    ![Publicar a guia Configurações comuns de aplicativo do Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. Sobre o **configurações avançadas** guia, verifique o **rótulo de implantação** e o **conta de armazenamento** estão corretos. Verificar se o **excluir implantação em caso de falha** caixa de seleção está desmarcada e verificar se o **atualização da implantação** caixa de seleção está selecionada. Ao desmarcar a **excluir implantação em caso de falha** caixa de seleção, você certifique-se de que seu VIP não será perdido se ocorrer um erro durante a implantação. Selecionando o **atualização de implantação** caixa de seleção, você certifique-se de que sua implantação não é excluída e o VIP não será perdido quando você republicar o aplicativo. 

    ![Publicar a guia Configurações avançadas de aplicativo do Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. Para especificações adicionais de como você deseja que as funções sejam atualizadas, selecione **as configurações** lado **atualização da implantação**. Selecione a **atualização Incremental** ou **atualização simultânea**e selecione **Okey**. Escolher **atualização Incremental** atualizar cada instância do seu aplicativo, uma após a outra, para que o aplicativo estará sempre disponível. Escolher **atualização simultânea** atualizar todas as instâncias do seu aplicativo ao mesmo tempo. A atualização simultânea é mais rápida, mas seu serviço pode não estar disponível durante o processo de atualização. Quando tiver terminado, selecione **próxima**.

    ![Publicar página de configurações de implantação de aplicativo do Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. No **publicar aplicativo do Azure** caixa de diálogo, selecione **próxima** até que o **resumo** página é exibida. Verifique as configurações e, em seguida, selecione **publicar**.
   
    ![Publicar página de resumo do aplicativo do Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>Próximas etapas
- [Usando o Visual Studio do Azure assistente Publicar aplicativo](vs-azure-tools-publish-azure-application-wizard.md)

