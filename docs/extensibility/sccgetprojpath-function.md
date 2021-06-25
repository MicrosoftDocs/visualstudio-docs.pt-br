---
description: Essa função solicita ao usuário um caminho de projeto, que é uma cadeia de caracteres que é significativa apenas para o plug-in de controle do código-fonte.
title: Função SccGetProjPath | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetProjPath
helpviewer_keywords:
- SccGetProjPath function
ms.assetid: 1079847e-d45f-4cb8-9d92-1e01ce5d08f6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 93266464249b8de037a618bab55ede31988384cb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901065"
---
# <a name="sccgetprojpath-function"></a>Função SccGetProjPath
Essa função solicita ao usuário um caminho de projeto, que é uma cadeia de caracteres que é significativa apenas para o plug-in de controle do código-fonte. Ele é chamado quando o usuário é:

- Crie um novo projeto

- Adicionando um projeto existente ao controle de versão

- Tentando localizar um projeto de controle de versão existente

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccGetProjPath (
   LPVOID pvContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPSTR  lpProjName,
   LPSTR  lpLocalPath,
   LPSTR  lpAuxProjPath,
   BOOL   bAllowChangePath,
   LPBOOL pbNew
);
```

### <a name="parameters"></a>Parâmetros
 pvContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 lpUser

[entrada, saída] O nome de usuário (sem exceder SCC_USER_SIZE, incluindo o terminador nulo)

 lpProjName

[entrada, saída] O nome do projeto IDE, espaço de trabalho do projeto ou Makefile (sem exceder SCC_PRJPATH_SIZE, incluindo o terminador nulo).

 lpLocalPath

[entrada, saída] O caminho de trabalho do projeto. Se `bAllowChangePath` for `TRUE` , o plug-in de controle do código-fonte poderá modificar essa cadeia de caracteres (sem exceder _MAX_PATH, incluindo o terminador nulo).

 lpAuxProjPath

[entrada, saída] Um buffer para o caminho do projeto retornado (sem exceder SCC_PRJPATH_SIZE, incluindo o terminador nulo).

 bAllowChangePath

no Se for `TRUE` , o plug-in de controle do código-fonte poderá solicitar e modificar a `lpLocalPath` cadeia de caracteres.

 pbNew

[entrada, saída] O valor em entrada indica se um novo projeto deve ser criado. O valor retornado indica o êxito da criação de um projeto:

|Entrada|Interpretação|
|--------------|--------------------|
|TRUE|O usuário pode criar um novo projeto.|
|FALSE|O usuário não pode criar um novo projeto.|

|Saída|Interpretação|
|--------------|--------------------|
|TRUE|Um novo projeto foi criado.|
|FALSE|Um projeto existente foi selecionado.|

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O projeto foi criado ou recuperado com êxito.|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção.|
|SCC_E_CONNECTIONFAILURE|Houve um problema ao tentar se conectar ao sistema de controle do código-fonte.|
|SCC_E_NONSPECIFICERROR|Ocorreu um erro não especificado.|

## <a name="remarks"></a>Comentários
 A finalidade dessa função é que o IDE adquira os parâmetros `lpProjName` e `lpAuxProjPath` . Depois que o plug-in de controle do código-fonte solicita ao usuário essas informações, ele passa essas duas cadeias de caracteres de volta para o IDE. O IDE persiste essas cadeias de caracteres em seu arquivo de solução e as transmite para o [SccOpenProject](../extensibility/sccopenproject-function.md) sempre que o usuário abrir esse projeto. Essas cadeias de caracteres permitem que o plug-in rastreie informações associadas a um projeto.

 Quando a função é chamada pela primeira vez, `lpAuxProjPath` é definida como uma cadeia de caracteres vazia. `lProjName` também pode estar vazio, ou pode conter o nome do projeto IDE, que o plug-in de controle do código-fonte pode usar ou ignorar. Quando a função retorna com êxito, o plug-in retorna as duas cadeias de caracteres correspondentes. O IDE não faz suposições sobre essas cadeias de caracteres, não as usará e não permitirá que o usuário as modifique. Se o usuário quiser alterar as configurações, o IDE chamará `SccGetProjPath` novamente, passando os mesmos valores recebidos na hora anterior. Isso fornece ao plug-in o controle completo sobre essas duas cadeias de caracteres.

 Para `lpUser` o, o IDE pode passar um nome de usuário ou pode simplesmente passar um ponteiro para uma cadeia de caracteres vazia. Se houver um nome de usuário, o plug-in de controle do código-fonte deverá usá-lo como padrão. No entanto, se nenhum nome foi passado ou se o logon falhou com o nome fornecido, o plug-in deverá solicitar um logon ao usuário e passar o nome novamente `lpUser` quando receber um logon válido. Como o plug-in pode alterar essa cadeia de caracteres, o IDE sempre aloca um buffer de tamanho ( `SCC_USER_LEN` + 1).

> [!NOTE]
> A primeira ação que o IDE executa pode ser uma chamada para a `SccOpenProject` função ou a `SccGetProjPath` função. Portanto, ambos têm um `lpUser` parâmetro idêntico, que habilita o plug-in de controle do código-fonte para registrar o usuário em qualquer momento. Mesmo que o retorno da função indique uma falha, o plug-in deve preencher essa cadeia de caracteres com um nome de logon válido.

 `lpLocalPath` é o diretório onde o usuário mantém o projeto. Pode ser uma cadeia de caracteres vazia. Se não houver nenhum diretório definido atualmente (como no caso de um usuário tentar baixar um projeto do sistema de controle do código-fonte) e `bAllowChangePath` , se for `TRUE` , o plug-in de controle do código-fonte poderá solicitar a entrada do usuário ou usar algum outro método para posicionar sua própria cadeia de caracteres `lpLocalPath` . Se `bAllowChangePath` for `FALSE` , o plug-in não deverá alterar a cadeia de caracteres, pois o usuário já está trabalhando no diretório especificado.

 Se o usuário criar um novo projeto a ser colocado no controle do código-fonte, o plug-in de controle do código-fonte poderá não criá-lo de fato no sistema de controle do código-fonte no momento que `SccGetProjPath` for chamado. Em vez disso, ele passa de volta a cadeia de caracteres junto com um valor diferente de zero para `pbNew` , indicando que o projeto será criado no sistema de controle do código-fonte.

 Por exemplo, se um usuário no assistente de **novo projeto** no Visual Studio Adicionar seu projeto ao controle do código-fonte, o Visual Studio chamará essa função, e o plug-in determinará se não há problema em criar um novo projeto no sistema de controle do código-fonte para conter o projeto do Visual Studio. Se o usuário clicar em **Cancelar** antes de concluir o assistente, o projeto nunca será criado. Se o usuário clicar em **OK**, o Visual Studio chamará `SccOpenProject` , passando `SCC_OPT_CREATEIFNEW` e o projeto controlado por origem será criado nesse momento.

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
