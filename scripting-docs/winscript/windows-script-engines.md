---
title: Mecanismos do Windows Script | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Windows script engines
ms.assetid: e576853d-7252-4eb9-81eb-9d5bb7626ab4
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 27a500f9df91738e2db563f7e37ee646925b674e
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835687"
---
# <a name="windows-script-engines"></a>Mecanismos de script do Windows
Para implementar um mecanismo do Microsoft Windows Script, crie um objeto OLE COM que dá suporte às interfaces a seguir.  
  
|||  
|-|-|  
|Interface|Descrição|  
|[IActiveScript](../winscript/reference/iactivescript.md)|Fornece a capacidade de script básico. A implementação dessa interface é necessária.|  
|[IActiveScriptParse](../winscript/reference/iactivescriptparse.md)|Fornece a capacidade de adicionar texto de script, avaliar expressões e assim por diante. A implementação dessa interface é opcional. No entanto, se ela não for implementada, o mecanismo de script deverá implementar uma das interfaces IPersist* para carregar um script.|  
|IPersist*|Fornece suporte a persistência. A implementação de pelo menos uma das interfaces a seguir é necessária se [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) não está implementado.<br /><br /> IPersistStorage: dá suporte ao atributo DATA={url} na marca OBJECT.<br /><br /> IPersistStreamInit: dá suporte para o mesmo que `IPersistStorage`, bem como o atributo DATA="string-encoded byte stream" na marca OBJECT.<br /><br /> IPersistPropertyBag: dá suporte ao atributo PARAM= na marca OBJECT.|  
  
> [!NOTE]
> É possível que o mecanismo de script nunca seja chamado para salvar ou restaurar um estado de script por meio de `IPersist*`. Em vez disso, [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) é usado chamando [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) para criar um script em branco, em seguida, miniscripts são adicionados e conectados aos eventos com [IActiveScriptParse::AddScriptlet](../winscript/reference/iactivescriptparse-addscriptlet.md) e o código geral é adicionado com [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md). No entanto, um mecanismo de script deve implementar totalmente pelo menos uma interface `IPersist*` (preferencialmente `IPersistStreamInit`), pois outros aplicativos de host podem tentar utilizá-las.  
  
 As seções a seguir descrevem como implementar um mecanismo do Windows Script em mais detalhes.  
  
 Consulte a [referência a interfaces do Windows Script](../winscript/reference/windows-script-interfaces-reference.md) para obter mais informações.  
  
## <a name="registry-standard"></a>Padrão de Registro  
 Um mecanismo do Windows Script pode se identificar usando identificadores de categoria. Atualmente, o Windows Script define dois identificadores de categoria.  
  
|||  
|-|-|  
|Categoria|Descrição|  
|CATID_ActiveScript|Indica que os identificadores de classe (CLSIDs) são mecanismos de script do Windows que suportam, no mínimo, a interface [IActiveScript](../winscript/reference/iactivescript.md) e um mecanismo de persistência (a `IPersistStorage` `IPersistStreamInit` interface, ou IPersistPropertyBag).|  
|CATID_ActiveScriptParse|Indica que o CLSIDs são mecanismos do Windows Script que dão suporte a, no mínimo, as interfaces [IActiveScript](../winscript/reference/iactivescript.md) e [IActiveScriptParse](../winscript/reference/iactivescriptparse.md).|  
  
 Embora [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) não seja um verdadeiro mecanismo de persistência, ele dá suporte ao método [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md), que é funcionalmente equivalente a `IPersist*::InitNew`.  
  
## <a name="script-engine-states"></a>Estados de mecanismo de script  
 A qualquer determinado momento, um mecanismo do Windows Script pode estar em um de vários estados.  
  
