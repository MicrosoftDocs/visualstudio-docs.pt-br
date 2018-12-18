---
title: Depurando extensões para as ferramentas do SharePoint no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, debugging extensions
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5f878284c6e181956cbd3e708334301963aa25cf
ms.sourcegitcommit: e6b13898cfbd89449f786c2e8f3e3e7377afcf25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36326089"
---
# <a name="debug-extensions-for-the-sharepoint-tools-in-visual-studio"></a>Depurar extensões para ferramentas do SharePoint no Visual Studio
  Você pode depurar extensões de ferramentas do SharePoint na instância experimental ou na instância normal do Visual Studio. Se você precisar solucionar problemas no comportamento de uma extensão, você também pode modificar os valores do registro para exibir informações de erro adicionais e para configurar como o Visual Studio executa comandos do SharePoint.

## <a name="debug-extensions-in-the-experimental-instance-of-visual-studio"></a>Depurar extensões na instância experimental do Visual Studio
 Para proteger seu ambiente de desenvolvimento do Visual Studio contra danos acidentais por extensões não testadas, o SDK do Visual Studio fornece uma instância alternativa do Visual Studio, chamada de *instância experimental*, que você pode usar Para instalar e testar extensões. Você desenvolve novas extensões usando a instância normal do Visual Studio, mas depurar e executá-los na instância experimental. Para obter mais informações, consulte [a instância Experimental](../extensibility/the-experimental-instance.md).

 Se você usar um projeto de VSIX para implantar sua extensão e o projeto do VSIX é o projeto de inicialização em sua solução, o Visual Studio automaticamente instala e executa a extensão na instância experimental, quando você depura sua solução. O projeto de inicialização é o projeto que é iniciado quando você depura uma solução que contém vários projetos. Para obter mais informações sobre como usar um projeto de VSIX para implantar sua extensão, consulte [implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

 Para obter exemplos que demonstram como depurar vários tipos de extensões na instância experimental do Visual Studio, consulte as instruções a seguir:

-   [Passo a passo: Estender um tipo de item de projeto do SharePoint](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)

-   [Passo a passo: Criar o item de projeto de ação personalizada com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)

-   [Passo a passo: Criar uma etapa de implantação para projetos do SharePoint](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)

-   [Passo a passo: Estenda o Gerenciador de servidores para exibir web parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)

-   [Passo a passo: Chamar o modelo de objeto de cliente do SharePoint em uma extensão do Gerenciador de servidores](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)

## <a name="debug-extensions-in-the-regular-instance-of-visual-studio"></a>Depurar extensões na instância normal do Visual Studio
 Se você quiser depurar seu projeto de extensão na instância normal do Visual Studio, primeiro instale a extensão na instância normal. Em seguida, anexe o depurador a um segundo processo do Visual Studio. Depois que você tiver terminado, você pode remover a extensão, de modo que ele não carrega no computador de desenvolvimento.

#### <a name="to-install-the-extension"></a>Para instalar a extensão

1.  Feche todas as instâncias do Visual Studio.

2.  Na pasta de saída de compilação para o projeto de extensão, abra o *. VSIX* arquivo clicando duas vezes nele ou abrindo o menu de atalho e, em seguida, escolhendo **abrir**:

3.  No **instalador de extensão do Visual Studio** diálogo caixa, escolha a edição do Visual Studio para o qual você deseja instalar a extensão e, em seguida, escolha o **instalar** botão.

     O Visual Studio instala os arquivos de extensão para %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions\\*nome do autor*\\*nome da extensão* \\ *versão*. As últimas três pastas neste caminho são construídas a partir de `Author`, `Name`, e `Version` elementos no *vsixmanifest* arquivo para a extensão.

4.  Depois que o Visual Studio instala a extensão, escolha o **fechar** botão.

#### <a name="to-debug-the-extension"></a>Para depurar a extensão

1.  Inicie o Visual Studio com privilégios de administrador e abra o projeto de extensão. As etapas a seguir se referem a essa instância do Visual Studio como o *pela primeira vez da instância*.

2.  Inicie outra instância do Visual Studio com privilégios de administrador. As etapas a seguir se referem a essa instância do Visual Studio como o *segunda instância*.

3.  Alterne para a primeira instância do Visual Studio.

4.  Na barra de menus, escolha **Debug**, **anexar ao processo**.

5.  No **processos disponíveis** , escolha *devenv.exe*. Essa entrada refere-se à segunda instância do Visual Studio; Essa é a instância que você deseja depurar a extensão do seu projeto.

6.  Escolha o **Attach** botão.

     Visual Studio executa o projeto de extensão no modo de depuração.

7.  Alterne para a segunda instância do Visual Studio.

8.  Crie um novo projeto do SharePoint que carrega sua extensão. Por exemplo, se você estiver depurando uma extensão para itens de projeto de definição de lista, crie uma **definição de lista** projeto.

9. Execute todas as etapas necessárias para testar o seu código de extensão.

10. Quando tiver terminado de depurar a extensão, feche a segunda instância do Visual Studio.

#### <a name="to-remove-the-extension"></a>Para remover a extensão

1.  No Visual Studio, na barra de menus, escolha **ferramentas**, **extensões e atualizações**.

     A caixa de diálogo **Extensões e Atualizações** é aberta.

2.  Na lista de extensões, escolha o nome da extensão e, em seguida, escolha o **desinstalação** botão.

3.  Na caixa de diálogo que aparece, escolha o **Sim** botão para confirmar que você deseja desinstalar a extensão.

4.  Escolha o **reiniciar agora** botão para concluir a desinstalação.

## <a name="debug-sharepoint-commands"></a>Depurar os comandos do SharePoint
 Se você quiser depurar um comando do SharePoint que faz parte de uma extensão de ferramentas do SharePoint, você deve anexar o depurador para o *vssphost4.exe* processo. Este é o processo de host de 64 bits que executa comandos do SharePoint. Para obter mais informações sobre os comandos do SharePoint e *vssphost4.exe*, consulte [chamam os modelos de objeto SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).

#### <a name="to-attach-the-debugger-to-the-vssphost4exe-process"></a>Para anexar o depurador ao processo vssphost4.exe

1.  Comece a depurar a extensão na instância experimental do Visual Studio ou na instância normal do Visual Studio, seguindo as instruções acima.

2.  Na instância do Visual Studio, no qual você está executando o depurador, na barra de menus, escolha **Debug**, **anexar ao processo**.

3.  No **processos disponíveis** , escolha *vssphost.exe*.

    > [!NOTE]
    >  Se vssphost.exe não aparecer na lista, você deve iniciar o *vssphost4.exe* processos na instância do Visual Studio na qual você está executando a extensão. Normalmente, você faz isso executando uma ação que faz com que o Visual Studio para se conectar ao site do SharePoint no computador de desenvolvimento. Por exemplo, o Visual Studio inicia *vssphost4.exe* quando você expande um nó de conexão de site (um nó que exibe uma URL do site) sob o **conexões do SharePoint** nó o **Gerenciador de servidores**  janela, ou quando você adiciona determinados itens de projeto do SharePoint, como **instância de lista** ou **receptor de evento** itens para um projeto do SharePoint.

4.  Escolha o **Attach** botão.

5.  Na instância do Visual Studio que está sendo depurada, execute as etapas necessárias para executar o comando.

## <a name="modify-registry-values-to-help-debug-sharepoint-tools-extensions"></a>Modificar valores do registro para ajudar a depurar extensões de ferramentas do SharePoint
 Quando você depura uma extensão das ferramentas do SharePoint no Visual Studio, você pode modificar valores no registro para ajudá-lo a solucionar problemas da extensão. Os valores existem sob o **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\SharePointTools** chave. Esses valores não existem por padrão.

 Para ajudar a solucionar problemas de qualquer extensão das ferramentas do SharePoint, você pode criar e definir o valor EnableDiagnostics. A tabela a seguir descreve esse valor.

|Valor|Descrição|
|-----------|-----------------|
|EnableDiagnostics|REG_DWORD que especifica se as mensagens de diagnóstico são exibidas na **saída** janela.<br /><br /> Para exibir mensagens de diagnóstico, defina esse valor como 1. Para interromper a exibição de mensagens, defina esse valor como 0 ou exclua esse valor.<br /><br /> Para gravar mensagens para o **saída** extensão das ferramentas de janela a partir do SharePoint, use o serviço de projeto do SharePoint. Para obter mais informações, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).|

 Se sua extensão incluir um comando do SharePoint, você pode criar e definir valores adicionais para ajudar a solucionar o comando. A tabela a seguir descreve esses valores.

