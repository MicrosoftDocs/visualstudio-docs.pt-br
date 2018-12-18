---
title: Dados do IntelliTrace no Visual Studio
ms.date: 10/13/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliTrace, configuring test settings
- Diagnostic Data Adapter, InteliTrace
- debugging [Visual Studio ALM], difficult issues using IntelliTrace
- Test Runner, InteliTrace
ms.assetid: 02b6716f-569e-4961-938a-e790a0c74b5c
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 8501f141c2fdf60a57daecda33a3ff7436a16a5d
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894632"
---
# <a name="how-to-collect-intellitrace-data-to-help-debug-difficult-issues"></a>Como coletar dados do IntelliTrace para ajudar a depurar problemas difíceis

Você pode configurar o adaptador de dados de diagnóstico para que o IntelliTrace colete informações de rastreamento de diagnóstico específicas no Visual Studio. Os testes podem usar esse adaptador, o teste pode coletar eventos de diagnóstico significativos para o aplicativo que um desenvolvedor poderá usar depois para rastrear o código para encontrar a causa de um bug. O adaptador de dados de diagnóstico para IntelliTrace pode ser usado em testes manuais ou automatizados.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> IntelliTrace só funciona em um aplicativo gravado usando-se código gerenciado. Se estiver testando um aplicativo Web que use um navegador como um cliente, você não deverá habilitar o IntelliTrace para o cliente nas configurações de teste porque nenhum código gerenciado está disponível para rastreamento. Nesse caso, você talvez queira configurar um ambiente e coletar remotamente os dados do IntelliTrace em seu servidor Web.

Os dados do IntelliTrace são armazenados em um arquivo com uma extensão *.iTrace*. Ao executar o teste e uma etapa falhar, você pode criar um bug. O arquivo do IntelliTrace que contém as informações de diagnóstico é anexado automaticamente a esse bug.

> [!NOTE]
> O adaptador de dados de diagnóstico do IntelliTrace não cria um arquivo do IntelliTrace quando um passo de teste é bem-sucedido. Ele salva um arquivo somente em um caso de teste com falha ou quando você envia um bug.

Os dados coletados no arquivo do IntelliTrace aumentam a produtividade de depuração reduzindo o tempo necessário para reproduzir e diagnosticar um erro no código. Além disso, como você pode compartilhar o arquivo do IntelliTrace com outra pessoa que pode replicar a sessão local no computador, ele reduz a probabilidade de um bug não ser reproduzível.

> [!NOTE]
> Se você habilitar o IntelliTrace em suas configurações de teste, coletar dados de cobertura de código não funcionará.

> [!WARNING]
> O adaptador de dados de diagnóstico do IntelliTrace funciona com a instrumentação de um processo gerenciado, que deverá ser realizado depois que os testes da execução de teste forem carregados. Se o processo que você deseja monitorar já tiver começado, nenhum arquivo do IntelliTrace será coletado porque o processo já está em execução. Para evitar isso, certifique-se de que o processo esteja parado antes dos testes serem carregados. Inicie o processo depois que os testes forem carregados ou o primeiro teste for iniciado.

O procedimento a seguir descreve como configurar os dados do IntelliTrace que você deseja coletar. Essas etapas se aplicam ao editor de configuração no Microsoft Test Manager e à caixa de diálogo Configurações de Teste no Visual Studio.

> [!NOTE]
> A conta de usuário do agente de teste usada para coletar dados do IntelliTrace deve ser um membro do grupo Administradores. Para obter mais informações, consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).

## <a name="configure-the-data-to-collect-with-the-intellitrace-diagnostic-data-adapter"></a>Configurar os dados a serem coletados com o adaptador de dados de diagnóstico do IntelliTrace

Antes de executar as etapas nesse procedimento, você deverá abrir as configurações de teste no Microsoft Test Manager ou no Visual Studio e selecionar a página **Dados e Diagnósticos**.

### <a name="to-configure-the-data-to-collect-with-the-intellitrace-diagnostic-data-adapter"></a>Para configurar os dados a serem coletados com o adaptador de dados de diagnóstico do IntelliTrace

1.  Selecione a função a ser usada para coletar dados do IntelliTrace.

2.  Selecione **IntelliTrace**.