|||  
|-|-|  
|Estado|Descrição|  
|não inicializado|O script não foi inicializado ou carregado usando uma interface IPersist* ou não tem uma interface [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) definida. O mecanismo de script geralmente não é utilizável neste estado até o script ser carregado.|  
|inicializado|O script foi inicializado com uma interface `IPersist*` e tem uma interface [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) definida, mas não está conectado a objetos de host e eventos de coletor. Observe que esse estado significa simplesmente que o método `IPersist*::Load`, `IPersist*::InitNew` ou [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) foi concluído e que o método [IActiveScript::SetScriptSite](../winscript/reference/iactivescript-setscriptsite.md) foi chamado. O mecanismo não é capaz de executar o código nesse modo. O mecanismo coloca na fila o código que o host passa a ele por meio do método [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) e executa o código após transicionar para o estado iniciado.<br /><br /> Já que as linguagens podem variar amplamente quanto à semântica, mecanismos de script não são necessários para dar suporte a essa transição de estado. Mecanismos que dão suporte ao método [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md) devem, no entanto, dar suporte a essa transição de estado. Os hosts devem se preparar para essa transição e executar a ação apropriada: liberar o mecanismo de script atual, criar um novo mecanismo de script e chamar `IPersist*::Load`, `IPersist*::InitNew` ou [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) (e possivelmente também chamar [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md)). O uso dessa transição deve ser considerado uma otimização das etapas acima. Observe que todas as informações que o mecanismo de script obteve sobre os nomes dos itens nomeados e as informações de tipo que descrevem itens nomeados permanecem válidas.<br /><br /> Já que as linguagens variarem muito, definir a semântica exata dessa transição é difícil. No mínimo, o mecanismo de script deve desconectar todos os eventos e liberar todos os ponteiros SCRIPTINFO_IUNKNOWN obtidos chamando o método [IActiveScriptSite::GetItemInfo](../winscript/reference/iactivescriptsite-getiteminfo.md). O mecanismo deverá obter novamente esses ponteiros depois que o script for executado novamente. O mecanismo de script também deve redefinir o script de volta para um estado inicial que apropriado para a linguagem. VBScript, por exemplo, redefine todas as variáveis e mantém qualquer código adicionado dinamicamente ao chamar [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) com o sinalizador SCRIPTTEXT_ISPERSISTENT definido. Outras linguagens talvez precisem manter os valores atuais (assim como Lisp, porque não há nenhuma separação de dados do código) ou redefinir para um estado conhecido (incluindo linguagens com variáveis inicializadas estaticamente).<br /><br /> Observe que a transição para o estado iniciado deve ter a mesma semântica (ou seja, ela deve deixar o mecanismo de script no mesmo estado) de uma chamada a `IPersist*::Save` para salvar o mecanismo de script e, em seguida, de uma chamada a `IPersist*::Load` para carregar um novo mecanismo de script; essas ações devem ter a mesma semântica de [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md). Os mecanismos de script que ainda não dão suporte a `IActiveScript::Clone` nem a `IPersist*` devem considerar com cautela como a transição para o estado iniciado deve se comportar, de modo que uma transição como essa não viole as condições acima caso o suporte a `IActiveScript::Clone` ou a `IPersist*` tenha sido adicionado posteriormente.<br /><br /> Durante a transição para o estado iniciado, o mecanismo de script se desconectará dos coletores de eventos após os destruidores apropriados serem executados no script. Para evitar que esses destruidores sejam executados, o host pode primeiro passar o script para o estado desconectado antes de passá-lo para o estado iniciado.<br /><br /> Use [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) para cancelar um thread em execução do script sem aguardar a conclusão da execução de eventos atuais.|  
|iniciado|A transição do estado inicializado para o estado iniciado faz com que o mecanismo execute qualquer código que tenha sido colocado em fila no estado inicializado. O mecanismo pode executar código enquanto está no estado iniciado, mas ele não está conectado a nenhum evento adicionado por meio do método [IActiveScript::AddNamedItem](../winscript/reference/iactivescript-addnameditem.md). O mecanismo pode executar código chamando a interface IDispatch obtida do método [IActiveScript::GetScriptDispatch](../winscript/reference/iactivescript-getscriptdispatch.md) ou chamando [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md). É possível que mais inicialização em segundo plano (carregamento progressivo) ainda esteja em andamento e que chamar o método [IActiveScript::SetScriptState](../winscript/reference/iactivescript-setscriptstate.md) com o sinalizador SCRIPTSTATE_CONNECTED definido pode fazer com que o script seja bloqueado até que a inicialização seja concluída.|  
|connected|O script é carregado e conectado para eventos de coletor de objetos de host. Se esta for uma transição do estado inicializado, o mecanismo de script deverá transicionar para o estado iniciado, executando as ações necessárias, antes de passar para o estado conectado e conectar-se a eventos.|  
|desconectado|O script é carregado e tem um estado de tempo de execução, mas fica temporariamente desconectado de eventos de coletor de objetos de host. Isso pode ser feito logicamente (ignorando eventos recebidos) ou fisicamente (chamando IConnectionPoint::Unadvise nos pontos de conexão apropriados). Se esta for uma transição do estado inicializado, o mecanismo de script deverá transicionar para o estado iniciado, executando as ações necessárias, antes de passar para o estado desconectado. Coletores de eventos que estão em andamento são concluídos antes das alterações de estado (use [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) para cancelar um thread de script em execução). Ao contrário do que ocorre com o estado inicializado, a transição para esse estado não causa a redefinição do script, o estado de tempo de execução do script não é redefinido e um procedimento de inicialização do script não é executado.|  
|closed|O script foi fechado. O mecanismo de script não funciona e retorna erros para a maioria dos métodos.|  
  
 A ilustração a seguir mostra as relações entre os diversos estados de mecanismo de script e mostra os métodos que causam transições de um estado para outro.  
  
 A ilustração a seguir mostra as ações que o mecanismo de script executa durante as várias transições de estado.  
  