|Valor|Descrição|
|-----------|-----------------|
|AttachDebuggerToHostProcess|REG_DWORD que especifica se deve exibir uma caixa de diálogo que permite que você anexar o depurador *vssphost4.exe* assim que ele é iniciado. Isso é útil se o comando que você deseja depurar for executado pelo vssphost.exe imediatamente após ele ser iniciado, e não há tempo suficiente para anexar o depurador manualmente antes do comando é executado. Para exibir a caixa de diálogo *vssphost4.exe* chamadas a <xref:System.Diagnostics.Debugger.Break%2A> método quando ele é iniciado.<br /><br /> Para habilitar esse comportamento, defina esse valor como 1. Para desativar esse comportamento, defina esse valor como 0 ou exclua esse valor.<br /><br /> Se você definir esse valor como 1, você talvez queira aumentar o valor de HostProcessStartupTimeout para fornecer tempo suficiente para anexar o depurador antes do Visual Studio espera *vssphost4.exe* para sinalizar que foi iniciado com êxito.|
|ChannelOperationTimeout|REG_DWORD que especifica o tempo, em segundos, que o Visual Studio aguarda executar um comando do SharePoint. Se o comando não for executado no momento, um <xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException> é gerada.<br /><br /> O padrão é 120 segundos.|
|HostProcessStartupTimeout|REG_DWORD que especifica o tempo, em segundos, que o Visual Studio aguarda *vssphost4.exe* para sinalizar que foi iniciado com êxito. Se *vssphost4.exe* não sinalizar um início bem-sucedido no tempo, um <xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException> é gerada.<br /><br /> O padrão é 60 segundos.|
|MaxReceivedMessageSize|REG_DWORD que especifica o tamanho máximo permitido, em bytes, de mensagens do WCF que são passadas entre o Visual Studio e *vssphost4.exe*.<br /><br /> O padrão é 1.048.576 bytes (1 MB).|
|MaxStringContentLength|REG_DWORD que especifica o tamanho máximo permitido, em bytes, de cadeias de caracteres que são passadas entre o Visual Studio e *vssphost4.exe*.<br /><br /> O padrão é 1.048.576 bytes (1 MB).|

## <a name="see-also"></a>Consulte também

- [Estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [Implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
