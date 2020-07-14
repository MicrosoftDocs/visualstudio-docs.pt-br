---
title: Usando o coletor autônomo do IntelliTrace | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.historicaldebug.collectdataoutsideVS
helpviewer_keywords:
- IntelliTrace, debugging applications in production
ms.assetid: 1bde9807-8219-4a2a-a440-ac5ee5178159
caps.latest.revision: 111
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 81eedeeb9a1b2470e87f0d865996ad3e456723fe
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520543"
---
# <a name="using-the-intellitrace-stand-alone-collector"></a>Usar o coletor autônomo do IntelliTrace
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **coletor autônomo do IntelliTrace** permite coletar dados de diagnóstico IntelliTrace para seus aplicativos em servidores de produção ou em outros ambientes, sem instalar o Visual Studio no computador de destino e sem alterar o ambiente do sistema de destino. O coletor independente do IntelliTrace funciona na Web, SharePoint, WPF e aplicativos do Windows Forms. Quando você terminar a coleta de dados, basta excluir o coletor para desinstalá-lo.

 Assista ao IntelliTrace em ação: [coletando e analisando dados do IntelliTrace na produção para depuração (vídeo do canal 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Collecting-and-analyzing-data-in-production)

> [!NOTE]
> Você também pode coletar os mesmos dados IntelliTrace para aplicativos da web e do Sharepoint executados em computadores remotos usando o **Microsoft Monitoring Agent** no modo **Rastrear**.
>
> Você pode coletar eventos relacionados ao desempenho nos dados IntelliTrace executando o agente no modo **Monitorar**. O modo **Monitorar** tem menos um impacto no desempenho que o modo **Rastrear** ou que o **coletor autônomo do IntelliTrace**. O Microsoft Monitoring Agent altera o ambiente do sistema de destino quando instalado. Consulte [usando o Microsoft Monitoring Agent](../debugger/using-the-microsoft-monitoring-agent.md).

 **Requisitos**

- .NET Framework 3.5, 4 ou 4.5

- Visual Studio Enterprise (mas não edições Professional ou Community) em um computador de desenvolvimento ou em outro computador para abrir arquivos. iTrace

  > [!NOTE]
  > Certifique-se de salvar o símbolo arquivos (.pdb). Para depurar com o IntelliTrace e percorrer o código, você deve ter os arquivos de origem e de símbolo correspondentes. Consulte [diagnosticar problemas após a implantação](../debugger/diagnose-problems-after-deployment.md).

  **perguntas frequentes**

- [Quais aplicativos funcionam com o coletor?](#WhatApps)

- [Como começar?](#GetStarted)

- [Como posso obter o máximo de dados sem deixar meu aplicativo mais lento?](#Minimizing)

- [Onde mais posso obter dados do IntelliTrace?](#WhereElse)

## <a name="what-apps-work-with-the-collector"></a><a name="WhatApps"></a>Quais aplicativos funcionam com o coletor?

- Aplicativos da Web ASP.NET hospedados no Internet Information Services (IIS) versão 7.0, 7.5 e 8.0

- Aplicativos SharePoint 2010 e SharePoint 2013

- Aplicativos do Windows Presentation Foundation (WPF) e Windows Forms.

## <a name="how-do-i-get-started"></a><a name="GetStarted"></a>Como fazer começar?

1. [Instalar o coletor](#BKMK_Install_the_IntelliTrace_Stand_Alone_Collector)

2. [Configurar as permissões para o diretório do coletor](#ConfigurePermissionsRunningCollector)

3. [Instale os cmdlets PowerShell do IntelliTrace a fim de coletar dados para aplicativos Web ou aplicativos do SharePoint](#BKMK_Set_up_the_IntelliTrace_PowerShell_commandlets)

4. [Configurar permissões para o diretório de arquivos .iTrace](#BKMK_Create_and_Configure_a_Log_File_Directory)

5. [Coletar os dados de um aplicativo da web ou do SharePoint](#BKMK_Collect_Data_from_IIS_Application_Pools)

     -ou-

     [Coletar dados de um aplicativo gerenciado](#BKMK_Collect_Data_from_Executables)

6. [Abra o arquivo. iTrace em Visual Studio Enterprise](#BKMK_View_IntelliTrace_Log_Files)

## <a name="install-the-collector"></a><a name="BKMK_Install_the_IntelliTrace_Stand_Alone_Collector"></a>Instalar o coletor

1. No servidor do seu aplicativo, crie o diretório do coletor, por exemplo: **C:\IntelliTraceCollector**

2. Obtenha o coletor no Centro de Download da Microsoft na pasta de instalação do Visual Studio 2103 atualização 3. [Coletor IntelliTrace para Visual Studio 2013 atualização 4](https://www.microsoft.com/download/details.aspx?id=44909)::

   - **Centro de download da Microsoft**:

     1. Ao lado de **IntelliTraceCollector.exe**, escolha **Baixar**.

     2. Salve IntelliTraceCollector.exe no diretório do coletor, por exemplo: **C:\IntelliTraceCollector**

     3. Execute o IntelliTraceCollector.exe. Isso extrai o arquivo IntelliTraceCollection.cab.

        \- ou –

   - **Pasta de instalação do Visual Studio**:

     1. Copie o IntelliTraceCollection.cab da pasta a seguir:

          **.. \Microsoft Visual Studio 12.0 \ Common7\IDE\CommonExtensions\Microsoft\IntelliTrace\12.0.0**

     2. Coloque IntelliTraceCollection.cab no diretório do coletor, por exemplo: **C:\IntelliTraceCollector**

3. Expanda o IntelliTraceCollection.cab:

   1. No servidor do aplicativo, abra uma janela de prompt de comando como administrador.

   2. Navegue até o diretório do coletor, por exemplo: **C:\IntelliTraceCollector**

   3. Use o comando **Expand** , incluindo o ponto (**.**) no final, para expandir IntelliTraceCollection.cab:

        `expand  /f:* IntelliTraceCollection.cab .`

       > [!NOTE]
       > O ponto (**.**) preserva as subpastas que contêm planos de coleta localizada.

## <a name="set-up-permissions-for-the-collector-directory"></a><a name="ConfigurePermissionsRunningCollector"></a>Configurar permissões para o diretório do coletor

1. No servidor do aplicativo, abra uma janela de prompt de comando como administrador.

2. Use o comando **icacls** do Windows para conceder ao administrador do servidor permissões completas para o diretório do coletor. Por exemplo:

     `icacls "C:\IntelliTraceCollector" /grant "` *\<Domain\AdministratorID>* `":F`

3. Para coletar dados de um aplicativo da web ou do SharePoint:

    1. Conceda permissão total ao diretório do coletor à pessoa que executará os cmdlets do IntelliTrace PowerShell.

         Por exemplo:

         `icacls "C:\IntelliTraceCollector" /grant "` *\<Domain\UserID>* `":F`

    2. Conceda ao pool de aplicativos para o aplicativo da web ou do SharePoint permissões de leitura e execução para o diretório do coletor.

         Por exemplo:

        - Para um aplicativo Web no pool de aplicativos **DefaultAppPool** :

             `icacls "C:\IntelliTraceCollector" /grant "IIS APPPOOL\DefaultAppPool":RX`

        - Para um aplicativo do SharePoint no pool de aplicativos **SharePoint - 80**:

             `icacls "C:\IntelliTraceCollector" /grant "IIS APPPOOL\SharePoint - 80":RX`

## <a name="install-intellitrace-powershell-cmdlets-to-collect-data-for-web-apps-or-sharepoint-applications"></a><a name="BKMK_Set_up_the_IntelliTrace_PowerShell_commandlets"></a>Instale os cmdlets do PowerShell do IntelliTrace para coletar dados de aplicativos Web ou do SharePoint

1. No servidor do aplicativo, certifique-se de que o PowerShell está habilitado. Na maioria das versões do Windows Server, você pode adicionar esse recurso na ferramenta administrativa **Gerenciador do Servidor**.

     ![Adicionando o PowerShell usando Gerenciador do Servidor](../debugger/media/intellitrace-servermanager-addpowershell.png "INTELLITRACE_ServerManager_AddPowerShell")

2. Instale os cmdlets do IntelliTrace PowerShell.

    1. Abra uma janela de comando do PowerShell como administrador.

        1. Selecione **Iniciar**, **Todos os Programas**, **Acessórios**, **Windows PowerShell**.

        2. Escolha uma das seguintes etapas:

            - Em sistemas operacionais de 64 bits, abra o menu de atalho do **Windows PowerShell**. Escolha **Executar como administrador**.

            - Em sistemas operacionais de 32 bits, abra o menu de atalho do **Windows PowerShell (x86)**. Escolha **Executar como administrador**.

    2. Na janela de comando do PowerShell, use o comando **Import-Module** para importar o **Microsoft.VisualStudio.IntelliTrace.PowerShell.dll**.

         Por exemplo:

         `Import-Module "C:\IntelliTraceCollector\Microsoft.VisualStudio.IntelliTrace.PowerShell.dll"`

## <a name="set-up-permissions-for-the-itrace-file-directory"></a><a name="BKMK_Create_and_Configure_a_Log_File_Directory"></a>Configurar permissões para o diretório de arquivos. iTrace

1. No servidor do seu aplicativo, crie o diretório do arquivo. iTrace, por exemplo: **C:\IntelliTraceLogFiles**

   > [!NOTE]
   > - Para evitar que seu aplicativo fique mais lento, escolha um local em um disco de alta velocidade local que não seja muito ativo.
   >   - Você pode colocar os arquivos .iTrace e os coletores no mesmo lugar. No entanto, se você tiver um aplicativo da web ou do SharePoint, verifique se que esse local está fora do diretório que hospeda o aplicativo.
   >
   > [!IMPORTANT]
   > - Restrinja o diretório do arquivo .iTrace a apenas as identidades que devem trabalhar com o coletor. Um arquivo .iTrace pode conter informações confidenciais, tais como dados de usuários, bancos de dados, outros locais de origem e cadeias de conexão como IntelliTrace podem registrar quaisquer dados que passem os parâmetros de método ou como valores de retorno.
   >   - Certifique-se de aqueles que podem abrir os arquivos .iTrace têm autoridade para ver dados confidenciais. Tenha cuidado ao compartilhar arquivos .iTrace. Se outras pessoas precisarem ter acesso, copie os arquivos para um local compartilhado seguro.

2. Para um aplicativo da web ou do SharePoint, conceda ao seu pool de aplicativos permissões totais para o diretório de arquivos .iTrace. Você pode usar o comando **icacls** do Windows ou usar o Windows Explorer (ou explorador de arquivos).

    Por exemplo:

   - Para configurar permissões com o comando **icacls** do Windows:

     - Para um aplicativo Web no pool de aplicativos **DefaultAppPool** :

        `icacls "C:\IntelliTraceLogFiles" /grant "IIS APPPOOL\DefaultAppPool":F`

     - Para um aplicativo do SharePoint no pool de aplicativos **SharePoint - 80**:

        `icacls "C:\IntelliTraceLogFiles" /grant "IIS APPPOOL\SharePoint - 80":F`

       -ou-

   - Para configurar permissões com o Windows Explorer (ou o Explorador de Arquivos):

     1. Abra as **Propriedades** do diretório de arquivos .iTrace.

     2. Na guia **Segurança**, escolha **Editar**, **Adicionar**.

     3. Verifique se **Entidades de segurança interna** é exibido na caixa **Selecione este tipo de objeto**. Se não estiver lá, escolha **tipos de objeto** para adicioná-lo.

     4. Verifique se o computador local é exibido na caixa **Deste local**. Se não estiver lá, escolha os **locais** para alterá-lo.

     5. Na caixa **Digite os nomes de objeto a serem selecionados**, adicione o pool de aplicativos do aplicativo Web ou do aplicativo do SharePoint.

     6. Escolha **Verificar Nomes** para resolver o nome. Selecione **OK**.

     7. Verifique se o pool de aplicativos tem **Controle total**.

## <a name="collect-data-from-a-web-app-or-sharepoint-application"></a><a name="BKMK_Collect_Data_from_IIS_Application_Pools"></a>Coletar dados de um aplicativo Web ou aplicativos do SharePoint

1. Para iniciar a coleta de dados, abra uma janela de comando do PowerShell como administrador e execute este comando:

     `Start-IntelliTraceCollection` `"` *\<ApplicationPool>* `"` *\<PathToCollectionPlan>* *\<FullPathToITraceFileDirectory>*

    > [!IMPORTANT]
    > Depois de executar esse comando, digite **Y** para confirmar que você deseja iniciar a coleta de dados.

     Por exemplo, para coletar dados de um aplicativo do SharePoint no pool de aplicativos **do SharePoint-80** :

     `Start-IntelliTraceCollection "SharePoint - 80" "C:\IntelliTraceCollector\collection_plan.ASP.NET.default.xml" "C:\IntelliTraceLogFiles"`

    |Item|Descrição|
    |-|-|
    |*ApplicationPool*|O nome do pool de aplicativos onde o aplicativo é executado|
    |*PathToCollectionPlan*|O caminho para um plano de coleta, um arquivo.xml que define as configurações para o coletor.<br /><br /> Você pode especificar um plano que vem com o coletor. Os seguintes planos funcionam para aplicativos da web e do SharePoint:<br /><br /> – collection_plan.ASP.NET.default.xml<br />     Coleta apenas eventos IntelliTrace do SharePoint, incluindo exceções, chamadas de banco de dados e solicitações no servidor da web.<br />– collection_plan.ASP.NET.trace.xml<br />     Coleta chamadas de função e todos os dados no collection_plan.ASP.NET.default.xml. Esse plano é útil para uma análise detalhada, mas pode causar lentidão no seu aplicativo mais do que no collection_plan.ASP.NET.default.xml.<br /><br /> Para evitar causar lentidão no seu aplicativo, personalize esses planos ou crie seu próprio plano. Por segurança, coloque planos personalizados no mesmo local seguro que os arquivos do coletor. Consulte [criando e personalizando planos de coleta do IntelliTrace](https://devblogs.microsoft.com/devops/modifying-an-intellitrace-collection-plan-for-the-stand-alone-collector/) e [como fazer obter a maioria dos dados sem atrasar o meu aplicativo?](#Minimizing) **Observação:**  Por padrão, o tamanho máximo do arquivo. iTrace é de 100 MB. Quando o arquivo .iTrace atingir esse limite, o coletor exclui as entradas de mais antigas do arquivo para dar espaço às entradas mais recentes. Para alterar esse limite, edite o atributo `MaximumLogFileSize` do plano de coleta. <br /><br /> *Onde posso encontrar versões localizadas desses planos de coleta?*<br /><br /> Você pode encontrar planos localizados nas subpastas do coletor.|
    |*FullPathToITraceFileDirectory*|O caminho completo para o diretório de arquivos .iTrace. **Observação de segurança:**  Forneça o caminho completo, não um caminho relativo.|

     O coletor anexa-se ao pool de aplicativos e inicia a coleta de dados.

     *Posso abrir o arquivo .iTrace neste momento?* Não, o arquivo fica bloqueado durante a coleta de dados.

2. Reproduza o problema.

3. Para obter um instantâneo do arquivo .iTrace, use a seguinte sintaxe:

     `Checkpoint-IntelliTraceCollection` `"` *\<ApplicationPool>* `"`

4. Para verificar o status da coleta, use a seguinte sintaxe:

     `Get-IntelliTraceCollectionStatus`

5. Para interromper a coleta de dados, use a seguinte sintaxe:

     `Stop-IntelliTraceCollection` `"` *\<ApplicationPool>* `"`

    > [!IMPORTANT]
    > Depois de executar esse comando, digite **Y** para confirmar que você deseja parar a coleta de dados. Caso contrário, o coletor podem continuar com a coleta de dados, o arquivo iTrace permanecerá bloqueado ou o arquivo pode não conter dados úteis.

6. [Abra o arquivo. iTrace em Visual Studio Enterprise](#BKMK_View_IntelliTrace_Log_Files)

## <a name="collect-data-from-a-managed-app"></a><a name="BKMK_Collect_Data_from_Executables"></a> Coletar dados de um aplicativo gerenciado

1. Para iniciar o aplicativo e coletar dados ao mesmo tempo, use a seguinte sintaxe:

     *\<FullPathToIntelliTraceCollectorExecutable>* `\IntelliTraceSC.exe launch /cp:` *\<PathToCollectionPlan>* `/f:` *\<FullPathToITraceFileDirectoryAndFileName>* *\<PathToAppExecutableFileAndFileName>*

     Por exemplo, para coletar dados de um aplicativo chamado **MyApp**:

     `C:IntelliTraceCollectorIntelliTraceSC.exe launch /cp:"C:IntelliTraceCollectorcollection_plan.ASP.NET.default.xml" /f:"C:IntelliTraceLogFilesMyApp.itrace" "C:MyAppMyApp.exe"`

    |Item|Descrição|
    |-|-|
    |*FullPathToIntelliTraceCollectorExecutable*|O caminho completo para o coletor executável, IntelliTraceSC.exe|
    |*PathToCollectionPlan*|O caminho para um plano de coleta, um arquivo.xml que define as configurações para o coletor.<br /><br /> Você pode especificar um plano que vem com o coletor. Os seguintes planos funcionam para aplicativos gerenciados:<br /><br /> – collection_plan.ASP.NET.default.xml<br />     Coleta somente eventos do IntelliTrace, incluindo exceções, chamadas de banco de dados e solicitações no servidor da web.<br />– collection_plan.ASP.NET.trace.xml<br />     Coleta chamadas de função e todos os dados no collection_plan.ASP.NET.default.xml. Esse plano é útil para uma análise detalhada, mas pode causar lentidão no seu aplicativo mais do que no collection_plan.ASP.NET.default.xml.<br /><br /> Para evitar causar lentidão no seu aplicativo, personalize esses planos ou crie seu próprio plano. Por segurança, coloque planos personalizados no mesmo local seguro que os arquivos do coletor. Consulte [criando e personalizando planos de coleta do IntelliTrace](https://devblogs.microsoft.com/devops/modifying-an-intellitrace-collection-plan-for-the-stand-alone-collector/) e [como fazer obter a maioria dos dados sem atrasar o meu aplicativo?](#Minimizing) **Observação:**  Por padrão, o tamanho máximo do arquivo. iTrace é de 100 MB. Quando o arquivo .iTrace atingir esse limite, o coletor exclui as entradas de mais antigas do arquivo para dar espaço às entradas mais recentes. Para alterar esse limite, edite o atributo `MaximumLogFileSize` do plano de coleta. <br /><br /> *Onde posso encontrar versões localizadas desses planos de coleta?*<br /><br /> Você pode encontrar planos localizados nas subpastas do coletor.|
    |*FullPathToITraceFileDirectoryAndFileName*|O caminho completo para o diretório do arquivo. iTrace e o nome do arquivo. iTrace com a extensão **. itrace** . **Observação de segurança:**  Forneça o caminho completo, não um caminho relativo.|
    |*PathToAppExecutableFileAndFileName*|O caminho e o nome de arquivo do seu aplicativo gerenciado|

2. Interrompa a coleta de dados saindo do aplicativo.

3. [Abra o arquivo. iTrace em Visual Studio Enterprise](#BKMK_View_IntelliTrace_Log_Files)

## <a name="open-the-itrace-file-in-visual-studio-enterprise"></a><a name="BKMK_View_IntelliTrace_Log_Files"></a>Abra o arquivo. iTrace em Visual Studio Enterprise

> [!NOTE]
> Para depurar com o IntelliTrace e percorrer o código, você deve ter os arquivos de origem e de símbolo correspondentes. Consulte [diagnosticar problemas após a implantação](../debugger/diagnose-problems-after-deployment.md).

1. Mova o arquivo. iTrace ou copie-o para um computador com Visual Studio Enterprise (mas não com as edições Professional ou Community).

2. Clique duas vezes no arquivo .iTrace fora do Visual Studio ou abra o arquivo de dentro do Visual Studio.

     O Visual Studio mostra a página **Resumo do IntelliTrace**. Na maioria das seções, você pode examinar eventos ou outros itens, escolher um item e iniciar a depuração com o IntelliTrace no ponto onde e quando um evento que ocorreu. Consulte [usando dados do IntelliTrace salvos](../debugger/using-saved-intellitrace-data.md).

    > [!NOTE]
    > Para depurar com o IntelliTrace e percorrer o código, você deve ter os arquivos de origem e de símbolo correspondentes no seu computador de desenvolvimento. Consulte [diagnosticar problemas após a implantação](../debugger/diagnose-problems-after-deployment.md).

## <a name="how-do-i-get-the-most-data-without-slowing-down-my-app"></a><a name="Minimizing"></a>Como fazer obter a maioria dos dados sem atrasar o meu aplicativo?
 O IntelliTrace pode coletar grandes quantidades de dados, por isso o impacto no desempenho do aplicativo depende dos dados que o IntelliTrace coleta e do tipo de código analisado. Consulte [otimizando a coleta do IntelliTrace em servidores de produção](https://devblogs.microsoft.com/devops/optimizing-intellitrace-collection-on-production-server/).

 Estas são algumas das maneiras de obter a maioria dos dados sem deixar seu aplicativo mais lento:

- Execute o coletor somente quando você achar que há um problema ou quando você puder reproduzir o problema.

   Inicie a coleta, reproduza o problema e, em seguida, pare a coleta. Abra o arquivo. iTrace em Visual Studio Enterprise e examine os dados. Consulte [abrir o arquivo. itrace em Visual Studio Enterprise](#BKMK_View_IntelliTrace_Log_Files).

- Para aplicativos da web e do SharePoint, o coletor grava os dados de todos os aplicativos que compartilham o pool de aplicativos especificado. Isso talvez deixe mais lento qualquer aplicativo que compartilhe o mesmo pool de aplicativos, mesmo que você possa especificar módulos para um único aplicativo no plano de coleta.

   Para evitar que o coletor deixe outros aplicativos mais lentos, hospede cada aplicativo em seu próprio pool de aplicativos.

- Revise os eventos no plano de coleta para o qual o IntelliTrace coleta os dados. Edite o plano de coleta para desabilitar eventos que não sejam relevantes ou que não sejam de seu interesse.

   Para desabilitar um evento, defina o atributo `enabled` para o elemento `<DiagnosticEventSpecification>` como `false`:

   `<DiagnosticEventSpecification enabled="false">`

   Se o atributo `enabled` não existir, o evento estará habilitado.

   *Como isso melhora o desempenho?*

  - Você pode reduzir o tempo de inicialização desabilitando eventos que não são relevantes para o aplicativo. Por exemplo, desabilite eventos do Fluxo de Trabalho do Windows para aplicativos que não usam o Fluxo de Trabalho do Windows.

  - Você pode melhorar o desempenho de inicialização e do runtime desabilitando eventos do registro para aplicativos que acessam o registro, mas não apresentam problemas com as configurações do registro.

- Revise os módulos no plano de coleta para o qual o IntelliTrace coleta os dados. Edite o plano de coleta para incluir somente os módulos de seu interesse:

  1. Abra o plano de coleta. Localize o elemento `<ModuleList>`.

  2. Em `<ModuleList>`, defina o atributo `isExclusionList` como `false`.

  3. Use o elemento `<Name>` para especificar cada módulo com um dos seguintes: nome do arquivo, valor da cadeia de caracteres para incluir qualquer módulo cujo nome contenha essa cadeia de caracteres ou chave pública.

     Por exemplo, para coletar dados apenas do módulo da web principal do aplicativo da web Fabrikam Fiber, crie uma lista como esta:

  ```xml
  <ModuleList isExclusionList="false">
     <Name>FabrikamFiber.Web.dll</Name>
  </ModuleList>

  ```

   Para coletar dados de qualquer módulo cujo nome inclua "Fabrikam", crie uma lista assim:

  ```xml
  <ModuleList isExclusionList="false">
     <Name>Fabrikam</Name>
  </ModuleList>

  ```

   Para coletar dados de módulos especificando seus tokens de chave pública, crie uma lista assim:

  ```xml
  <ModuleList isExclusionList="false">
     <Name>PublicKeyToken:B77A5C561934E089</Name>
     <Name>PublicKeyToken:B03F5F7F11D50A3A</Name>
     <Name>PublicKeyToken:31BF3856AD364E35</Name>
     <Name>PublicKeyToken:89845DCD8080CC91</Name>
     <Name>PublicKeyToken:71E9BCE111E9429C</Name>
  </ModuleList>

  ```

   *Como isso melhora o desempenho?*

   Isso reduz a quantidade de informações de chamada de método e outros dados de instrumentação que o IntelliTrace coleta quando o aplicativo é iniciado e executado. Esses dados permite:

  - Percorrer o código após a coleta de dados.

  - Examinar os valores passados e retornados das chamadas de função.

    *Por que não excluir módulos em vez disso?*

    Por padrão, os planos de coleta excluem módulos definindo o atributo `isExclusionList` como `true`. Entretanto, excluir módulos ainda pode resultar na coleta de dados de módulos que não atendem aos critérios da lista ou que talvez não o interessem, como módulos de terceiros ou de software livre.

- *Há dados que IntelliTrace não coleta?*

   Sim, para reduzir o impacto no desempenho, o IntelliTrace restringe a coleta de dados aos valores de tipos de dados primitivos passado e retornados de métodos e a valores de tipos de dados primitivos nos campos em objetos de nível superior passado e retornados dos métodos.

   Por exemplo, suponhamos que você tenha uma assinatura de método `AlterEmployee` que aceite um inteiro `id` e um objeto `Employee``oldemployee`:

   `public Employee AlterEmployee(int id, Employee oldemployee)`

   O tipo `Employee` tem os seguintes atributos: `Id`, `Name` e `HomeAddress`. Existe uma relação de associação entre `Employee` e o tipo `Address`.

   ![Relação entre o funcionário e o endereço](../debugger/media/employeeaddressrelationship.png "EmployeeAddressRelationship")

   O coletor registra valores de `id`, `Employee.Id`, `Employee.Name` e o objeto `Employee` retornado pelo método `AlterEmployee`. Entretanto, o coletor não registra informações sobre o objeto `Address`, exceto se ele era nulo ou não. O coletor também não registra dados sobre variáveis locais no método `AlterEmployee`, a menos que outros métodos usem essas variáveis locais como parâmetros em que eles são gravados como parâmetros de método.

## <a name="where-else-can-i-get-intellitrace-data"></a><a name="WhereElse"></a>Onde mais posso obter dados do IntelliTrace?

- Em uma sessão de depuração do IntelliTrace no Visual Studio Enterprise, consulte [recursos do IntelliTrace](../debugger/intellitrace-features.md).

- Em uma sessão de teste no Microsoft Test Manager, consulte [como: coletar dados do IntelliTrace para ajudar a depurar problemas difíceis](/visualstudio/test/how-to-collect-intellitrace-data-to-help-debug-difficult-issues?view=vs-2015).

## <a name="where-can-i-get-more-information"></a>Onde posso obter mais informações?
 [Usando os dados salvos do IntelliTrace](../debugger/using-saved-intellitrace-data.md)

 [IntelliTrace](../debugger/intellitrace.md)

### <a name="blogs"></a>Blogs
 [Usando o coletor autônomo do IntelliTrace remotamente](https://devblogs.microsoft.com/devops/using-the-intellitrace-standalone-collector-remotely/)

 [Criando e personalizando planos de coleta do IntelliTrace](https://devblogs.microsoft.com/devops/modifying-an-intellitrace-collection-plan-for-the-stand-alone-collector/)

 [Como otimizar a coleta do IntelliTrace em servidores de produção](https://devblogs.microsoft.com/devops/optimizing-intellitrace-collection-on-production-server/)

 [Blog do TFS do Visual Studio ALM +](https://devblogs.microsoft.com/devops/welcome-to-the-visual-studio-alm-team-foundation-server-blog/)

### <a name="forums"></a>Fóruns
 [Depurador do Visual Studio](https://social.msdn.microsoft.com/Forums/vsdebug)

### <a name="videos"></a>vídeos
 [Vídeo do Channel 9: coleta e análise de dados do IntelliTrace](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Collecting-and-analyzing-data-in-production)
