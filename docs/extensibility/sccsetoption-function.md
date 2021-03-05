---
description: Essa função define opções que controlam o comportamento do plug-in de controle do código-fonte.
title: Função SccSetOption | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccSetOption
helpviewer_keywords:
- SccSetOption function
ms.assetid: 4b5e6666-c24c-438a-a9df-9c52f58f8175
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e25647eb8d2e5796665f072af6df43b2f585c7b0
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221373"
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

no A estrutura de contexto do plug-in de controle do código-fonte.

 nOption

no A opção que está sendo definida.

 dwVal

no Configurações da opção.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A opção foi definida com êxito.|
|SCC_I_SHARESUBPROJOK|Retornado se `nOption` `SCC_OPT_SHARESUBPROJ` o WAS e o plug-in de controle do código-fonte permitir que o IDE defina a pasta de destino.|
|SCC_E_OPNOTSUPPORTED|A opção não foi definida e não deve ser confiável.|

## <a name="remarks"></a>Comentários
 O IDE chama essa função para controlar o comportamento do plug-in de controle do código-fonte. O primeiro parâmetro, `nOption` , indica o valor que está sendo definido, enquanto o segundo, `dwVal` , indica o que fazer com esse valor. O plug-in armazena essas informações associadas a um `pvContext``,` , portanto, o IDE deve chamar essa função depois de chamar o [SccInitialize](../extensibility/sccinitialize-function.md) (mas não necessariamente após cada chamada para o [SccOpenProject](../extensibility/sccopenproject-function.md)).

 Resumo das opções e seus valores:

|`nOption`|`dwValue`|Descrição|
|---------------|---------------|-----------------|
|`SCC_OPT_EVENTQUEUE`|`SCC_OPT_EQ_DISABLE`<br /><br /> `SCC_OPT_EQ_ENABLE`|Habilita/desabilita o enfileiramento de eventos em segundo plano.|
|`SCC_OPT_USERDATA`|Valor arbitrário|Especifica um valor de usuário a ser passado para a função de retorno de chamada [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md) .|
|`SCC_OPT_HASCANCELMODE`|`SCC_OPT_HCM_NO`<br /><br /> `SCC_OPT_HCM_YES`|Indica se o IDE dá suporte atualmente à cancelamento de uma operação.|
|`SCC_OPT_NAMECHANGEPFN`|Ponteiro para a função de retorno de chamada [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)|Define um ponteiro para uma função de retorno de chamada de nome-alteração.|
|`SCC_OPT_SCCCHECKOUTONLY`|`SCC_OPT_SCO_NO`<br /><br /> `SCC_OPT_SCO_YES`|Indica se o IDE permite o check-out de seus arquivos manualmente (por meio da interface do usuário do controle do código-fonte) ou se eles devem ser verificados somente por meio do plug-in de controle do código-fonte.|
|`SCC_OPT_SHARESUBPROJ`|N/D|Se o plug-in de controle do código-fonte permitir que o IDE especifique a pasta do projeto local, o plug-in retornará `SCC_I_SHARESUBPROJOK` .|

## <a name="scc_opt_eventqueue"></a>SCC_OPT_EVENTQUEUE
 Se `nOption` for `SCC_OPT_EVENTQUEUE` , o IDE está desabilitando (ou reabilitando) o processamento em segundo plano. Por exemplo, durante uma compilação, o IDE pode instruir o plug-in de controle do código-fonte para interromper o processamento ocioso de qualquer tipo. Após a compilação, ele reabilitará o processamento em segundo plano para manter a fila de eventos do plug-in atualizada. Correspondente ao `SCC_OPT_EVENTQUEUE` valor de `nOption` , há dois valores possíveis para `dwVal` , ou seja, `SCC_OPT_EQ_ENABLE` e `SCC_OPT_EQ_DISABLE` .

