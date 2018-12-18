---
title: IntelliTrace | Microsoft Docs
ms.custom: ''
ms.date: 09/19/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.historicaldebug.overview
helpviewer_keywords:
- debugger, recording execution history
- debugging, recording execution history
- IntelliTrace [Visual Studio ALM]
- IntelliTrace, debugging applications
- debugger, (See also IntelliTrace [Visual Studio ALM])
- debugging, (See also IntelliTrace [Visual Studio ALM])
- IntelliTrace, collecting data from Test Manager
- IntelliTrace
- Test Manager, debugging with IntelliTrace
- IntelliTrace, debugging after a crash
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e2ee2e3662e550e013b2f8436cc32ee9585a419d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49825407"
---
# <a name="intellitrace"></a>IntelliTrace

Você pode gastar menos tempo depurando seu aplicativo ao usar o IntelliTrace para registrar e rastrear o histórico de execução do seu código. Você pode localizar bugs facilmente, porque o IntelliTrace permite:

- Registrar eventos específicos

   Examinar o código relacionado, dados que aparecem na **Locals** janela durante eventos do depurador e informações de chamada de função

- Depurar erros que são difíceis de reproduzir ou que ocorrem na implantação

Você pode usar o IntelliTrace no Visual Studio Enterprise edition (mas não as edições Professional ou Community).

## <a name="what-do-you-want-to-do"></a>O que você deseja fazer?

|||
|-|-|
|**Depure meu aplicativo com o IntelliTrace:**<br /><br /> -Mostre eventos anteriores.<br />-Mostrar-me informações de chamadas com eventos passados.<br />-Salve minha sessão do IntelliTrace.<br />-Controle os dados que o IntelliTrace coleta.|- [Inspecione o estado anterior do aplicativo usando o IntelliTrace](../debugger/view-historical-application-state.md)<br />- [Passo a passo: Usando o IntelliTrace](../debugger/walkthrough-using-intellitrace.md)<br />- [Recursos do IntelliTrace](../debugger/intellitrace-features.md)<br />- [Histórico de depuração](../debugger/historical-debugging.md)|
|**Coletar dados do IntelliTrace durante uma sessão de teste no Test Manager**|- [Coletar mais dados de diagnóstico em testes manuais](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)|
|**Coletar dados do IntelliTrace de aplicativos implantados**|- [Usando o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md)|
|**Inicie a depuração de um arquivo de log do IntelliTrace (arquivo. itrace).**|- [Usando dados salvos do IntelliTrace](../debugger/using-saved-intellitrace-data.md)|

## <a name="IntelliTraceSupport"></a> Quais aplicativos posso depurar com o IntelliTrace?

| | |
|---------------------| - |
| **Suporte completo** | – Aplicativos Visual Basic e Visual c# que usam o .NET Framework 2.0 ou versões superiores.<br/>É possível depurar a maioria dos aplicativos, inclusive ASP.NET, Microsoft Azure, Windows Forms, WCF, WPF, Windows Workflow, SharePoint 2010, SharePoint 2013 e aplicativos de 64 bits.<br/>Para depurar aplicativos do SharePoint com o IntelliTrace, consulte [instruções passo a passo: depurando um aplicativo do SharePoint usando o IntelliTrace](../sharepoint/walkthrough-debugging-a-sharepoint-application-by-using-intellitrace.md).<br/> Para depurar aplicativos do Microsoft Azure com o IntelliTrace, consulte [depurando um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](/azure/vs-azure-tools-intellitrace-debug-published-cloud-services). |
| **Suporte limitado** | -Direcionamento de suporte do Windows exibir instantâneos usando o retrocesso do IntelliTrace de aplicativos nativos. Há suporte para apenas os eventos de depurador e a exceção.<br />-.NET core e aplicativos ASP.NET Core tem suporte para determinados os eventos somente controlador MVC, ADO.NET e HTTPClicent na depuração local. Não há suporte para o coletor autônomo para aplicativos .NET Core ou ASP.NET Core.<br />-Aplicativos F # em uma base de avaliação<br />-Aplicativos UWP com suporte somente para eventos |
| **Não tem suporte** | -Outras linguagens e script<br />-Windows Services, Silverlight, Xbox ou [!INCLUDE[winmobile](../debugger/includes/winmobile_md.md)] aplicativos |