## <a name="scripting-engine-threading"></a>Threading de mecanismo de script  
 Já que um mecanismo do Windows Script pode ser usado em muitos ambientes, é importante manter o seu modelo de execução o mais flexível possível. Por exemplo, um host baseado em servidor talvez precise preservar um design multi-threaded enquanto usa o Windows Script de forma eficiente. Ao mesmo tempo, um host que não usa threading, como um aplicativo típico, não deve ser sobrecarregado com gerenciamento de threading. O Windows Script atinge esse equilíbrio, restringindo as maneiras pelas quais um mecanismo de script de threading livre pode retornar a chamada para o host, liberando os hosts dessa carga.  
  
 Mecanismos de script usados nos servidores normalmente são implementados como objetos de thread livre. Isso significa que métodos na interface [IActiveScript](../winscript/reference/iactivescript.md) e respectivas interfaces associadas podem ser chamados de qualquer thread no processo, sem marshaling. (Infelizmente, isso também significa que o mecanismo de script deve ser implementado como um servidor em processo, porque o OLE atualmente não dá suporte ao marshaling entre processos de objetos de thread livre.) A sincronização é responsabilidade do mecanismo de script. Para mecanismos de script que não são reentrantes internamente ou para modelos de idioma que não são multi-threaded, a sincronização pode ser tão simples quanto serializar o acesso ao mecanismo de script com um mutex. É claro que certos métodos, tais como [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md), não devem ser serializados dessa forma, de modo que um script travado possa ser encerrado de outro thread.  
  
 O fato de que [IActiveScript](../winscript/reference/iactivescript.md) é normalmente de thread livre geralmente implica que a interface [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) e o modelo de objeto do host também devem ser de thread livre. Isso tornaria a implementação do host difícil, especialmente no caso comum em que o host é um aplicativo de thread único baseado em Windows com controles ActiveX de thread único ou modelo-apartamento em seu modelo de objeto. Por esse motivo, as restrições a seguir são colocadas sobre o uso do mecanismo de script de [IActiveScriptSite](../winscript/reference/iactivescriptsite.md):  
  
 O site de script é chamado no contexto de um thread de host. Ou seja, o script do mecanismo nunca chama o site de script no contexto de um thread que o mecanismo de script criou, mas apenas de dentro de um método de mecanismo de script que foi chamado do host por meio de [IActiveScript](../winscript/reference/iactivescript.md) e seus derivativos, por meio do objeto de expedição do mecanismo de script exposto, por meio de uma mensagem do Windows ou de uma origem do evento no modelo de objeto do host.  
  
 O site de script nunca é chamado de dentro do contexto de um simples método de controle de estado de thread (por exemplo, o método [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md)) ou o método [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md).  
  
## <a name="see-also"></a>Confira também  
 [Interfaces do Windows Script](../winscript/windows-script-interfaces.md)
