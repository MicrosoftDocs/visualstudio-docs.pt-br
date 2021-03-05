---
description: As interfaces a seguir são as principais interfaces para estender o depurador usando o SDK do VS.
title: Interfaces principais | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], core interfaces
ms.assetid: 666b9116-8550-4bdd-bc15-55fc57de87df
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4f24dd16656144fa155d0473d7f722487c0edd03
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170751"
---
# <a name="core-interfaces"></a>Interfaces principais
As interfaces a seguir são as principais interfaces para estender o depurador usando o [!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)] .

## <a name="discussion"></a>Discussão
 Essas interfaces são usadas principalmente para criar o mecanismo de depuração (DE). Eles são organizados aqui por categorias:

- [Pontos de Interrupção](#Breakpoints)

- [Contextos](#Contexts)

- [Servidor núcleo](#CoreServer)

- [Mecanismos de depuração](#DebugEngines)

- [Documentos](#Documents)

- [Eventos](#Events)

- [Expressões](#Expressions)

- [Memória](#Memory)

- [Módulos](#Modules)

- [Portas](#Ports)

- [Processos](#Processes)

- [Programas](#Programs)

- [Propriedades](#Properties)

- [Quadros de pilhas](#StackFrames)

- [Threads](#Threads)

- [Visualizadores de tipo](#TypeVisualizers)

  As entidades que podem implementar as interfaces são:

- Mecanismo DE depuração (DE)

- Fornecedor de porta (PS)

- Avaliador de expressão (EE)

- Visual Studio (VS)

## <a name="breakpoints"></a><a name="Breakpoints"></a> Interrupção
 Essas interfaces estão relacionadas à implementação e ao acompanhamento de pontos de interrupção.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)|DE|Representa um ponto de interrupção associado a um local de memória.|
|[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|DE|Enviado pelo DE quando um ponto de interrupção está associado a um local de memória.|
|[IDebugBreakpointChecksumRequest2](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2.md)|VS|Representa uma soma de verificação de documento para uma solicitação de ponto de interrupção.|
|[IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|DE|Enviado pelo DE quando um ponto de interrupção não está ligado a um local de memória.|
|[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)|DE|Enviado pelo DE quando um ponto de interrupção é atingido.|
|[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)|VS|Representa uma solicitação para um ponto de interrupção; usado na criação de um ponto de interrupção pendente.|
|[IDebugBreakpointRequest3](../../../extensibility/debugger/reference/idebugbreakpointrequest3.md)|VS|Representa uma solicitação para um ponto de interrupção; usado na criação de um ponto de interrupção pendente.|
|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|DE|Representa as informações usadas para associar um ponto de interrupção.|
|[IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|DE|Enviado pelo DE quando um ponto de interrupção é desassociado de um local de memória.|
|[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)|DE|Representa um ponto de interrupção inválido (retornado por `IDebugBreakpointErrorEvent2` ).|
|[IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)|DE|Representa as informações de resolução sobre um ponto de interrupção inválido.|
|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|DE|Representa uma posição em uma função em que um ponto de interrupção é definido.|
|[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)|DE|Representa um ponto de interrupção que deve ser associado; usado na criação de um ponto de interrupção associado.|
|[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)|DE|Representa uma enumeração em um conjunto de pontos de interrupção associados.|
|[IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)|DE|Representa uma enumeração em um conjunto de pontos de interrupção que não puderam ser associados a um local de memória.|

## <a name="contexts"></a><a name="Contexts"></a> Contextos
 Essas interfaces representam vários tipos de contextos dentro do programa que está sendo depurado.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|DE|Representa a posição inicial de uma instrução de código.|
|[IDebugCodeContext3](../../../extensibility/debugger/reference/idebugcodecontext3.md)|DE|Estende a interface [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) para habilitar a recuperação de interfaces de módulo e de processo.|
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS, DE|Representa uma posição em um documento.|
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|Representa o contexto no qual avaliar uma expressão.|
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|Representa o local inicial na memória de uma coleção de bytes.|
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|Representa um contexto de quadro de pilha em um ponto de interrupção ou exceção.|
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|Representa um contexto de quadro de pilha em um ponto de interrupção ou exceção.|
|[IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)|DE|Representa uma enumeração sobre um conjunto de contextos de código.|

## <a name="core-server"></a><a name="CoreServer"></a> Servidor núcleo
 Essas interfaces representam o computador no qual um programa está sendo depurado. Eles são implementados pelo [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] , mas podem ser chamados por mecanismos de depuração.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)|VS|Fornece acesso a portas e fornecedores de porta, bem como informações sobre o computador.|
|[IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)|VS|Representa um [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) que dá suporte à depuração remota.|

## <a name="debug-engines"></a><a name="DebugEngines"></a> Mecanismos de depuração
 Essas interfaces representam os mecanismos de depuração e seus eventos associados.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)|DE|Representa um mecanismo de depuração personalizado.|
|[IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)|DE|Representa um mecanismo de depuração personalizado que dá suporte ao carregamento de símbolos, JustMyCode e exceções.|
|[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)|DE|Enviado por cada nova instância de de para indicar que está pronto para lidar com tarefas de depuração.|
|[IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)|DE|Representa um mecanismo de depuração personalizado que dá suporte a programas de inicialização.|
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE, PS|Representa um nó de programa que manipula vários mecanismos de depuração.|
|[IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)|DE|Fornece uma maneira para o SDM obter uma interface para o mecanismo de depuração de um thread, programa ou quadro de pilha.|

## <a name="documents"></a><a name="Documents"></a> Documento
 Essas interfaces representam documentos (arquivos de origem) e seus elementos associados.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|DE|Enviado pelo DE para solicitar que um documento seja aberto.|
|[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)|DE|Representa um fluxo de instruções desmontadas de um documento.|
|[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)|VS, DE|Representa um documento fornecido pelo DE, especificando um nome e uma ID de classe (CLSID).|
|[IDebugDocumentChecksum2](../../../extensibility/debugger/reference/idebugdocumentchecksum2.md)|DE, EE|Representa uma soma de verificação para um documento de depuração e permite passar a soma de verificação entre componentes.|
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS, DE|Representa um contexto de documento, uma posição dentro de um documento correspondente a uma instrução e contexto de código específicos.|
|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|VS, DE|Representa uma posição geral dentro de um documento.|
|[IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)|VS|Representa uma posição em um arquivo de origem como um deslocamento de caractere.|
|[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)|VS, DE|Representa um documento DE texto fornecido pelo (derivado de [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)), fornecendo o texto real.|
|[IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|DE|Enviado pelo DE para especificar alterações em um arquivo de origem que está na memória.|

## <a name="events"></a><a name="Events"></a> LostFocus
 Essas interfaces representam todos os eventos que são enviados entre o e o SDM (Gerenciador de depuração de sessão).

| Interface | Implementado por | Descrição |
| - |----------------| - |
| [IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md) | DE | Enviado pelo DE para solicitar que um documento seja aberto. |
| [IDebugBeforeSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2.md) | DE | O mecanismo de depuração (DE) envia essa interface para o SDM (Gerenciador de depuração de sessão) para definir a mensagem da barra de status durante cargas de símbolo. |
| [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) | DE | Enviado pelo DE quando uma interrupção no programa for concluída. |
| [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) | DE | Enviado pelo DE quando um ponto de interrupção é associado. |
| [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) | DE | Enviado pelo DE quando um ponto de interrupção falha ao ser associado. |
| [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) | DE | Enviado pelo DE quando um ponto de interrupção é atingido. |
| [IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md) | DE | Enviado pelo DE quando um ponto de interrupção é desassociado. |
| [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md) | DE | Enviado pelo DE para determinar se ele deve parar em um local específico. |
| [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md) | DE | Enviado pelo DE para especificar alterações em um arquivo de origem que está na memória. |
| [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) | DE | Enviado por cada nova instância de de para indicar que está pronto para lidar com tarefas de depuração. |
| [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) | DE | Enviado pelo DE para indicar que o programa que está sendo depurado está pronto para executar a primeira instrução. |
| [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md) | DE | Uma interface que é usada por outras interfaces de evento, que podem retornar um erro, para fornecer mensagens de erro legíveis ao humano. |
| [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) | DE, PS | Interface base da qual todas as outras interfaces de evento são derivadas. |
| [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) | VS | Representa uma interface implementada pelo SDM para os quais os eventos (expressos como objetos que implementam uma interface de evento específica) são enviados. |
| [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) | DE | Enviado pelo DE quando uma exceção ocorreu no programa que está sendo depurado. |
| [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) | DE | Enviado pelo DE quando uma avaliação de expressão assíncrona é concluída. |
| IDebugFindSymbolEvent2 | | OBSOLETO. NÃO USE. |
| [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md) | DE | Enviado pelo processo de quando o processamento para uma exceção interceptada foi concluído. |
| [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) | DE | Enviado pelo DE quando um programa concluiu o carregamento. |
| [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md) | DE | Enviado pelo DE para que o IDE exiba uma mensagem informativa para o usuário. |
| [IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md) | DE | Enviado pelo DE quando um módulo é carregado ou descarregado. |
| [IDebugNoSymbolsEvent2](../../../extensibility/debugger/reference/idebugnosymbolsevent2.md) | DE | Sinaliza a interface de usuário do [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] depurador para avisar ao usuário que não foi possível localizar os símbolos para o executável iniciado. |
| [IDebugOutputStringEvent2](../../../extensibility/debugger/reference/idebugoutputstringevent2.md) | DE | Enviado pelo DE para que o IDE exiba uma cadeia de caracteres arbitrária. |
| [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) | VS, DE | Enviado por uma porta para comunicar eventos de porta a qualquer ouvinte. |
| [IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md) | DE, PS | Enviado pela porta DE ou quando um processo tiver sido criado. |
| [IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md) | DE, PS | Enviado pela porta DE ou quando um processo foi destruído. |
| [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) | DE, PS | Enviado pela porta DE ou quando um programa foi criado. |
| [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) | DE, PS | Enviado pela porta DE ou quando um programa foi destruído. |
| [IDebugProgramDestroyEventFlags2](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2.md) | DE | Permite que um mecanismo de depuração substitua o comportamento padrão da [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] interface do usuário quando você finaliza uma sessão de depuração. |
| [IDebugProgramNameChangedEvent2](../../../extensibility/debugger/reference/idebugprogramnamechangedevent2.md) | DE | Enviado do mecanismo de depuração (DE) para o SDM (Gerenciador de depuração de sessão) quando o nome de um programa é alterado. |
| [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md) | DE | Enviado pelo DE quando uma nova propriedade (representada pela `IDebugProperty2` interface) tiver sido criada. |
| [IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md) | DE | Enviado pelo DE quando uma propriedade foi destruída. |
| [IDebugReturnValueEvent2](../../../extensibility/debugger/reference/idebugreturnvalueevent2.md) | DE | Enviado pelo DE quando estiver saindo de ou em uma função, de modo que o valor de retorno possa ser exibido corretamente. |
| [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md) | VS | Habilita os mecanismos de depuração para ler as configurações de métrica remotamente. |
| [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md) | DE | Enviado pelo DE quando uma etapa para, acima ou fora de uma instrução foi concluída. |
| [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) | DE | Enviado pelo DE para indicar o êxito ou a falha de carregamento de símbolos para um módulo. |
| [IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md) | DE | Enviado pelo DE quando um thread foi criado. |
| [IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md) | DE | Enviado pelo DE quando um thread foi destruído. |
| [IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md) | DE | Enviado pelo DE quando um thread alterou seu nome. |

## <a name="expressions"></a>Expressões <a name="Expressions"></a>
 Essas interfaces representam expressões a serem avaliadas em um contexto específico.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)|DE|Representa uma expressão a ser avaliada. Obtido da interface [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) .|
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|Representa um contexto no qual uma expressão é avaliada. Obtido da interface [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) .|
|[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|DE|Enviado pelo DE quando uma avaliação de expressão assíncrona é concluída.|

## <a name="memory"></a><a name="Memory"></a> Memória
 Essas interfaces representam sequências de bytes na memória.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)|DE|Representa uma sequência de bytes na memória que podem ser lidos ou gravados.|
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|Representa um local na memória de uma sequência de bytes.|

## <a name="modules"></a><a name="Modules"></a> Módulos
 Essas interfaces representam um módulo, que corresponde a um executável ou. Arquivo DLL.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)|DE|Representa um único executável ou DLL.|
|[IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)|DE|Representa um [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) que dá suporte a símbolos.|
|[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|DE|Enviado pelo DE quando um módulo é carregado ou descarregado.|
|[IDebugSourceServerModule](../../../extensibility/debugger/reference/idebugsourceservermodule.md)|DE|Representa as informações do servidor de origem contidas em um arquivo PDB.|
|[IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)|DE|Representa uma enumeração em um conjunto de módulos que são conhecidos por um [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md).|

## <a name="ports"></a><a name="Ports"></a> Porta
 Essas interfaces representam portas e fornecedores de porta.

| Interface | Implementado por | Descrição |
| - |----------------| - |
| [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md) | VS, PS | Representa a porta padrão no computador local. |
| [IDebugFirewallConfigurationCallback2](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2.md) | VS | Habilita um mecanismo de depuração que usa DCOM para solicitar [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] que a interface do usuário Verifique se o firewall não bloqueará a depuração remota. |
| [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) | VS, PS | Representa uma porta. |
| [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) | PS | Enviado por uma porta para comunicar eventos de porta a qualquer ouvinte. |
| [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md) | PS | Representa uma porta que pode iniciar e encerrar processos. |
| [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) | PS | Usado para registrar e cancelar o registro de programas com uma porta; permite que a porta acompanhe os programas que estão sendo depurados no momento. |
| [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md) | PS | Representa uma interface do usuário personalizada para selecionar a porta. |
| [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) | VS | Representa uma solicitação para uma porta da qual uma nova porta será criada ou localizada. |
| [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) | PS | Representa um fornecedor de portas. |
| [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md) | PS | Representa um fornecedor de portas que podem persistir (salvar em disco) informações sobre as portas que ele criou. |
| [IDebugPortSupplierDescription2](../../../extensibility/debugger/reference/idebugportsupplierdescription2.md) | PS | Permite que a [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] interface do usuário exiba texto dentro da seção **informações de transporte** da caixa de diálogo **anexar ao processo** . |
| [IDebugWindowsComputerPort2](../../../extensibility/debugger/reference/idebugwindowscomputerport2.md) | VS | Permite consultar informações sobre o computador de destino. |
| [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md) | VS, PS | Representa uma enumeração em um conjunto de portas. |
| [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md) | VS | Representa uma enumeração em um conjunto de fornecedores de porta. |

## <a name="processes"></a><a name="Processes"></a> Processar
 Essas interfaces representam processos, um único executável que contém um ou mais programas.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)|PS, DE|Representa um processo que está sendo executado em um computador.|
|[IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)|PS, DE|Representa um processo que dá suporte ativamente à depuração (usado para substituir os métodos Step, continue e execute na interface [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) ).|
|[IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)|DE, PS|Enviado pela porta DE ou quando um processo tiver sido criado.|
|[IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)|DE, PS|Enviado pela porta DE ou quando um processo foi destruído.|
|[IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)|PS|Representa um processo que deve controlar qual sessão está anexada a ela.|
|[IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)|PS|Representa uma enumeração de um conjunto de processos em uma porta.|

## <a name="programs"></a><a name="Programs"></a> Suplementa
 Essas interfaces representam programas, unidades lógicas de execução que não necessariamente correspondem a um executável ou módulo físico.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)|DE|Representa um [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que precisa trabalhar em conjunto com outros programas sendo depurados ao mesmo tempo.|
|[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)|DE, PS|Representa uma unidade lógica de execução.|
|[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|DE, PS|Enviado pela porta DE ou quando um programa foi criado.|
|[IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|DE, PS|Enviado pela porta DE ou quando um programa foi destruído.|
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE, PS|Representa um [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) que pode ser manipulado por vários mecanismos de depuração.|
|[IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)|PS|Representa um [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que deve ser capaz de controlar qual sessão está anexada a ela.|
|[IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)|DE, PS|Representa um [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) que pode retornar informações sobre o processo no qual ele está sendo executado.|
|[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)|DE, PS|Representa um programa que pode ser depurado.|
|[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)|DE, PS|Permite que um nó de programa seja notificado sobre uma tentativa de anexar ao programa associado.|
|[IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)|DE|Fornece uma maneira para o SDM consultar um DE sobre os programas controlados por esse DE.|
|[IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)|VS|Usado pelo DEs para registrar programas com o SDM para mostrar que estão sendo depurados.|
|[IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)|DE, PS|Representa um [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) que pode empacotar interfaces entre limites de thread ou processo.|
|[IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)|DE, PS|Representa uma enumeração de um conjunto de programas.|

## <a name="properties"></a><a name="Properties"></a> propriedades
 Essas interfaces representam propriedades, um valor associado a um contexto específico, geralmente o resultado de uma avaliação de expressão.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)|EE|Representa um [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que pode exibir seu valor de forma personalizada.|
|[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)|DE|Representa um valor de um quadro de pilha, documento ou o resultado de uma avaliação de expressão.|
|[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)|DE|Representa um [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que dá suporte a cadeias de caracteres longas arbitrariamente.|
|[IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|DE|Enviado pelo DE quando uma nova propriedade (representada pela interface [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) ) foi criada.|
|[IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|DE|Enviado pelo DE quando uma propriedade foi destruída.|
|[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)|DE|Representa uma referência a uma propriedade que pode existir fora de qualquer quadro de pilha específico.|
|[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)|DE|Representa uma enumeração em um conjunto de estruturas [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) que descrevem variáveis, registros, parâmetros e expressões.|
|[IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)|DE|Representa uma enumeração em um conjunto de estruturas de [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) .|

## <a name="stack-frames"></a><a name="StackFrames"></a> Quadros de pilha
 Essas interfaces representam um quadro de pilha, um contexto no qual ocorreu um ponto de interrupção ou uma exceção.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|Representa um contexto no qual ocorreu um ponto de interrupção ou uma exceção.|
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|Representa um [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) que pode manipular exceções interceptadas.|
|[IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)|DE|Representa uma enumeração sobre o conjunto de [CODE_PATH](../../../extensibility/debugger/reference/code-path.md) estruturas que especificam a sequência de chamada de função usada para chegar em um determinado registro de ativação.|
|[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)|DE|Representa uma enumeração em um conjunto de estruturas [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) , que descrevem os quadros de pilhas.|

## <a name="threads"></a><a name="Threads"></a> Threads
 Essas interfaces representam threads e seus eventos associados.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|DE|Representa um thread de execução.|
|[IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|DE|Enviado pelo DE quando um thread foi criado.|
|[IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|DE|Enviado pelo DE quando um thread foi destruído.|
|[IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|DE|Enviado pelo DE quando um thread alterou seu nome.|
|[IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)|DE|Representa uma enumeração em um conjunto de threads.|

## <a name="type-visualizers"></a><a name="TypeVisualizers"></a> Visualizadores de tipo
 Essas interfaces fornecem suporte para visualizadores de tipo. Essas interfaces normalmente são implementadas por um avaliador de expressão.

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)|EE|Representa uma matriz de bytes a ser apresentada a um visualizador de tipo.|
|[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)|EE|Fornece métodos para obter acesso aos dados a serem passados para um visualizador de tipo.|
|[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)|EE|Representa uma propriedade que fornece acesso a implementações de [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) .|

## <a name="see-also"></a>Confira também
- [Referência da API](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
- [Criando um mecanismo de depuração personalizado](../../../extensibility/debugger/creating-a-custom-debug-engine.md)
