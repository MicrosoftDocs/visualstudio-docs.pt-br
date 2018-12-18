---
title: Configurar o diagnóstico para máquinas virtuais e serviços de nuvem do Azure | Microsoft Docs
description: Saiba como configurar o diagnóstico para depurar os serviços de nuvem do Azure e máquinas virtuais (VMs) no Visual Studio.
author: mikejo5000
manager: douge
ms.assetid: e70cd7b4-6298-43aa-adea-6fd618414c26
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 06/28/2018
ms.author: mikejo
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.openlocfilehash: 4448825c5d443887833a405aab14d2243a0e5216
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001339"
---
# <a name="set-up-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Configurar o diagnóstico para Serviços de Nuvem e máquinas virtuais do Azure
Quando você precisar solucionar problemas de uma máquina virtual ou serviço de nuvem do Azure, você pode usar o Visual Studio para configurar mais facilmente o diagnóstico do Azure. O diagnóstico captura dados do sistema e dados de log em máquinas virtuais e instâncias de máquinas virtuais que executam o serviço de nuvem. Dados de diagnóstico são transferidos para uma conta de armazenamento que você escolher. Para obter mais informações sobre o diagnóstico de registro em log no Azure, consulte [habilitar o log de diagnóstico para aplicativos Web no serviço de aplicativo do Azure](/azure/app-service/web-sites-enable-diagnostic-log).

Neste artigo, mostramos como usar o Visual Studio para ativar e configurar o diagnóstico do Azure, antes e após a implantação. Saiba como configurar o diagnóstico em máquinas virtuais do Azure, como selecionar os tipos de informações de diagnóstico para coletar e como exibir as informações depois de coletadas.

Você pode usar uma das opções a seguir para configurar o diagnóstico do Azure:

* Alterar as configurações de diagnóstico na **configuração de diagnóstico** caixa de diálogo no Visual Studio. As configurações são salvas em um arquivo chamado Diagnostics. wadcfgx (no Azure SDK 2.4 e anteriores, o arquivo é chamado Diagnostics. wadcfg). Você também pode modificar diretamente o arquivo de configuração. Se você atualizar manualmente o arquivo, a alterações de configuração entrarão em vigor na próxima vez que você implanta a nuvem de serviço para o Azure ou executar o serviço no emulador.
* Use o Cloud Explorer ou Gerenciador de servidores no Visual Studio para alterar as configurações de diagnóstico para um serviço de nuvem ou máquina virtual que está em execução.

## <a name="azure-sdk-26-diagnostics-changes"></a>Alterações de diagnóstico do Azure SDK 2.6
As alterações a seguir se aplicam a SDK do Azure 2.6 e posteriores projetos no Visual Studio:

* O emulador local agora dá suporte a diagnóstico. Isso significa que você pode coletar dados de diagnóstico e certifique-se de que seu aplicativo cria os rastreamentos corretos enquanto você desenvolve e testa no Visual Studio. A cadeia de caracteres de conexão `UseDevelopmentStorage=true` ativa a coleta de dados de diagnóstico enquanto você estiver executando seu projeto de serviço de nuvem no Visual Studio usando o emulador de armazenamento do Azure. Todos os dados de diagnóstico são coletados na conta de armazenamento no armazenamento de desenvolvimento.
* A cadeia de conexão de conta de armazenamento de diagnóstico `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` é armazenado no arquivo de configuração (. cscfg) de serviço. No Azure SDK 2.5, a conta de armazenamento de diagnóstico é especificada no arquivo Diagnostics. wadcfgx.

A cadeia de caracteres de conexão funciona de maneira diferente de algumas maneiras principais no SDK do Azure 2.6 e posteriores versus Azure SDK 2.4 e anteriores:

* No SDK do Azure 2.4 e anteriores, a cadeia de caracteres de conexão é usada como um tempo de execução, o plug-in de diagnóstico para obter as informações de conta de armazenamento para transferir os logs de diagnóstico.
* No SDK do Azure 2.6 e posterior, o Visual Studio usa a cadeia de caracteres de conexão de diagnóstico para configurar a extensão de diagnóstico do Azure com as informações de conta de armazenamento apropriadas durante a publicação. Você pode usar a cadeia de caracteres de conexão para definir diferentes contas de armazenamento para diferentes configurações de serviço que usa o Visual Studio durante a publicação. No entanto, como o plug-in de diagnóstico não está disponível após o Azure SDK 2.5, o arquivo. cscfg sozinho não é possível definir a extensão de diagnóstico. Você deve configurar a extensão separadamente usando ferramentas como o Visual Studio ou o PowerShell.
* Para simplificar o processo de configurar a extensão de diagnóstico usando o PowerShell, a saída do pacote do Visual Studio inclui o XML de configuração pública da extensão de diagnóstico para cada função. Visual Studio usa a cadeia de caracteres de conexão de diagnóstico para preencher as informações de conta de armazenamento na configuração pública. Os arquivos de configuração pública são criados na pasta extensões. Os arquivos de configuração pública usam o padrão de nomenclatura PaaSDiagnostics. &lt;nome da função\>. Pubconfig. Todas as implantações com base em PowerShell podem usar esse padrão para mapear cada configuração para uma função.
* O [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) usa a cadeia de caracteres de conexão no arquivo. cscfg para acessar os dados de diagnóstico. Os dados aparecem na **monitoramento** guia. A cadeia de caracteres de conexão é necessária para configurar o serviço para mostrar os dados do monitoramento detalhado no portal.

