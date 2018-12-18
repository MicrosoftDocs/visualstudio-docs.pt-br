---
title: Usando o Microsoft Monitoring Agent | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: fd0a86b9-015d-408e-aa58-59a0a97826ac
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3146de7efb7db567149b7741f2868a932f8476ac
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49842060"
---
# <a name="using-the-microsoft-monitoring-agent"></a>Usando o Microsoft Monitoring Agent
Você pode monitorar localmente aplicativos web do ASP.NET hospedados no IIS e o SharePoint 2010 ou 2013 aplicativos de erros, problemas de desempenho ou outros problemas usando **Microsoft Monitoring Agent**. Você pode salvar eventos de diagnóstico do agente em um arquivo de log do IntelliTrace (.iTrace). Em seguida, você pode abrir o log no Visual Studio Enterprise (mas não as edições Professional ou Community) para depurar problemas com todas as ferramentas de diagnóstico do Visual Studio. Você também pode coletar dados de diagnóstico do IntelliTrace e dados de método executando o agente **rastreamento** modo. Microsoft Monitoring Agent podem ser integrado [Application Insights](/azure/application-insights/) e [System Center Operation Manager](/previous-versions/system-center/system-center-2012-R2/hh205987(v=sc.12)). O Microsoft Monitoring Agent altera o ambiente do sistema de destino quando instalado.  
  
> [!NOTE]
>  Você também pode coletar dados de diagnóstico e método do IntelliTrace para web, SharePoint, WPF e aplicativos de formulário do Windows em computadores remotos sem alterar o ambiente de destino usando o **coletor autônomo do IntelliTrace**. O coletor autônomo tem um impacto de desempenho maior do que executando o Microsoft Monitoring Agent **Monitor** modo. Ver [usando o coletor autônomo IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md).  
  
 Se você usar o System Center 2012, use o Microsoft Monitoring Agent com Operations Manager para obter alertas sobre problemas e criar itens de trabalho do Team Foundation Server com links para os logs do IntelliTrace salvos. Você pode atribuir esses itens de trabalho a outros para uma depuração adicional. Ver [integração do Operations Manager com processos de desenvolvimento](/previous-versions/system-center/system-center-2012-R2/jj614609(v=sc.12)) e [monitorando com o Microsoft Monitoring Agent](/previous-versions/system-center/system-center-2012-R2/dn465153(v=sc.12)).  
  
 Antes de começar, verifique se você tem a origem e os símbolos correspondentes para o código compilado e implantado. Isso ajuda você a ir diretamente até o código do aplicativo ao iniciar a depuração e a navegação em eventos de diagnóstico no log do IntelliTrace. [Configure suas compilações](../debugger/diagnose-problems-after-deployment.md) para que o Visual Studio pode encontrar e abrir o código-fonte correspondente ao código implantado automaticamente.  
  
