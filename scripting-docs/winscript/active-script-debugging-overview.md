---
title: Visão geral da depuração de script ativo | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Active Script Debugging overview
ms.assetid: ce4ec768-d017-4dfa-a7e3-cced3a29e679
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d8624c1405931edefe2e1e53e579ad28a7b238f1
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220216"
---
# <a name="active-script-debugging-overview"></a>Visão geral de depuração de script ativo
As interfaces de depuração de script ativo permitem a depuração com neutralidade de idioma e de host e dão suporte a uma ampla variedade de ambientes de desenvolvimento.  
  
 ![Processo de host de script](../winscript/media/scp56activdbgarchgif.gif "Scp56ActivDbgArchgif")  
Figura 1  
  
 Um ambiente de depuração com neutralidade de idioma pode dar suporte a qualquer linguagem de programação ou uma combinação de linguagens de programação, sem a necessidade de conhecimento específico de qualquer uma dessas linguagens. O ambiente de depuração também dá suporte a pontos de interrupção e execução em etapas entre linguagens diferentes. (Esta visão geral concentra-se principalmente em suporte a linguagens de script, tais como VBScript e [!INCLUDE[javascript](../javascript/includes/javascript-md.md)].)  
  
 Um depurador com neutralidade de host pode ser usado automaticamente com qualquer host de script ativo, assim como o Internet Explorer ou um host personalizado. O host controla o que o depurador apresenta ao usuário, desde a estrutura da árvore de documentos até o conteúdo e a colorização de sintaxe dos documentos de depuração. Isso permite que o código-fonte depurado seja mostrado no contexto do documento de host. Por exemplo, o Internet Explorer pode mostrar um script em uma página HTML.  
  
 Nas subseções a seguir, cada componente principal na depuração ativa e as respectivas interfaces associadas são discutidos. No entanto, antes de continuar, vários conceitos principais de depuração ativa devem ser definidos:  
  
 **aplicativo host**  
 O aplicativo que hospeda os mecanismos de script e fornece um conjunto de objetos que podem ser escritos em script (ou "modelo de objeto").  
  
 **mecanismo de linguagem**  
 Um componente que fornece abstrações de análise, execução e depuração para uma linguagem específica.  
  
 **IDE do depurador**  
 O aplicativo que fornece depuração da interface do usuário por meio da comunicação com o aplicativo host e os mecanismos de linguagem.  
  
 **gerenciador de depuração do computador** Um componente que mantém um registro dos processos de aplicativos depuráveis.  
  
 **gerenciador de depuração do processo**  
 Um componente que mantém a árvore de documentos depuráveis para um determinado aplicativo, controla os threads em execução e assim por diante.  
  
 **contexto de documento**  
 Um contexto de documento é uma abstração que representa um intervalo específico no código-fonte de um documento de host.  
  
 **contexto de código**  
 Um contexto de código representa um local específico no código em execução de um mecanismo de linguagem (um "ponteiro de instrução virtual".)  
  
 **contexto de expressão**  
 Um contexto específico (por exemplo, um registro de ativação) no qual as expressões podem ser avaliadas por um mecanismo de linguagem.  
  
 **navegação de objeto**  
 Uma representação estruturada independente de linguagem do nome, tipo, valor e subobjetos de um determinado objeto, adequados para a implementação de uma interface do usuário de "janela de inspeção".  
  
 Abaixo está uma visão geral de cada um dos principais componentes de depuração ativa e das interfaces associadas correspondentes, seguida dos detalhes dessas interfaces.  
  
## <a name="language-engine"></a>Mecanismo de linguagem  
 O mecanismo de linguagem fornece:  
  
- Análise e execução de linguagem.  
  
- Suporte à depuração (pontos de interrupção e assim por diante).  
  
- Avaliação de expressão.  
  
- Colorização de sintaxe.  
  
- Navegação de objeto.  
  