3.  Se estiver adicionando o IntelliTrace para uma função de cliente da Web ou para um aplicativo Web ASP.NET, você também deverá selecionar **Proxy de Cliente do ASP.NET para IntelliTrace e Impacto de Teste**.

     Esse proxy permite que você colete informações sobre as chamadas http de um cliente para um servidor Web para os adaptadores de dados de diagnóstico do IntelliTrace e de Impacto de Teste.

    > [!WARNING]
    > Se optar por usar uma conta personalizada para a identidade que está sendo usada no pool de aplicativos do IIS (Servidor de informações da Internet) onde deseja coletar dados do Intellitrace, você deverá criar o perfil de usuário local no computador do IIS para a conta personalizada que está sendo usada. Você pode criar o perfil local para a conta personalizada fazendo logon no computador do IIS localmente uma vez ou executando a seguinte linha de comando com as credenciais da conta personalizada:
    >
    > **runas /user:domain\name /profile cmd.exe**

4.  Escolha **Configurar** para o **IntelliTrace** para modificar as configurações padrão do IntelliTrace.

     A caixa de diálogo para configurar os dados que serão coletados é exibida.

    > [!WARNING]
    > Se você habilitar a coleta de dados do IntelliTrace, a coleta de dados de cobertura de código não funcionará.

5.  Escolha a guia **Geral**. Selecione **Apenas eventos do IntelliTrace** para registrar eventos de diagnóstico significativos que tenham impacto mínimo sobre o desempenho durante o teste.

     -ou-

     Selecione **Eventos do IntelliTrace e informações de chamada** para registrar eventos de diagnóstico e rastreamento no nível de método que mostram informações de chamada. Esse nível de rastreamento pode afetar o desempenho quando você executa os testes.

6.  Para coletar dados do aplicativo ASP.NET em execução nos Serviços de Informações da Internet, selecione **Coletar dados de aplicativos ASP.NET em execução nos Serviços de Informações da Internet**. Configure o agente de teste na função servidor Web. Consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).

7.  Escolha a guia **Módulos**. Selecione **Coletar dados de todos os módulos, exceto os seguintes** e use **Adicionar** para adicionar à lista de módulos e **Remover** para remover um módulo. Essa opção permite incluir todos os módulos em execução no sistema, exceto os módulos que você especifica.

     -ou-

     Selecione **Coletar dados apenas dos módulos a seguir** e use **Adicionar** para adicionar à lista de módulos e **Remover** para remover um módulo. Essa opção permite especificar exatamente quais módulos você deseja.

    > [!NOTE]
    > Se possível, selecione os processos específicos que deseja monitorar. Isso é recomendado para ter o desempenho ideal.

8.  Escolha a guia **Processos**. Selecione **Coletar dados de todos os processos, exceto os seguintes** e use **Adicionar** para adicionar à lista de processos e **Remover** para remover um processo. Essa opção permite incluir todos os processos em execução no sistema, exceto os processos que você especifica.

     -ou-

     Selecione **Coletar dados apenas nos processos especificados** e use **Adicionar** para adicionar à lista de processos e **Remover** para remover um processo. Essa opção permite especificar exatamente quais processos você deseja.

9. (Opcional) Escolha a guia **Eventos do IntelliTrace**. Marque ou desmarque cada categoria de evento do IntelliTrace que você deseja incluir ou excluir ao coletar eventos de diagnóstico.

10. (Opcional) Expanda cada categoria de evento do IntelliTrace e marque ou desmarque cada evento específico que você deseja incluir ou excluir nos eventos do IntelliTrace.

11. (Opcional) Escolha a guia **Avançado**. Em seguida, escolha a seta ao lado de **Quantidade de espaço máximo em disco para registro** e selecione o tamanho máximo que você deseja habilitar para o arquivo do IntelliTrace a ser usado.

    > [!NOTE]
    > Se você aumentar o tamanho do registro, um problema de tempo limite poderá ocorrer quando você salvar esse registro com seus resultados de análise.

12. Se estiver usando o Microsoft Test Manager, escolha **Salvar**. Se estiver usando o Visual Studio, escolha **OK**. As configurações do IntelliTrace agora estão definidas e salvas em suas configurações de teste.

    > [!NOTE]
    > Para redefinir a configuração desse adaptador de dados de diagnóstico, escolha **Restaurar configuração padrão** para o Visual Studio ou **Redefinir como padrão** para o Microsoft Test Manager.

## <a name="see-also"></a>Consulte também

- [Coletar dados de diagnóstico durante testes (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts)
- [Coletar dados de diagnóstico em testes manuais (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)
- [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md)
- [Coletar dados do IntelliTrace](../test/how-to-collect-intellitrace-data-to-help-debug-difficult-issues.md)