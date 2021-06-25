---
description: Essa função solicita ao usuário opções avançadas para um determinado comando.
title: Função SccGetCommandOptions | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetCommandOptions
helpviewer_keywords:
- SccGetCommandOptions function
ms.assetid: bbe4aa4e-b4b0-403e-b7a0-5dd6eb24e5a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7972d874668649b8bb86adc15008880c5fc4152e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903925"
---
# <a name="sccgetcommandoptions-function"></a>Função SccGetCommandOptions
Essa função solicita ao usuário opções avançadas para um determinado comando.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccGetCommandOptions(
   LPVOID pvContext,
   HWND hWnd,
   enum SCCCOMMAND iCommand,
   LPCMDOPTS* ppvOptions
);
```

### <a name="parameters"></a>Parâmetros
 pvContext

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 Icommand

[in] O comando para o qual as opções avançadas são solicitadas (consulte [Código de comando](../extensibility/command-code-enumerator.md) para ver os valores possíveis).

 ppvOptions

[in] A estrutura de opções (também pode ser `NULL` ).

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Sucesso.|
|SCC_I_ADV_SUPPORT|O plug-in de controle do código-fonte dá suporte a opções avançadas para o comando.|
|SCC_I_OPERATIONCANCELED|O usuário cancelou a caixa de diálogo Opções do plug-in do controle **do** código-fonte.|
|SCC_E_OPTNOTSUPPORTED|O plug-in de controle do código-fonte não dá suporte a essa operação.|
|SCC_E_ISCHECKEDOUT|Não é possível executar essa operação em um arquivo que está sendo verificado no momento.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção. Uma nova tentativa é recomendada.|
|SCC_E_NONSPECIFICERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 O IDE chama essa função pela primeira vez com para determinar se o plug-in de controle do código-fonte dá suporte ao recurso de opções avançadas para `ppvOptions` = `NULL` o comando especificado. Se o plug-in dá suporte ao recurso para esse comando, o IDE chama essa  função novamente quando o usuário solicita opções avançadas (geralmente implementadas como um botão Avançado em uma caixa de diálogo) e fornece um ponteiro não NULL para que aponta para `ppvOptions` um `NULL` ponteiro. O plug-in armazena todas as opções avançadas especificadas pelo usuário em uma estrutura privada e retorna um ponteiro para essa estrutura no `ppvOptions` . Essa estrutura é então passada para todas as outras funções de API de plug-in de controle do código-fonte que precisam saber sobre ela, incluindo chamadas subsequentes para a `SccGetCommandOptions` função.

 Um exemplo pode ajudar a esclarecer essa situação.

 Um usuário escolhe o comando **Obter** e o IDE exibe uma caixa **de diálogo** Obter. O IDE chama a `SccGetCommandOptions` função com definido como e definido como `iCommand` `SCC_COMMAND_GET` `ppvOptions` `NULL` . Isso é interpretado pelo plug-in de controle do código-fonte como a pergunta "Você tem opções avançadas para esse comando?" Se o plug-in retornar `SCC_I_ADV_SUPPORT` , o IDE exibirá um **botão** Avançado em sua caixa **de diálogo** Obter.

 Na primeira vez que o usuário clicar no **botão** Avançado, o IDE chamará novamente a função , desta vez com um que não aponta `SccGetCommandOptions` para um `NULL``ppvOptions` `NULL` ponteiro. O plug-in exibe  sua própria caixa de diálogo Obter Opções, solicita informações ao usuário, coloca essas informações em sua própria estrutura e retorna um ponteiro para essa estrutura no `ppvOptions` .

 Se o usuário clicar em **Avançado** novamente na mesma caixa de diálogo, o IDE chamará a função novamente sem alterar , para que a estrutura seja passada de volta para `SccGetCommandOptions` o `ppvOptions` plug-in. Isso permite que o plug-in reinicializar sua caixa de diálogo para os valores que o usuário definiu anteriormente. O plug-in modifica a estrutura no local antes de retornar.

 Por fim, quando o usuário clica em  **OK** na caixa de diálogo Obter do IDE, o IDE chama o [SccGet](../extensibility/sccget-function.md), passando a estrutura retornada em que contém as `ppvOptions` opções avançadas.

> [!NOTE]
> O comando é usado quando o IDE exibe uma caixa de diálogo Opções que permite ao usuário definir preferências que controlam `SCC_COMMAND_OPTIONS` como a integração funciona.  Se o plug-in de controle do código-fonte quiser fornecer suas  próprias preferências, ele poderá exibi-lo de um botão Avançado na caixa de diálogo Preferências do IDE. O plug-in é exclusivamente responsável por obter e persistir essas informações; O IDE não o usa nem o modifica.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Código de comando](../extensibility/command-code-enumerator.md)