- Enumeração e análise de pilha.  
  
  Abaixo estão as interfaces às quais um mecanismo de script precisa dar suporte para fornecer depuração, avaliação de expressão e navegação de objeto. Essas interfaces são usadas pelo aplicativo host para mapear entre seu contexto de documento e contextos de código do mecanismo, além de serem usadas pelo depurador da interface do usuário para fazer a avaliação da expressão, a enumeração de pilha e a navegação de objeto.  
  
  [IActiveScriptDebug Interface](../winscript/reference/iactivescriptdebug-interface.md)  
  Fornece a enumeração de contexto de código e a colorização de sintaxe.  
  
  [IActiveScriptErrorDebug Interface](../winscript/reference/iactivescripterrordebug-interface.md)  
  Retorna contextos de documento e registros de ativação para erros.  
  
  [IActiveScriptSiteDebug Interface](../winscript/reference/iactivescriptsitedebug-interface.md)  
  Link fornecido pelo host do mecanismo de script para o depurador.  
  
  [Interface IDebugCodeContext](../winscript/reference/idebugcodecontext-interface.md)  
  Fornece um "ponteiro de instrução" virtual em um thread.  
  
  [Interface IEnumDebugCodeContexts](../winscript/reference/ienumdebugcodecontexts-interface.md)  
  Enumera os contextos de código que correspondem a um contexto de documento.  
  
  [Interface IDebugStackFrame](../winscript/reference/idebugstackframe-interface.md)  
  Representa um registro de ativação lógico na pilha de thread.  
  
  [Interface IDebugExpressionContext](../winscript/reference/idebugexpressioncontext-interface.md)  
  Fornece o contexto no qual as expressões podem ser avaliadas.  
  
  [Interface IDebugStackFrameSniffer](../winscript/reference/idebugstackframesniffer-interface.md)  
  Fornece uma maneira para enumerar os registros de ativação lógicos.  
  
  [Interface IDebugExpression](../winscript/reference/idebugexpression-interface.md)  
  Representa uma expressão avaliada de forma assíncrona.  
  
  [Interface IDebugSyncOperation](../winscript/reference/idebugsyncoperation-interface.md)  
  Permite que um mecanismo de script extraia uma operação que precisa ser executada enquanto aninhado em um thread bloqueado específico.  
  
  [IDebugAsyncOperation Interface](../winscript/reference/idebugasyncoperation-interface.md)  
  Fornece acesso assíncrono a uma operação de depuração síncrona.  
  
  [IDebugAsyncOperationCallBack Interface](../winscript/reference/idebugasyncoperationcallback-interface.md)  
  Fornece eventos de status relacionados ao andamento da avaliação de uma interface `IDebugAsyncOperation`.  
  
  [Interface IEnumDebugExpressionContexts](../winscript/reference/ienumdebugexpressioncontexts-interface.md)  
  Enumera uma coleção de objetos `IDebugExpressionContexts`.  
  
  [IProvideExpressionContexts Interface](../winscript/reference/iprovideexpressioncontexts-interface.md)  
  Fornece uma maneira de enumerar os contextos de expressão conhecidos por um determinado componente.  
  
  [Interface IDebugFormatter](../winscript/reference/idebugformatter-interface.md)  
  Permite que uma linguagem ou IDE personalize a conversão entre valores VARIANT ou tipos e cadeias de caracteres VARTYPE.  
  
  [Interface IDebugStackFrameSnifferEx](../winscript/reference/idebugstackframesnifferex-interface.md)  
  Enumera os registros de ativação lógicos para o PDM.  
  
## <a name="hosts"></a>Hosts  
 O host:  
  
- Hospeda os mecanismos de linguagem.  
  
- Fornece um modelo de objeto (conjunto de objetos que podem ser incluídos no script).  
  
- Define uma árvore de documentos que pode ser depurada e o respectivo conteúdo.  
  
- Organiza os scripts em aplicativos virtuais.  
  
  Há dois tipos de hosts:  
  
- Um host não inteligente dá suporte apenas às interfaces básicas de script ativo. Ele não tem controle sobre a estrutura ou organizações do documento; isso é determinado inteiramente pelos scripts fornecidos para os mecanismos de linguagem.  
  
- Um host inteligente dá suporte a um conjunto maior de interfaces que lhe permite definir a árvore de documentos, o conteúdo do documento e a colorização de sintaxe. Há um conjunto de interfaces auxiliares descrito na próxima subseção, que torna muito mais fácil para um host ser um host inteligente.  
  