## <a name="migrate-projects-to-azure-sdk-26-and-later"></a>Migre projetos para o Azure SDK 2.6 e posterior
Quando você migra do Azure SDK 2.5 para SDK do Azure 2.6 ou posterior, se você tiver uma conta de armazenamento de diagnóstico especificada no arquivo. wadcfgx, a conta de armazenamento permanecerá naquele arquivo. Para tirar proveito da flexibilidade de usar contas de armazenamento diferentes para diferentes configurações de armazenamento, adicione manualmente a cadeia de caracteres de conexão ao seu projeto. Se você estiver migrando um projeto do SDK do Azure 2.4 ou anterior para o SDK do Azure 2.6, as cadeias de caracteres de conexão de diagnóstico serão preservadas. No entanto, observe as alterações na forma como as cadeias de caracteres de conexão são tratadas no SDK do Azure 2.6, descritas na seção anterior.

### <a name="how-visual-studio-determines-the-diagnostics-storage-account"></a>Como o Visual Studio determina a conta de armazenamento de diagnóstico
* Se uma cadeia de caracteres de conexão de diagnóstico é especificada no arquivo. cscfg, o Visual Studio a usa para configurar a extensão de diagnóstico durante a publicação e ao gerar os arquivos XML de configuração pública durante o empacotamento.
* Se uma cadeia de caracteres de conexão de diagnóstico não for especificada no arquivo. cscfg, o Visual Studio voltará a usar a conta de armazenamento que é especificada no arquivo. wadcfgx para configurar a extensão de diagnóstico para a publicação e para gerar o XML de configuração pública arquivos durante o empacotamento.
* A cadeia de caracteres de conexão de diagnóstico no arquivo. cscfg tem precedência sobre a conta de armazenamento no arquivo. wadcfgx. Se for uma cadeia de caracteres de conexão de diagnóstico especificada no arquivo. cscfg, o Visual Studio usa essa cadeia de caracteres de conexão e ignora a conta de armazenamento em. wadcfgx.

### <a name="what-does-the-update-development-storage-connection-strings-check-box-do"></a>O que faz a caixa de seleção "Atualizar cadeias de conexão de armazenamento de desenvolvimento..."?
O **atualizar cadeias de conexão do armazenamento de desenvolvimento para diagnóstico e cache com credenciais de conta de armazenamento do Microsoft Azure, ao publicar no Microsoft Azure** caixa de seleção é uma maneira conveniente para atualizar qualquer armazenamento de desenvolvimento cadeias de caracteres de conexão de conta com a conta de armazenamento do Azure que você especificar durante a publicação.

Por exemplo, se você selecionar essa caixa de seleção e a cadeia de caracteres de conexão de diagnóstico especifica `UseDevelopmentStorage=true`, quando você publica o projeto no Azure, Visual Studio atualiza automaticamente a cadeia de caracteres de conexão de diagnóstico com a conta de armazenamento que você especificou no o Assistente de publicação. No entanto, se uma conta de armazenamento real foi especificada como a cadeia de caracteres de conexão de diagnóstico, essa conta será usada em vez disso.

## <a name="diagnostics-functionality-differences-in-azure-sdk-24-and-earlier-vs-azure-sdk-25-and-later"></a>Diferenças de funcionalidade de diagnóstico no Azure SDK 2.4 e anteriores vs. SDK do Azure 2.5 e posterior
Se você estiver atualizando seu projeto do Azure SDK 2.4 e anterior para o SDK do Azure 2.5 ou posterior, tenha em mente as seguintes diferenças de funcionalidade de diagnóstico:

