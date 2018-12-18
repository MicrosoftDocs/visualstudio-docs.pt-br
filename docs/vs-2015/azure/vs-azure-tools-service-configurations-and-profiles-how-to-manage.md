---
title: Como gerenciar perfis e configurações de serviço | Microsoft Docs
description: Saiba como trabalhar com arquivos de configuração de perfis e configurações de serviço | que armazenar as definições para os ambientes de implantação e configurações de publicação para serviços de nuvem.
author: ghogen
manager: douge
assetId: 7da8c551-fb06-4057-b5c7-c77f4b39d803
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 8/11/2017
ms.author: ghogen
ms.openlocfilehash: 3f7c7341b115f0899ac4c90d574a65dfdb4087bc
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001308"
---
# <a name="how-to-manage-service-configurations-and-profiles"></a>Como gerenciar perfis e configurações de serviço
## <a name="overview"></a>Visão geral
Quando você publica um serviço de nuvem, o Visual Studio armazena informações de configuração em dois tipos de arquivos de configuração: perfis e configurações de serviço. Configurações de serviço (arquivos. cscfg) armazenam configurações para os ambientes de implantação para um serviço de nuvem do Azure. O Azure usa esses arquivos de configuração quando ele gerencia seus serviços de nuvem. Por outro lado, o armazenamento de perfis (arquivos. azurePubxml) configurações de publicação para serviços de nuvem. Essas configurações são um registro do que você escolhe quando você usa o Assistente de publicação e é usadas localmente pelo Visual Studio. Este tópico explica como trabalhar com ambos os tipos de arquivos de configuração.

## <a name="service-configurations"></a>Configurações de serviço
Você pode criar várias configurações de serviço a ser usado para cada um dos seus ambientes de implantação. Por exemplo, você pode criar uma configuração de serviço para o ambiente local que você usa para executar e testar um aplicativo do Azure e outra configuração de serviço para seu ambiente de produção.

Você pode adicionar, excluir, renomear e modificar essas configurações de serviço com base em seus requisitos. Você pode gerenciar essas configurações de serviço do Visual Studio, conforme mostrado na ilustração a seguir.

![Gerenciar configurações de serviço](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-service-config.png)

Você também pode abrir o **gerenciar configurações** caixa de diálogo páginas de propriedades da função. Para abrir as propriedades para uma função no projeto do Azure, abra o menu de atalho para essa função e, em seguida, escolha **propriedades**. No **as configurações** guia, expanda o **configuração de serviço** lista e, em seguida, selecione **gerenciar** para abrir o **gerenciar configurações** caixa de diálogo.

### <a name="to-add-a-service-configuration"></a>Para adicionar uma configuração de serviço
1. No Gerenciador de soluções, abra o menu de atalho do projeto do Azure e, em seguida, selecione **gerenciar configurações**.
   
    O **gerenciar configurações de serviço** caixa de diálogo é exibida.
2. Para adicionar uma configuração de serviço, você deve criar uma cópia de uma configuração existente. Para fazer isso, escolha a configuração que você deseja copiar na lista nome e, em seguida, selecione **criar cópia**.
3. (Opcional) Para atribuir a configuração de serviço com um nome diferente, escolha a nova configuração de serviço na lista nome e, em seguida, selecione **Renomear**. No **nome** texto, digite o nome que você deseja usar para essa configuração de serviço e, em seguida, selecione **Okey**.
   
    Um novo arquivo de configuração de serviço chamado ServiceConfiguration. [Novo nome]. cscfg é adicionado ao projeto do Azure no Gerenciador de soluções.

### <a name="to-delete-a-service-configuration"></a>Para excluir uma configuração de serviço
1. No Gerenciador de soluções, abra o menu de atalho do projeto do Azure e, em seguida, selecione **gerenciar configurações**.
   
    O **gerenciar configurações de serviço** caixa de diálogo é exibida.
2. Para excluir uma configuração de serviço, escolha a configuração que você deseja excluir do **nome** e, em seguida, selecione **remover**. Uma caixa de diálogo é exibida para verificar que você deseja excluir esta configuração.
3. Selecione **excluir**.
   
     O arquivo de configuração de serviço é removido do projeto do Azure no Gerenciador de soluções.

### <a name="to-rename-a-service-configuration"></a>Para renomear uma configuração de serviço
1. No Gerenciador de soluções, abra o menu de atalho do projeto do Azure e, em seguida, selecione **gerenciar configurações**.
   
    O **gerenciar configurações de serviço** caixa de diálogo é exibida.