### <a name="smart-host-helper-interfaces"></a>Interfaces auxiliares de host inteligente  
 Os métodos `IDebugDocumentHelper` fornecem um conjunto incrivelmente simplificado de interfaces que um host pode usar para obter os benefícios de hospedagem inteligente sem lidar com toda a complexidade (e poder) das interfaces de host completo.  
  
 É claro que não é obrigatório para um host usar essas interfaces. No entanto, usar essas interfaces pode evitar implementação ou uso de um número de interfaces mais complicadas.  
  
 [IDebugDocumentHelper Interface](../winscript/reference/idebugdocumenthelper-interface.md)  
 Implementado pelo PDM e fornece implementações de várias interfaces necessárias para hospedagem inteligente.  
  
 [IDebugDocumentHost Interface](../winscript/reference/idebugdocumenthost-interface.md)  
 Implementado (opcionalmente) pelo host para expor a funcionalidade específica do host, como colorização de sintaxe, para o depurador.  
  
 Para obter mais informações, consulte [Implementação de interfaces auxiliares do host inteligente](../winscript/implementing-smart-host-helper-interfaces.md).  
  
### <a name="full-smart-host-interfaces"></a>Interfaces de host inteligente completo  
 Abaixo está o conjunto completo de interfaces que um host inteligente deve implementar ou usar se ele não está usando as interfaces auxiliares.  
  
 Interfaces implementadas pelo host:  
  
 [Interface IDebugDocumentInfo](../winscript/reference/idebugdocumentinfo-interface.md)  
 Fornece informações sobre um documento, que pode ou não ser instanciado.  
  
 [Interface IDebugDocumentProvider](../winscript/reference/idebugdocumentprovider-interface.md)  
 Fornece os meios para instanciar um documento sob demanda.  
  
 [Interface IDebugDocument](../winscript/reference/idebugdocument-interface.md)  
 A interface base para todos os documentos de depuração.  
  
 [Interface IDebugDocumentText](../winscript/reference/idebugdocumenttext-interface.md)  
 Fornece acesso a uma versão somente texto do documento de depuração.  
  
 [Interface IDebugDocumentTextAuthor](../winscript/reference/idebugdocumenttextauthor-interface.md)  
 Permite a edição da versão do documento de depuração somente texto.  
  
 [Interface IDebugDocumentContext](../winscript/reference/idebugdocumentcontext-interface.md)  
 Fornece uma representação abstrata de uma parte do documento sendo depurado.  
  
 Interfaces implementadas pelo PDM em nome do host:  
  
 [IDebugApplicationNode Interface](../winscript/reference/idebugapplicationnode-interface.md)  
 Estende a funcionalidade da interface `IDebugDocumentProvider` fornecendo um contexto dentro de uma árvore de projeto.  
  
## <a name="debugger-ide"></a>IDE de depurador  
 O IDE é uma interface do usuário de depuração independente de linguagem. Ele fornece:  
  
- Visualizadores/editores de documento.  
  
- Gerenciamento de ponto de interrupção.  
  
- Janelas de inspeção e avaliação de expressão.  
  
- Navegação de registro de ativação.  
  
- Navegação de objeto/classe.  
  
- Navegação pela estrutura de aplicativo virtual.  
  
  Interfaces implementadas pelo depurador:  
  
  [IApplicationDebugger Interface](../winscript/reference/iapplicationdebugger-interface.md)  
  A interface primária exposta por uma sessão IDE do depurador.  
  
  [IApplicationDebuggerUI Interface](../winscript/reference/iapplicationdebuggerui-interface.md)  
  Fornece a um componente externo mais controle sobre a IU (interface do usuário) do depurador.  
  
  [IDebugExpressionCallBack Interface](../winscript/reference/idebugexpressioncallback-interface.md)  
  Fornece eventos de status para o andamento da avaliação de `IDebugExpression`.  
  
  [Interface IDebugDocumentTextEvents](../winscript/reference/idebugdocumenttextevents-interface.md)  
  Fornece eventos que indicam alterações no documento de texto associado.  
  
  [IDebugApplicationNodeEvents Interface](../winscript/reference/idebugapplicationnodeevents-interface.md)  
  Fornece a interface de eventos para a interface `IDebugApplicationNode`.  
  
