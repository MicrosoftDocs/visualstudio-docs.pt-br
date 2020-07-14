---
title: Usando o Microsoft Monitoring Agent | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: fd0a86b9-015d-408e-aa58-59a0a97826ac
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f3f70d3799bfae96b15c13a42c3c11246d1e89ba
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520569"
---
# <a name="using-the-microsoft-monitoring-agent"></a>Usando o Microsoft Monitoring Agent
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente sobre o Visual Studio, consulte [usando o Microsoft Monitoring Agent](/visualstudio/debugger/using-the-microsoft-monitoring-agent).

Você pode monitorar localmente aplicativos Web do ASP.NET hospedados no IIS e os aplicativos do SharePoint 2010 ou 2013 em busca de erros, problemas de desempenho ou outros problemas usando o **Microsoft Monitoring Agent**. Você pode salvar eventos de diagnóstico do agente em um arquivo de log do IntelliTrace (.iTrace). Em seguida, você pode abrir o arquivo de log em Visual Studio Enterprise (mas não em edições Professional ou Community) para depurar problemas com todas as ferramentas de diagnóstico do Visual Studio. Você também pode coletar dados de diagnóstico do IntelliTrace e dados de método executando o agente em modo **Rastrear**. Microsoft Monitoring Agent pode ser integrado com o [Application insights](/azure/azure-monitor/app/app-insights-overview) e o [System Center Operations Manager](https://technet.microsoft.com/library/hh205987.aspx). O Microsoft Monitoring Agent altera o ambiente do sistema de destino quando instalado.  
  
> [!NOTE]
> Você também pode coletar dados de diagnóstico e método do IntelliTrace para aplicativos Web, SharePoint, WPF e Windows Form em computadores remotos sem alterar o ambiente de destino usando o **coletor autônomo do IntelliTrace**. O coletor autônomo tem um impacto de desempenho maior do que quando executar o Microsoft Monitoring Agent no modo **Monitorar**. Consulte [usando o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md).  
  
 Se você usar o System Center 2012, use o Microsoft Monitoring Agent com Operations Manager para obter alertas sobre problemas e criar itens de trabalho do Team Foundation Server com links para os logs do IntelliTrace salvos. Você pode atribuir esses itens de trabalho a outros para uma depuração adicional. Confira [Integrando o Operations Manager aos processos de desenvolvimento](https://technet.microsoft.com/library/jj614609.aspx) e [Monitorando com Microsoft Monitoring Agent](https://technet.microsoft.com/library/dn465153.aspx).  
  
 Antes de começar, verifique se você tem a origem e os símbolos correspondentes para o código compilado e implantado. Isso ajuda você a ir diretamente até o código do aplicativo ao iniciar a depuração e a navegação em eventos de diagnóstico no log do IntelliTrace. [Configure os builds](../debugger/diagnose-problems-after-deployment.md) de modo que o Visual Studio possa encontrar e abrir automaticamente a origem correspondente ao código implantado.  
  
1. [Etapa 1: configurar Microsoft Monitoring Agent](#SetUpMonitoring)  
  
2. [Etapa 2: Iniciar o monitoramento do aplicativo](#MonitorEvents)  
  
3. [Etapa 3: salvar eventos gravados](#SaveEvents)  
  
## <a name="step-1-set-up-microsoft-monitoring-agent"></a><a name="SetUpMonitoring"></a> Etapa 1: Configurar o Microsoft Monitoring Agent  
 Configure o agente autônomo no servidor Web para realizar o monitoramento local sem alterar seu aplicativo. Se você usar o System Center 2012, confira [Instalando o Microsoft Monitoring Agent](https://technet.microsoft.com/library/dn465156.aspx).  
  
### <a name="set-up-the-standalone-agent"></a><a name="SetUpStandaloneMMA"></a> Configurar o agente autônomo  
  
1. Certifique-se de que:  
  
    - O servidor Web está executando [versões compatíveis do IIS (Serviços de Informações da Internet)](https://technet.microsoft.com/library/dn465154.aspx).  
  
    - Seu servidor Web tem o .NET Framework 3.5, 4 ou 4.5.  
  
    - O servidor Web está executando o Windows PowerShell 3.0 ou posterior. [P: e se eu tiver o Windows PowerShell 2,0?](#PowerShell2)  
  
    - Você tem permissões de administrador em seu servidor Web para executar comandos do PowerShell e reciclar o pool do aplicativos ao iniciar o monitoramento.  
  
    - Você desinstalou alguma versão anterior do Microsoft Monitoring Agent.  
  
2. [Baixe o Microsoft Monitoring Agent gratuitamente](https://go.microsoft.com/fwlink/?LinkID=309771), na versão 32 bits **MMASetup-i386.exe** ou na versão 64 bits **MMASetup-AMD64.exe**, do Centro de Download da Microsoft para o servidor Web.  
  
3. Execute o executável baixado para iniciar o assistente de instalação.  
  
4. Crie um diretório seguro em seu servidor Web para armazenar os logs do IntelliTrace, por exemplo, **C:\IntelliTraceLogs**.  
  
     Não se esqueça de criar esse diretório antes de começar o monitoramento. Para evitar que seu aplicativo fique mais lento, escolha um local em um disco de alta velocidade local que não seja muito ativo.  
  
    > [!IMPORTANT]
    > Os logs do IntelliTrace podem conter dados pessoais e confidenciais. Restrinja esse diretório a apenas essas identidades que devam funcionar com os arquivos. Verifique as políticas de privacidade da empresa.  
  
5. Para executar ou monitorar aplicativos do SharePoint de monitoramento detalhados, no nível da função, dê ao pool de aplicativos que hospeda o aplicativo Web ou o aplicativo do SharePoint permissões de leitura e gravação para o diretório do log do IntelliTrace. [P: Como fazer configurar permissões para o pool de aplicativos?](#FullPermissionsITLog)  
  
### <a name="q--a"></a>Perguntas e respostas  
  
#### <a name="q-what-if-i-have-windows-powershell-20"></a><a name="PowerShell2"></a>P: E se eu tiver o Windows PowerShell 2.0?  
 **R** É altamente recomendável usar o PowerShell 3.0. Do contrário, você precisará importar os cmdlets do Microsoft Monitoring Agent PowerShell sempre que executar o PowerShell. Você também não terá acesso ao conteúdo baixável da Ajuda.  
  
1. Abra uma janela de prompt de comando do **Windows PowerShell** ou do **ISE do Windows PowerShell** como administrador.  
  
2. Importe o módulo Microsoft Monitoring Agent PowerShell do local de instalação padrão:  
  
     **PS C:>Import-Module "C:\Arquivos de Programas\Microsoft Monitoring Agent\Agent\PowerShell\Microsoft.MonitoringAgent.PowerShell\Microsoft.MonitoringAgent.PowerShell.dll"**  
  
3. [Visite o TechNet](https://technet.microsoft.com/systemcenter/default) para obter o conteúdo mais recente da Ajuda.  
  
#### <a name="q-how-do-i-set-up-permissions-for-the-application-pool"></a><a name="FullPermissionsITLog"></a>P: Como configuro permissões para o pool de aplicativos?  
 **R:** Use o comando **icacls** do Windows ou use o Windows Explorer (ou explorador de arquivos). Por exemplo:  
  
- Para configurar permissões com o comando **icacls** do Windows:  
  
  - Para um aplicativo Web no pool de aplicativos **DefaultAppPool**:  
  
     `icacls "C:\IntelliTraceLogs" /grant "IIS APPPOOL\DefaultAppPool":RX`  
  
  - Para um aplicativo do SharePoint no pool de aplicativos **SharePoint - 80**:  
  
     `icacls "C:\IntelliTraceLogs" /grant "IIS APPPOOL\SharePoint - 80":RX`  
  
    -ou-  
  
- Para configurar permissões com o Windows Explorer (ou o Explorador de Arquivos):  
  
  1. Abra **Propriedades** do diretório do log do IntelliTrace.  
  
  2. Na guia **Segurança**, escolha **Editar**, **Adicionar**.  
  
  3. Verifique se **Entidades de segurança interna** é exibido na caixa **Selecione este tipo de objeto**. Se não estiver lá, escolha **tipos de objeto** para adicioná-lo.  
  
  4. Verifique se o computador local é exibido na caixa **Deste local**. Se não estiver lá, escolha os **locais** para alterá-lo.  
  
  5. Na caixa **Inserir os nomes de objeto a serem selecionados** , adicione o pool de aplicativos para o aplicativo Web ou para o SharePoint.  
  
  6. Escolha **Verificar Nomes** para resolver o nome. Selecione **OK**.  
  
  7. Verifique se o pool de aplicativos tem permissões de **Leitura e execução**.  
  
## <a name="step-2-start-monitoring-your-app"></a><a name="MonitorEvents"></a>Etapa 2: iniciar o monitoramento de seu aplicativo  
 Use o comando [Start-WebApplicationMonitoring](https://technet.microsoft.com/library/dn472749(v=sc.20).aspx) do Windows PowerShell para iniciar o monitoramento do aplicativo. Se você usar o System Center 2012, confira [Monitorando aplicativos Web com o Microsoft Monitoring Agent](https://technet.microsoft.com/library/dn465157.aspx).  
  
1. No servidor Web, abra uma janela de prompt de comando do **Windows PowerShell** ou do **ISE do Windows PowerShell** como administrador.  
  
     ![Abrir o Windows PowerShell como administrador](../debugger/media/ffr-powershellrunadmin.png "FFR_PowerShellRunAdmin")  
  
2. Execute o comando [Start-WebApplicationMonitoring](https://technet.microsoft.com/library/dn472749(v=sc.20).aspx) para iniciar o monitoramento do aplicativo. Isso reiniciará todos os aplicativos Web no servidor Web.  
  
     Aqui está a sintaxe abreviada:  
  
     **Start-WebApplicationMonitoring** *" \<appName> "* "" " *\<monitoringMode>* * \<outputPath> * " *\<UInt32>* * \<collectionPlanPathAndFileName> *  
  
     Aqui está um exemplo que usa apenas o nome do aplicativo Web e o modo de **Monitor** leve:  
  
     **PS C: >Start-WebApplicationMonitoring "FabrikamFabrikamFiber. Web" Monitor "C:IntelliTraceLogs"**  
  
     Veja um exemplo que usa o caminho do IIS e o modo de **Monitor** leve:  
  
     **PS C:>Start-WebApplicationMonitoring "IIS:sitesFabrikamFabrikamFiber.Web" Monitor "C:IntelliTraceLogs"**  
  
     Depois de iniciar o monitoramento, você poderá ver o Microsoft Monitoring Agent pausar enquanto seus aplicativos são reiniciados.  
  
     ![Iniciar monitoramento com a confirmação do MMA](../debugger/media/ffr-powershellstartmonitoringconfirmation.png "FFR_PowerShellStartMonitoringConfirmation")  
  
    |Item|Descrição|  
    |-|-|  
    |*"\<appName>"*|Especifique o caminho para o site e o nome do aplicativo Web no IIS. Você também poderá incluir o caminho do IIS, se preferir.<br /><br /> *" \<IISWebsiteName> \\<IISWebAppName \> "*<br /><br /> -ou-<br /><br /> **"IIS: \ sites** * \\<IISWebsiteName \> \\<IISWebAppName \> "*<br /><br /> Você pode encontrar esse caminho no Gerenciador do IIS. Por exemplo:<br /><br /> ![Caminho para o site do IIS e para o aplicativo Web](../debugger/media/ffr-iismanager.png "FFR_IISManager")<br /><br /> Você também pode usar os comandos [Get-WebSite](https://technet.microsoft.com/library/ee807832.aspx) e [Get WebApplication](https://technet.microsoft.com/library/ee790554.aspx).|  
    |*\<monitoringMode>*|Especifique o modo de monitoramento:<br /><br /> <ul><li>**Monitor**: Registre os detalhes mínimos sobre eventos de exceção e eventos de desempenho. Esse modo usa o plano de coleta padrão.</li><li>**Rastreamento**: registre detalhes no nível da função ou monitore aplicativos do SharePoint 2010 e do SharePoint 2013, usando o plano de coleta especificado. Esse modo pode fazer o aplicativo ser executado mais lentamente.<br /><br /> <ul><li>[P: Como fazer configurar permissões para o pool de aplicativos?](#FullPermissionsITLog)</li><li>[P: Como fazer obter a maioria dos dados sem atrasar o aplicativo?](#Minimizing)</li></ul><br />     Esse exemplo registra eventos de um aplicativo do SharePoint hospedado em um site do SharePoint:<br /><br />     **Start-WebApplicationMonitoring "FabrikamSharePointSite\FabrikamSharePointApp" Trace "C:\Arquivos de Programas\microsoft Monitoring Agent\Agent\IntelliTraceCollector\collection_plan.ASP.NET.default.xml" "C:\IntelliTraceLogs"**</li><li>**Personalizado**: Registre detalhes personalizados usando o plano de coleta personalizado especificado. Você precisará reiniciar o monitoramento se editar o plano de coleta depois que o monitoramento já tiver começado.</li></ul>|  
    |*"\<outputPath>"*|Especifique o caminho do diretório completo para armazenar os logs do IntelliTrace. Não se esqueça de criar esse diretório antes de começar o monitoramento.|  
    |*\<UInt32>*|Especifique o tamanho máximo para o log do IntelliTrace. O tamanho máximo padrão do log do IntelliTrace é de 250 MB.<br /><br /> Quando o log atinge esse limite, o agent substitui as entradas mais antigas para liberar espaço para mais entradas. Para alterar esse limite, use a opção **-MaximumFileSizeInMegabytes** ou edite o `MaximumLogFileSize` atributo no plano de coleta.|  
    |*"\<collectionPlanPathAndFileName>"*|Especifique o caminho completo ou relativo e o nome de arquivo do plano de coleta. Esse plano é um arquivo .xml que define configurações do agente.<br /><br /> Esses planos são incluídos no agente e funcionam com aplicativos Web e aplicativos do SharePoint:<br /><br /> -   **collection_plan.ASP.NET.default.xml**<br />     Coleta apenas eventos, como exceções, eventos de desempenho, chamadas de banco de dados e solicitações do servidor Web.<br />-   **collection_plan.ASP.NET.trace.xml**<br />     Coleta chamadas no nível da função, mais todos os dados no plano de coleta padrão. Esse plano é bom para análise detalhada, mas pode deixar seu aplicativo mais lento.<br /><br /> Você pode encontrar versões localizadas desses planos nas subpastas do agente. Você também pode [personalizar esses planos ou criar planos próprios](https://devblogs.microsoft.com/devops/modifying-an-intellitrace-collection-plan-for-the-stand-alone-collector/) para evitar que seu aplicativo fique lento. Coloque todos os planos personalizados no mesmo local seguro do agente.<br /><br /> [P: Como fazer obter a maioria dos dados sem atrasar o aplicativo?](#Minimizing)|  
  
     Para obter mais informações sobre a sintaxe completa e outros exemplos, execute o comando **Get-Help Start-WebApplicationMonitoring – detailed** ou o comando **Get-Help Start-WebApplicationMonitoring – examples** .  
  
3. Para verificar o status de todos os aplicativos Web monitorados, execute o comando [Get-WebApplicationMonitoringStatus](https://technet.microsoft.com/library/dn472751(v=sc.20).aspx).  
  
### <a name="q--a"></a>Perguntas e respostas  
  
#### <a name="q-how-do-i-get-the-most-data-without-slowing-down-my-app"></a><a name="Minimizing"></a> P: Como obtenho o máximo de dados sem deixar meu aplicativo mais lento?  
 **R:** O Microsoft Monitoring Agent pode coletar lotes de dados e afeta o desempenho de seu aplicativo, dependendo dos dados escolhidos para coletar e como você os coleta. Estas são algumas das maneiras de obter a maioria dos dados sem deixar seu aplicativo mais lento:  
  
- Para aplicativos Web e aplicativos do SharePoint, o agente grava os dados de todos os aplicativos que compartilham o pool de aplicativos especificado. Isso talvez deixe mais lento qualquer aplicativo que compartilhe o mesmo pool de aplicativos, mesmo que você possa restringir a coleta aos módulos de um único aplicativo. Para evitar que outros aplicativos fiquem mais lentos, hospede cada aplicativo em seu próprio pool de aplicativos.  
  
- Examine os eventos para os quais o agente coleta dados no plano de coleta. Edite o plano de coleta para desabilitar eventos que não sejam relevantes ou que não sejam de seu interesse. Isso pode melhorar o desempenho da inicialização e o desempenho do runtime.  
  
   Para desabilitar um evento, defina o atributo `enabled` para o elemento `<DiagnosticEventSpecification>` como `false`:  
  
   `<DiagnosticEventSpecification enabled="false">`  
  
   Se o atributo `enabled` não existir, o evento estará habilitado.  
  
   Por exemplo:  
  
  - Desabilite eventos do Fluxo de Trabalho do Windows para aplicativos que não usem o Fluxo de Trabalho do Windows.  
  
  - Desabilite eventos do Registro para aplicativos que acessem o Registro, mas não mostrem problemas com configurações do Registro.  
  
- Examine os módulos para os quais o agente coleta dados no plano de coleta. Edite o plano de coleta para incluir somente os módulos de seu interesse.  
  
   Isso reduz a quantidade de informações de chamada de método e outros dados de instrumentação que o agente coleta quando o aplicativo é iniciado e executado. Esses dados ajudam a navegar pelo código quando você está depurando e examinando os valores passados para e retornados de chamadas de função.  
  
  1. Abra o plano de coleta. Localize o elemento `<ModuleList>`.  
  
  2. Em `<ModuleList>`, defina o atributo `isExclusionList` como `false`.  
  
  3. Use o elemento `<Name>` para especificar cada módulo com um dos seguintes: nome do arquivo, valor da cadeia de caracteres para incluir qualquer módulo cujo nome contenha essa cadeia de caracteres ou chave pública.  
  
     Esse exemplo cria uma lista que coleta dados apenas do módulo principal do aplicativo Web Fabrikam Fiber:  
  
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
  
   **P: Por que não excluir apenas os módulos em seu lugar?**  
  
   **R:** Por padrão, os planos de coleta excluem módulos, definindo o atributo `isExclusionList` como `true`. Entretanto, ele ainda pode coletar dados de módulos que não atendam aos critérios da lista ou que talvez não o interesse, como módulos de terceiros ou de software livre.  
  
#### <a name="q-what-values-does-the-agent-collect"></a>P: Quais valores o agente coleta?  
 **R:** Para reduzir o impacto sobre o desempenho, o agente coleta apenas estes valores:  
  
- Tipos de dados primitivos passados e retornados de métodos  
  
- Tipos de dados primitivos em campos para objetos no nível superior passados e retornados de métodos  
  
  Por exemplo, suponhamos que você tenha uma assinatura de método `AlterEmployee` que aceite um inteiro `id` e um objeto `Employee``oldemployee`:  
  
  `public Employee AlterEmployee(int id, Employee oldemployee)`  
  
  O tipo `Employee` tem os seguintes atributos: `Id`, `Name` e `HomeAddress`. Existe uma relação de associação entre `Employee` e o tipo `Address`.  
  
  ![Relação entre o funcionário e o endereço](../debugger/media/employeeaddressrelationship.png "EmployeeAddressRelationship")  
  
  O agente registra valores de `id`, `Employee.Id`, `Employee.Name` e o objeto `Employee` retornado pelo método `AlterEmployee`. Entretanto, o agente não registra informações sobre o objeto `Address` que não sejam se ele era nulo ou não. O agente também não registra dados sobre variáveis locais no método `AlterEmployee`, a menos que outros métodos usem essas variáveis locais como parâmetros em que eles são gravados como parâmetros de método.  
  
## <a name="step-3-save-recorded-events"></a><a name="SaveEvents"></a>Etapa 3: Salvar eventos registrados  
 Quando você encontrar um erro ou um problema de desempenho, salve os eventos registrados em um log do IntelliTrace. O agente só criará o log se tiver registrado eventos. Se você usar o System Center 2012, confira [Monitorando aplicativos Web com o Microsoft Monitoring Agent](https://technet.microsoft.com/library/dn465157.aspx).  
  
### <a name="save-recorded-events-but-continue-monitoring"></a>Salvar eventos registrados, mas continuar monitorando  
 Siga estas etapas quando você quiser criar o log do IntelliTrace, mas não quiser reiniciar o aplicativo ou parar de monitorá-lo. O agente continua o monitoramento, mesmo que o servidor ou o aplicativo seja reiniciado.  
  
1. No servidor Web, abra uma janela do prompt de comando do Windows PowerShell como administrador.  
  
2. Execute o comando [Checkpoint-WebApplicationMonitoring](https://technet.microsoft.com/library/dn472750(v=sc.20).aspx) para salvar um instantâneo do log do IntelliTrace:  
  
    **Checkpoint-WebApplicationMonitoring** *" \<IISWebsiteName> \\<IISWebAppName \> "*  
  
    \- ou –  
  
    **Checkpoint-WebApplicationMonitoring "IIS: \ sites** * \\<IISWebsiteName \> \\<IISWebAppName \> "*  
  
    Por exemplo:  
  
    **PS C: \\>Checkpoint-WebApplicationMonitoring "Fabrikam\FabrikamFiber.Web"**  
  
    -ou-  
  
    **PS C: >Checkpoint-WebApplicationMonitoring "IIS: sitesFabrikamFabrikamFiber. Web"**  
  
    Para obter mais informações, execute o comando **Get-Help Checkpoint-WebApplicationMonitoring – detailed** ou o comando **Get-Help Checkpoint-WebApplicationMonitoring – examples** .  
  
3. Copie o log para uma pasta compartilhada segura e, em seguida, abra o log de um computador que tenha Visual Studio Enterprise (mas não com as edições Professional ou Community).  
  
   > [!IMPORTANT]
   > Tome cuidado ao compartilhar logs do IntelliTrace, porque eles podem conter dados pessoais e confidenciais. Verifique se a pessoa que pode acessar esses logs tem permissões para analisar esses dados. Verifique as políticas de privacidade da empresa.  
  
   **Em seguida:** [diagnosticar eventos registrados no Visual Studio Enterprise](../debugger/diagnose-problems-after-deployment.md#InvestigateEvents)  
  
### <a name="save-recorded-events-and-stop-monitoring"></a>Salvar eventos registrados e parar o monitoramento  
 Siga estas etapas quando quiser somente informações de diagnóstico durante a reprodução de um problema específico. Isso reiniciará todos os aplicativos Web no servidor Web.  
  
1. No servidor Web, abra uma janela do prompt de comando do Windows PowerShell como administrador.  
  
2. Execute o comando [Stop-WebApplicationMonitoring](https://technet.microsoft.com/library/dn472753(v=sc.20).aspx) para criar o log do IntelliTrace e pare o monitoramento de um aplicativo Web específico:  
  
    **Stop-WebApplicationMonitoring** *" \<IISWebsiteName> \\<IISWebAppName \> "*  
  
    \- ou –  
  
    **Stop-WebApplicationMonitoring "IIS: \ sites** * \\<IISWebsiteName \> \\<IISWebAppName \> "*  
  
    Ou pare o monitoramento de todos os aplicativos Web:  
  
    **Stop-WebApplicationMonitoring-All**  
  
    Por exemplo:  
  
    **PS C: \\>Stop-WebApplicationMonitoring "Fabrikam\iFabrikamFiber.Web"**  
  
    \- ou –  
  
    **PS C:\\>Stop-WebApplicationMonitoring "IIS:\sites\Fabrikam\FabrikamFiber.Web"**  
  
    Para obter mais informações, execute o comando **Get-Help Stop-WebApplicationMonitoring – detailed** ou o comando **Get-Help Stop-WebApplicationMonitoring – examples** .  
  
3. Copie o log para uma pasta compartilhada segura e, em seguida, abra o log de um computador que tenha Visual Studio Enterprise.  
  
   **Em seguida:** [diagnosticar eventos registrados no Visual Studio Enterprise](../debugger/diagnose-problems-after-deployment.md#InvestigateEvents)  
  
## <a name="q--a"></a>Perguntas e respostas  
  
### <a name="q-where-can-i-get-more-information"></a>P: Onde posso obter mais informações?  
  
#### <a name="blogs"></a>Blogs  
 [Apresentando o Microsoft Monitoring Agent](https://devblogs.microsoft.com/devops/introducing-microsoft-monitoring-agent-2/)  
  
 [Como otimizar a coleta do IntelliTrace em servidores de produção](https://devblogs.microsoft.com/devops/optimizing-intellitrace-collection-on-production-server/)  
  
#### <a name="forums"></a>Fóruns  
 [Diagnóstico do Visual Studio](https://social.msdn.microsoft.com/Forums/vsdebug)
