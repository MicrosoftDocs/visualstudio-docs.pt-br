---
title: IntelliTrace | Microsoft Docs
ms.date: 09/19/2018
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
- IntelliTrace
- IntelliTrace, debugging after a crash
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4cbe14e1bf8c3a5e010e3c9e887a208b7e045b4c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536507"
---
# <a name="intellitrace-for-visual-studio-enterprise-c-visual-basic-c"></a>IntelliTrace para Visual Studio Enterprise (C#, Visual Basic, C++)

Você pode gastar menos tempo Depurando seu aplicativo ao usar o IntelliTrace para registrar e rastrear o histórico de execução do código. Você pode encontrar bugs facilmente porque o IntelliTrace permite:

- Registrar eventos específicos

- Examine o código relacionado, os dados que aparecem na janela **locais** durante os eventos do depurador e informações de chamada de função

- Depurar erros difíceis de reproduzir ou que ocorrem na implantação

Você pode usar o IntelliTrace no Visual Studio Enterprise Edition (mas não as edições Professional ou Community).

## <a name="what-do-you-want-to-do"></a>O que você deseja fazer?

|Cenário|Título|
|-|-|
|**Depurar meu aplicativo com o IntelliTrace:**<br /><br /> – Mostrar-me eventos passados.<br />– Mostrar-me informações de chamadas com eventos passados.<br />– Salvar minha sessão do IntelliTrace.<br />– Controlar os dados que são coletados pelo IntelliTrace.|- [Inspecionar os Estados do aplicativo anterior usando o IntelliTrace](../debugger/view-historical-application-state.md)<br />- [Walkthrough: usando o IntelliTrace](../debugger/walkthrough-using-intellitrace.md)<br />- [Recursos do IntelliTrace](../debugger/intellitrace-features.md)<br />- [Depuração histórica](../debugger/historical-debugging.md)|
|**Coletar dados do IntelliTrace de aplicativos implantados**|- [Usando o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md)|
|**Iniciar a depuração a partir de um arquivo de log do IntelliTrace (arquivo .iTrace).**|- [Usando dados do IntelliTrace salvos](../debugger/using-saved-intellitrace-data.md)|

## <a name="what-apps-can-i-debug-with-intellitrace"></a><a name="IntelliTraceSupport"></a> Que aplicativos posso depurar com o IntelliTrace?

| Nível de suporte| Tipos de aplicativos |
|---------------------| - |
| **Suporte completo** | -Visual Basic e aplicativos do Visual C# que usam .NET Framework 2,0 ou versões posteriores.<br/>É possível depurar a maioria dos aplicativos, inclusive ASP.NET, Microsoft Azure, Windows Forms, WCF, WPF, Windows Workflow, SharePoint 2010, SharePoint 2013 e aplicativos de 64 bits.<br/>Para depurar aplicativos do SharePoint com o IntelliTrace, consulte [Walkthrough: Depurando um aplicativo do SharePoint usando o IntelliTrace](../sharepoint/walkthrough-debugging-a-sharepoint-application-by-using-intellitrace.md).<br/> Para depurar Microsoft Azure aplicativos com o IntelliTrace, consulte [Depurando um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](../azure/vs-azure-tools-intellitrace-debug-published-cloud-services.md). |
| **Suporte limitado** | -Aplicativos C++ voltados para o suporte do Windows exibindo instantâneos usando o passo do IntelliTrace. Somente os eventos Debugger e Exception têm suporte.<br />-.NET Core e ASP.NET Core aplicativos com suporte para determinados eventos somente (eventos do controlador MVC, ADO.NET e HTTPClient) na depuração local. O coletor autônomo não tem suporte para aplicativos .NET Core ou ASP.NET Core.<br />– Aplicativos F# em uma base de avaliação<br />-Aplicativos UWP com suporte somente para eventos |
| **Sem suporte** | -Outros idiomas e script<br />-Serviços do Windows, Silverlight, Xbox ou aplicativos Windows Mobile |

> [!NOTE]
> Se desejar depurar um processo que já esteja em execução, você poderá coletar somente eventos do IntelliTrace (sem informações de chamada). Você pode anexar a um processo de 32 bits ou 64 bits somente no computador local. Os eventos que ocorrem antes de você anexar ao processo não são coletados.

## <a name="why-debug-with-intellitrace"></a><a name="IntelliTraceVSTraditional"></a> Por que depurar com o IntelliTrace?

A depuração tradicional ou *dinâmica* mostra apenas o estado atual do aplicativo, com dados limitados sobre eventos passados. Você precisa inferir esses eventos com base no estado atual do aplicativo ou precisa recriar esses eventos executando novamente seu aplicativo.

