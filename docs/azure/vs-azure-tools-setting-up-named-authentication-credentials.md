---
title: Configurando credenciais de autenticação nomeadas | Microsoft Docs
description: Saiba como fornecer credenciais que o Visual Studio possa usar para autenticar solicitações no Azure, de modo que você possa publicar um aplicativo no Azure do Visual Studio ou monitorar um serviço de nuvem existente.
author: ghogen
manager: jillfra
assetId: 61570907-42a1-40e8-bcd6-952b21a55786
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2017
ms.author: ghogen
ms.openlocfilehash: 57841baaf147c2aae02ac89a8401c46d3bd64ca3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "72911674"
---
# <a name="set-up-named-authentication-credentials"></a>Configurar credenciais de autenticação nomeadas

Para publicar um aplicativo no Azure ou monitorar um serviço de nuvem existente, o Visual Studio exige credenciais para autenticar solicitações para o Azure, ou seja, sua ID de assinatura do Azure e um certificado X.509 v3 válido com uma chave de pelo menos 2048 bits. Forneça essas credenciais por meio de um destes métodos:

- No Visual Studio, selecione **Exibir > Gerenciador de Servidores**, clique com o botão direito no nó **Azure**, selecione **Conectar-se à Assinatura do Microsoft Azure** e entre.
- Criar um arquivo de assinatura (`.publishsettings`), que contém uma chave pública para o certificado. O arquivo de assinatura pode conter credenciais para mais de uma assinatura, conforme descrito neste artigo.

Observação: essas credenciais são diferentes das credenciais usadas para autenticar solicitações para os serviços de armazenamento do Azure.

## <a name="create-a-subscription-file"></a>Criar um arquivo de assinatura

No Gerenciador de Servidores, clique com o botão direito do mouse no nó **Azure** e selecione **Gerenciar e Filtrar Assinaturas**. Em seguida, selecione a guia **Certificados** e realize qualquer uma das ações a seguir:

- Selecione **Importar** para abrir a caixa de diálogo **Importar Assinaturas do Microsoft Azure**. Selecione o link **Baixar arquivo de assinatura** e, no navegador, salve o arquivo baixado em um local temporário. De volta à caixa de diálogo, navegue até o local do download e, em seguida, importe-o para usar na autenticação.
- Escolha uma assinatura ativa e selecione **Editar**, que abre uma caixa de diálogo na qual você edita uma assinatura existente para usar na autenticação.
- Selecione **Novo** para abrir a caixa de diálogo **Nova Assinatura** e forneça os detalhes necessários. Para carregar o certificado na sua nuvem de serviço que está indicada na caixa de diálogo, entre no Portal do Azure, navegue até o serviço de nuvem, selecione **Configurações > Certificados de Gerenciamento**, selecione **Carregar**, em seguida, especifique o caminho até o arquivo `.cer`.

Se você deseja criar um certificado por conta própria, pode consultar as instruções em [Criar e carregar um certificado de gerenciamento do Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) e depois carregar manualmente o certificado para o [Portal do Azure](https://portal.azure.com/).

## <a name="next-steps"></a>Próximas etapas

- [Visão geral de aplicativos Web](/azure/app-service/)
- [Implantar seu aplicativo no serviço Azure App](/azure/app-service/app-service-deploy-local-git)
- [Implantar Trabalhos Web usando o Visual Studio](/azure/app-service/websites-dotnet-deploy-webjobs)
- [Criar e implantar um serviço de nuvem](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
