---
description: Essa função define opções que controlam o comportamento do plug-in de controle do código-fonte.
title: Função SccSetOption | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccSetOption
helpviewer_keywords:
- SccSetOption function
ms.assetid: 4b5e6666-c24c-438a-a9df-9c52f58f8175
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 18e33cbb8dbee9b332456826ed33e46e4d2e76de
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904094"
---
# <a name="sccsetoption-function"></a>Função SccSetOption
Essa função define opções que controlam o comportamento do plug-in de controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccSetOption(
   LPVOID pvContext,
   LONG   nOption,
   LONG   dwVal
);
```

#### <a name="parameters"></a>Parâmetros
 pvContext

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 nOption

[in] A opção que está sendo definida.

 dwVal

[in] Configurações para a opção.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A opção foi definida com êxito.|
|SCC_I_SHARESUBPROJOK|Retornado se `nOption` era `SCC_OPT_SHARESUBPROJ` e o plug-in de controle do código-fonte permite que o IDE de definir a pasta de destino.|
|SCC_E_OPNOTSUPPORTED|A opção não foi definida e não deve ser confiada.|

## <a name="remarks"></a>Comentários
 O IDE chama essa função para controlar o comportamento do plug-in de controle do código-fonte. O primeiro parâmetro, , indica o valor que está sendo definido, enquanto o segundo, , indica o `nOption` que fazer com esse `dwVal` valor. O plug-in armazena essas informações associadas a um, de modo que o IDE deve chamar essa função depois de chamar `pvContext``,` [sccInitialize](../extensibility/sccinitialize-function.md) (mas não necessariamente após cada chamada para [o SccOpenProject](../extensibility/sccopenproject-function.md)).

 Resumo das opções e seus valores:

|`nOption`|`dwValue`|Descrição|
|---------------|---------------|-----------------|
|`SCC_OPT_EVENTQUEUE`|`SCC_OPT_EQ_DISABLE`<br /><br /> `SCC_OPT_EQ_ENABLE`|Habilita/desabilita a fila de eventos em segundo plano.|
|`SCC_OPT_USERDATA`|Valor arbitrário|Especifica um valor de usuário a ser passado para a função de retorno de chamada [OPTNAMECHANGEPFN.](../extensibility/optnamechangepfn.md)|
|`SCC_OPT_HASCANCELMODE`|`SCC_OPT_HCM_NO`<br /><br /> `SCC_OPT_HCM_YES`|Indica se o IDE atualmente dá suporte ao cancelamento de uma operação.|
|`SCC_OPT_NAMECHANGEPFN`|Ponteiro para a função de retorno de chamada [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)|Define um ponteiro para uma função de retorno de chamada de alteração de nome.|
|`SCC_OPT_SCCCHECKOUTONLY`|`SCC_OPT_SCO_NO`<br /><br /> `SCC_OPT_SCO_YES`|Indica se o IDE permite fazer check-out de seus arquivos manualmente (por meio da interface do usuário do controle do código-fonte) ou se eles devem ser verificados somente por meio do plug-in de controle do código-fonte.|
|`SCC_OPT_SHARESUBPROJ`|N/D|Se o plug-in de controle do código-fonte permitir que o IDE especifique a pasta do projeto local, o plug-in retornará `SCC_I_SHARESUBPROJOK` .|

## <a name="scc_opt_eventqueue"></a>SCC_OPT_EVENTQUEUE
 Se `nOption` for , o `SCC_OPT_EVENTQUEUE` IDE está desabilitando (ou reabilitando) o processamento em segundo plano. Por exemplo, durante uma compilação, o IDE pode instruir o plug-in de controle do código-fonte a parar o processamento inativo de qualquer tipo. Após a compilação, ele reabilitaria o processamento em segundo plano para manter a fila de eventos do plug-in atualizada. Correspondente ao `SCC_OPT_EVENTQUEUE` valor de , há dois valores `nOption` possíveis para , ou `dwVal` seja, e `SCC_OPT_EQ_ENABLE` `SCC_OPT_EQ_DISABLE` .

## <a name="scc_opt_hascancelmode"></a>SCC_OPT_HASCANCELMODE
 Se o valor para `nOption` for `SCC_OPT_HASCANCELMODE` , o IDE permitirá que os usuários cancelem operações longas. Definir `dwVal` como `SCC_OPT_HCM_NO` (o padrão) indica que o IDE não tem nenhum modo de cancelamento. O plug-in de controle do código-fonte deve oferecer seu próprio botão Cancelar se quiser que o usuário possa cancelar. `SCC_OPT_HCM_YES` indica que o IDE fornece a capacidade de cancelar uma operação, portanto, o plug-in SCC não precisa exibir seu próprio botão Cancelar. Se o IDE define como , ele está preparado para responder às mensagens e enviadas à função de retorno de chamada `dwVal` `SCC_OPT_HCM_YES` `SCC_MSG_STATUS` `DOCANCEL` `lpTextOutProc` [(consulte LPTEXTOUTPROC](../extensibility/lptextoutproc.md)). Se o IDE não definir essa variável, o plug-in não deverá enviar essas duas mensagens.

## <a name="scc_opt_namechangepfn"></a>SCC_OPT_NAMECHANGEPFN
 Se nOption estiver definido como e o plug-in de controle do código-fonte e o IDE permitirem, o plug-in poderá realmente renomear ou mover um arquivo durante uma operação de controle `SCC_OPT_NAMECHANGEPFN` do código-fonte. O `dwVal` será definido como um ponteiro de função do tipo [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md). Durante uma operação de controle do código-fonte, o plug-in pode chamar essa função, passando três parâmetros. Esses são o nome antigo (com caminho totalmente qualificado) de um arquivo, o novo nome (com caminho totalmente qualificado) desse arquivo e um ponteiro para informações que têm relevância para o IDE. O IDE envia neste último ponteiro chamando `SccSetOption` com definido como , apontando para os `nOption` `SCC_OPT_USERDATA` `dwVal` dados. O suporte para essa função é opcional. Um plug-in VSSCI que usa essa capacidade deve inicializar seu ponteiro de função e as variáveis de dados do usuário para e não deve chamar uma função de renomeação, a menos que tenha sido `NULL` dada uma. Ele também deve estar preparado para manter o valor que foi dado ou alterá-lo em resposta a uma nova chamada para `SccSetOption` . Isso não acontecerá no meio de uma operação de comando de controle do código-fonte, mas isso pode acontecer entre comandos.

## <a name="scc_opt_scccheckoutonly"></a>SCC_OPT_SCCCHECKOUTONLY
 Se nOption estiver definido como , o IDE indicará que os arquivos no projeto aberto no momento nunca devem ser verificados manualmente por meio da interface do usuário do sistema de controle do `SCC_OPT_SCCCHECKOUTONLY` código-fonte. Em vez disso, os arquivos devem ser verificados somente por meio do plug-in de controle do código-fonte no controle IDE. Se for definido como , isso significa que os arquivos devem ser tratados normalmente pelo plug-in e podem ser verificados por meio da interface do usuário `dwValue` `SCC_OPT_SCO_NO` do controle do código-fonte. Se for definido como , somente o plug-in poderá fazer check-out de arquivos e a interface do usuário do sistema de controle do `dwValue` `SCC_OPT_SCO_YES` código-fonte não deverá ser invocada. Isso se trata de situações em que o IDE pode ter "pseudo-arquivos" que fazem sentido fazer check-out somente por meio do IDE.

## <a name="scc_opt_sharesubproj"></a>SCC_OPT_SHARESUBPROJ
 Se for definido como , o IDE testará se o plug-in de controle do código-fonte pode usar uma pasta local especificada ao adicionar `nOption` arquivos do controle do `SCC_OPT_SHARESUBPROJ` código-fonte. O valor do `dwVal` parâmetro não importa nesse caso. Se o plug-in permitir que o IDE especifique a pasta de destino local em que os arquivos serão adicionados do controle do código-fonte quando [o SccAddFromScc](../extensibility/sccaddfromscc-function.md) for chamado, o plug-in deverá retornar quando a função for `SCC_I_SHARESUBPROJOK` `SccSetOption` chamada. Em seguida, o IDE `lplpFileNames` usa o parâmetro da função para passar a pasta de `SccAddFromScc` destino. O plug-in usa essa pasta de destino para colocar os arquivos adicionados do controle do código-fonte. Se o plug-in não retornar quando a opção for definida, o IDE assumirá que o plug-in é capaz de adicionar arquivos somente na `SCC_I_SHARESUBPROJOK` `SCC_OPT_SHARESUBPROJ` pasta local atual.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccAddFromScc](../extensibility/sccaddfromscc-function.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)
