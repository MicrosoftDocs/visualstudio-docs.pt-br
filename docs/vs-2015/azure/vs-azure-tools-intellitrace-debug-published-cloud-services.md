---
title: Depuração de uma publicação serviço com o Visual Studio e IntelliTrace de nuvem do Azure | Microsoft Docs
description: Saiba como depurar um serviço de nuvem com Visual Studio e o IntelliTrace
author: mikejo5000
manager: douge
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.topic: conceptual
ms.custom: vs-azure
ms.workload: azure-vs
ms.date: 03/21/2017
ms.author: mikejo
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.openlocfilehash: 865642bb7c8e41f81ff4b44ce628082e19b63a56
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001314"
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a>Depuração de um serviço de nuvem do Azure publicado com o Visual Studio e o IntelliTrace
Com o IntelliTrace, você pode registrar informações de depuração abrangentes para uma instância de função quando ele é executado no Azure. Se você precisar descobrir a causa de um problema, você pode usar os logs do IntelliTrace para depurar seu código do Visual Studio como se ele estivesse em execução no Azure. Na verdade, IntelliTrace registra os principais dados de ambiente e execução de código quando seu aplicativo do Azure está sendo executado como um serviço de nuvem no Azure e permite que você reproduza os dados gravados no Visual Studio. 

Você pode usar o IntelliTrace se tiver o Visual Studio Enterprise instalado e o destino do seu aplicativo do Azure .NET Framework 4 ou posterior. O IntelliTrace coleta informações para as funções do Azure. As máquinas de virtuais para essas funções sempre executam sistemas operacionais de 64 bits.

Como alternativa, você pode usar [depuração remota](http://go.microsoft.com/fwlink/p/?LinkId=623041) para anexação direta a um serviço de nuvem que está em execução no Azure.

> [!IMPORTANT]
> O IntelliTrace destina-se somente a cenários de depuração e não deve ser usado para uma implantação de produção.
> 

## <a name="configure-an-azure-application-for-intellitrace"></a>Configurar um aplicativo do Azure para que o IntelliTrace
Para habilitar o IntelliTrace para um aplicativo do Azure, você deve criar e publicar o aplicativo de um projeto do Azure no Visual Studio. Você deve configurar o IntelliTrace para seu aplicativo do Azure antes de publicá-lo para o Azure. Se você publicar seu aplicativo sem configurar o IntelliTrace, você precisará publicar novamente o projeto. Para obter mais informações, consulte [projetos usando o Visual Studio de serviços de publicação de uma nuvem do Azure](http://go.microsoft.com/fwlink/p/?LinkId=623012).

1. Quando você estiver pronto para implantar seu aplicativo do Azure, verifique se que os destinos de compilação do projeto são definidos como **depurar**.

1. Na **Gerenciador de soluções**, clique com botão direito e, no menu de contexto, selecione **publicar**.
   
1. No **publicar aplicativo do Azure** caixa de diálogo, selecione a assinatura do Azure e selecione **próxima**.

1. No **as configurações** página, selecione o **configurações avançadas** guia.

1. Ativar o **habilitar IntelliTrace** opção para coletar logs do IntelliTrace para seu aplicativo quando ele é publicado na nuvem.
   
1. Para personalizar a configuração básica do IntelliTrace, selecione **as configurações** lado **habilitar IntelliTrace**.

    ![Link de configurações do IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. No **configurações do IntelliTrace** caixa de diálogo, você pode especificar quais eventos de log, se deseja coletar informações de chamada, quais módulos e processos para coletar logs e a quantidade de espaço para alocar para o registro. Para obter mais informações sobre o IntelliTrace, consulte [depuração com o IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).
   
    ![Configurações do IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

O log do IntelliTrace é um arquivo de log circular do tamanho máximo especificado nas configurações do IntelliTrace (o tamanho padrão é 250 MB). Os logs do IntelliTrace são coletados em um arquivo no sistema de arquivos da máquina virtual. Quando você solicita os logs, um instantâneo é feito no momento e baixado no computador local.

Depois que o serviço de nuvem do Azure tiver sido publicado para o Azure, você pode determinar se o IntelliTrace foi habilitado do nó do Azure no **Gerenciador de servidores**, conforme mostrado na imagem a seguir:

![Gerenciador de servidores – IntelliTrace habilitado](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a>Baixar logs do IntelliTrace para uma instância de função
Usando o Visual Studio, você pode baixar logs do IntelliTrace para uma instância de função seguindo estas etapas:

1. Na **Gerenciador de servidores**, expanda o **serviços de nuvem** nó e localize a instância de função cujos logs você deseja baixar. 

1. A instância de função com o botão direito e, em seguida, no menu de contexto s, selecione **Exibir Logs do IntelliTrace**. 

    ![Exibir logs do IntelliTrace opção de menu](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. Os logs do IntelliTrace são baixados em um arquivo em um diretório no computador local. Cada vez que você solicite o IntelliTrace registra em log, um novo instantâneo é criado. Enquanto os logs estão sendo baixados, o Visual Studio exibe o progresso da operação na **Log de atividades do Azure** janela. Conforme mostrado na figura a seguir, você pode expandir o item de linha para a operação ver mais detalhes.

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

Você pode continuar a trabalhar no Visual Studio, enquanto os logs do IntelliTrace são baixadas. Quando o log de download for concluído, ele é aberto no Visual Studio.

> [!NOTE]
> Os logs do IntelliTrace podem conter exceções que o framework geradas e tratadas posteriormente. Código interno da estrutura gera essas exceções como uma parte normal de inicialização de uma função, portanto, você pode ignorá-las com segurança.
> 
> 

## <a name="next-steps"></a>Próximas etapas
- [Opções de depuração de serviços de nuvem do Azure](vs-azure-tools-debugging-cloud-services-overview.md)
- [Publicando um serviço de nuvem do Azure usando o Visual Studio](vs-azure-tools-publishing-a-cloud-service.md)