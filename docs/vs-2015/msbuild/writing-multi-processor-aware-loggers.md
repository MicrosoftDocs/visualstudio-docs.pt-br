---
title: Escrevendo agentes com reconhecimento de multiprocessador | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- msbuild, multi-proc aware loggers
- multi-proc loggers
- loggers, multi-proc
ms.assetid: ff987d1b-1798-4803-9ef6-cc8fcc263516
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2b05c0f1782382f437a5e1d90bf19c724a05ca6a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49826353"
---
# <a name="writing-multi-processor-aware-loggers"></a>Escrevendo agentes de log com reconhecimento de multiprocessador
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A capacidade do [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] de tirar proveito de vários processadores pode diminuir o tempo de criação do projeto, mas também adiciona complexidade para criar o log de eventos. Em um ambiente de processador único, eventos, erros, avisos e mensagens chegam ao agente de uma maneira previsível e sequencial. No entanto, em um ambiente com vários processadores, eventos de origens diferentes podem chegar ao mesmo tempo ou fora de sequência. Para isso, [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] fornece um agente com reconhecimento de multiprocessador e um novo modelo de registro em log e permite que você crie "agentes de encaminhamento" personalizados.  
  
## <a name="multi-processor-logging-challenges"></a>Desafios de registro em log de multiprocessador  
 Quando você cria um ou mais projetos em um sistema com vários processadores ou vários núcleos, os eventos de build [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] para todos os projetos são gerados ao mesmo tempo. Uma avalanche de mensagens de eventos pode chegar ao agente ao mesmo tempo ou fora de sequência. Como um agente do [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 2.0 não foi projetado para lidar com essa situação, ele pode sobrecarregar o agente e causar tempos de build maiores, saída de agente incorreta ou até mesmo um build danificado. Para resolver esses problemas, o agente (a partir do [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 3.5) pode processar eventos fora de sequência e correlacionar eventos e suas fontes.  
  
 Você pode melhorar a eficiência de registro em log ainda mais criando um agente personalizado de encaminhamento. Um agente personalizado de encaminhamento atua como um filtro, permitindo que você escolha, antes de criar, somente os eventos que você deseja monitorar. Quando você usa um agente personalizado de encaminhamento, eventos indesejados não podem sobrecarregar o agente, truncar os logs ou reduzir os tempos de build.  
  
## <a name="multi-processor-logging-models"></a>Modelos de registro em log de multiprocessador  
 Para solucionar problemas de build relacionados a multiprocessador, o [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] dá suporte a dois modelos de registro em log, centrais e distribuídos.  
  
### <a name="central-logging-model"></a>Modelo de registro em log central  
 No modelo de registro em log central, uma única instância de MSBuild.exe age como o "nó central" e as instâncias filho do nó central ("nós secundários") são anexadas ao nó central para ajudar na execução de tarefas de build.  
  
 ![Modelo de agente central](../msbuild/media/centralnode.png "CentralNode")  
  
 Agentes de vários tipos anexados ao nó central são conhecidos como "agentes centrais". Apenas uma instância de cada tipo de agente pode ser anexada ao nó central ao mesmo tempo.  
  
 Quando ocorre um build, os nós secundários encaminham os eventos de build para o nó central. O nó central encaminha todos os seus eventos e também os de nós secundários, para um ou mais dos agentes centrais anexados. Os agentes, em seguida, criam arquivos de log que são baseados nos dados de entrada.  
  
 Embora é necessário implementar somente o <xref:Microsoft.Build.Framework.ILogger> pelo agente central, é recomendável que você implemente também <xref:Microsoft.Build.Framework.INodeLogger> para que o agente central inicialize com o número de nós que participam do build. A sobrecarga do método <xref:Microsoft.Build.Framework.ILogger.Initialize%2A> a seguir invoca quando o mecanismo inicializa o agente.  
  
```  
public interface INodeLogger: ILogger  
{  
    public void Initialize(IEventSource eventSource, int nodeCount);  
}  
```  
  
 Qualquer agente pré-existente com base em <xref:Microsoft.Build.Framework.ILogger> pode atuar como agente central e pode ser anexado ao build. No entanto, agentes centrais escritos sem suporte explícito para cenários de registro em log de multiprocessador e eventos fora de ordem podem quebrar um build ou produzir saída sem sentido.  
  
### <a name="distributed-logging-model"></a>Modelo de Registro em Log Distribuído  
 No modelo de registro em log central, muito tráfego de mensagens de entrada pode sobrecarregar o nó central, por exemplo, ao criar vários projetos ao mesmo tempo. Isso pode enfatizar os recursos do sistema e diminuir o desempenho do build. Para facilitar esse problema, o [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] dá suporte a um modelo de registro em log distribuído.  
  
 ![Modelo de registro em log distribuído](../msbuild/media/distnode.png "DistNode")  
  
 O modelo de registro em log distribuído estende o modelo de registro em log central, permitindo que você crie um agente de encaminhamento.  
  
#### <a name="forwarding-loggers"></a>Agentes de encaminhamento  
 Um agente de encaminhamento é um agente secundário leve que tem um filtro de evento que anexa um nó secundário e recebe eventos de build de entrada desse nó. Ele filtra os eventos de entrada e encaminha apenas os que você especifica para o nó central. Isso reduz o tráfego de mensagem que é enviado para o nó central e melhora o desempenho geral do build.  
  
 Há duas maneiras de usar o registro em log distribuído:  
  
- Personalize o agente de encaminhamento pré-fabricado denominado <xref:Microsoft.Build.BuildEngine.ConfigurableForwardingLogger>.  
  
- Escrever seu próprio agente de encaminhamento personalizado.  
  
  Você pode modificar o ConfigurableForwardingLogger para atender às suas necessidades. Para fazer isso, chame o agente na linha de comando usando MSBuild.exe e liste os eventos de build que você deseja que o agente encaminhe para o nó central.  
  
  Como alternativa, você pode criar um agente de encaminhamento personalizado. Ao criar um agente de encaminhamento personalizado, você pode ajustar o comportamento do agente. No entanto, criar um agente de encaminhamento personalizado é mais complexo do que apenas personalizar o ConfigurableForwardingLogger. Para obter mais informações, consulte [Criando Agentes de Encaminhamento](../msbuild/creating-forwarding-loggers.md).  
  
## <a name="using-the-configurableforwardinglogger-for-simple-distributed-logging"></a>Usando o ConfigurableForwardingLogger para registro em log distribuído simples  
 Para anexar um ConfigurableForwardingLogger ou um agente de encaminhamento personalizado, use a opção `/distributedlogger` (`/dl` para a forma abreviada) em um build de linha de comando MSBuild.exe. O formato para especificar os nomes dos tipos de agente e classes é o mesmo que para a opção `/logger`, exceto em casos em que um agente distribuído tenha sempre duas classes de registro em log em vez de uma, o agente de encaminhamento e o agente central. Este é um exemplo de como anexar um agente de encaminhamento personalizado chamado XMLForwardingLogger.  
  
```  
msbuild.exe myproj.proj/distributedlogger:XMLCentralLogger,MyLogger,Version=1.0.2,Culture=neutral*XMLForwardingLogger,MyLogger,Version=1.0.2,Culture=neutral  
```  
  
> [!NOTE]
>  Um asterisco (*) deve separar os dois nomes de agentes na opção `/dl`.  
  
 Usar o ConfigurableForwardingLogger é como usar qualquer outro agente (conforme descrito Em [Obtendo logs de build](../msbuild/obtaining-build-logs-with-msbuild.md)), exceto se você anexar o agente ConfigurableForwardingLogger em vez do agente [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] típico e especificar como parâmetros os eventos que você deseja que o ConfigurableForwardingLogger passe para o nó central.  
  
 Por exemplo, se você quiser ser notificado somente quando um build começar e terminar, e quando ocorrer um erro, você terá que passar `BUILDSTARTEDEVENT`, `BUILDFINISHEDEVENT` e `ERROREVENT` como parâmetros. Vários parâmetros podem ser passados, separando-os com ponto e vírgula. A seguir está um exemplo de como usar o ConfigurableForwardingLogger para encaminhar apenas os eventos `BUILDSTARTEDEVENT`, `BUILDFINISHEDEVENT` e `ERROREVENT`.  
  
```  
msbuild.exe myproj.proj /distributedlogger:XMLCentralLogger,MyLogger,Version=1.0.2,Culture=neutral*ConfigureableForwardingLogger,C:\My.dll;BUILDSTARTEDEVENT; BUILDFINISHEDEVENT;ERROREVENT  
```  
  
 A seguir está uma lista dos parâmetros do ConfigurableForwardingLogger disponíveis.  
  
|Parâmetros do ConfigurableForwardingLogger|  
|---------------------------------------------|  
|BUILDSTARTEDEVENT|  
|BUILDFINISHEDEVENT|  
|PROJECTSTARTEDEVENT|  
|PROJECTFINISHEDEVENT|  
|TARGETSTARTEDEVENT|  
|TARGETFINISHEDEVENT|  
|TASKSTARTEDEVENT|  
|TASKFINISHEDEVENT|  
|ERROREVENT|  
|WARNINGEVENT|  
|HIGHMESSAGEEVENT|  
|NORMALMESSAGEEVENT|  
|LOWMESSAGEEVENT|  
|CUSTOMEVENT|  
|COMMANDLINE|  
|PERFORMANCESUMMARY|  
|NOSUMMARY|  
|SHOWCOMMANDLINE|  
  
## <a name="see-also"></a>Consulte também  
 [Criando agentes de log de encaminhamento](../msbuild/creating-forwarding-loggers.md)



