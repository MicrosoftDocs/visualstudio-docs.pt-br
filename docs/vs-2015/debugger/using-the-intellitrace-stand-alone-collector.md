---
title: Usando o coletor autônomo IntelliTrace | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.historicaldebug.collectdataoutsideVS
helpviewer_keywords:
- IntelliTrace, debugging applications in production
ms.assetid: 1bde9807-8219-4a2a-a440-ac5ee5178159
caps.latest.revision: 111
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c2e2fc006874316974dc92ea45b112399f6f5aad
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792873"
---
# <a name="using-the-intellitrace-stand-alone-collector"></a>Usar o coletor autônomo do IntelliTrace
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **coletor autônomo do IntelliTrace** permite coletar dados de diagnóstico do IntelliTrace para seus aplicativos em servidores de produção ou em outros ambientes sem instalar o Visual Studio no computador de destino e sem alterar o ambiente do sistema de destino. O coletor autônomo IntelliTrace funciona em aplicativos web, SharePoint, do WPF e Windows Forms. Quando você terminar a coleta de dados, basta excluir o coletor para desinstalá-lo.  
  
 Veja o IntelliTrace em ação: [coletando e analisando dados IntelliTrace em produção para depuração (vídeo do Channel 9)](http://go.microsoft.com/fwlink/?LinkID=251851)  
  
> [!NOTE]
>  Você também pode coletar os mesmos dados de IntelliTrace para aplicativos web e do SharePoint em execução em computadores remotos usando o **Microsoft Monitoring Agent** na **rastreamento** modo.  
>   
>  Você pode coletar eventos relacionados ao desempenho nos dados IntelliTrace executando o agente **Monitor** modo. **Monitor** modo tem menos de um impacto de desempenho que **rastreamento** modo ou o **coletor autônomo do IntelliTrace**. O Microsoft Monitoring Agent altera o ambiente do sistema de destino quando instalado. Ver [usando o Microsoft Monitoring Agent](../debugger/using-the-microsoft-monitoring-agent.md).  
  
 **Requisitos**  
  
- .NET Framework 3.5, 4 ou 4.5  
  
- Visual Studio Enterprise (mas não no Professional ou Community edições) em um computador de desenvolvimento ou em outro computador para abrir arquivos. itrace  
  
  > [!NOTE]
  >  Certifique-se de salvar o símbolo arquivos (.pdb). Para depurar com o IntelliTrace e percorrer o código, você deve ter os arquivos de origem e de símbolo correspondentes. Ver [diagnosticar problemas após a implantação](../debugger/diagnose-problems-after-deployment.md).  
  
  **PERGUNTAS FREQUENTES**  
  
- [Quais aplicativos funcionam com o coletor?](#WhatApps)  
  
- [Como posso começar?](#GetStarted)  
  
- [Como posso obter a maioria dos dados sem afetar a velocidade do meu aplicativo?](#Minimizing)  
  
- [Onde mais posso obter dados do IntelliTrace?](#WhereElse)  
  
##  <a name="WhatApps"></a> Quais aplicativos funcionam com o coletor?  
  
-   Aplicativos da Web ASP.NET hospedados no Internet Information Services (IIS) versão 7.0, 7.5 e 8.0  
  
-   Aplicativos SharePoint 2010 e SharePoint 2013  
  
-   Aplicativos do Windows Presentation Foundation (WPF) e Windows Forms.  
  
##  <a name="GetStarted"></a> Como posso começar?  
  
1.  [Instalar o coletor](#BKMK_Install_the_IntelliTrace_Stand_Alone_Collector)  
  
2.  [Configurar permissões para o diretório do coletor](#ConfigurePermissionsRunningCollector)  
  
3.  [Instalar cmdlets do PowerShell do IntelliTrace para coletar dados para aplicativos Web ou aplicativos do SharePoint](#BKMK_Set_up_the_IntelliTrace_PowerShell_commandlets)  
  
4.  [Configurar permissões para o diretório do arquivo. itrace](#BKMK_Create_and_Configure_a_Log_File_Directory)  
  
5.  [Coletar dados de um aplicativo Web ou aplicativo do SharePoint](#BKMK_Collect_Data_from_IIS_Application_Pools)  
  
     -ou-  
  
     [Coletar dados de um aplicativo gerenciado](#BKMK_Collect_Data_from_Executables)  
  
6.  [Abra o arquivo. itrace no Visual Studio Enterprise](#BKMK_View_IntelliTrace_Log_Files)  
  
##  <a name="BKMK_Install_the_IntelliTrace_Stand_Alone_Collector"></a> Instalar o coletor  
  
1. No servidor do seu aplicativo, crie o diretório do coletor, por exemplo: **C:\IntelliTraceCollector**  
  
2. Obtenha o coletor no Centro de Download da Microsoft na pasta de instalação do Visual Studio 2103 atualização 3. [Coletor IntelliTrace para Visual Studio 2013 atualização 4](https://www.microsoft.com/download/details.aspx?id=44909)::  
  
   - **Centro de Download da Microsoft**:  
  
     1. Lado **IntelliTraceCollector.exe**, escolha **baixar**.  
  
     2. Salvar IntelliTraceCollector.exe ao diretório do coletor, por exemplo: **C:\IntelliTraceCollector**  
  
     3. Execute o IntelliTraceCollector.exe. Isso extrai o arquivo IntelliTraceCollection.cab.  
  
        \- ou -  
  
   - **Pasta de instalação do Visual Studio**:  
  
     1.  Copie o IntelliTraceCollection.cab da pasta a seguir:  
  
          **.. \Microsoft visual Studio 12.0\Common7\IDE\CommonExtensions\Microsoft\IntelliTrace\12.0.0**  
  
     2.  Coloque o intellitracecollection. cab no diretório do coletor, por exemplo: **C:\IntelliTraceCollector**  
  
3. Expanda o IntelliTraceCollection.cab:  
  
   1.  No servidor do aplicativo, abra uma janela de prompt de comando como administrador.  
  
   2.  Navegue até o diretório do coletor, por exemplo: **C:\IntelliTraceCollector**  
  
   3.  Use o **expandir** comando, incluindo o período (**.**) no final, para expandir o intellitracecollection. cab:  
  
        `expand  /f:* IntelliTraceCollection.cab .`  
  
       > [!NOTE]
       >  O período (**.**) preserva as subpastas que contêm planos de coleta localizada.  
  
##  <a name="ConfigurePermissionsRunningCollector"></a> Configurar permissões para o diretório do coletor  
  
1.  No servidor do aplicativo, abra uma janela de prompt de comando como administrador.  
  
2.  Usar o Windows **icacls** comando para conceder permissões completas de administrador para o diretório do coletor de servidor. Por exemplo:  
  
     `icacls "C:\IntelliTraceCollector" /grant "` *\<Amp;lt;1}{2&gt;&lt;domain\administratorid&gt;&lt;2}{3&gt;":f&lt;3 >* `":F`  
  
3.  Para coletar dados de um aplicativo da web ou do SharePoint:  
  
    1.  Conceda permissão total ao diretório do coletor à pessoa que executará os cmdlets do IntelliTrace PowerShell.  
  
         Por exemplo:  
  
         `icacls "C:\IntelliTraceCollector" /grant "` *\<Domínio \ id_do_usuário >* `":F`  
  
    2.  Conceda ao pool de aplicativos para o aplicativo da web ou do SharePoint permissões de leitura e execução para o diretório do coletor.  
  
         Por exemplo:  
  
        -   Para um aplicativo Web na **DefaultAppPool** pool de aplicativos:  
  
             `icacls "C:\IntelliTraceCollector" /grant "IIS APPPOOL\DefaultAppPool":RX`  
  
        -   Para um aplicativo do SharePoint na **SharePoint - 80** pool de aplicativos:  
  
             `icacls "C:\IntelliTraceCollector" /grant "IIS APPPOOL\SharePoint - 80":RX`  
  
##  <a name="BKMK_Set_up_the_IntelliTrace_PowerShell_commandlets"></a> Instalar cmdlets do PowerShell do IntelliTrace para coletar dados para aplicativos Web ou aplicativos do SharePoint  
  
1.  No servidor do aplicativo, certifique-se de que o PowerShell está habilitado. Na maioria das versões do Windows Server, você pode adicionar esse recurso nas **Gerenciador do servidor** ferramenta administrativa.  
  
     ![Adição do PowerShell usando o Gerenciador do servidor](../debugger/media/intellitrace-servermanager-addpowershell.png "INTELLITRACE_ServerManager_AddPowerShell")  
  
2.  Instale os cmdlets do IntelliTrace PowerShell.  
  
    1.  Abra uma janela de comando do PowerShell como administrador.  
  
        1.  Escolher **inicie**, **todos os programas**, **Acessórios**, **Windows PowerShell**.  
  
        2.  Escolha uma das seguintes etapas:  
  
            -   Em sistemas operacionais de 64 bits, abra o menu de atalho **Windows PowerShell**. Escolha **Executar como administrador**.  
  
            -   Em sistemas operacionais de 32 bits, abra o menu de atalho **Windows PowerShell (x86)**. Escolha **Executar como administrador**.  
  
    2.  Na janela de comando do PowerShell, use o **Import-Module** comando para importar **VisualStudio**.  
  
         Por exemplo:  
  
         `Import-Module "C:\IntelliTraceCollector\Microsoft.VisualStudio.IntelliTrace.PowerShell.dll"`  
  
##  <a name="BKMK_Create_and_Configure_a_Log_File_Directory"></a> Configurar permissões para o diretório do arquivo. itrace  
  
1. No servidor do seu aplicativo, crie o diretório do arquivo. itrace, por exemplo: **C:\IntelliTraceLogFiles**  
  
   > [!NOTE]
   > - Para evitar que seu aplicativo fique mais lento, escolha um local em um disco de alta velocidade local que não seja muito ativo.  
   >   -   Você pode colocar os arquivos .iTrace e os coletores no mesmo lugar. No entanto, se você tiver um aplicativo da web ou do SharePoint, verifique se que esse local está fora do diretório que hospeda o aplicativo.  
   > 
   > [!IMPORTANT]
   > - Restrinja o diretório do arquivo .iTrace a apenas as identidades que devem trabalhar com o coletor. Um arquivo .iTrace pode conter informações confidenciais, tais como dados de usuários, bancos de dados, outros locais de origem e cadeias de conexão como IntelliTrace podem registrar quaisquer dados que passem os parâmetros de método ou como valores de retorno.  
   >   -   Certifique-se de aqueles que podem abrir os arquivos .iTrace têm autoridade para ver dados confidenciais. Tenha cuidado ao compartilhar arquivos .iTrace. Se outras pessoas precisarem ter acesso, copie os arquivos para um local compartilhado seguro.  
  
2. Para um aplicativo da web ou do SharePoint, conceda ao seu pool de aplicativos permissões totais para o diretório de arquivos .iTrace. Você pode usar o Windows **icacls** de comando ou use o Windows Explorer (ou Explorador de arquivos).  
  
    Por exemplo:  
  
   - Para configurar as permissões com o Windows **icacls** comando:  
  
     - Para um aplicativo Web na **DefaultAppPool** pool de aplicativos:  
  
        `icacls "C:\IntelliTraceLogFiles" /grant "IIS APPPOOL\DefaultAppPool":F`  
  
     - Para um aplicativo do SharePoint na **SharePoint - 80** pool de aplicativos:  
  
        `icacls "C:\IntelliTraceLogFiles" /grant "IIS APPPOOL\SharePoint - 80":F`  
  
       -ou-  
  
   - Para configurar permissões com o Windows Explorer (ou o Explorador de Arquivos):  
  
     1.  Abra **propriedades** para o diretório do arquivo. itrace.  
  
     2.  Sobre o **segurança** guia, escolha **editar**, **adicionar**.  
  
     3.  Certifique-se **entidades de segurança internas** aparece na **Selecione este tipo de objeto** caixa. Se ele não estiver presente, escolha **tipos de objeto** para adicioná-lo.  
  
     4.  Verifique se o computador local aparece na **desse local** caixa. Se ele não estiver presente, escolha **locais** alterá-la.  
  
     5.  No **insira os nomes de objeto a selecionar** caixa, adicione o pool de aplicativos para o aplicativo Web ou aplicativo do SharePoint.  
  
     6.  Escolher **verificar nomes** para resolver o nome. Escolha **OK**.  
  
     7.  Verifique se o pool de aplicativos tem **controle total**.  
  
##  <a name="BKMK_Collect_Data_from_IIS_Application_Pools"></a> Coletar dados de um aplicativo Web ou aplicativo do SharePoint  
  
1.  Para iniciar a coleta de dados, abra uma janela de comando do PowerShell como administrador e execute este comando:  
  
     `Start-IntelliTraceCollection` `"` *\<ApplicationPool>* `"` *\<PathToCollectionPlan>* *\<FullPathToITraceFileDirectory>*  
  
    > [!IMPORTANT]
    >  Depois de executar esse comando, digite **Y** para confirmar que você deseja iniciar a coleta de dados.  
  
     Por exemplo, para coletar dados de um aplicativo do SharePoint na **SharePoint - 80** pool de aplicativos:  
  
     `Start-IntelliTraceCollection "SharePoint - 80" "C:\IntelliTraceCollector\collection_plan.ASP.NET.default.xml" "C:\IntelliTraceLogFiles"`  
  
    |||  
    |-|-|  
    |*ApplicationPool*|O nome do pool de aplicativos onde o aplicativo é executado|  
    |*PathToCollectionPlan*|O caminho para um plano de coleta, um arquivo.xml que define as configurações para o coletor.<br /><br /> Você pode especificar um plano que vem com o coletor. Os seguintes planos funcionam para aplicativos da web e do SharePoint:<br /><br /> -collection_plan<br />     Coleta apenas eventos IntelliTrace do SharePoint, incluindo exceções, chamadas de banco de dados e solicitações no servidor da web.<br />-collection_plan.ASP.NET.trace.xml<br />     Coleta chamadas de função e todos os dados no collection_plan.ASP.NET.default.xml. Esse plano é útil para uma análise detalhada, mas pode causar lentidão no seu aplicativo mais do que no collection_plan.ASP.NET.default.xml.<br /><br /> Para evitar causar lentidão no seu aplicativo, personalize esses planos ou crie seu próprio plano. Por segurança, coloque planos personalizados no mesmo local seguro que os arquivos do coletor. Ver [criando e personalizando planos de coleta do IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=227871) e [como obter a maioria dos dados sem afetar a velocidade do meu aplicativo?](#Minimizing) **Observação:** por padrão, o tamanho máximo do arquivo. itrace é 100 MB. Quando o arquivo .iTrace atingir esse limite, o coletor exclui as entradas de mais antigas do arquivo para dar espaço às entradas mais recentes. Para alterar esse limite, edite o atributo `MaximumLogFileSize` do plano de coleta. <br /><br /> *Onde posso encontrar versões localizadas desses planos de coleção?*<br /><br /> Você pode encontrar planos localizados nas subpastas do coletor.|  
    |*FullPathToITraceFileDirectory*|O caminho completo para o diretório de arquivos .iTrace. **Observação de segurança:** forneça o caminho completo, não um caminho relativo.|  
  
     O coletor anexa-se ao pool de aplicativos e inicia a coleta de dados.  
  
     *Pode abrir o arquivo. itrace neste momento?* Não, o arquivo está bloqueado durante a coleta de dados.  
  
2.  Reproduza o problema.  
  
3.  Para obter um instantâneo do arquivo .iTrace, use a seguinte sintaxe:  
  
     `Checkpoint-IntelliTraceCollection` `"` *\<ApplicationPool>* `"`  
  
4.  Para verificar o status da coleta, use a seguinte sintaxe:  
  
     `Get-IntelliTraceCollectionStatus`  
  
5.  Para interromper a coleta de dados, use a seguinte sintaxe:  
  
     `Stop-IntelliTraceCollection` `"` *\<ApplicationPool>* `"`  
  
    > [!IMPORTANT]
    >  Depois de executar esse comando, digite **Y** para confirmar que você deseja interromper a coleta de dados. Caso contrário, o coletor podem continuar com a coleta de dados, o arquivo iTrace permanecerá bloqueado ou o arquivo pode não conter dados úteis.  
  
6.  [Abra o arquivo. itrace no Visual Studio Enterprise](#BKMK_View_IntelliTrace_Log_Files)  
  
##  <a name="BKMK_Collect_Data_from_Executables"></a> Coletar dados de um aplicativo gerenciado  
  
1.  Para iniciar o aplicativo e coletar dados ao mesmo tempo, use a seguinte sintaxe:  
  
     *\<FullPathToIntelliTraceCollectorExecutable>* `\IntelliTraceSC.exe launch /cp:` *\<PathToCollectionPlan>* `/f:` *\<FullPathToITraceFileDirectoryAndFileName>* *\<PathToAppExecutableFileAndFileName>*  
  
     Por exemplo, para coletar dados de um aplicativo chamado **MyApp**:  
  
     `C:IntelliTraceCollectorIntelliTraceSC.exe launch /cp:"C:IntelliTraceCollectorcollection_plan.ASP.NET.default.xml" /f:"C:IntelliTraceLogFilesMyApp.itrace" "C:MyAppMyApp.exe"`  
  
    |||  
    |-|-|  
    |*FullPathToIntelliTraceCollectorExecutable*|O caminho completo para o coletor executável, IntelliTraceSC.exe|  
    |*PathToCollectionPlan*|O caminho para um plano de coleta, um arquivo.xml que define as configurações para o coletor.<br /><br /> Você pode especificar um plano que vem com o coletor. Os seguintes planos funcionam para aplicativos gerenciados:<br /><br /> -collection_plan<br />     Coleta somente eventos do IntelliTrace, incluindo exceções, chamadas de banco de dados e solicitações no servidor da web.<br />-collection_plan.ASP.NET.trace.xml<br />     Coleta chamadas de função e todos os dados no collection_plan.ASP.NET.default.xml. Esse plano é útil para uma análise detalhada, mas pode causar lentidão no seu aplicativo mais do que no collection_plan.ASP.NET.default.xml.<br /><br /> Para evitar causar lentidão no seu aplicativo, personalize esses planos ou crie seu próprio plano. Por segurança, coloque planos personalizados no mesmo local seguro que os arquivos do coletor. Ver [criando e personalizando planos de coleta do IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=227871) e [como obter a maioria dos dados sem afetar a velocidade do meu aplicativo?](#Minimizing) **Observação:** por padrão, o tamanho máximo do arquivo. itrace é 100 MB. Quando o arquivo .iTrace atingir esse limite, o coletor exclui as entradas de mais antigas do arquivo para dar espaço às entradas mais recentes. Para alterar esse limite, edite o atributo `MaximumLogFileSize` do plano de coleta. <br /><br /> *Onde posso encontrar versões localizadas desses planos de coleção?*<br /><br /> Você pode encontrar planos localizados nas subpastas do coletor.|  
    |*FullPathToITraceFileDirectoryAndFileName*|O caminho completo para o diretório do arquivo. itrace e o nome do arquivo. itrace com a **. itrace** extensão. **Observação de segurança:** forneça o caminho completo, não um caminho relativo.|  
    |*PathToAppExecutableFileAndFileName*|O caminho e o nome de arquivo do seu aplicativo gerenciado|  
  
2.  Interrompa a coleta de dados saindo do aplicativo.  
  
3.  [Abra o arquivo. itrace no Visual Studio Enterprise](#BKMK_View_IntelliTrace_Log_Files)  
  
##  <a name="BKMK_View_IntelliTrace_Log_Files"></a> Abra o arquivo. itrace no Visual Studio Enterprise  
  
> [!NOTE]
>  Para depurar com o IntelliTrace e percorrer o código, você deve ter os arquivos de origem e de símbolo correspondentes. Ver [diagnosticar problemas após a implantação](../debugger/diagnose-problems-after-deployment.md).  
  
1.  Mover o arquivo. itrace ou copie-o para um computador com Visual Studio Enterprise (mas as edições não Professional ou Community).  
  
2.  Clique duas vezes no arquivo .iTrace fora do Visual Studio ou abra o arquivo de dentro do Visual Studio.  
  
     O Visual Studio mostra a **resumo do IntelliTrace** página. Na maioria das seções, você pode examinar eventos ou outros itens, escolher um item e iniciar a depuração com o IntelliTrace no ponto onde e quando um evento que ocorreu. Ver [usando dados salvo do IntelliTrace](../debugger/using-saved-intellitrace-data.md).  
  
    > [!NOTE]
    >  Para depurar com o IntelliTrace e percorrer o código, você deve ter os arquivos de origem e de símbolo correspondentes no seu computador de desenvolvimento. Ver [diagnosticar problemas após a implantação](../debugger/diagnose-problems-after-deployment.md).  
  
##  <a name="Minimizing"></a> Como posso obter a maioria dos dados sem afetar a velocidade do meu aplicativo?  
 O IntelliTrace pode coletar grandes quantidades de dados, por isso o impacto no desempenho do aplicativo depende dos dados que o IntelliTrace coleta e do tipo de código analisado. Ver [otimizando a coleção de IntelliTrace em servidores de produção](http://go.microsoft.com/fwlink/?LinkId=255233).  
  
 Estas são algumas das maneiras de obter a maioria dos dados sem deixar seu aplicativo mais lento:  
  
- Execute o coletor somente quando você achar que há um problema ou quando você puder reproduzir o problema.  
  
   Inicie a coleta, reproduza o problema e, em seguida, pare a coleta. Abra o arquivo. itrace no Visual Studio Enterprise e examinar os dados. Ver [abrir o arquivo. itrace no Visual Studio Enterprise](#BKMK_View_IntelliTrace_Log_Files).  
  
- Para aplicativos da web e do SharePoint, o coletor grava os dados de todos os aplicativos que compartilham o pool de aplicativos especificado. Isso talvez deixe mais lento qualquer aplicativo que compartilhe o mesmo pool de aplicativos, mesmo que você possa especificar módulos para um único aplicativo no plano de coleta.  
  
   Para evitar que o coletor deixe outros aplicativos mais lentos, hospede cada aplicativo em seu próprio pool de aplicativos.  
  
- Revise os eventos no plano de coleta para o qual o IntelliTrace coleta os dados. Edite o plano de coleta para desabilitar eventos que não sejam relevantes ou que não sejam de seu interesse.  
  
   Para desabilitar um evento, defina o atributo `enabled` para o elemento `<DiagnosticEventSpecification>` como `false`:  
  
   `<DiagnosticEventSpecification enabled="false">`  
  
   Se o atributo `enabled` não existir, o evento estará habilitado.  
  
   *Como isso melhora o desempenho?*  
  
  -   Você pode reduzir o tempo de inicialização desabilitando eventos que não são relevantes para o aplicativo. Por exemplo, desabilite eventos do Fluxo de Trabalho do Windows para aplicativos que não usam o Fluxo de Trabalho do Windows.  
  
  -   Você pode melhorar o desempenho de inicialização e do tempo de execução desabilitando eventos do registro para aplicativos que acessam o registro, mas não apresentam problemas com as configurações do registro.  
  
- Revise os módulos no plano de coleta para o qual o IntelliTrace coleta os dados. Edite o plano de coleta para incluir somente os módulos de seu interesse:  
  
  1. Abra o plano de coleta. Encontre o elemento `<ModuleList>`.  
  
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
  
- *Há todos os dados que IntelliTrace não coleta?*  
  
   Sim, para reduzir o impacto no desempenho, o IntelliTrace restringe a coleta de dados aos valores de tipos de dados primitivos passado e retornados de métodos e a valores de tipos de dados primitivos nos campos em objetos de nível superior passado e retornados dos métodos.  
  
   Por exemplo, suponhamos que você tenha uma assinatura de método `AlterEmployee` que aceite um inteiro `id` e um objeto `Employee``oldemployee`:  
  
   `public Employee AlterEmployee(int id, Employee oldemployee)`  
  
   O tipo `Employee` tem os seguintes atributos: `Id`, `Name` e `HomeAddress`. Existe uma relação de associação entre `Employee` e o tipo `Address`.  
  
   ![Relação entre o funcionário e o endereço](../debugger/media/employeeaddressrelationship.png "EmployeeAddressRelationship")  
  
   O coletor registra valores de `id`, `Employee.Id`, `Employee.Name` e o objeto `Employee` retornado pelo método `AlterEmployee`. Entretanto, o coletor não registra informações sobre o objeto `Address`, exceto se ele era nulo ou não. O coletor também não registra dados sobre variáveis locais no método `AlterEmployee`, a menos que outros métodos usem essas variáveis locais como parâmetros em que eles são gravados como parâmetros de método.  
  
##  <a name="WhereElse"></a> Onde mais posso obter dados do IntelliTrace?  
  
-   De uma sessão no Visual Studio Enterprise de depuração do IntelliTrace, consulte [recursos do IntelliTrace](../debugger/intellitrace-features.md).  
  
-   Em uma sessão de teste no Microsoft Test Manager, consulte [como: coletar dados do IntelliTrace para ajudar a depurar problemas difíceis](~/E:/Repos/visualstudio-docs-pr/docs/test/how-to-collect-intellitrace-data-to-help-debug-difficult-issues.md).  
  
## <a name="where-can-i-get-more-information"></a>Onde posso obter mais informações?  
 [Usando dados salvos do IntelliTrace](../debugger/using-saved-intellitrace-data.md)  
  
 [IntelliTrace](../debugger/intellitrace.md)  
  
### <a name="blogs"></a>Blogs  
 [Usando o coletor autônomo IntelliTrace remotamente](http://go.microsoft.com/fwlink/?LinkId=262277)  
  
 [Criando e personalizando planos de coleta do IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=227871)  
  
 [Otimizando a coleção de IntelliTrace em servidores de produção](http://go.microsoft.com/fwlink/?LinkId=255233)  
  
 [Visual Studio ALM + Blog do TFS](http://go.microsoft.com/fwlink/?LinkID=201340)  
  
### <a name="forums"></a>Fóruns  
 [Depurador do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=262263)  
  
### <a name="videos"></a>Vídeos  
 [Vídeo do Channel 9: coletando e analisando dados IntelliTrace](http://go.microsoft.com/fwlink/?LinkID=251851)





