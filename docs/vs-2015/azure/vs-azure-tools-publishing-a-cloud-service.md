---
title: Publicando um serviço de nuvem usando as ferramentas do Azure | Microsoft Docs
description: Saiba mais sobre como publicar projetos de serviço de nuvem do Azure usando o Visual Studio.
author: ghogen
manager: douge
assetId: 1a07b6e4-3678-4cbf-b37e-4520b402a3d9
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2017
ms.author: ghogen
ms.openlocfilehash: cf29e1cdde71d2e8ef7caa9bc91bc31c30c7bc41
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001296"
---
# <a name="publishing-a-cloud-service-using-visual-studio"></a>Publicando um serviço de nuvem usando o Visual Studio

Visual Studio pode publicar um aplicativo diretamente no Azure, com suporte para ambientes de produção e preparo de um serviço de nuvem. Ao publicar, selecione o ambiente de implantação e uma conta de armazenamento usada temporariamente para o pacote de implantação.

Quando você está desenvolvendo e testando um aplicativo do Azure, você pode usar a implantação da Web para publicar alterações incrementalmente para funções web. Depois de publicar seu aplicativo para um ambiente de implantação, implantação da Web permite implantar alterações diretamente para a máquina virtual que está executando a função da web. Você não precisa empacotar e publicar seu aplicativo do Azure inteiro sempre que você deseja atualizar a função web para testar as alterações. Com essa abordagem, você pode ter suas alterações de função da web disponíveis na nuvem para testes sem aguardar a publicação em um ambiente de implantação do aplicativo.

Use os procedimentos a seguir para publicar seu aplicativo do Azure e para atualizar uma função web usando a implantação da Web:

- Publicar ou empacotar um aplicativo do Azure do Visual Studio
- Atualizar uma função web como parte do ciclo de testes e desenvolvimento

## <a name="publish-or-package-an-azure-application-from-visual-studio"></a>Publicar ou empacotar um aplicativo do Azure do Visual Studio

Quando você publica seu aplicativo do Azure, você pode fazer uma das seguintes tarefas:

