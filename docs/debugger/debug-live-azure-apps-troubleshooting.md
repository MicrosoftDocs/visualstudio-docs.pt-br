---
title: Solucionar problemas de depuração de instantâneos | Microsoft Docs
description: Entenda a solução de problemas e problemas conhecidos para depuração de instantâneos Visual Studio. Carregue ICorProfiler sem causar tempo de inatividade em seu site de produção.
ms.custom: SEO-VS-2020
ms.date: 04/24/2019
ms.topic: troubleshooting
helpviewer_keywords:
- debugger
ms.assetid: 511a0697-c68a-4988-9e29-8d0166ca044a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: aad883ac0c3f703b2d6a4e10d3a0ef2468cd8465
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798434"
---
# <a name="troubleshooting-and-known-issues-for-snapshot-debugging-in-visual-studio"></a>Solução de problemas e problemas conhecidos da depuração de instantâneos no Visual Studio

Se as etapas descritas neste artigo não resolverem [](https://aka.ms/feedback/suggest?space=8) o problema, pesquise o problema no Developer Community ou reporte um novo problema escolhendo Ajuda para enviar comentários relatar um problema  >    >   Visual Studio.

## <a name="issue-attach-snapshot-debugger-encounters-an-http-status-code-error"></a>Problema: "Anexar Depurador de Instantâneos" encontra um erro de código de status HTTP

Se você vir o seguinte erro na **janela** Saída durante a tentativa de anexação, pode ser um problema conhecido listado abaixo. Experimente as soluções propostas e, se o problema continuar a persistir, entre em contato com o alias anterior.

`[TIMESTAMP] Error --- Unable to Start Snapshot Debugger - Attach Snapshot Debugger failed: System.Net.WebException: The remote server returned an error: (###) XXXXXX`

### <a name="401-unauthorized"></a>(401) Não autorizado

Esse erro indica que a chamada REST emitida pelo Visual Studio para o Azure usa uma credencial inválida. 

Siga estas etapas:

* Certifique-se de que sua Visual Studio de personalização do banco de dados tenha permissões para a assinatura e o recurso do Azure ao que você está anexando. Uma maneira rápida de determinar isso é verificar se o recurso está disponível na caixa de diálogo de **Anexação** de  >  **Depuração Depurador de Instantâneos...**  >  **Recurso do Azure**  >  **Selecione Existente ou** no Cloud Explorer.
* Se esse erro persistir, use um dos canais de comentários descritos no início deste artigo.

Se você habilitar a Autenticação/Autorização (EasyAuth) em seu Serviço de Aplicativo, poderá encontrar um erro 401 com LaunchAgentAsync na mensagem de erro da pilha de chamada. Verifique  se a ação a ser tomada quando a solicitação não está autenticada está definida como Permitir solicitações anônimas **(sem ação)** no portal do Azure e forneça um authorization.json em D:\Home\sites\wwwroot com o conteúdo a seguir. 

```
{
  "routes": [
    {
      "path_prefix": "/",
      "policies": {
        "unauthenticated_action": "RedirectToLoginPage"
      }
    },
    {
      "http_methods": [ "POST" ],
      "path_prefix": "/41C07CED-2E08-4609-9D9F-882468261608/api/agent",
      "policies": {
        "unauthenticated_action": "AllowAnonymous"
      }
    }
  ]
}
```

A primeira rota efetivamente protegerá seu domínio de aplicativo semelhante a Fazer **logoff com [IdentityProvider]**. A segunda rota expõe o ponto de extremidade SnapshotDebugger AgentLaunch fora da autenticação, que executa a ação predefinida de iniciar o agente de diagnóstico SnapshotDebugger *somente se* a extensão de site pré-instalada do SnapshotDebugger estiver habilitada para seu serviço de aplicativo. Para obter mais detalhes sobre o authorization.jssobre configuração, consulte [regras de autorização de URL](https://azure.github.io/AppService/2016/11/17/URL-Authorization-Rules.html).

### <a name="403-forbidden"></a>(403) Proibido

Esse erro indica que a permissão foi negada. Isso pode ser causado por muitos problemas diferentes.

Siga estas etapas:

* Verifique se sua conta do Visual Studio tem uma assinatura válida do Azure com as permissões de RBAC (controle de acesso Role-Based) necessárias para o recurso. Para AppService, verifique se você tem permissões para [consultar](/rest/api/appservice/appserviceplans/get) o plano do serviço de aplicativo que hospeda seu aplicativo.
* Verifique se o carimbo de data/hora do computador cliente está correto e atualizado. Os servidores com carimbos de data/hora em mais de 15 minutos do carimbo de hora da solicitação geralmente produzem esse erro.
* Se esse erro continuar a persistir, use um dos canais de comentários descritos no início deste artigo.

### <a name="404-not-found"></a>(404) não encontrado

Esse erro indica que o site não pôde ser encontrado no servidor.

Siga estas etapas:

* Verifique se você tem um site implantado e em execução no recurso de serviço de aplicativo ao qual você está anexando.
* Verifique se o site está disponível em https:// \<resource\> . azurewebsites.net
* Verifique se o aplicativo Web personalizado em execução correta não retorna um código de status 404 quando acessado em https:// \<resource\> . azurewebsites.net
* Se esse erro continuar a persistir, use um dos canais de comentários descritos no início deste artigo.

### <a name="406-not-acceptable"></a>(406) não aceitável

Esse erro indica que o servidor não pode responder ao tipo definido no cabeçalho Accept da solicitação.

Siga estas etapas:

* Verifique se seu site está disponível em https:// \<resource\> . azurewebsites.net
* Verifique se o site não foi migrado para novas instâncias. Depurador de Instantâneos usa a noção de ARRAffinity para rotear solicitações para instâncias específicas que podem produzir esse erro intermitentemente.
* Se esse erro persistir, use um dos canais de comentários descritos no início deste artigo.

### <a name="409-conflict"></a>(409) Conflito

Esse erro indica que a solicitação está em conflito com o estado do servidor atual.

Esse é um problema conhecido que ocorre quando um usuário tenta anexar Depurador de Instantâneos a um AppService que habilitar o ApplicationInsights. O ApplicationInsights define as AppSettings com um uso de Visual Studio, causando esse problema.

::: moniker range=">= vs-2019"
Isso foi resolvido em Visual Studio 2019.
::: moniker-end

Siga estas etapas:

::: moniker range="vs-2017"

* Verifique no portal do Azure se as AppSettings para SnapshotDebugger (SNAPSHOTDEBUGGER_EXTENSION_VERSION) e InstrumentationEngine (INSTRUMENTATIONENGINE_EXTENSION_VERSION) estão em letras maiúsculas. Caso não, atualize as configurações manualmente, o que força a reinicialização do site.
::: moniker-end
* Se esse erro persistir, use um dos canais de comentários descritos no início deste artigo.

### <a name="500-internal-server-error"></a>(500) Erro interno do servidor

Esse erro indica que o site está completamente inoossado ou que o servidor não pode lidar com a solicitação. Depurador de Instantâneos funções somente em aplicativos em execução. [Application Insights Depurador de Instantâneos](/azure/azure-monitor/app/snapshot-debugger) fornece instantâneos em exceções e pode ser a melhor ferramenta para suas necessidades.

### <a name="502-bad-gateway"></a>(502) Gateway ruim

Esse erro indica um problema de rede do lado do servidor e pode ser temporário.

Siga estas etapas:

* Tente aguardar alguns minutos antes de anexar o Depurador de Instantâneos novamente.
* Se esse erro persistir, use um dos canais de comentários descritos no início deste artigo.

## <a name="issue-snappoint-does-not-turn-on"></a>Problema: o snappoint não é ativado

Se você vir um ícone de aviso Ícone de aviso do ![snappoint](../debugger/media/snapshot-troubleshooting-snappoint-warning-icon.png "Ícone de aviso do Snappoint") com o snappoint em vez do ícone de snappoint normal, o snappoint não será ligado.

![O Snappoint não é a ligar](../debugger/media/snapshot-troubleshooting-dont-turn-on.png "Snappoint não ativa")

Siga estas etapas:

1. Certifique-se de ter a mesma versão do código-fonte que foi usada para criar e implantar seu aplicativo. Verifique se que você está carregando os símbolos corretos para sua implantação. Para isso, exiba a janela **Módulos** durante a depuração de instantâneos e verifique se a coluna Arquivo de Símbolos mostra um arquivo .pdb carregado para o módulo que você está depurando. O Depurador de Instantâneos tentará baixar automaticamente e usar os símbolos em sua implantação.

## <a name="issue-symbols-do-not-load-when-i-open-a-snapshot"></a>Problema: os símbolos não são carregados quando eu abro um instantâneo

Se você vir a janela a seguir, significa que os símbolos não foram carregados.

![Os símbolos não são carregados](../debugger/media/snapshot-troubleshooting-symbols-wont-load.png "Os símbolos não são carregados")

Siga estas etapas:

- Clique em **Alterar Configurações de Símbolo…** nesta página. Nas configurações **Depuração > Símbolos**, adicione um diretório de cache de símbolos. Reinicie a depuração de instantâneos depois que o caminho de símbolos for definido.

   Os símbolos ou arquivos .pdb disponíveis em seu projeto devem corresponder à sua implantação do Serviço de Aplicativo. A maioria das implantações (implantação por meio do Visual Studio, CI/CD com Azure Pipelines ou Kudu etc.) publicará os arquivos de símbolos no seu Serviço de Aplicativo. A definição do diretório de cache de símbolos permite que o Visual Studio use esses símbolos.

   ![Configurações de símbolo](../debugger/media/snapshot-troubleshooting-symbol-settings.png "Configurações de símbolo")

- Como alternativa, se sua organização usa um servidor de símbolos ou deixa os símbolos em um caminho diferente, use as configurações de símbolo para carregar os símbolos corretos para sua implantação.

## <a name="issue-i-cannot-see-the-attach-snapshot-debugger-option-in-the-cloud-explorer"></a>Problema: não consigo ver a opção "Anexar Depurador de Instantâneos" no Cloud Explorer

Siga estas etapas:

- Verifique se o componente do Depurador de Instantâneos está instalado. Abra o Instalador do Visual Studio e marque o componente **Depurador de Instantâneos** na carga de trabalho do Azure.
::: moniker range="< vs-2019"
- Verifique se há suporte para o seu aplicativo. Atualmente, há suporte apenas para aplicativos ASP.NET (4.6.1+) e ASP.NET Core (2.0+) implementados nos Serviços de Aplicativos do Azure.
::: moniker-end
::: moniker range=">= vs-2019"
- Verifique se há suporte para o seu aplicativo:
  - Serviços de Aplicativos do Azure – Aplicativos ASP.NET em execução no .NET Framework 4.6.1 ou posterior.
  - Serviços de Aplicativos do Azure – Aplicativos ASP.NET Core em execução no .NET Core 2.0 ou posterior no Windows.
  - Máquinas Virtuais do Azure (e conjunto de dimensionamento de máquinas virtuais) – aplicativos ASP.NET em execução no .NET Framework 4.6.1 ou posterior.
  - Máquinas Virtuais do Azure (e conjunto de dimensionamento de máquinas virtuais) – aplicativos ASP.NET Core em execução no .NET Core 2.0 ou posterior no Windows.
  - Serviços de Kubernetes do Azure – Aplicativos ASP.NET Core em execução no .NET Core 2.2 ou posterior no Debian 9.
  - Serviços de Kubernetes do Azure – Aplicativos ASP.NET Core em execução no .NET Core 2.2 ou posterior no Alpine 3.8.
  - Serviços de Kubernetes do Azure – Aplicativos ASP.NET Core em execução no .NET Core 2.2 ou posterior no Ubuntu 18.04.
::: moniker-end

## <a name="issue-i-only-see-throttled-snapshots-in-the-diagnostic-tools"></a>Problema: vejo apenas instantâneos limitados nas Ferramentas de Diagnóstico

![Snappoint limitada](../debugger/media/snapshot-troubleshooting-throttled-snapshots.png "Snappoint limitada")

Siga estas etapas:

- Instantâneos ocupam pouca memória, mas têm um custo de confirmação. Se o Depurador de Instantâneos detectar que o servidor está sob carga pesada de memória, ele não fará a captura de instantâneos. Para excluir instantâneos já capturados, interrompa a sessão do Depurador de Instantâneos e tente novamente.

::: moniker range=">= vs-2019"
## <a name="issue-snapshot-debugging-with-multiple-versions-of-the-visual-studio-gives-me-errors"></a>Problema: a depuração de instantâneos com várias versões do Visual Studio apresenta erros

O Visual Studio 2019 requer uma versão mais recente do Depurador de Instantâneos extensão de site em seu serviço de Azure App.  Esta versão não é compatível com a versão mais antiga do Depurador de Instantâneos a extensão de site usada pelo Visual Studio 2017.  Você receberá o erro a seguir se tentar anexar o Depurador de Instantâneos no Visual Studio 2019 a um serviço Azure App que foi previamente depurado pelo Depurador de Instantâneos no Visual Studio 2017:

![Depurador de Instantâneos de extensão de site incompatível no Visual Studio 2019](../debugger/media/snapshot-troubleshooting-incompatible-vs2019.png "Depurador de Instantâneos de extensão de site incompatível no Visual Studio 2019")

Por outro lado, se você usar o Visual Studio 2017 para anexar o Depurador de Instantâneos a um serviço de Azure App que foi previamente depurado pelo Depurador de Instantâneos no Visual Studio 2019, você obterá o seguinte erro:

![Depurador de Instantâneos de extensão de site incompatível no Visual Studio 2017](../debugger/media/snapshot-troubleshooting-incompatible-vs2017.png "Depurador de Instantâneos de extensão de site incompatível no Visual Studio 2017")

Para corrigir esse problema, exclua as seguintes configurações de aplicativo no portal do Azure e anexe o Depurador de Instantâneos novamente:

- INSTRUMENTATIONENGINE_EXTENSION_VERSION
- SNAPSHOTDEBUGGER_EXTENSION_VERSION
::: moniker-end

## <a name="issue-i-am-having-problems-snapshot-debugging-and-i-need-to-enable-more-logging"></a>Problema: estou com problemas para depurar instantâneos e preciso habilitar mais registro em log

### <a name="enable-agent-logs"></a>Habilitar logs de agente

Para habilitar e desabilitar o registro em log do agente em log, abra o Visual Studio, navegue até *Ferramentas > Opções > Depurador de instantâneos > Habilitar registro em log do agente*. Se *Excluir logs de agente antigos no início da sessão* também estiver habilitado, cada anexo bem-sucedido do Visual Studio excluirá os logs de agente anteriores.

Logs de agente podem ser encontrados nos seguintes locais:

- Serviços de Aplicativos:
  - Navegue até o site do Kudu do Serviço de Aplicativo (ou seja, seu serviçodeaplicativo.**scm**.azurewebsites.net) e vá até o Console de Depuração.
  - Os logs de agente são armazenados no seguinte diretório: D:\home\LogFiles\SiteExtensions\DiagnosticsAgentLogs\
- VM/VMSS:
  - Entre em sua VM, os logs de agente são armazenados da seguinte maneira: C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics \<Version> \ SnapshotDebuggerAgent_ *. txt
- AKS
  - Navegue até o diretório a seguir: /tmp/diag/AgentLogs/*

### <a name="enable-profilerinstrumentation-logs"></a>Habilitar logs de instrumentação/Profiler

Logs de instrumentação podem ser encontrados nos seguintes locais:

- Serviços de Aplicativos:
  - O log de erros é enviado automaticamente para D:\Home\LogFiles\eventlog.xml, os eventos são marcados com `<Provider Name="Instrumentation Engine" />` ou "pontos de interrupção de produção"
- VM/VMSS:
  - Entre em sua VM e abra o Visualizador de Eventos.
  - Abra a exibição a seguir: *Logs do Windows > Aplicativo*.
  - *Filtrar Log Atual* por *Origem do Evento* usando *Pontos de Interrupção de Produção* ou *Mecanismo de Instrumentação*.
- AKS
  - Logs de mecanismo de instrumentação em /tmp/diag/log.txt /tmp/diag/log.txt (defina MicrosoftInstrumentationEngine_FileLogPath no DockerFile)
  - Log de ponto de interrupção de produção em /tmp/diag/shLog.txt

## <a name="known-issues"></a>Problemas conhecidos

- Atualmente, não há suporte para a depuração de instantâneos com vários clientes do Visual Studio no mesmo Serviço de Aplicativo.
- Otimizações Roslyn IL não têm suporte total em projetos ASP.NET Core. Para alguns projetos ASP.NET Core, talvez não seja possível ver algumas variáveis ou usar algumas variáveis em instruções condicionais.
- Variáveis especiais, como *$FUNCTION* ou *$CALLER*, não podem ser avaliadas em instruções condicionais ou logpoints para projetos ASP.NET Core.
- A depuração de instantâneos não funciona nos Serviços de Aplicativos com [Cache Local](/azure/app-service/app-service-local-cache) ativado.
- Atualmente, não há suporte para Aplicativos de API de depuração de instantâneos.

## <a name="site-extension-upgrade"></a>Atualização de extensão de site

A depuração de instantâneos e o Application Insights dependem de um ICorProfiler, que é carregado no processo do site e causa problemas de bloqueio de arquivo durante a atualização. Esse processo é recomendável para garantir que não haja tempo de inatividade em seu site de produção.

- Crie um [Slot de implantação](/azure/app-service/web-sites-staged-publishing) dentro de seu Serviço de Aplicativo e implante seu site no slot.
- Troque o Slot com a produção do Cloud Explorer no Visual Studio ou do portal do Azure.
- Interrompa o site do Slot. Levará alguns segundos para eliminar o processo de w3wp.exe do site de todas as instâncias.
- Atualize a extensão de site do Slot no site do Kudu ou no portal do Azure (*Folha de Serviço de Aplicativo > Ferramentas de Desenvolvimento > Extensões > Atualização*).
- Inicie o site do Slot. Recomendamos que você visite o site para aquecê-lo novamente.
- Troque o Slot com a produção.

## <a name="see-also"></a>Consulte também

- [Depurando no Visual Studio](../debugger/index.yml)
- [Depurar aplicativos ASP.NET dinâmicos usando o Depurador de Instantâneos](../debugger/debug-live-azure-applications.md)
- [Depurar Máquinas Virtuais ASP.NET Azure\Conjuntos de Dimensionamento de VMs dinâmicos usando o Depurador de Instantâneos](../debugger/debug-live-azure-virtual-machines.md)
- [Depurar Kubernetes ASP.NET dinâmicos usando o Depurador de Instantâneos](../debugger/debug-live-azure-kubernetes.md)
- [Perguntas frequentes sobre depuração de instantâneo](../debugger/debug-live-azure-apps-faq.yml)
