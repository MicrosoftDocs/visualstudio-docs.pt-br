---
description: Essa função solicita ao usuário opções avançadas para um determinado comando.
title: Função SccGetCommandOptions | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGetCommandOptions
helpviewer_keywords:
- SccGetCommandOptions function
ms.assetid: bbe4aa4e-b4b0-403e-b7a0-5dd6eb24e5a9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 400b778cf5e26b0cabad0fb19c548b2faa0a803f
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102220801"
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

no A estrutura de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 iCommand

no O comando para o qual as opções avançadas são solicitadas (consulte o [código de comando](../extensibility/command-code-enumerator.md) para obter os valores possíveis).

 ppvOptions

no A estrutura da opção (também pode ser `NULL` ).

## <a name="return-value"></a>Retornar valor
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Sucesso.|
|SCC_I_ADV_SUPPORT|O plug-in de controle do código-fonte dá suporte a opções avançadas para o comando.|
|SCC_I_OPERATIONCANCELED|O usuário cancelou a caixa de diálogo **Opções** do plug-in de controle do código-fonte.|
|SCC_E_OPTNOTSUPPORTED|O plug-in de controle do código-fonte não oferece suporte a esta operação.|
|SCC_E_ISCHECKEDOUT|Não é possível executar esta operação em um arquivo que está com check-out no momento.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. Uma nova tentativa é recomendada.|
|SCC_E_NONSPECIFICERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 O IDE chama essa função pela primeira vez com o `ppvOptions` = `NULL` para determinar se o plug-in de controle do código-fonte dá suporte ao recurso de opções avançadas para o comando especificado. Se o plug-in oferece suporte ao recurso para esse comando, o IDE chama essa função novamente quando o usuário solicita opções avançadas (geralmente implementadas como um botão **avançado** em uma caixa de diálogo) e fornece um ponteiro não nulo para os `ppvOptions` pontos para um `NULL` ponteiro. O plug-in armazena todas as opções avançadas especificadas pelo usuário em uma estrutura privada e retorna um ponteiro para essa estrutura no `ppvOptions` . Essa estrutura é passada para todas as outras funções da API de plug-in de controle do código-fonte que precisam saber sobre ela, incluindo chamadas subsequentes para a `SccGetCommandOptions` função.

 Um exemplo pode ajudar a esclarecer essa situação.

 Um usuário escolhe o comando **Get** e o IDE exibe uma caixa de diálogo **Get** . O IDE chama a `SccGetCommandOptions` função com `iCommand` definido como `SCC_COMMAND_GET` e `ppvOptions` definido como `NULL` . Isso é interpretado pelo plug-in de controle do código-fonte como a pergunta "você tem alguma opção avançada para este comando?" Se o plug-in retornar `SCC_I_ADV_SUPPORT` , o IDE exibirá um botão **avançado** na caixa de diálogo **obter** .

 Na primeira vez que o usuário clica no botão **avançado** , o IDE chama a `SccGetCommandOptions` função novamente, desta vez com um `NULL``ppvOptions` que não aponta para um `NULL` ponteiro. O plug-in exibe sua própria caixa de diálogo de **Opções Get** , solicita informações ao usuário, coloca essas informações em sua própria estrutura e retorna um ponteiro para essa estrutura no `ppvOptions` .

 Se o usuário clicar em **avançado** novamente na mesma caixa de diálogo, o IDE chamará a `SccGetCommandOptions` função novamente sem alterar `ppvOptions` , para que a estrutura seja passada de volta para o plug-in. Isso permite que o plug-in reinicialize sua caixa de diálogo para os valores que o usuário definiu anteriormente. O plug-in modifica a estrutura em vigor antes de retornar.

 Por fim, quando o usuário clica em **OK** na caixa de diálogo **Get** do IDE, o IDE chama o [SccGet](../extensibility/sccget-function.md), passando a estrutura retornada no `ppvOptions` que contém as opções avançadas.

> [!NOTE]
> O comando `SCC_COMMAND_OPTIONS` é usado quando o IDE exibe uma caixa de diálogo **Opções** que permite que o usuário defina as preferências que controlam como a integração funciona. Se o plug-in de controle do código-fonte quiser fornecer sua própria caixa de diálogo de preferências, ele poderá exibi-lo de um botão **avançado** na caixa de diálogo Preferências do IDE. O plug-in é exclusivamente responsável por obter e persistir essas informações; o IDE não o usa ou o modifica.

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Código de comando](../extensibility/command-code-enumerator.md)