## <a name="scc_opt_hascancelmode"></a>SCC_OPT_HASCANCELMODE
 Se o valor de `nOption` for `SCC_OPT_HASCANCELMODE` , o IDE permitirá que os usuários cancelem operações longas. A configuração `dwVal` para `SCC_OPT_HCM_NO` (o padrão) indica que o IDE não tem modo de cancelamento. O plug-in de controle do código-fonte deve oferecer seu próprio botão cancelar se desejar que o usuário seja capaz de cancelar. `SCC_OPT_HCM_YES` indica que o IDE fornece a capacidade de cancelar uma operação, de modo que o plug-in SCC não precisa exibir seu próprio botão Cancelar. Se o IDE `dwVal` for definido como `SCC_OPT_HCM_YES` , ele será preparado para responder `SCC_MSG_STATUS` e `DOCANCEL` mensagens enviadas para a `lpTextOutProc` função de retorno de chamada (consulte [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)). Se o IDE não definir essa variável, o plug-in não deverá enviar essas duas mensagens.

## <a name="scc_opt_namechangepfn"></a>SCC_OPT_NAMECHANGEPFN
 Se nOption for definido como `SCC_OPT_NAMECHANGEPFN` , e o plug-in de controle do código-fonte e o IDE permitirem, o plug-in poderá realmente renomear ou mover um arquivo durante uma operação de controle do código-fonte. O `dwVal` será definido como um ponteiro de função do tipo [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md). Durante uma operação de controle do código-fonte, o plug-in pode chamar essa função, passando três parâmetros. Esses são os nomes antigos (com caminho totalmente qualificado) de um arquivo, o novo nome (com caminho totalmente qualificado) desse arquivo e um ponteiro para informações que têm relevância para o IDE. O IDE envia nesse último ponteiro chamando `SccSetOption` with `nOption` definido como `SCC_OPT_USERDATA` , `dwVal` apontando para os dados. O suporte para essa função é opcional. Um plug-VSSCI que usa essa capacidade deve inicializar seu ponteiro de função e variáveis de dados de usuário para `NULL` , e não deve chamar uma função de renomeação, a menos que tenha sido fornecida uma. Ele também deve estar preparado para manter o valor fornecido ou alterá-lo em resposta a uma nova chamada para `SccSetOption` . Isso não ocorrerá no meio de uma operação de comando de controle do código-fonte, mas pode acontecer entre os comandos.

## <a name="scc_opt_scccheckoutonly"></a>SCC_OPT_SCCCHECKOUTONLY
 Se nOption for definido como `SCC_OPT_SCCCHECKOUTONLY` , o IDE indica que os arquivos no projeto aberto no momento nunca devem fazer check-out manualmente por meio da interface do usuário do sistema de controle do código-fonte. Em vez disso, os arquivos devem ser verificados somente por meio do plug-in de controle do código-fonte sob controle IDE. Se `dwValue` é definido como `SCC_OPT_SCO_NO` , isso significa que os arquivos devem ser tratados normalmente pelo plug-in e podem ser submetidos a check-out por meio da interface do usuário do controle do código-fonte. Se `dwValue` é definido como `SCC_OPT_SCO_YES` , somente o plug-in tem permissão para fazer check-out de arquivos e a interface do usuário do sistema de controle do código-fonte não deve ser invocada. Isso é para situações em que o IDE pode ter "pseudo-arquivos" que fazem sentido fazer check-out apenas pelo IDE.

## <a name="scc_opt_sharesubproj"></a>SCC_OPT_SHARESUBPROJ
 Se `nOption` é definido como `SCC_OPT_SHARESUBPROJ` , o IDE está testando se o plug-in de controle do código-fonte pode usar uma pasta local especificada ao adicionar arquivos do controle do código-fonte. O valor do `dwVal` parâmetro não importa nesse caso. Se o plug-in permitir que o IDE especifique a pasta de destino local em que os arquivos serão adicionados do controle do código-fonte quando o [SccAddFromScc](../extensibility/sccaddfromscc-function.md) for chamado, o plug-in deverá retornar `SCC_I_SHARESUBPROJOK` quando a `SccSetOption` função for chamada. Em seguida, o IDE usa o `lplpFileNames` parâmetro da `SccAddFromScc` função para passar a pasta de destino. O plug-in usa essa pasta de destino para posicionar os arquivos adicionados do controle do código-fonte. Se o plug-in não retornar `SCC_I_SHARESUBPROJOK` quando a `SCC_OPT_SHARESUBPROJ` opção for definida, o IDE assumirá que o plug-in é capaz de adicionar arquivos somente na pasta local atual.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccAddFromScc](../extensibility/sccaddfromscc-function.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)