2. Para renomear uma configuração de serviço, escolha a nova configuração de serviço do **nome** e, em seguida, selecione **Renomear**. No **nome** texto, digite o nome que você deseja usar para essa configuração de serviço e, em seguida, selecione **Okey**.
   
    O nome do arquivo de configuração de serviço é alterado no projeto do Azure no Gerenciador de soluções.

### <a name="to-change-a-service-configuration"></a>Para alterar uma configuração de serviço
* Se você quiser alterar uma configuração de serviço, abra o menu de atalho da função específica que você deseja alterar no projeto do Azure e, em seguida, selecione **propriedades**. Ver [como: configurar as funções para um serviço de nuvem do Azure com o Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md) para obter mais informações.

## <a name="make-different-setting-combinations-by-using-profiles"></a>Fazer diferentes combinações de configurações usando os perfis
Usando um perfil, você pode preencher automaticamente a **Assistente de publicação** com diferentes combinações de configurações para diferentes finalidades. Por exemplo, você pode ter um perfil para depuração e outra versão de compilações. Nesse caso, sua **Debug** perfil teria **IntelliTrace** habilitado e o **depurar** configuração selecionada e seu **versão** perfil teria **IntelliTrace** desabilitada e o **versão** configuração selecionada. Você também pode usar perfis diferentes para implantar um serviço usando uma conta de armazenamento diferentes.

Quando você executa o assistente pela primeira vez, um perfil padrão é criado. O Visual Studio armazena o perfil em um arquivo que tem uma extensão. azurePubxml, que é adicionada ao seu projeto do Azure sob a **perfis** pasta. Se você especificar diferentes opções manualmente quando você executa o assistente mais tarde, o arquivo é atualizado automaticamente. Antes de executar o procedimento a seguir, você já deve ter publicado seu serviço de nuvem pelo menos uma vez.

### <a name="to-add-a-profile"></a>Para adicionar um perfil
1. Abra o menu de atalho do seu projeto do Azure e, em seguida, selecione **publicar**.
2. Ao lado de **perfil de destino** lista, selecione o **Salvar perfil** botão, como mostra a ilustração a seguir. Isso cria um perfil para você.
   
    ![Criar um novo perfil](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/create-new-profile.png)
3. Depois que o perfil é criado, selecione **< gerenciar... >** na **perfil de destino** lista.
   
    O **gerenciar perfis** caixa de diálogo for exibida, como mostra a ilustração a seguir.
   
    ![Gerenciar perfis de caixa de diálogo](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-profiles.png)
4. No **nome** lista, escolha um perfil e, em seguida, selecione **criar cópia**.
5. Escolha o **fechar** botão.
   
    O novo perfil aparece na lista perfil de destino.
6. No **perfil de destino** lista, selecione o perfil que você acabou de criar. As configurações do Assistente de publicação são preenchidas com as opções do perfil selecionado.
7. Selecione o **Previous** e **próxima** botões para exibir cada página do Assistente de publicação e, em seguida, personalizar as configurações para este perfil. Ver [assistente Publicar aplicativo do Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) para obter informações.
8. Quando terminar de personalizar as configurações, selecione **próxima** para voltar para a página de configurações. O perfil é salvo quando você publica o serviço usando essas configurações ou se você selecionar **salvar** ao lado da lista de perfis.

### <a name="to-rename-or-delete-a-profile"></a>Para renomear ou excluir um perfil
1. Abra o menu de atalho do seu projeto do Azure e, em seguida, selecione **publicar**.
2. No **perfil de destino** lista, selecione **gerenciar**.
3. No **gerenciar perfis** caixa de diálogo, selecione o perfil que você deseja excluir e selecione **remover**.
4. Na caixa de diálogo de confirmação é exibida, selecione **Okey**.
5. Selecione **fechar**.

### <a name="to-change-a-profile"></a>Para alterar um perfil
1. Abra o menu de atalho do seu projeto do Azure e, em seguida, selecione **publicar**.
2. No **perfil de destino** lista, selecione o perfil que você deseja alterar.
3. Selecione o **Previous** e **próxima** botões para exibir cada página do Assistente de publicação e, em seguida, altere as configurações desejadas. Ver [assistente Publicar aplicativo do Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) para obter informações.
4. Depois de terminar de alterar as configurações, selecione **próxima** para voltar para o **configurações** página.
5. (Opcional) selecione **publicar** para publicar o serviço de nuvem usando as novas configurações. Se você não quiser publicar seu serviço de nuvem no momento e fechar o Assistente de publicação, o Visual Studio pergunta se você deseja salvar as alterações no perfil.

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como configurar outras partes do seu projeto do Azure do Visual Studio, consulte [Configurando um projeto do Azure](http://go.microsoft.com/fwlink/p/?LinkID=623075)

