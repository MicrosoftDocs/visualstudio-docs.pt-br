---
title: Criando agentes de log de encaminhamento | Microsoft Docs
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
- MSBuild, forwarding loggers
- MSBuild, logging
ms.assetid: 3aebf9c8-b62c-4cb2-b2d6-8cdfcd369a24
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 46cff57e8238e00f914f8437fbc81d1887e7d629
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49281236"
---
# <a name="creating-forwarding-loggers"></a>Criando agentes de log de encaminhamento
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Agentes de encaminhamento melhoram a eficiência de log, permitindo que você escolha os eventos que deseja monitorar ao compilar projetos em um sistema com vários processadores. Ao habilitar agentes de encaminhamento, você pode impedir que eventos indesejados sobrecarreguem o agente central, diminuindo o tempo de build e desorganizando o log.  
  
 Para criar um agente de encaminhamento, você pode implementar a interface <xref:Microsoft.Build.Framework.IForwardingLogger> e, em seguida, implementar seus métodos manualmente ou usar a classe <xref:Microsoft.Build.BuildEngine.ConfigurableForwardingLogger> e seus métodos pré-configurados. (O último será suficiente para a maioria dos aplicativos.)  
  
## <a name="register-events-and-respond-to-them"></a>Registre eventos e responda a eles  
 Um agente de encaminhamento reúne informações sobre eventos de build à medida que são relatados pelo mecanismo de build secundária, que é um processo de trabalho criado pelo processo de build principal durante um build em um sistema com vários processadores. Em seguida, o agente de encaminhamento seleciona eventos para encaminhar para o agente central, com base nas instruções que você atribuiu a ele.  
  
 Você deve registrar os agentes de encaminhamento para manipular os eventos que deseja monitorar. Para registrar-se para eventos, os agentes devem substituir o método <xref:Microsoft.Build.Utilities.Logger.Initialize%2A>. Este método agora inclui um parâmetro opcional, `nodecount`, que pode ser definido como o número de processadores no sistema. (Por padrão, o valor é 1.)  
  
 Alguns exemplos de eventos que você pode monitorar são <xref:Microsoft.Build.Framework.IEventSource.TargetStarted>, <xref:Microsoft.Build.Framework.IEventSource.ProjectStarted> e <xref:Microsoft.Build.Framework.IEventSource.ProjectFinished>.  
  
 Em um ambiente com vários processadores, mensagens de evento, provavelmente, serão recebidas fora de ordem. Portanto, você deve avaliar os eventos usando o manipulador de eventos no agente de encaminhamento e programá-lo para determinar quais eventos passar para o redirecionador para serem encaminhados para o agente central. Para fazer isso, você pode usar a classe <xref:Microsoft.Build.Framework.BuildEventContext>, que está anexada a cada mensagem, para ajudar a identificar eventos que deseja encaminhar e, em seguida, transmitir os nomes de eventos para a classe <xref:Microsoft.Build.BuildEngine.ConfigurableForwardingLogger> (ou uma subclasse dela). Quando você usa esse método, nenhuma outra codificação específica é necessária para encaminhar eventos.  
  
## <a name="specify-a-forwarding-logger"></a>Especificar um agente de encaminhamento  
 Depois que o agente de encaminhamento tiver sido compilado em um assembly, você deve informar o [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] para usá-lo durante builds. Para fazer isso, use as opções `/FileLogger`, `/FileLoggerParameters` e `/DistributedFileLogger` junto com MSBuild.exe. A opção `/FileLogger` informa ao MSBuild.exe que o agente está diretamente anexado. A opção `/DistributedFileLogger` significa que há um arquivo de log por nó. Para definir parâmetros no agente de encaminhamento, use a opção `/FileLoggerParameters`. Para obter mais informações sobre essas e outras opções do MSBuild.exe, consulte [Referência de Linha de Comando](../msbuild/msbuild-command-line-reference.md).  
  
## <a name="multi-processor-aware-loggers"></a>Agentes com reconhecimento de multiprocessador  
 Quando você cria um projeto em um sistema com vários processadores, as mensagens de build de cada processador não são intercaladas automaticamente em uma sequência unificada. Em vez disso, você deve estabelecer uma prioridade de agrupamento de mensagens usando a classe <xref:Microsoft.Build.Framework.BuildEventContext> que está anexada a cada mensagem. Para obter mais informações sobre o build de vários processadores, consulte [Registrando em log em um ambiente multiprocessador](../msbuild/logging-in-a-multi-processor-environment.md).  
  
## <a name="see-also"></a>Consulte também  
 [Obtaining Build Logs (Obtendo logs de build)](../msbuild/obtaining-build-logs-with-msbuild.md)   
 [Agentes de Log de Build](../msbuild/build-loggers.md)   
 [Registrando em log em um ambiente multiprocessador](../msbuild/logging-in-a-multi-processor-environment.md)