### <a name="machine-debug-manager"></a>Gerenciador de depuração do computador  
 O gerenciador de depuração do computador fornece o ponto de conexão entre depuradores de aplicativos virtuais, mantendo e enumerando uma lista de aplicativos virtuais ativos.  
  
 [Interface IDebugSessionProvider](../winscript/reference/idebugsessionprovider-interface.md)  
 Estabelece uma sessão de depuração para um aplicativo em execução.  
  
 [Interface IMachineDebugManager](../winscript/reference/imachinedebugmanager-interface.md)  
 A interface primária para o gerenciador de depuração do computador.  
  
 [Interface IMachineDebugManagerCookie](../winscript/reference/imachinedebugmanagercookie-interface.md)  
 Semelhante à interface `IMachineDebugManager`, mas esta interface dá suporte a cookies de depuração.  
  
 [Interface IMachineDebugManagerEvents](../winscript/reference/imachinedebugmanagerevents-interface.md)  
 Sinaliza as alterações na lista de aplicativos em execução mantida pelo gerenciador de depuração do computador.  
  
 [Interface IEnumRemoteDebugApplications](../winscript/reference/ienumremotedebugapplications-interface.md)  
 Enumera os aplicativos em execução em um computador.  
  
### <a name="process-debug-manager"></a>Gerenciador de depuração do processo  
 O PDM faz o seguinte:  
  
- Sincroniza a depuração de vários mecanismos de linguagem.  
  
- Mantém uma árvore de documentos depuráveis.  
  
- Mescla registros de ativação.  
  
- Coordena pontos de interrupção e divisão em etapas entre mecanismos de linguagem.  
  
- Rastreia threads.  
  
- Mantém um thread do depurador para processamento assíncrono.  
  
- Comunica-se com o gerenciador de depuração do computador e o IDE do depurador.  
  
  A seguir estão as interfaces fornecidas pelo gerenciador de depuração do processo.  
  
  [Interface IProcessDebugManager](../winscript/reference/iprocessdebugmanager-interface.md)  
  A interface primária para o gerenciador de depuração do processo. Essa interface pode criar, adicionar ou remover um aplicativo virtual de um processo.  
  
  [IRemoteDebugApplication Interface](../winscript/reference/iremotedebugapplication-interface.md)  
  Representa um aplicativo em execução.  
  
  [IDebugApplication Interface](../winscript/reference/idebugapplication-interface.md)  
  Expõe métodos de depuração não configuráveis como remotos para uso por hosts e mecanismos de idioma.  
  
  [Interface IRemoteDebugApplicationThread](../winscript/reference/iremotedebugapplicationthread-interface.md)  
  Representa um thread de execução dentro de um aplicativo específico.  
  
  [Interface IDebugApplicationThread](../winscript/reference/idebugapplicationthread-interface.md)  
  Permite que os hosts e mecanismos de linguagem forneçam sincronização de thread e mantenham informações sobre o estado de depuração específicas de thread.  
  
  [IEnumRemoteDebugApplicationThreads Interface](../winscript/reference/ienumremotedebugapplicationthreads-interface.md)  
  Enumera os threads em execução em um aplicativo.  
  
  [Interface IDebugThreadCall](../winscript/reference/idebugthreadcall-interface.md)  
  Expede chamadas com marshalling.  
  
  [IDebugApplicationNode Interface](../winscript/reference/idebugapplicationnode-interface.md)  
  Mantém uma posição para um documento na hierarquia.  
  
  [Interface IEnumDebugApplicationNodes](../winscript/reference/ienumdebugapplicationnodes-interface.md)  
  Enumera nós filho de um nó associado a um aplicativo.  
  
  [Interface IEnumDebugStackFrames](../winscript/reference/ienumdebugstackframes-interface.md)  
  Enumera os registros de ativação correspondentes a um thread, mesclados dos mecanismos.  
  
  [Interface IDebugCookie](../winscript/reference/idebugcookie-interface.md)  
  Permite que o cookie de depuração seja definido nos depuradores de script.  
  
  [Interface IDebugHelper](../winscript/reference/idebughelper-interface.md)  
  Serve como uma fábrica para navegadores de objetos e pontos de conexão simples para mecanismos de script.  
  
  [Interface ISimpleConnectionPoint](../winscript/reference/isimpleconnectionpoint-interface.md)  
  Fornece uma maneira simples para descrever e enumerar os eventos acionados em um ponto de conexão específico, para mecanismos de script.  
  
## <a name="see-also"></a>Consulte também  
 [Active Script Debugger Interfaces](../winscript/reference/active-script-debugger-interfaces.md)