* **APIs de configuração são preteridas**. Configuração programática de diagnóstico está disponível no SDK do Azure 2.4 e anteriores, mas foi preterida no SDK do Azure 2.5 e posteriores. Se sua configuração de diagnóstico está definida atualmente no código, você deve reconfigurar as configurações do zero no projeto migrado para o diagnóstico continue a funcionar. O arquivo de configuração de diagnóstico para o Azure SDK 2.4 é Diagnostics. wadcfg. O arquivo de configuração de diagnóstico do Azure SDK 2.5 e posteriores é Diagnostics. wadcfgx.
* **Diagnóstico para aplicativos de serviço de nuvem pode ser configurado somente no nível de função**. No SDK do Azure 2.5 e posterior, você não pode configurar o diagnóstico para aplicativos de serviço de nuvem no nível de instância.
* **Sempre que você implanta seu aplicativo, a configuração de diagnóstico é atualizada**. Isso pode causar problemas de paridade se você alterar sua configuração de diagnóstico do Visual Studio Server Explorer e, em seguida, reimplante o aplicativo.
* **No SDK do Azure 2.5 e posteriores, despejos são configurados no arquivo de configuração de diagnóstico e não no código**. Se você tiver despejos configurados no código, você deve transferir manualmente a configuração do código ao arquivo de configuração. Os despejos de memória não são transferidos durante a migração para o Azure SDK 2.6.

## <a name="turn-on-diagnostics-in-cloud-service-projects-before-you-deploy-them"></a>Ativar o diagnóstico em projetos de serviço de nuvem antes de implantá-los
No Visual Studio, você pode coletar dados de diagnóstico para funções executadas no Azure quando você executa o serviço no emulador antes da implantação. Todas as alterações às configurações de diagnóstico no Visual Studio são salvas no arquivo de configuração Diagnostics. wadcfgx. Essas configurações especificam a conta de armazenamento onde os dados de diagnóstico são salvos quando você implanta seu serviço de nuvem.

[!INCLUDE [cloud-services-wad-warning](./includes/cloud-services-wad-warning.md)]

### <a name="to-turn-on-diagnostics-in-visual-studio-before-deployment"></a>Para ativar o diagnóstico no Visual Studio antes da implantação

