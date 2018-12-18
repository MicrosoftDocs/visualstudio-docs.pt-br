---
title: Configurar credenciais de autenticação nomeadas | Microsoft Docs
description: Saiba como fornecer credenciais que o Visual Studio pode usar para autenticar solicitações para o Azure, para que você possa publicar um aplicativo do Azure do Visual Studio ou monitorar um serviço de nuvem existente.
author: ghogen
manager: douge
assetId: 61570907-42a1-40e8-bcd6-952b21a55786
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2017
ms.author: ghogen
ms.openlocfilehash: 6f41ea2072ef5791735fac61205f68151d5a9f7e
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001307"
---
# <a name="set-up-named-authentication-credentials"></a>Configurar credenciais de autenticação nomeadas

Para publicar um aplicativo no Azure ou monitorar um serviço de nuvem existente, o Visual Studio exige credenciais para autenticar solicitações no Azure, ou seja, sua ID de assinatura do Azure e um certificado X.509 v3 válido com uma chave de pelo menos 2048 bits. Forneça essas credenciais por meio de um dos seguintes métodos:

- No Visual Studio, selecione **exibição > Gerenciador de servidores**, com o botão direito do **Azure** nó, selecione **conectar-se a assinatura do Microsoft Azure**e entre.
- Criar um arquivo de assinatura (`.publishsettings`), que contém uma chave pública do certificado. O arquivo de assinatura pode conter credenciais para mais de uma assinatura, conforme descrito neste artigo.

Observação: essas credenciais são diferentes das credenciais usadas para autenticar solicitações para serviços de armazenamento do Azure.

## <a name="create-a-subscription-file"></a>Criar um arquivo de assinatura

No Gerenciador de servidores, clique com botão direito do **Azure** nó e selecione **gerenciar e filtrar assinaturas**. Em seguida, selecione a **certificados** guia e, em seguida, execute uma das seguintes ações:

- Selecione **importação** para abrir o **importar assinaturas do Microsoft Azure** caixa de diálogo. Selecione o **baixar arquivo de assinatura** vincular e, no navegador, salve o arquivo baixado para um local temporário. Na caixa de diálogo, navegue até o local de download e, em seguida, importá-lo para uso na autenticação.
- Escolha uma assinatura ativa e selecione **editar**, que abre uma caixa de diálogo na qual você editar uma assinatura existente para uso na autenticação.
- Selecione **New** para abrir o **nova assinatura** caixa de diálogo caixa e forneça os detalhes necessários. Para carregar o certificado à sua nuvem de serviço são indicados na caixa de diálogo, entre no portal do Azure, navegue até seu serviço de nuvem, selecione **Configurações > certificados de gerenciamento**, selecione **carregar**, em seguida, Especifique o caminho para o `.cer` arquivo.

Se você quiser criar um certificado por conta própria, você pode consultar as instruções em [criar e carregar um certificado de gerenciamento do Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) e, em seguida, carregar manualmente o certificado para o [portal do Azure](https://portal.azure.com/).

## <a name="next-steps"></a>Próximas etapas

- [Visão geral de aplicativos Web](https://docs.microsoft.com/azure/app-service/)
- [Implantar seu aplicativo no serviço de aplicativo do Azure](https://docs.microsoft.com/azure/app-service/app-service-deploy-local-git) 
- [Implantar o WebJobs usando o Visual Studio](https://docs.microsoft.com/azure/app-service/websites-dotnet-deploy-webjobs)
- [Criar e implantar um serviço de nuvem](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy-portal)