O IntelliTrace expande esta experiência tradicional de depuração ao registrar eventos específicos e os dados nesses pontos de tempo. Isso permite que você veja o que aconteceu em seu aplicativo sem reiniciá-lo, especialmente se você passar para onde o bug está. O IntelliTrace é ativado por padrão durante a depuração tradicional e coleta dados automaticamente e de forma invisível. Isso permite que você alterne facilmente entre a depuração tradicional e a depuração do IntelliTrace para consultar as informações registradas. Confira os [recursos do IntelliTrace](../debugger/intellitrace-features.md) e [quais dados o IntelliTrace coleta?](#WhatData)

O IntelliTrace também pode ajudá-lo a depurar erros que são difíceis de reproduzir ou que ocorrem na implantação. Você pode coletar dados do IntelliTrace e salvá-los em um arquivo de log do IntelliTrace (arquivo .iTrace). Um arquivo .iTrace contém detalhes sobre exceções, eventos de desempenho, solicitações da Web, dados de teste, threads, módulos e outras informações do sistema. Você pode abrir esse arquivo em Visual Studio Enterprise, selecionar um item e iniciar a depuração com o IntelliTrace. Isso permite que você vá para qualquer evento no arquivo e veja detalhes específicos sobre seu aplicativo nesse momento.

Você pode salvar dados do IntelliTrace a partir destas fontes:

- Uma sessão do IntelliTrace no Visual Studio 2015 Enterprise ou versões posteriores ou versões anteriores do Visual Studio Ultimate.

- Aplicativos Web em ASP.NET hospedados no IIS ou aplicativos SharePoint 2010 e SharePoint 2013 em execução na implantação quando você usa o Agente de Monitoramento da Microsoft, sozinhos ou com o System Center 2012. Consulte [usar o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md) e [monitoramento com Microsoft Monitoring Agent](https://technet.microsoft.com/library/dn465153.aspx).

Estes são alguns exemplos de como o IntelliTrace pode ajudar na depuração:

- Seu aplicativo danificou um arquivo de dados, mas você não sabe onde esse evento ocorreu.

  Sem o IntelliTrace, você precisa examinar o código para localizar todos os acessos de arquivo possíveis, colocar pontos de interrupção nesses acessos e executar novamente o aplicativo para descobrir onde o problema ocorreu. Com o IntelliTrace, você pode ver todos os eventos de acesso a arquivos coletados e detalhes específicos sobre seu aplicativo quando cada evento ocorreu.

- Uma exceção ocorre.

  Sem o IntelliTrace, você receberá uma mensagem sobre uma exceção, mas não terá muitas informações sobre os eventos que levaram à exceção. Você pode examinar a pilha de chamadas para ver a cadeia de chamadas que conduziu à exceção, mas não pode ver a sequência dos eventos que aconteceram durante essas chamadas. Com o IntelliTrace, você pode examinar os eventos que ocorreram antes da exceção.

- Um bug ou uma falha ocorre em um aplicativo implantado.

  Para aplicativos baseados em Microsoft Azure, você pode configurar a coleta de dados do IntelliTrace antes de publicar o aplicativo. Enquanto o aplicativo é executado, o IntelliTrace salva os dados em um arquivo. iTrace. Consulte [depurar um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](../azure/vs-azure-tools-intellitrace-debug-published-cloud-services.md).

  Para aplicativos Web em ASP.NET hospedados no IIS 7.0, 7.5 e 8.0 e aplicativos SharePoint 2010 ou SharePoint 2013, use o Agente de Monitoramento da Microsoft sozinho ou com o System Center 2012 para salvar dados do IntelliTrace em um arquivo .iTrace.

  Isso é útil quando você deseja diagnosticar problemas com os aplicativos durante a implantação. Consulte [usar o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md).

## <a name="what-data-does-intellitrace-collect"></a><a name="WhatData"></a> Que dados são coletados pelo IntelliTrace?

**Coletar informações do evento**

Por padrão, o IntelliTrace registra apenas eventos do IntelliTrace: eventos do depurador, exceções, .NET Framework eventos e outros eventos do sistema que podem ajudá-lo com a depuração. Você pode escolher os tipos de eventos do IntelliTrace que deseja coletar, exceto para eventos do depurador e exceções, os quais são coletados sempre. Consulte [recursos do IntelliTrace](../debugger/intellitrace-features.md).

- **Eventos do depurador**

  O IntelliTrace sempre registra eventos que acontecem no depurador do Visual Studio. Por exemplo, iniciar seu aplicativo é um evento do depurador. Outros eventos do depurador estão parando eventos, o que faz com que seu aplicativo interrompa a execução. Por exemplo, seu programa atinge um ponto de interrupção, atinge um ponto de controle ou executa um comando **Etapa**.

  Por padrão, para ajudar com o desempenho, o IntelliTrace não registra cada valor possível para um evento do depurador. Em vez de isso, ele registra estes valores:

  - Valores na janela **Locais**. Mantenha a janela **Locais** aberta para consultar esses valores.

  - Valores na janela **Autos** somente se a janela **Autos** estiver aberta

  - Valores em DataTips que surgem quando você move o ponteiro do mouse sobre uma variável na janela de origem para ver seu valor. O IntelliTrace não coleta valores em DataTips fixados.

    Quando os eventos do IntelliTrace e o modo de instantâneos estiverem habilitados, o IntelliTrace tirará um instantâneo do processo do aplicativo em cada evento de **etapa** e **ponto de interrupção** do depurador. Isso registrará valores nas janelas **locais**, **automáticos**e **inspecionar** , independentemente de as janelas estarem abertas ou não. Os valores em quaisquer dicas de dados fixados também serão coletados.

- **Exceções**

  O IntelliTrace registra o tipo e a mensagem de exceção para estes tipos de exceções:

  - Exceções tratadas onde a exceção é gerada e capturada

  - Exceções sem tratamento

- **Eventos do .NET Framework**

  Por padrão, o IntelliTrace registra os eventos mais comuns do .NET Framework. Por exemplo, para um <xref:System.Windows.Forms.CheckBox.CheckedChanged?displayProperty=nameWithType> evento, o IntelliTrace coleta o estado e o texto da caixa de seleção.

- **Eventos de aplicativos SharePoint 2010 e SharePoint 2013**

  Você pode registrar eventos de perfil de usuário e um subconjunto de eventos do ULS (Sistema de Registro Unificado) para os aplicativos SharePoint 2010 e 2013 que são executados fora do Visual Studio. Você pode salvar esses eventos em um arquivo de .iTrace. Requer o Visual Studio Enterprise 2015 ou versões posteriores, uma versão anterior do Visual Studio Ultimate ou [Microsoft Monitoring Agent](https://www.microsoft.com/download/details.aspx?id=40316) em execução no modo de **rastreamento** .

  Ao abrir o arquivo .iTrace, insira uma identificação de correlação do SharePoint para localizar a solicitação da Web correspondente, exibir os eventos registrados e iniciar a depuração de um evento específico. Se o arquivo contiver exceções sem tratamento, você poderá escolher uma identificação de correlação para iniciar a depuração de uma exceção.

  Consulte:

  - [Usar o coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md)

  - [Usar dados salvos do IntelliTrace](../debugger/using-saved-intellitrace-data.md)

  - [Instruções passo a passo: depurando um aplicativo do SharePoint usando o IntelliTrace](../sharepoint/walkthrough-debugging-a-sharepoint-application-by-using-intellitrace.md)

**Capturar instantâneos**

Você pode configurar o IntelliTrace para capturar instantâneos em cada ponto de interrupção e evento de etapa do depurador. O IntelliTrace registra o estado completo do aplicativo em cada instantâneo, o que permite que você exiba variáveis complexas e avalie expressões.

> [!NOTE]
> O [coletor autônomo do IntelliTrace](../debugger/using-the-intellitrace-stand-alone-collector.md) não dá suporte à captura de instantâneos.

Consulte [inspecionar os Estados do aplicativo anterior usando o IntelliTrace](../debugger/view-historical-application-state.md).

**Coletar informações de chamada de função**

Você pode configurar o IntelliTrace para coletar informações de chamada para funções. Essas informações permitem que você veja um histórico da pilha de chamadas e permitem que você percorra para frente e para trás as chamadas no código. Para cada chamada de função, o IntelliTrace registra estes dados:

- Nome da função
- Valores de tipos de dados primitivos passados como parâmetros em pontos de entrada de função e retornados em pontos de saída de função
- Valores de propriedades automáticas quando elas são lidas ou alteradas
- Ponteiros para objetos filhos de primeiro nível, mas não seus valores diferentes caso eles fossem nulos ou não

> [!NOTE]
> O IntelliTrace coleta somente os 256 primeiros objetos em matrizes e os 256 primeiros caracteres para cadeias de caracteres.

Consulte [inspecionar seu aplicativo com a depuração histórica](../debugger/historical-debugging-inspect-app.md).

**Coletar informações do módulo**

Para controlar a quantidade de informações de chamadas que o IntelliTrace coleta, especifique somente os módulos que interessem a você. Isso pode ajudar a melhorar o desempenho do seu aplicativo durante a coleta. Consulte a seção [controlar a quantidade de informações que o IntelliTrace coleta](../debugger/intellitrace-features.md#ControlCallData) nos recursos do IntelliTrace.

## <a name="will-intellitrace-slow-down-my-application"></a><a name="AffectPerformance"></a>O IntelliTrace reduzirá o meu aplicativo?

Por padrão, o IntelliTrace coleta dados somente para eventos do IntelliTrace selecionados. Isso pode ou não retardar o seu aplicativo, dependendo da estrutura e da organização do seu código. Por exemplo, se o IntelliTrace registra um evento com frequência, isso pode tornar o aplicativo mais lento. Isso também pode fazer com que você considere refatorar seu aplicativo.

Coletar informações de chamada pode retardar significativamente seu aplicativo. Ela também pode aumentar o tamanho de qualquer arquivo de log do IntelliTrace (arquivos .iTrace) que você possa estar salvando em disco. Para minimizar esses efeitos, colete informações de chamada somente para os módulos desejados.  Para alterar o tamanho máximo de seus arquivos de .iTrace, vá para **Ferramentas**, **Opções**, **IntelliTrace**, **Avançado**.

### <a name="blogs"></a>Blogs

[Microsoft DevOps](https://devblogs.microsoft.com/devops/)

### <a name="forums"></a>Fóruns

[Diagnóstico do Visual Studio](https://social.msdn.microsoft.com/Forums/en-US/home)