1. No menu de atalho para a função, selecione **propriedades**. A função **propriedades** caixa de diálogo, selecione o **configuração** guia.
2. No **diagnósticos** seção, certifique-se de que o **habilitar diagnóstico** caixa de seleção está selecionada.
   
    ![Acessar a opção Habilitar diagnóstico](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Para especificar a conta de armazenamento para os dados de diagnóstico, selecione o botão de reticências (...).
   
    ![Especifique a conta de armazenamento para usar](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. No **criar cadeia de Conexão de armazenamento** caixa de diálogo caixa, especifique se você deseja se conectar usando o emulador de armazenamento do Azure, uma assinatura do Azure, ou credenciais inseridas manualmente.
   
    ![Caixa de diálogo da conta de armazenamento](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Se você selecionar **emulador de armazenamento do Microsoft Azure**, a cadeia de caracteres de conexão é definida como `UseDevelopmentStorage=true`.
   * Se você selecionar **sua subscrição**, você pode selecionar a assinatura do Azure que você deseja usar e insira um nome de conta. Para gerenciar suas assinaturas do Azure, selecione **gerenciar contas**.
   * Se você selecionar **credenciais inseridas manualmente**, insira o nome e a chave da conta do Azure que você deseja usar.
5. Para exibir o **configuração de diagnóstico** caixa de diálogo, selecione **configurar**. Exceto para **gerais** e **diretórios de Log**, cada guia representa uma fonte de dados de diagnóstico que você pode coletar. O padrão **gerais** guia Opções de coleta de dados de diagnóstico a seguir oferece: **somente erros**, **todas as informações**, e **plano personalizado**. O padrão **somente erros** opção usa a menor quantidade de armazenamento, porque não transfere avisos ou mensagens de rastreamento. O **todas as informações** opção transfere a maioria das informações, usa o máximo de armazenamento e, portanto, a opção mais cara.

   > [!NOTE]
   > Tamanho mínimo com suporte para "Cota de disco em MB" é de 4GB. No entanto, se você estiver coletando os despejos de memória, aumente isso para um valor mais alto, como 10GB.
   >
  
    ![Habilitar a configuração e o diagnóstico do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. Neste exemplo, selecione a **plano personalizado** opção, para que você possa personalizar os dados coletados.
7. No **cota de disco em MB** caixa, você pode definir quanto espaço alocar na sua conta de armazenamento para dados de diagnóstico. Você pode alterar ou aceite o valor padrão.
8. Em cada guia de dados de diagnóstico que você deseja coletar, selecione a **Habilitar transferência dos \<tipo de log\>**  caixa de seleção. Por exemplo, se você quiser coletar logs de aplicativo, na **Logs de aplicativo** guia, selecione o **Habilitar transferência dos Logs de aplicativo** caixa de seleção. Além disso, especifique qualquer outra informação que é necessária para cada tipo de dados de diagnóstico. Para obter informações de configuração para cada guia, consulte a seção **configurar fontes de dados de diagnóstico** mais adiante neste artigo. 
9. Depois de habilitar a coleção de todos os dados de diagnóstico que você deseja, selecione **Okey**.
10. Execute seu projeto de serviço de nuvem do Azure no Visual Studio, como de costume. Como usar o seu aplicativo, as informações de log que você habilitou é salvo para a conta de armazenamento do Azure que você especificou.

## <a name="turn-on-diagnostics-on-azure-virtual-machines"></a>Ativar o diagnóstico em máquinas virtuais do Azure
No Visual Studio, você pode coletar dados de diagnóstico para máquinas virtuais do Azure.

### <a name="to-turn-on-diagnostics-on-azure-virtual-machines"></a>Para ativar o diagnóstico em máquinas virtuais do Azure

1. No Gerenciador de servidores, selecione o nó do Azure e conecte-se à sua assinatura do Azure, se você ainda não estiver conectado.
2. Expanda o **máquinas virtuais** nó. Você pode criar uma nova máquina virtual ou selecione um nó existente.
3. No menu de atalho para a máquina virtual que você deseja, selecione **configurar**. A caixa de diálogo de configuração de máquina virtual é exibida.
   
    ![Configurar uma máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Se ainda não estiver instalado, adicione a extensão de diagnóstico do Microsoft Monitoring Agent. Com essa extensão, você pode coletar dados de diagnóstico para a máquina virtual do Azure. Sob **extensões instaladas**, no **selecionar uma extensão disponível** caixa de lista suspensa, selecione **diagnóstico do Microsoft Monitoring Agent**.
   
    ![Instalar uma extensão de máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
    > [!NOTE]
   > Outras extensões de diagnóstico estão disponíveis para suas máquinas virtuais. Para obter mais informações, consulte [recursos e extensões de máquina Virtual para Windows](https://docs.microsoft.com/azure/virtual-machines/windows/extensions-features).
   > 
   > 
5. Para adicionar a extensão e exibir seus **configuração de diagnóstico** caixa de diálogo, selecione **Add**.
6. Para especificar uma conta de armazenamento, selecione **configurar**e, em seguida, selecione **Okey**.
   
    Cada guia (exceto para **gerais** e **diretórios de Log**) representa uma fonte de dados de diagnóstico que você pode coletar.
   
    ![Habilitar a configuração e o diagnóstico do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    A guia padrão, **gerais**, oferece as seguintes opções de coleta de dados de diagnóstico: **somente erros**, **todas as informações**, e **plano personalizado**. A opção padrão, **somente erros**, leva a menor quantidade de armazenamento porque não transfere avisos ou mensagens de rastreamento. O **todas as informações** opção transfere a maioria das informações e é, portanto, a opção mais cara em termos de armazenamento.
7. Neste exemplo, selecione a **plano personalizado** opção para que você possa personalizar os dados coletados.
8. O **cota de disco em MB** caixa especifica a quantidade de espaço que deseja alocar na sua conta de armazenamento para dados de diagnóstico. Você pode alterar o valor padrão se desejar.
9. Em cada guia de dados de diagnóstico que você deseja coletar, selecione suas **Habilitar transferência dos \<tipo de log\>**  caixa de seleção.
   
    Por exemplo, se você quiser coletar logs de aplicativo, selecione a **Habilitar transferência dos Logs de aplicativo** caixa de seleção a **Logs de aplicativo** guia. Além disso, especifique outras informações necessárias para cada tipo de dados de diagnóstico. Para obter informações de configuração para cada guia, consulte a seção **configurar fontes de dados de diagnóstico** mais adiante neste artigo.
10. Depois de habilitar a coleção de todos os dados de diagnóstico que você deseja, selecione **Okey**.
11. Salve o projeto atualizado.
    
    Uma mensagem na **Log de atividades do Microsoft Azure** janela indica que a máquina virtual foi atualizada.

## <a name="set-up-diagnostics-data-sources"></a>Configurar fontes de dados de diagnóstico
Depois de habilitar a coleta de dados de diagnóstico, você pode escolher exatamente quais fontes de dados que você deseja coletar e quais informações são coletadas. As próximas seções descrevem as guias a **configuração de diagnóstico** caixa de diálogo e significa que cada opção de configuração.

### <a name="application-logs"></a>Logs de aplicativo
Os logs de aplicativo têm informações de diagnóstico que são produzidas por um aplicativo web. Se você quiser capturar os logs de aplicativo, selecione a **Habilitar transferência dos Logs de aplicativo** caixa de seleção. Para aumentar ou diminuir o intervalo entre a transferência dos logs de aplicativo para sua conta de armazenamento, altere o **período de transferência (min)** valor. Você também pode alterar a quantidade de informações capturadas no log definindo o **nível de Log** valor. Por exemplo, selecione **Verbose** para obter mais informações, ou selecione **crítico** para capturar somente erros críticos. Se você tiver um provedor de diagnósticos específico que emite os logs de aplicativo, você pode capturar os logs, adicionando o GUID do provedor na **GUID do provedor** caixa.

  ![Logs de aplicativo](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

Para obter mais informações sobre logs de aplicativo, consulte [habilitar o log de diagnóstico para aplicativos Web no serviço de aplicativo do Azure](/azure/app-service/web-sites-enable-diagnostic-log).

### <a name="windows-event-logs"></a>Logs de eventos do Windows
Para capturar os logs de eventos do Windows, selecione o **Habilitar transferência dos Logs de eventos do Windows** caixa de seleção. Para aumentar ou diminuir o intervalo entre a transferência de logs de eventos para sua conta de armazenamento, altere o **período de transferência (min)** valor. Marque as caixas de seleção para os tipos de eventos que você deseja controlar.

![Logs de eventos](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Se você estiver usando o SDK do Azure 2.6 ou posterior e você deseja especificar uma fonte de dados personalizada, insira-a na **\<nome da fonte de dados\>** caixa de texto e, em seguida, selecione **adicionar**. A fonte de dados é adicionada ao arquivo cfcfg.

Se você estiver usando o Azure SDK 2.5 e deseja especificar uma fonte de dados personalizada, você pode adicioná-lo para o `WindowsEventLog` seção wadcfgx do arquivo, como no exemplo a seguir:

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Contadores de desempenho
Informações do contador de desempenho podem ajudá-lo a localizar gargalos do sistema e ajustar o desempenho do sistema e do aplicativo. Para obter mais informações, consulte [criar e usar contadores de desempenho em um aplicativo do Azure](https://msdn.microsoft.com/library/azure/hh411542.aspx). Para capturar os contadores de desempenho, selecione o **habilitar a transferência de contadores de desempenho** caixa de seleção. Para aumentar ou diminuir o intervalo entre a transferência de logs de eventos para sua conta de armazenamento, altere o **período de transferência (min)** valor. Marque as caixas de seleção dos contadores de desempenho que você deseja controlar.

![Contadores de desempenho](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

Para rastrear um contador de desempenho que não está listado, insira o contador de desempenho usando a sintaxe sugerida. e, em seguida, selecione **adicionar**. O sistema operacional na máquina virtual determina quais contadores de desempenho que você pode acompanhar. Para obter mais informações sobre a sintaxe, consulte [especificar um caminho de contador](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Logs de infraestrutura
Logs de infraestrutura têm informações sobre a infraestrutura de diagnóstico do Azure, o módulo RemoteAccess e o módulo RemoteForwarder. Para coletar informações sobre logs de infraestrutura, selecione a **habilitar a transferência de Logs de infraestrutura** caixa de seleção. Para aumentar ou diminuir o intervalo entre a transferência de logs de infraestrutura para sua conta de armazenamento, altere o **período de transferência (min)** valor.

![Logs de infraestrutura de diagnóstico](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

Para obter mais informações, consulte [coletar dados de registro em log usando o diagnóstico do Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx).

### <a name="log-directories"></a>Diretórios de log
Diretórios de log têm dados coletados de diretórios de log para solicitações de serviços de informações da Internet (IIS), solicitações com falha ou pastas que você escolher. Para capturar os diretórios de log, selecione a **habilitar a transferência de diretórios de Log** caixa de seleção. Para aumentar ou diminuir o intervalo entre a transferência de logs para sua conta de armazenamento, altere o **período de transferência (min)** valor.

Marque as caixas de seleção dos logs que você deseja coletar, tais como **Logs do IIS** e **solicitação com falha** logs. Nomes de contêiner de armazenamento padrão são fornecidos, mas você pode alterar os nomes.

Você pode capturar logs de qualquer pasta. Especifique o caminho na **Log do diretório absoluto** seção e, em seguida, selecione **Adicionar diretório**. Os logs são capturados nos contêineres especificados.

![Diretórios de log](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>Logs do ETW
Se você usar [rastreamento de eventos para Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) e desejar capturar logs de ETW, selecione o **Habilitar transferência dos Logs de ETW** caixa de seleção. Para aumentar ou diminuir o intervalo entre a transferência de logs para sua conta de armazenamento, altere o **período de transferência (min)** valor.

Os eventos são capturados das origens de eventos e manifestos de evento que você especificar. Para especificar uma origem de evento, na **origens do evento** seção, insira um nome e, em seguida, selecione **Adicionar origem de evento**. Da mesma forma, você pode especificar um manifesto de evento na **manifestos de evento** seção e, em seguida, selecione **adicionar manifesto de evento**.

![Logs do ETW](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

A estrutura do ETW tem suporte no ASP.NET por meio de classes na [System.Diagnostics.aspx](https://msdn.microsoft.com/library/system.diagnostics(v=vs.110)) namespace. O namespace do windowsazure, que herda e estende o padrão [System.Diagnostics.aspx](https://msdn.microsoft.com/library/system.diagnostics(v=vs.110)) classe, permite o uso de [System.Diagnostics.aspx](https://msdn.microsoft.com/library/system.diagnostics(v=vs.110)) como um registro em log estrutura no ambiente do Azure. Para obter mais informações, consulte [assumir o controle de registro em log e rastreamento no Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) e [habilitar o diagnóstico nos serviços de nuvem do Azure e máquinas virtuais](/azure/cloud-services/cloud-services-dotnet-diagnostics).

### <a name="crash-dumps"></a>Despejos de falhas
Para capturar informações sobre quando uma instância de função falha, selecione o **Habilitar transferência de despejos** caixa de seleção. (Como o ASP.NET manipula a maioria das exceções, isso geralmente é útil somente para funções de trabalho.) Para aumentar ou diminuir a porcentagem de espaço de armazenamento dedicado aos despejos, altere o **cota de diretório (%)** valor. Você pode alterar o contêiner de armazenamento em que os despejos de memória são armazenados e selecionar se deseja capturar uma **completo** ou **Mini** despejo.

Os processos que estão sendo controlados no momento são listados na seguinte captura de tela. Marque as caixas de seleção para os processos que você deseja capturar. Para adicionar outro processo à lista, insira o nome do processo e, em seguida, selecione **adicionar processo**.

![Despejos de falhas](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

Para obter mais informações, consulte [assumir o controle de registro em log e rastreamento no Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) e [diagnóstico do Microsoft Azure parte 4: componentes de registro em log personalizados e alterações de diagnóstico do Azure 1.3](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/).

## <a name="view-the-diagnostics-data"></a>Exibir os dados de diagnóstico
Depois que você coletou os dados de diagnóstico para um serviço de nuvem ou máquina virtual, você pode exibi-lo.

### <a name="to-view-cloud-service-diagnostics-data"></a>Para exibir dados de diagnóstico do serviço de nuvem
1. Implante seu serviço de nuvem como de costume e, em seguida, executá-lo.
2. Você pode exibir os dados de diagnóstico em um relatório que o Visual Studio gera ou em tabelas em sua conta de armazenamento. Para exibir os dados em um relatório, abra Cloud Explorer ou Gerenciador de servidores, abra o menu de atalho do nó para a função que você deseja e, em seguida, selecione **exibir dados de diagnóstico**.
   
    ![Exibir dados de diagnóstico](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Um relatório que mostra os dados disponíveis é exibida.
   
    ![Relatório de diagnóstico do Microsoft Azure no Visual Studio](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Se os dados mais recentes não forem mostrados, você terá que aguardar o período de transferência.
   
    Para atualizar imediatamente os dados, selecione a **Refresh** link. Para que os dados atualizados automaticamente, selecione um intervalo na **Autoatualizar** caixa de listagem suspensa. Para exportar os dados de erro, selecione a **exportar para CSV** botão para criar um arquivo de valores separados por vírgula que pode ser aberto em uma planilha do Excel.
   
    No Cloud Explorer ou Gerenciador de servidores, abra a conta de armazenamento que está associada com a implantação.
3. Abra as tabelas de diagnóstico no Visualizador de tabela e, em seguida, examine os dados coletados. Para logs do IIS e logs personalizados, você pode abrir um contêiner de blob. A tabela a seguir lista as tabelas ou contêineres de blob que contêm os dados para os arquivos de log diferente. Além dos dados para esse arquivo de log, as entradas de tabela contêm **EventTickCount**, **DeploymentId**, **função**, e **RoleInstance** , para ajudá-lo a identificar qual máquina virtual e a função geraram os dados e quando. 
   
   | Dados de diagnóstico | Descrição | Local |
   | --- | --- | --- |
   | Logs de aplicativo |Os logs que seu código gera chamando métodos das **Trace** classe. |WADLogsTable |
   | Logs de eventos |Dados de logs de eventos do Windows nas máquinas virtuais. Windows armazena informações nesses logs, mas os aplicativos e serviços também usam os logs para relatar erros ou informações de log. |WADWindowsEventLogsTable |
   | Contadores de desempenho |Você pode coletar dados em qualquer contador de desempenho que está disponível na máquina virtual. O sistema operacional fornece contadores de desempenho, que inclui muitas estatísticas, como tempo de processador e uso de memória. |WADPerformanceCountersTable |
   | Logs de infraestrutura |Logs que são gerados a partir da própria infraestrutura de diagnóstico. |WADDiagnosticInfrastructureLogsTable |
   | Logs IIS |Logs que registram solicitações da web. Se seu serviço de nuvem obtiver uma quantidade significativa de tráfego, esses logs podem ser demorados. É uma boa ideia coletar e armazenar esses dados somente quando necessário. |Você pode encontrar os logs de solicitação com falha no contêiner de blob em wad-iis-failedreqlogs em um caminho para essa implantação, função e instância. Você pode encontrar logs completos em wad-iis-logfiles. As entradas para cada arquivo são feitas na tabela WADDirectories. |
   | Despejos de falhas |Fornecem imagens binárias do processo do serviço de nuvem (normalmente uma função de trabalho). |contêiner de blob wad-crush-dumps |
   | Arquivos de log personalizados |Logs de dados que você predefiniu. |Você pode especificar no código o local dos arquivos de log personalizado em sua conta de armazenamento. Por exemplo, você pode especificar um contêiner de blob personalizado. |
4. Se os dados de qualquer tipo estão truncados, você pode tentar aumentar o buffer para os dados de tipo ou encurtar o intervalo entre transferências de dados da máquina virtual para sua conta de armazenamento.
5. (Opcional) Limpe os dados da conta de armazenamento, ocasionalmente, para reduzir os custos gerais de armazenamento.
6. Quando você fizer uma implantação completa, o arquivo Diagnostics dll (. wadcfgx para SDK 2.5 do Azure) é atualizado no Azure e seu serviço de nuvem seleciona as alterações à sua configuração de diagnóstico. Se atualizar uma implantação existente em vez disso, o arquivo. cscfg não será atualizado no Azure. Você ainda pode alterar as configurações de diagnóstico, porém, seguindo as etapas na próxima seção. Para obter mais informações sobre como executar uma implantação completa e atualizar uma implantação existente, consulte [assistente Publicar aplicativo do Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="to-view-virtual-machine-diagnostics-data"></a>Para exibir dados de diagnóstico de máquina virtual
1. No menu de atalho para a máquina virtual, selecione **exibir dados de diagnóstico**.
   
    ![Exibir dados de diagnóstico em uma máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    O **resumo de diagnóstico** caixa de diálogo é exibida.
   
    ![Resumo de diagnóstico de máquina virtual do Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Se os dados mais recentes não forem mostrados, você terá que aguardar o período de transferência.
   
    Para atualizar imediatamente os dados, selecione a **Refresh** link. Para que os dados atualizados automaticamente, selecione um intervalo na **Autoatualizar** caixa de listagem suspensa. Para exportar os dados de erro, selecione a **exportar para CSV** botão para criar um arquivo de valores separados por vírgula que pode ser aberto em uma planilha do Excel.

## <a name="set-up-cloud-service-diagnostics-after-deployment"></a>Configurar o diagnóstico do serviço de nuvem após a implantação
Se você estiver investigando um problema com um serviço de nuvem que já está em execução, você talvez queira coletar os dados que você não especificou antes de implantar originalmente a função. Nesse caso, você pode começar a coletar dados alterando as configurações no Gerenciador de servidores. Você pode configurar o diagnóstico para uma única instância ou para todas as instâncias de função, dependendo se você abrir o **configuração de diagnóstico** caixa de diálogo no menu de atalho para a instância ou a função. Se você configurar o nó da função, as alterações que você fizer se aplicam a todas as instâncias. Se você configurar o nó da instância, as alterações que você fizer se aplicam somente a essa instância.

### <a name="to-set-up-diagnostics-for-a-running-cloud-service"></a>Para configurar o diagnóstico para um serviço de nuvem em execução
1. No Gerenciador de servidores, expanda o **serviços de nuvem** nó e, em seguida, expanda a lista de nós para localizar a função ou instância (ou ambos) que você deseja investigar.
   
    ![Configurar o diagnóstico](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. No menu de atalho para um nó da instância ou o nó da função, selecione **atualizar configurações de diagnóstico**e, em seguida, selecione as configurações de diagnóstico que você deseja coletar.
   
    Para obter informações sobre as definições de configuração, consulte a seção **configurar fontes de dados de diagnóstico** neste artigo. Para obter informações sobre como exibir os dados de diagnóstico, consulte a seção **exibir os dados de diagnóstico** neste artigo.
   
    Se você alterar a coleta de dados no Gerenciador de servidores, as alterações permanecerão em vigor até que você reimplante seu serviço de nuvem. Se você usar o padrão, as configurações de publicação, as alterações não são substituídas. Configuração de publicação padrão é para atualizar a implantação existente, em vez de fazer uma reimplantação completa. Para garantir que as configurações estão limpas no momento da implantação, vá para o **configurações avançadas** guia no Assistente de publicação e, em seguida, desmarque as **atualização da implantação** caixa de seleção. Quando você reimplanta com essa caixa de seleção desmarcada, as configurações revertem aquelas no arquivo. wadcfgx (ou wadcfg) conforme definido por meio de **propriedades** editor para a função. Se você atualizar sua implantação, o Azure mantém as configurações anteriores.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Solucionar problemas do serviço de nuvem do Azure
Se você tiver problemas com seus projetos de serviço de nuvem, como uma função travar no status "ocupado", repetidamente recicla ou lança um erro interno do servidor, existem ferramentas e técnicas que você pode usar para diagnosticar e corrigir o problema. Para obter exemplos específicos de problemas e soluções comuns e para uma visão geral dos conceitos e ferramentas que você pode usar para diagnosticar e corrigir esses erros, consulte [dados de diagnóstico de computação de PaaS do Azure](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>Perguntas e respostas
**O que é o tamanho do buffer e o tamanho deve ser?**

Em cada instância de máquina virtual, as cotas limitam quantos dados de diagnóstico podem ser armazenados no sistema de arquivos local. Além disso, você pode especificar um tamanho de buffer para cada tipo de dados de diagnóstico que estão disponíveis. Esse tamanho do buffer age como uma cota individual para esse tipo de dados. Para determinar a cota geral e a quantidade de memória que permanece, consulte a parte inferior da caixa de diálogo para o tipo de dados de diagnóstico. Se você especificar buffers maiores ou mais tipos de dados, abordará a cota geral. Você pode alterar a cota geral modificando o arquivo de configuração Diagnostics. wadcfg ou. wadcfgx. Os dados de diagnóstico são armazenados no sistema de arquivos como os dados do aplicativo. Se seu aplicativo usa uma grande quantidade de espaço em disco, você não deve aumentar a cota de diagnóstico geral.

**Qual é o período de transferência, e quanto tempo deve ser?**

O período de transferência é a quantidade de tempo que decorreu data Capture. Depois de cada período de transferência, dados são movidos do sistema de arquivos local em uma máquina virtual para tabelas em sua conta de armazenamento. Se a quantidade de dados que são coletados excede a cota antes do final de um período de transferência, dados mais antigos serão descartados. Se você estiver perdendo dados porque seus dados excedem o tamanho do buffer ou a cota geral, você talvez queira diminuir o período de transferência.

**Fuso horário são os carimbos de hora em?**

Carimbos de data / hora está no fuso horário local do datacenter que hospeda seu serviço de nuvem. As seguintes colunas de carimbo de data / hora três nas tabelas de log são usadas:

* **PreciseTimeStamp**: ETW o carimbo de hora do evento. Ou seja, a hora em que o evento é registrado no cliente.
* **Carimbo de hora**: O valor para **PreciseTimeStamp** arredondado para baixo até o limite de frequência de upload. Por exemplo, se a frequência de upload é 5 minutos e o evento 00:17:12 de tempo, o carimbo de hora é 15:00:00.
* **Carimbo de hora**: O carimbo de hora em que a entidade foi criada na tabela do Azure.

**Como gerenciar custos ao coletar informações de diagnóstico?**

As configurações padrão (**nível de Log** definido como **erro**, e **período de transferência** definido como **1 minuto**) são projetados para minimizar os custos. Os custos de computação aumentam quando você coleta mais dados de diagnóstico ou se você diminuir o período de transferência. Não colete mais dados do que você precisa e não se esqueça de desabilitar a coleta de dados quando você não precisa mais dela. Você sempre poderá habilitá-lo novamente, até mesmo em tempo de execução, conforme descrito anteriormente neste artigo.

**Como coletar logs de solicitação com falha do IIS?**

Por padrão, o IIS não coleta logs de solicitação com falha. Você pode configurar o IIS para coletar logs de solicitação com falha editando o arquivo Web. config para sua função web.

**Não estou obtendo informações de rastreamento de métodos RoleEntryPoint como OnStart. O que há de errado?**

Os métodos de **RoleEntryPoint** são chamados no contexto de WAIISHost.exe, não no IIS. As informações de configuração Web. config que normalmente habilitam o rastreamento não se aplicam. Para resolver esse problema, adicione um arquivo. config ao seu projeto de função web e nomeie o arquivo para corresponder ao assembly de saída que contém o **RoleEntryPoint** código. No projeto de função da web padrão, o nome do arquivo. config deve ser Waiishost. Adicione as seguintes linhas a esse arquivo:

```
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

No **propriedades** janela, defina as **Copy to Output Directory** propriedade a ser **copiar sempre**.

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre o log de diagnóstico no Azure, consulte [habilitar o diagnóstico nos serviços de nuvem do Azure e máquinas virtuais](/azure/cloud-services/cloud-services-dotnet-diagnostics.md) e [habilitar registro em log de diagnóstico para aplicativos Web no serviço de aplicativo do Azure](/azure/app-service/web-sites-enable-diagnostic-log).