> [!NOTE]
> Se você quiser depurar um processo que já está em execução, você pode coletar somente eventos do IntelliTrace (nenhuma informação de chamada). Você pode anexar a um processo de 32 bits ou 64 bits no computador local. Eventos que ocorrem antes de anexar ao processo não são coletados.

##  <a name="IntelliTraceVSTraditional"></a> Por que depurar com o IntelliTrace?

Tradicional ou *live* depuração mostra apenas o estado do aplicativo atual, com dados limitados sobre eventos passados. Você terá que interpretar esses eventos com base no estado atual do aplicativo, ou você precisa recriar esses eventos ao executar novamente o seu aplicativo.

O IntelliTrace expande esta experiência tradicional de depuração ao registrar eventos específicos e os dados nesses pontos de tempo. Isso permite que você veja o que aconteceu no seu aplicativo sem reiniciá-lo, especialmente se você passar pelo onde está o bug. O IntelliTrace é ativado por padrão durante a depuração tradicional e coleta dados automaticamente e de forma invisível. Isso permite que você alterne facilmente entre a depuração tradicional e a depuração do IntelliTrace para consultar as informações registradas. Ver [recursos do IntelliTrace](../debugger/intellitrace-features.md) e [quais dados são coletados pelo IntelliTrace?](#WhatData)

O IntelliTrace também pode ajudá-lo a depurar erros que são difíceis de reproduzir ou que ocorrem na implantação. Você pode coletar dados do IntelliTrace e salvá-los em um arquivo de log do IntelliTrace (arquivo .iTrace). Um arquivo .iTrace contém detalhes sobre exceções, eventos de desempenho, solicitações da Web, dados de teste, threads, módulos e outras informações do sistema. Você pode abrir este arquivo no Visual Studio Enterprise, selecione um item e iniciar a depuração com o IntelliTrace. Isso permite que você acesse qualquer evento no arquivo e ver detalhes específicos sobre seu aplicativo no momento.

Você pode salvar dados do IntelliTrace a partir destas fontes:

- Uma sessão do IntelliTrace no Visual Studio 2017 Enterprise, Visual Studio 2015 Enterprise ou em versões anteriores do Visual Studio Ultimate.

- Uma sessão de teste no Microsoft Test Manager

- Aplicativos Web em ASP.NET hospedados no IIS ou aplicativos SharePoint 2010 e SharePoint 2013 em execução na implantação quando você usa o Agente de Monitoramento da Microsoft, sozinhos ou com o System Center 2012. Ver [usar o coletor autônomo IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md) e [monitorando com o Microsoft Monitoring Agent](http://technet.microsoft.com/library/dn465153.aspx).

  Estes são alguns exemplos de como o IntelliTrace pode ajudar na depuração:

- O aplicativo corrompeu um arquivo de dados, mas você não sabe onde esse evento ocorreu.

     Sem o IntelliTrace, você precisará examinar o código para localizar todos os possíveis acessos de arquivo, coloque os pontos de interrupção nesses acessos e executar novamente o seu aplicativo para localizar onde ocorreu o problema. Com o IntelliTrace, você pode ver todos os eventos de acesso a arquivo coletados e detalhes específicos sobre seu aplicativo quando cada evento ocorreu.

- Uma exceção ocorre.

     Sem o IntelliTrace, você receberá uma mensagem sobre uma exceção, mas você não tem muitas informações sobre os eventos que levaram à exceção. Você pode examinar a pilha de chamadas para ver a cadeia de chamadas que conduziu à exceção, mas não é possível ver a sequência de eventos que aconteceram durante essas chamadas. Com o IntelliTrace, você pode examinar os eventos que ocorreram antes da exceção.

- Seu aplicativo falha em um computador de teste, mas é executado com êxito em um computador de desenvolvimento.

     Você pode coletar dados do IntelliTrace do Microsoft Test Manager, salvar os dados em um arquivo .iTrace e anexar esse arquivo a um item de trabalho do Team Foundation Server para investigação posterior. Ver [coletar mais dados de diagnóstico em testes manuais](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts) e [Use dados salvos do IntelliTrace](../debugger/using-saved-intellitrace-data.md).

- Um bug ou uma falha ocorre em um aplicativo implantado.

     Para aplicativos baseados no Azure da Microsoft, você pode configurar a coleta de dados do IntelliTrace antes de publicar o aplicativo. Enquanto seu aplicativo é executado, o IntelliTrace salva dados em um arquivo. itrace. Ver [depurar um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](http://go.microsoft.com/fwlink/?LinkID=262248).

     Para aplicativos Web em ASP.NET hospedados no IIS 7.0, 7.5 e 8.0 e aplicativos SharePoint 2010 ou SharePoint 2013, use o Agente de Monitoramento da Microsoft sozinho ou com o System Center 2012 para salvar dados do IntelliTrace em um arquivo .iTrace.

     Isso é útil quando você deseja diagnosticar problemas com os aplicativos durante a implantação. Ver [usar o coletor autônomo IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md).

##  <a name="WhatData"></a> Que dados são coletados pelo IntelliTrace?

**Coletar informações de evento**

Por padrão, o IntelliTrace registra apenas eventos do IntelliTrace: eventos, exceções, eventos do .NET Framework e outros eventos do sistema que podem ajudar você com a depuração do depurador. Você pode escolher os tipos de eventos do IntelliTrace que deseja coletar, exceto para eventos do depurador e exceções, os quais são coletados sempre. Ver [recursos do IntelliTrace](../debugger/intellitrace-features.md).

- **Eventos do depurador**

     O IntelliTrace sempre registra eventos que acontecem no depurador do Visual Studio. Por exemplo, iniciar seu aplicativo é um evento do depurador. Outros eventos do depurador estão interrompendo eventos, o que fazer com que seu aplicativo para interromper a execução. Por exemplo, seu programa atinge um ponto de interrupção, atinge um tracepoint ou executa um **etapa** comando.

     Por padrão, para ajudar no desempenho, IntelliTrace não registra todos os valores possíveis para um evento do depurador. Em vez de isso, ele registra estes valores:

  - Os valores na **Locals** janela. Manter o **Locals** janela aberta para consultar esses valores.

  - Os valores na **Autos** somente se de janela a **Autos** janela está aberta

  - Valores em DataTips que surgem quando você move o ponteiro do mouse sobre uma variável na janela de origem para ver seu valor. O IntelliTrace não coleta valores em DataTips fixados.

    Quando o modo de eventos do IntelliTrace e de instantâneos está habilitado, o IntelliTrace será tirar um instantâneo do processo do aplicativo em cada depurador **ponto de interrupção** e **etapa** eventos. Isso registrará os valores na **Locals**, **Autos**, e **Assista** windows, independentemente se as janelas estão abertas ou não. Valores em quaisquer dicas de dados fixos também serão coletados.

- **Exceções**

     O IntelliTrace registra o tipo e a mensagem de exceção para estes tipos de exceções:

    - Exceções tratadas onde a exceção é gerada e capturada

    - Exceções sem tratamento

- **Eventos do .NET framework**

   Por padrão, o IntelliTrace registra os eventos mais comuns do .NET Framework. Por exemplo, ror um evento de caixa de seleção verificar, o IntelliTrace coleta o estado da caixa de seleção e o texto.

- **Eventos de aplicativo do SharePoint 2010 e SharePoint 2013**

     Você pode registrar eventos de perfil de usuário e um subconjunto de eventos do ULS (Sistema de Registro Unificado) para os aplicativos SharePoint 2010 e 2013 que são executados fora do Visual Studio. Você pode salvar esses eventos em um arquivo de .iTrace. Requer o Visual Studio Enterprise 2017, Visual Studio Enterprise 2015, uma versão anterior do Visual Studio Ultimate, ou [Microsoft Monitoring Agent](http://go.microsoft.com/fwlink/?LinkId=320384) em execução no **rastreamento** modo.

     Ao abrir o arquivo .iTrace, insira uma identificação de correlação do SharePoint para localizar a solicitação da Web correspondente, exibir os eventos registrados e iniciar a depuração de um evento específico. Se o arquivo contiver exceções sem tratamento, você poderá escolher uma identificação de correlação para iniciar a depuração de uma exceção.

     Consulte:

    - [Usar o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md)

    - [Usar dados salvos do IntelliTrace](../debugger/using-saved-intellitrace-data.md)

    - [Instruções passo a passo: depurando um aplicativo do SharePoint usando o IntelliTrace](../sharepoint/walkthrough-debugging-a-sharepoint-application-by-using-intellitrace.md)

**Capturar instantâneos**

Você pode configurar o IntelliTrace para capturar instantâneos em cada ponto de interrupção e evento de etapa do depurador. O IntelliTrace registra o estado do aplicativo completo em cada instantâneo, que permite a você exibir variáveis complexas e avaliar expressões.

Ver [inspecionar estados anteriores do aplicativo usando o IntelliTrace](../debugger/view-historical-application-state.md).

**Coletar informações de chamada de função**

Você pode configurar o IntelliTrace para coletar informações de chamada para funções. Essas informações permitem que você veja um histórico da pilha de chamadas e permitem que você percorra para frente e para trás as chamadas no código. Para cada chamada de função, o IntelliTrace registra estes dados:

- Nome da função
- Valores de tipos de dados primitivos passados como parâmetros em pontos de entrada de função e retornados em pontos de saída de função
- Valores de propriedades automáticas quando elas são lidas ou alteradas
- Ponteiros para objetos filhos de primeiro nível, mas não seus valores diferentes caso eles fossem nulos ou não

> [!NOTE]
> O IntelliTrace coleta somente os 256 primeiros objetos em matrizes e os 256 primeiros caracteres para cadeias de caracteres.

Ver [inspecionar seu aplicativo com o histórico de depuração](../debugger/historical-debugging-inspect-app.md).

**Coletar informações de módulo**

Para controlar a quantidade de informações de chamadas que o IntelliTrace coleta, especifique somente os módulos que interessem a você. Isso pode ajudar a melhorar o desempenho do seu aplicativo durante a coleta. Consulte a seção [controlar a quantidade de informações do IntelliTrace coleta](../debugger/intellitrace-features.md#ControlCallData) em recursos do IntelliTrace.

## <a name="AffectPerformance"></a> IntelliTrace faz com que velocidade meu aplicativo?

Por padrão, o IntelliTrace coleta dados somente para eventos do IntelliTrace selecionados. Isso pode ou não pode causar lentidão na seu aplicativo, dependendo da estrutura e organização do seu código. Por exemplo, se o IntelliTrace registra um evento muitas vezes, isso pode retardar o aplicativo. Ele também pode fazer você considerar refatorar seu aplicativo.

A coleta de informações de chamada pode significativamente mais lento seu aplicativo. Ela também pode aumentar o tamanho de qualquer arquivo de log do IntelliTrace (arquivos .iTrace) que você possa estar salvando em disco. Para minimizar esses efeitos, colete informações de chamada somente para os módulos desejados.  Para alterar o tamanho máximo dos seus arquivos. itrace, vá para **ferramentas**, **opções**, **IntelliTrace**, **avançado**.

## <a name="in-this-section"></a>Nesta seção

[Recursos do IntelliTrace](../debugger/intellitrace-features.md)

[Diagnosticar problemas após a implantação](../debugger/diagnose-problems-after-deployment.md)

[Usar dados salvos do IntelliTrace](../debugger/using-saved-intellitrace-data.md)

### <a name="blogs"></a>Blogs

[Microsoft DevOps](https://blogs.msdn.microsoft.com/devops/)

### <a name="forums"></a>Fóruns

[Diagnóstico do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=262263)
