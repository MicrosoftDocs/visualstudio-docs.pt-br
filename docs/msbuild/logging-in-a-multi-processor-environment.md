---
title: Registrando em logs em um ambiente multiprocessador | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, multi-processor logging
- MSBuild, logging
ms.assetid: dd4dae65-ed04-4883-b48d-59bcb891c4dc
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6f418c9f3823aaceb4237546cadc68ea2f2bf95e
ms.sourcegitcommit: 71218ffc33da325cc1b886f69ff2ca50d44f5f33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48879246"
---
# <a name="logging-in-a-multi-processor-environment"></a>Registrando em log em um ambiente multiprocessador
A capacidade do MSBuild de usar vários processadores pode diminuir bastante o tempo de criação do projeto, mas também adiciona complexidade ao registrar em logs. Em um ambiente de processador único, o agente pode gerenciar eventos recebidos, mensagens, avisos e erros de uma maneira previsível e sequencial. No entanto, em um ambiente com vários processadores, eventos de origens diferentes podem surgir simultaneamente ou fora de sequência. O MSBuild fornece um novo agente com reconhecimento de vários processadores e permite a criação de “agentes de encaminhamento” personalizados.  
  
## <a name="log-multiple-processor-builds"></a>Registrar em log builds de vários processadores  
 Quando você cria um ou mais projetos em um sistema com vários processadores ou vários núcleos, os eventos de build do MSBuild para todos os projetos são gerados simultaneamente. Uma avalanche de dados de eventos pode chegar ao agente ao mesmo tempo ou fora de sequência. Isso pode sobrecarregar o agente e causar tempos de build maiores, saída de agente incorreta ou até mesmo um build danificado. Para resolver esses problemas, o agente do MSBuild pode processar eventos fora de sequência e correlacionar eventos e suas fontes.  
  
 Você pode melhorar a eficiência de registro em log ainda mais criando um agente personalizado de encaminhamento. Um agente personalizado de encaminhamento atua como um filtro, permitindo que você escolha, antes de criar, os eventos que você deseja monitorar. Quando você usa um agente personalizado de encaminhamento, eventos indesejados não sobrecarregam o agente, truncam os logs nem reduzem os tempos de build.  
  
### <a name="central-logging-model"></a>Modelo de log central  
 Para builds para vários processadores, o MSBuild usa um "modelo de log central". No modelo de log central, uma instância de *MSBuild.exe* atua como o processo de build primário ou "nó central". As instâncias secundárias do *MSBuild.exe*, ou os "nós secundários", são anexadas ao nó central. Qualquer agente de ILogger anexado ao nó central é conhecido como "agentes centrais" e agentes anexados a nós secundários são conhecidos como "agentes secundários".  
  
 Quando ocorre um build, os agentes secundários encaminham o tráfego de eventos para os agentes centrais. Como eventos se originam em vários nós secundários, os dados chegam ao nó central simultaneamente, mas intercalados. Para resolver referências de evento para projeto e evento para destino, os argumentos do evento incluem informações adicionais de contexto do evento de build.  
  
 Embora somente <xref:Microsoft.Build.Framework.ILogger> seja necessário ser implementado pelo agente central, é recomendável que você implemente também <xref:Microsoft.Build.Framework.INodeLogger> se desejar que o agente central inicialize com o número de nós que participam do build. A sobrecarga do método <xref:Microsoft.Build.Framework.ILogger.Initialize%2A> a seguir é invocada quando o mecanismo inicializa o agente:  
  
```csharp
public interface INodeLogger: ILogger  
{  
    public void Initialize(IEventSource eventSource, int nodeCount);  
}  
```  
  
### <a name="distributed-logging-model"></a>Modelo de log distribuído  
 No modelo de log central, muito tráfego de mensagens recebidas, como quando muitos projetos são criados ao mesmo tempo, pode sobrecarregar o nó central, que desgasta o sistema e reduz o desempenho do build.  
  
 Para reduzir esse problema, o MSBuild também permite um "modelo de registro em log distribuído" que estende o modelo de registro em log central, permitindo criar agentes de encaminhamento. Um agente de encaminhamento está conectado a um nó secundário e recebe eventos de build de entrada desse nó. O agente de encaminhamento é como um agente comum, exceto que pode filtrar os eventos e, em seguida, encaminhar somente os desejados para o nó central. Isso reduz o tráfego de mensagens no nó central e, portanto, permite um melhor desempenho.  
  
 Você pode criar um agente de encaminhamento ao implementar a interface <xref:Microsoft.Build.Framework.IForwardingLogger>, que deriva de <xref:Microsoft.Build.Framework.ILogger>. A interface é definida como:  
  
```csharp
public interface IForwardingLogger: INodeLogger  
{  
    public IEventRedirector EventRedirector { get; set; }  
    public int NodeId { get; set; }  
}  
```  
  
 Para encaminhar eventos em um agente de encaminhamento, chame o método <xref:Microsoft.Build.Framework.IEventRedirector.ForwardEvent%2A> da interface <xref:Microsoft.Build.Framework.IEventRedirector>. Passar a <xref:Microsoft.Build.Framework.BuildEventArgs> adequada ou uma derivativa, como o parâmetro.  
  
 Para obter mais informações, confira [Criar agentes de encaminhamento](../msbuild/creating-forwarding-loggers.md).  
  
### <a name="attaching-a-distributed-logger"></a>Anexando um agente distribuído  
 Para anexar um agente distribuído em um build de linha de comando, use a opção `-distributedlogger` (ou, `-dl` de forma abreviada). O formato para especificar os nomes dos tipos de agente e classes é o mesmo que para a opção `-logger`, exceto em casos em que um agente distribuído seja composto por duas classes de registro em log: um agente de encaminhamento e um agente central. A seguir, está um exemplo de como anexar um agente distribuído:  
  
```cmd  
msbuild.exe *.proj -distributedlogger:XMLCentralLogger,MyLogger,Version=1.0.2,  
Culture=neutral*XMLForwardingLogger,MyLogger,Version=1.0.2,  
Culture=neutral  
```  
  
 Um asterisco (*) separa os dois nomes de agentes na opção `-dl`.  
  
## <a name="see-also"></a>Consulte também  
 [Agentes de build](../msbuild/build-loggers.md)   
 [Criar agentes de encaminhamento](../msbuild/creating-forwarding-loggers.md)