- Criar um pacote de serviço: você pode usar este pacote e o arquivo de configuração de serviço para publicar seu aplicativo em um ambiente de implantação dos [portal do Azure](https://portal.azure.com).

- Publicar seu projeto do Azure do Visual Studio: para publicar seu aplicativo diretamente no Azure, use o Assistente de publicação. Para obter informações, consulte [assistente Publicar aplicativo do Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="to-create-a-service-package-from-visual-studio"></a>Para criar um pacote de serviço do Visual Studio

1. Quando você estiver pronto para publicar seu aplicativo, abra o Gerenciador de soluções, abra o menu de atalho do projeto do Azure que contém suas funções e selecione publicar.

1. Para criar um pacote de serviço, siga estas etapas:

   a. No menu de atalho do projeto do Azure, escolha **pacote**.

   b. No **empacotar aplicativo do Azure** caixa de diálogo, escolha a configuração do serviço para o qual você deseja criar um pacote e, em seguida, escolha a configuração de compilação.

   c. (Opcional) Para ativar área de trabalho remota para o serviço de nuvem após publicá-lo, selecione **habilitar a área de trabalho remota para todas as funções**e, em seguida, selecione **configurações** para configurar as credenciais de área de trabalho remota. Para obter mais informações, consulte [habilitar a Conexão de área de trabalho remota para uma função nos serviços de nuvem do Azure usando o Visual Studio](/azure/cloud-services/cloud-services-role-enable-remote-desktop-visual-studio).

      Se você quiser depurar seu serviço de nuvem após publicá-lo, ative a depuração remota, selecionando **habilitar depurador remoto para todas as funções**.

   d. Para criar o pacote, escolha o **pacote** link.

      Explorador de arquivos mostra o local do arquivo do pacote recém-criado. Você pode copiar esse local para que você pode usá-lo do portal do Azure.

   e. Para publicar esse pacote em um ambiente de implantação, você deve usar esse local como o local do pacote quando você cria um serviço de nuvem e implanta esse pacote em um ambiente com o portal do Azure.

1. (Opcional) Para cancelar o processo de implantação, no menu de atalho para o item de linha no log de atividades, escolha **Cancelar e remover**. Esse comando interrompe o processo de implantação e exclui o ambiente de implantação do Azure. Para remover o ambiente após a implantação, use o portal do Azure.

1. (Opcional) Depois de ter iniciado as instâncias de função, o Visual Studio mostra automaticamente o ambiente de implantação na **serviços de nuvem** nó no Gerenciador de servidores. A partir daqui, você pode ver o status das instâncias de função individuais. Ver [recursos de gerenciamento do Azure com o Gerenciador de nuvem](vs-azure-tools-resources-managing-with-cloud-explorer.md). A ilustração a seguir mostra as instâncias de função enquanto eles ainda estão no estado Inicializando:

    ![VST_DeployComputeNode](./media/vs-azure-tools-publishing-a-cloud-service/IC744134.png)

## <a name="update-a-web-role-as-part-of-the-development-and-testing-cycle"></a>Atualizar uma função web como parte do ciclo de testes e desenvolvimento

Se a infraestrutura de back-end do seu aplicativo for estável, mas as funções web precisarem de mais frequentes atualizando, você pode usar a implantação da Web para atualizar apenas uma função web em seu projeto. A implantação da Web é útil quando você não deseja recriar e reimplantar as funções de trabalhador de back-end, ou se você tiver várias funções web e você deseja atualizar somente uma das funções da web.

### <a name="requirements-for-using-web-deploy"></a>Requisitos para usar a implantação da Web

- **Apenas para fins de desenvolvimento e teste**: as alterações são feitas diretamente à máquina virtual em que a função web está em execução. Se essa máquina virtual deve ser reciclado, as alterações são perdidas porque o pacote original que você publicou é usado para recriar a máquina virtual para a função. Republique seu aplicativo para obter as alterações mais recentes para a função web.

- **Apenas funções web podem ser atualizadas**: funções de trabalho não podem ser atualizadas. Além disso, você não pode atualizar o `RoleEntryPoint` em `web role.cs`.

- **Só há suporte a uma única instância de uma função web**: você não pode ter várias instâncias da função web em seu ambiente de implantação. No entanto, há suporte para várias funções web, cada com apenas uma instância.

- **Habilitar conexões de área de trabalho remota**: esse requisito permite que a implantação da Web para usar o usuário e a senha para se conectar à máquina virtual para implantar as alterações para o servidor que está executando serviços de informações da Internet (IIS). Além disso, talvez você precise se conectar à máquina virtual para adicionar um certificado confiável ao IIS nessa máquina virtual. (Esse certificado garante que a conexão remota para o IIS é usado pela implantação da Web é segura).

O procedimento a seguir pressupõe que você está usando o **publicar aplicativo do Azure** assistente.

### <a name="enable-web-deploy-when-you-publish-your-application"></a>Habilitar implantação da Web quando você publica seu aplicativo

1. Para habilitar o **habilitar implantação da Web para todas as funções web** opção, primeiro você deve configurar conexões de área de trabalho remota. Selecione **habilitar a área de trabalho remota** para todas as funções e, em seguida, forneça as credenciais que é usado para se conectar remotamente na **configuração de área de trabalho remota** caixa que aparece. Ver [habilitar a Conexão de área de trabalho remota para uma função nos serviços de nuvem do Azure usando o Visual Studio](/azure/cloud-services/cloud-services-role-enable-remote-desktop-visual-studio).

1. Para habilitar a implantação da Web para todas as funções da web em seu aplicativo, selecione **habilitar implantação da Web para todas as funções da web**.

    Um triângulo amarelo de aviso é exibido. A implantação da Web usa um certificado não confiável, autoassinado por padrão, o que não é recomendado para carregar dados confidenciais. Se você precisar proteger esse processo para dados confidenciais, você pode adicionar um certificado SSL a ser usado para conexões de implantação da Web. Esse certificado deve ser um certificado confiável. Para obter mais informações, consulte [tornar a implantação da web segura](#make-web-deploy-secure).

1. Escolher **próxima** para mostrar a **resumo** tela e, em seguida, escolha **publicar** para implantar o serviço de nuvem.

    O serviço de nuvem é publicado. A máquina virtual que é criada tem conexões remotas habilitadas para o IIS para que a implantação da Web pode ser usada para atualizar suas funções web sem publicá-los novamente.

   > [!NOTE]
   > Se você tiver mais de uma instância configurada para uma função web, aparecerá uma mensagem de aviso informando que cada função web é limitada a uma instância somente no pacote que é criado para publicar seu aplicativo. Selecione **Okey** para continuar. Conforme mencionado na seção requisitos, você pode ter mais de uma função web, mas apenas uma instância de cada função.

### <a name="update-your-web-role-by-using-web-deploy"></a>Atualizar sua função web usando a implantação da Web

1. Para usar a implantação da Web, faça as alterações de código para o projeto para qualquer uma das funções web no Visual Studio que você deseja publicar e, em seguida, clique com botão direito no nó do projeto em sua solução e aponte para **publicar**. O **publicar na Web** caixa de diálogo é exibida.

1. (Opcional) Se você adicionou um certificado SSL confiável a ser usado para conexões remotas para o IIS, você pode limpar a **permitir certificado não confiável** caixa de seleção. Para obter informações sobre como adicionar um certificado para proteger a implantação da Web, consulte a seção **para fazer implantação da Web segura** mais adiante neste artigo.

1. Para usar a implantação da Web, o mecanismo de publicação precisa do nome de usuário e senha que você configurou para sua conexão de área de trabalho remota quando publicou o pacote pela primeira vez.

   a. Na **nome de usuário**, insira o nome de usuário.

   b. Na **senha**, digite a senha.

   c. (Opcional) Se você quiser salvar esta senha neste perfil, escolha **salvar senha**.

1. Para publicar as alterações à sua função web, escolha **publicar**.

    A linha de status exibe **publicação iniciada**. Quando a publicação for concluída, **publicação bem-sucedida** é exibida. As alterações agora foram implantadas para a função web em sua máquina virtual. Agora você pode iniciar seu aplicativo do Azure no ambiente do Azure para testar as alterações.

### <a name="make-web-deploy-secure"></a>Tornar a implantação da web segura

1. A implantação da Web usa um certificado não confiável, autoassinado por padrão, o que não é recomendado para carregar dados confidenciais. Se você precisar proteger esse processo para dados confidenciais, você pode adicionar um certificado SSL a ser usado para conexões de implantação da Web. Esse certificado deve ser um certificado confiável, o que você obtém de uma autoridade de certificação (CA).

    Para tornar a implantação da Web segura para cada máquina virtual para cada uma das funções web, você deve carregar o certificado confiável que você deseja usar para a web implantar no portal do Azure. Esse certificado garante que o certificado é adicionado à máquina virtual que é criada para a função web quando você publica seu aplicativo.

1. Para adicionar um certificado SSL confiável ao IIS a ser usado para conexões remotas, siga estas etapas:

   a. Para se conectar à máquina virtual que está executando a função da web, selecione a instância de função web no **Cloud Explorer** ou **Gerenciador de servidores**e, em seguida, escolha o **se conectar usando a área de trabalho remota**  comando. Para obter etapas detalhadas sobre como se conectar à máquina virtual, consulte [habilitar a Conexão de área de trabalho remota para uma função nos serviços de nuvem do Azure usando o Visual Studio](/azure/cloud-services/cloud-services-role-enable-remote-desktop-visual-studio). O navegador solicitará que você baixe um `.rdp` arquivo.

   b. Para adicionar um certificado SSL, abra o serviço de gerenciamento no Gerenciador do IIS. No Gerenciador do IIS, habilite o SSL abrindo o **ligações** link na **ação** painel. O **adicionar ligação do Site** caixa de diálogo é exibida. Escolher **Add**e então escolha HTTPS na **tipo** lista suspensa. No **certificado SSL** , escolha o certificado SSL que foi assinado por uma autoridade de certificação e que você carregou no portal do Azure. Para obter mais informações, consulte [definir configurações de Conexão para o serviço de gerenciamento](http://go.microsoft.com/fwlink/?LinkId=215824).

      > [!NOTE]
      > Se você adicionar um certificado SSL confiável, o triângulo amarelo de aviso não aparece mais na **Assistente de publicação**.

## <a name="include-files-in-the-service-package"></a>Incluir arquivos no pacote de serviço

Talvez você precise incluir arquivos específicos em seu pacote de serviço para que eles estejam disponíveis na máquina virtual que é criada para uma função. Por exemplo, talvez você queira adicionar um `.exe` ou um `.msi` arquivo que é usado por um script de inicialização para o pacote de serviço. Ou você talvez precise adicionar um assembly que exige um projeto de função de trabalho ou função web. Para incluir arquivos, eles devem ser adicionados à solução para seu aplicativo do Azure.

1. Para adicionar um assembly a um pacote de serviço, use as seguintes etapas:

   a. Na **Gerenciador de soluções**, abra o nó de projeto para o projeto que está faltando o assembly referenciado.
   b. Para adicionar o assembly ao projeto, abra o menu de atalho para o **referências** pasta e, em seguida, escolha **adicionar referência**. Aparece a caixa de diálogo Adicionar referência.
   c. Escolha a referência que você deseja adicionar e, em seguida, escolha **Okey**. A referência é adicionada à lista sob o **referências** pasta.
   d. Abra o menu de atalho para o assembly que você adicionou e escolha **propriedades**. O **propriedades** janela é exibida.

      Para incluir esse assembly no pacote de serviço, na **lista de locais de cópia** escolher **verdadeiro**.
1. Na **Gerenciador de soluções** abra o nó de projeto para o projeto que está faltando o assembly referenciado.

1. Para adicionar o assembly ao projeto, abra o menu de atalho para o **referências** pasta e, em seguida, escolha **adicionar referência**. O **adicionar referência** caixa de diálogo é exibida.

1. Escolha a referência que você deseja adicionar e, em seguida, escolha o **Okey** botão.

    A referência é adicionada à lista sob o **referências** pasta.

1. Abra o menu de atalho para o assembly que você adicionou e escolha **propriedades**. A janela de propriedades é exibida.

1. Para incluir esse assembly no pacote de serviço, na **Copy Local** , escolha **verdadeiro**.

1. Para incluir arquivos no pacote de serviço que foram adicionados ao seu projeto de função web, abra o menu de atalho para o arquivo e, em seguida, escolha **propriedades**. Dos **propriedades** janela, escolha **conteúdo** do **Build Action** caixa de listagem.

1. Para incluir arquivos no pacote de serviço que foram adicionados ao seu projeto de função de trabalho, abra o menu de atalho para o arquivo e, em seguida, escolha **propriedades**. Dos **propriedades** janela, escolha **copiar se mais recente** do **copiar para diretório de saída** caixa de listagem.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como publicar no Azure do Visual Studio, consulte [assistente Publicar aplicativo do Azure](vs-azure-tools-publish-azure-application-wizard.md).