1.  [Etapa 1: Configurar o Microsoft Monitoring Agent](#SetUpMonitoring)  
  
2.  [Etapa 2: Iniciar o monitoramento de seu aplicativo](#MonitorEvents)  
  
3.  [Etapa 3: Salvar eventos registrados](#SaveEvents)  
  
##  <a name="SetUpMonitoring"></a> Etapa 1: Configurar o Microsoft Monitoring Agent  
 Configure o agente autônomo no servidor Web para realizar o monitoramento local sem alterar seu aplicativo. Se você usar o System Center 2012, consulte [instalando o Microsoft Monitoring Agent](/previous-versions/system-center/system-center-2012-R2/dn465156(v=sc.12)).  
  
###  <a name="SetUpStandaloneMMA"></a> Configurar o agente autônomo  
  
1.  Verifique se:  
  
    -   Seu servidor web está em execução [suporte para versões do Internet Information Services (IIS)](/previous-versions/system-center/system-center-2012-R2/dn465154(v=sc.12)).  
  
    -   Seu servidor Web tem o .NET Framework 3.5, 4 ou 4.5.  
  
    -   O servidor Web está executando o Windows PowerShell 3.0 ou posterior. [P: E se eu tiver o Windows PowerShell 2.0?](#PowerShell2)  
  
    -   Você tem permissões de administrador em seu servidor Web para executar comandos do PowerShell e reciclar o pool do aplicativos ao iniciar o monitoramento.  
  
    -   Você desinstalou alguma versão anterior do Microsoft Monitoring Agent.  
  
2.  [Baixe o Microsoft Monitoring Agent](http://go.microsoft.com/fwlink/?LinkId=320384), a versão 32 bits **MMASetup-i386.exe** ou a versão de 64 bits **MMASetup-AMD64.exe**, do Microsoft Download Center para a web servidor.  
  
3.  Execute o executável baixado para iniciar o assistente de instalação.  
  
4.  Crie um diretório seguro em seu servidor web para armazenar os logs do IntelliTrace, por exemplo, **C:\IntelliTraceLogs**.  
  
     Não se esqueça de criar esse diretório antes de começar o monitoramento. Para evitar a lentidão no aplicativo, escolha um local em um disco de alta velocidade local que não seja muito ativo.  
  
    > [!IMPORTANT]
    >  Os logs do IntelliTrace podem conter dados pessoais e confidenciais. Restrinja esse diretório a apenas essas identidades que devam funcionar com os arquivos. Verifique as políticas de privacidade da empresa.  
  
5.  Para executar ou monitorar aplicativos do SharePoint de monitoramento detalhados, no nível da função, dê ao pool de aplicativos que hospeda o aplicativo Web ou o aplicativo do SharePoint permissões de leitura e gravação para o diretório do log do IntelliTrace. [P: como configurar permissões para o pool de aplicativos?](#FullPermissionsITLog)  
  
### <a name="q--a"></a>Perguntas e respostas  
  
####  <a name="PowerShell2"></a> P: E se eu tiver o Windows PowerShell 2.0?  
 **R:** é altamente recomendável que você use o PowerShell 3.0. Do contrário, você precisará importar os cmdlets do Microsoft Monitoring Agent PowerShell sempre que executar o PowerShell. Você também não terá acesso ao conteúdo baixável da Ajuda.  
  
1.  Abra uma **Windows PowerShell** ou **Windows PowerShell ISE** janela de prompt de comando como administrador.  
  
2.  Importe o módulo Microsoft Monitoring Agent PowerShell do local de instalação padrão:  
  
     **PS C: > Import-Module "Monitoramento Agent\Agent\PowerShell\Microsoft.MonitoringAgent.PowerShell\Microsoft.MonitoringAgent.PowerShell.dll de C:\Program Files\Microsoft"**  
  
3.  [Visite o TechNet](http://technet.microsoft.com/systemcenter/default) para obter o conteúdo da Ajuda mais recente.  
  
####  <a name="FullPermissionsITLog"></a> P: como configurar permissões para o pool de aplicativos?  
 **R:** usar o Windows **icacls** de comando ou use o Windows Explorer (ou Explorador de arquivos). Por exemplo:  
  
- Para configurar as permissões com o Windows **icacls** comando:  
  
  - Para um aplicativo web na **DefaultAppPool** pool de aplicativos:  
  
     `icacls "C:\IntelliTraceLogs" /grant "IIS APPPOOL\DefaultAppPool":RX`  
  
  - Para um aplicativo do SharePoint na **SharePoint - 80** pool de aplicativos:  
  
     `icacls "C:\IntelliTraceLogs" /grant "IIS APPPOOL\SharePoint - 80":RX`  
  
    -ou-  
  
- Para configurar permissões com o Windows Explorer (ou o Explorador de Arquivos):  
  
  1.  Abra **propriedades** para o diretório de log do IntelliTrace.  
  
  2.  Sobre o **segurança** guia, escolha **editar**, **adicionar**.  
  
  3.  Certifique-se de que **entidades de segurança internas** aparece na **Selecione este tipo de objeto** caixa. Se ele não estiver presente, escolha **tipos de objeto** para adicioná-lo.  
  
  4.  Verifique se o computador local aparece na **desse local** caixa. Se ele não estiver presente, escolha **locais** alterá-la.  
  
  5.  No **insira os nomes de objeto a selecionar** caixa, adicione o pool de aplicativos para o aplicativo web ou aplicativo do SharePoint.  
  
  6.  Escolher **verificar nomes** para resolver o nome. Escolha **OK**.  
  
  7.  Verifique se o pool de aplicativos tem **ler & executar** permissões.  
  
##  <a name="MonitorEvents"></a> Etapa 2: Iniciar o monitoramento de seu aplicativo  
 Usar o Windows PowerShell [Start-WebApplicationMonitoring](http://go.microsoft.com/fwlink/?LinkID=313686) comando para iniciar o monitoramento de seu aplicativo. Se você usar o System Center 2012, consulte [Monitorando aplicativos Web com o Microsoft Monitoring Agent](http://technet.microsoft.com/library/dn465157.aspx).  
  
1.  No seu servidor web, abra uma **Windows PowerShell** ou **Windows PowerShell ISE** janela de prompt de comando como administrador.  
  
     ![Abra o Windows PowerShell como administrador](../debugger/media/ffr_powershellrunadmin.png "FFR_PowerShellRunAdmin")  
  
2.  Execute o [Start-WebApplicationMonitoring](http://go.microsoft.com/fwlink/?LinkID=313686) comando para iniciar o monitoramento de seu aplicativo. Isso reiniciará todos os aplicativos Web no servidor Web.  
  
     Aqui está a sintaxe abreviada:  
  
     **Start-WebApplicationMonitoring** *"\<appName >"*  *\<monitoringMode >* *"\<outputPath >"*  *\<UInt32 >* *"\<collectionPlanPathAndFileName >"*  
  
     Aqui está um exemplo que usa apenas o nome do aplicativo web e lightweight **Monitor** modo:  
  
     **PS C: > Start-WebApplicationMonitoring "FabrikamFabrikamFiber.Web" monitorar "C:IntelliTraceLogs"**  
  
     Aqui está um exemplo que usa o caminho do IIS e lightweight **Monitor** modo:  
  
     **PS C: > Start-WebApplicationMonitoring "IIS:sitesFabrikamFabrikamFiber.Web" monitorar "C:IntelliTraceLogs"**  
  
     Depois de iniciar o monitoramento, você poderá ver o Microsoft Monitoring Agent pausar enquanto seus aplicativos são reiniciados.  
  
     ![Iniciar o monitoramento com confirmação MMA](../debugger/media/ffr_powershellstartmonitoringconfirmation.png "FFR_PowerShellStartMonitoringConfirmation")  
  
    |||  
    |-|-|  
    |*"\<appName >"*|Especifique o caminho para o site e o nome do aplicativo Web no IIS. Você também poderá incluir o caminho do IIS, se preferir.<br /><br /> *"\<IISWebsiteName >\\< IISWebAppName\>"*<br /><br /> -ou-<br /><br /> **"IIS:\sites**  *\\< IISWebsiteName\>\\< IISWebAppName\>"*<br /><br /> Você pode encontrar esse caminho no Gerenciador do IIS. Por exemplo:<br /><br /> ![Caminho para o site do IIS e o aplicativo web](../debugger/media/ffr_iismanager.png "FFR_IISManager")<br /><br /> Você também pode usar o [Get-WebSite](http://technet.microsoft.com/library/ee807832.aspx) e [Get WebApplication](http://technet.microsoft.com/library/ee790554.aspx) comandos.|  
    |*\<monitoringMode >*|Especifique o modo de monitoramento:<br /><br /> <ul><li>**Monitor**: registre detalhes mínimos sobre eventos de exceção e eventos de desempenho. Esse modo usa o plano de coleta padrão.</li><li>**Rastreamento**: registre detalhes de nível de função ou monitore aplicativos SharePoint 2010 e SharePoint 2013 usando o plano de coleta especificado. Esse modo pode fazer o aplicativo ser executado mais lentamente.<br /><br /> <ul><li>[P: como configurar permissões para o pool de aplicativos?](#FullPermissionsITLog)</li><li>[P: como posso obter a maioria dos dados sem afetar a velocidade do meu aplicativo?](#Minimizing)</li></ul><br />     Esse exemplo registra eventos de um aplicativo do SharePoint hospedado em um site do SharePoint:<br /><br />     **Start-WebApplicationMonitoring "FabrikamSharePointSite\FabrikamSharePointApp" rastrear "C:\IntelliTraceLogs" "C:\Program Files\Microsoft monitoramento Agent\Agent\IntelliTraceCollector\collection_plan.ASP.NET.default.xml"**</li><li>**Personalizado**: registre detalhes personalizadas usando o plano de coleta personalizado especificado. Você precisará reiniciar o monitoramento se editar o plano de coleta depois que o monitoramento já tiver começado.</li></ul>|  
    |*"\<outputPath >"*|Especifique o caminho do diretório completo para armazenar os logs do IntelliTrace. Não se esqueça de criar esse diretório antes de começar o monitoramento.|  
    |*\<UInt32 >*|Especifique o tamanho máximo para o log do IntelliTrace. O tamanho máximo padrão do log do IntelliTrace é de 250 MB.<br /><br /> Quando o log atinge esse limite, o agent substitui as entradas mais antigas para liberar espaço para mais entradas. Para alterar esse limite, use o **- MaximumFileSizeInMegabytes** opção ou editar o `MaximumLogFileSize` atributo no plano de coleta.|  
    |*"\<collectionPlanPathAndFileName >"*|Especifique o caminho completo ou relativo e o nome de arquivo do plano de coleta. Esse plano é um arquivo .xml que define configurações do agente.<br /><br /> Esses planos são incluídos no agente e funcionam com aplicativos Web e aplicativos do SharePoint:<br /><br /> -   **collection_plan**<br />     Coleta apenas eventos, como exceções, eventos de desempenho, chamadas de banco de dados e solicitações do servidor Web.<br />-   **collection_plan.ASP.NET.Trace.XML**<br />     Coleta chamadas no nível da função, mais todos os dados no plano de coleta padrão. Esse plano é bom para análise detalhada, mas pode deixar seu aplicativo mais lento.<br /><br /> Você pode encontrar versões localizadas desses planos nas subpastas do agente. Você também pode [personalizar esses planos ou criar seus próprios planos](http://go.microsoft.com/fwlink/?LinkId=227871) para evitar a lentidão no aplicativo. Coloque todos os planos personalizados no mesmo local seguro do agente.<br /><br /> [P: como posso obter a maioria dos dados sem afetar a velocidade do meu aplicativo?](#Minimizing)|  
  
     Para obter mais informações sobre a sintaxe completa e outros exemplos, execute as **get-help Start-WebApplicationMonitoring-detailed** comando ou o **get-help Start-WebApplicationMonitoring-exemplos** comando.  
  
3.  Para verificar o status de todos os aplicativos web monitorados, executados as [Get-WebApplicationMonitoringStatus](http://go.microsoft.com/fwlink/?LinkID=313685) comando.  
  
### <a name="q--a"></a>Perguntas e respostas  
  
####  <a name="Minimizing"></a> P: como posso obter a maioria dos dados sem afetar a velocidade do meu aplicativo?  
 **R:** Microsoft Monitoring Agent pode coletar grandes quantidades de dados e afeta o desempenho do seu aplicativo dependendo dos dados que você optar por coletar e como coletá-los. Estas são algumas das maneiras de obter a maioria dos dados sem deixar seu aplicativo mais lento:  
  
- Para aplicativos Web e aplicativos do SharePoint, o agente grava os dados de todos os aplicativos que compartilham o pool de aplicativos especificado. Isso talvez deixe mais lento qualquer aplicativo que compartilhe o mesmo pool de aplicativos, mesmo que você possa restringir a coleta aos módulos de um único aplicativo. Para evitar que outros aplicativos fiquem mais lentos, hospede cada aplicativo em seu próprio pool de aplicativos.  
  
- Examine os eventos para os quais o agente coleta dados no plano de coleta. Edite o plano de coleta para desabilitar eventos que não sejam relevantes ou que não sejam de seu interesse. Isso pode melhorar o desempenho da inicialização e o desempenho do tempo de execução.  
  
   Para desabilitar um evento, defina o atributo `enabled` para o elemento `<DiagnosticEventSpecification>` como `false`:  
  
   `<DiagnosticEventSpecification enabled="false">`  
  
   Se o atributo `enabled` não existir, o evento estará habilitado.  
  
   Por exemplo:  
  
  -   Desabilite eventos do Fluxo de Trabalho do Windows para aplicativos que não usem o Fluxo de Trabalho do Windows.  
  
  -   Desabilite eventos do Registro para aplicativos que acessem o Registro, mas não mostrem problemas com configurações do Registro.  
  
- Examine os módulos para os quais o agente coleta dados no plano de coleta. Edite o plano de coleta para incluir somente os módulos de seu interesse.  
  
   Isso reduz a quantidade de informações de chamada de método e outros dados de instrumentação que o agente coleta quando o aplicativo é iniciado e executado. Esses dados ajudam a navegar pelo código quando você está depurando e examinando os valores passados para e retornados de chamadas de função.  
  
  1. Abra o plano de coleta. Encontre o elemento `<ModuleList>`.  
  
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
  
   **P: por que não excluir apenas os módulos em vez disso?**  
  
   **R:** por padrão, os planos de coleta excluem módulos definindo o `isExclusionList` atributo `true`. Entretanto, ele ainda pode coletar dados de módulos que não atendam aos critérios da lista ou que talvez não o interesse, como módulos de terceiros ou de software livre.  
  
#### <a name="q-what-values-does-the-agent-collect"></a>P: Quais valores o agente coleta?  
 **R:** para reduzir o impacto no desempenho, o agente coleta apenas estes valores:  
  
- Tipos de dados primitivos passados e retornados de métodos  
  
- Tipos de dados primitivos em campos para objetos no nível superior passados e retornados de métodos  
  
  Por exemplo, suponhamos que você tenha uma assinatura de método `AlterEmployee` que aceite um inteiro `id` e um objeto `Employee` `oldemployee`:  
  
  `public Employee AlterEmployee(int id, Employee oldemployee)`  
  
  O tipo `Employee` tem os seguintes atributos: `Id`, `Name` e `HomeAddress`. Existe uma relação de associação entre `Employee` e o tipo `Address`.  
  
  ![Relação entre o funcionário e o endereço](../debugger/media/employeeaddressrelationship.png "EmployeeAddressRelationship")  
  
  O agente registra valores de `id`, `Employee.Id`, `Employee.Name` e o objeto `Employee` retornado pelo método `AlterEmployee`. Entretanto, o agente não registra informações sobre o objeto `Address` que não sejam se ele era nulo ou não. O agente também não registra dados sobre variáveis locais no método `AlterEmployee`, a menos que outros métodos usem essas variáveis locais como parâmetros em que eles são gravados como parâmetros de método.  
  
##  <a name="SaveEvents"></a> Etapa 3: Salvar eventos registrados  
 Quando você encontrar um erro ou um problema de desempenho, salve os eventos registrados em um log do IntelliTrace. O agente só criará o log se tiver registrado eventos. Se você usar o System Center 2012, consulte [Monitorando aplicativos Web com o Microsoft Monitoring Agent](http://technet.microsoft.com/library/dn465157.aspx).  
  
### <a name="save-recorded-events-but-continue-monitoring"></a>Salvar eventos registrados, mas continuar monitorando  
 Siga estas etapas quando você quiser criar o log do IntelliTrace, mas não quiser reiniciar o aplicativo ou parar de monitorá-lo. O agente continua o monitoramento, mesmo que o servidor ou o aplicativo seja reiniciado.  
  
1. No servidor Web, abra uma janela do prompt de comando do Windows PowerShell como administrador.  
  
2. Execute o [Checkpoint-WebApplicationMonitoring](http://go.microsoft.com/fwlink/?LinkID=313684) comando para salvar um instantâneo do log do IntelliTrace:  
  
    **CheckPoint-WebApplicationMonitoring** *"\<IISWebsiteName >\\< IISWebAppName\>"*  
  
    \- ou -  
  
    **CheckPoint-WebApplicationMonitoring "IIS:\sites**  *\\< IISWebsiteName\>\\< IISWebAppName\>"*  
  
    Por exemplo:  
  
    **PS C:\\> Checkpoint-WebApplicationMonitoring "Fabrikam\FabrikamFiber.Web"**  
  
    -ou-  
  
    **PS C: > Checkpoint-WebApplicationMonitoring "IIS:sitesFabrikamFabrikamFiber.Web"**  
  
    Para obter mais informações, execute as **get-help Checkpoint-WebApplicationMonitoring-detalhada** comando ou o **get-help Checkpoint-WebApplicationMonitoring-exemplos** comando.  
  
3. Copie o log para uma pasta compartilhada segura e, em seguida, abra o log de um computador que tem o Visual Studio Enterprise (mas não as edições Professional ou Community).  
  
   > [!IMPORTANT]
   >  Tome cuidado ao compartilhar logs do IntelliTrace, porque eles podem conter dados pessoais e confidenciais. Verifique se a pessoa que pode acessar esses logs tem permissões para analisar esses dados. Verifique as políticas de privacidade da empresa.  
  
   **Em seguida:** [Diagnose registrou eventos no Visual Studio Enterprise](../debugger/diagnose-problems-after-deployment.md#InvestigateEvents)  
  
### <a name="save-recorded-events-and-stop-monitoring"></a>Salvar eventos registrados e parar o monitoramento  
 Siga estas etapas quando quiser somente informações de diagnóstico durante a reprodução de um problema específico. Isso reiniciará todos os aplicativos Web no servidor Web.  
  
1. No servidor Web, abra uma janela do prompt de comando do Windows PowerShell como administrador.  
  
2. Execute o [Stop-WebApplicationMonitoring](http://go.microsoft.com/fwlink/?LinkID=313687) comando para criar o log do IntelliTrace e parar de monitorar um aplicativo web específico:  
  
    **Stop-WebApplicationMonitoring** *"\<IISWebsiteName >\\< IISWebAppName\>"*  
  
    \- ou -  
  
    **Stop-WebApplicationMonitoring "IIS:\sites**  *\\< IISWebsiteName\>\\< IISWebAppName\>"*  
  
    Ou pare o monitoramento de todos os aplicativos Web:  
  
    **Stop-WebApplicationMonitoring - todos**  
  
    Por exemplo:  
  
    **PS C:\\> Stop-WebApplicationMonitoring "Fabrikam\iFabrikamFiber.Web"**  
  
    \- ou -  
  
    **PS C:\\> Stop-WebApplicationMonitoring "IIS:\sites\Fabrikam\FabrikamFiber.Web"**  
  
    Para obter mais informações, execute as **get-help Stop-WebApplicationMonitoring-detailed** comando ou o **get-help Stop-WebApplicationMonitoring-exemplos** comando.  
  
3. Copie o log para uma pasta compartilhada segura e, em seguida, abra o log de um computador que tenha o Visual Studio Enterprise.  
  
   **Em seguida:** [Diagnose registrou eventos no Visual Studio Enterprise](../debugger/diagnose-problems-after-deployment.md#InvestigateEvents)  
  
## <a name="q--a"></a>Perguntas e respostas  
  
### <a name="q-where-can-i-get-more-information"></a>P: Onde posso obter mais informações?  
  
#### <a name="blogs"></a>Blogs  
 [Introdução ao Microsoft Monitoring Agent](https://blogs.msdn.microsoft.com/devops/2013/09/20/introducing-microsoft-monitoring-agent/)  
  
 [Otimizando a coleção de IntelliTrace em servidores de produção](http://go.microsoft.com/fwlink/?LinkId=255233)  
  
#### <a name="forums"></a>Fóruns  
 [Diagnóstico do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=262263)
