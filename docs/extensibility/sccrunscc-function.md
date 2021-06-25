---
description: Essa função invoca a ferramenta de administração do controle do código-fonte.
title: Função SccRunScc | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccRunScc
helpviewer_keywords:
- SccRunScc function
ms.assetid: bbe7c931-b17a-4779-9cf6-59e5f9f0c172
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c865931ed52601761f0bd519bf360d584d49ec04
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904107"
---
# <a name="sccrunscc-function"></a>Função SccRunScc
Essa função invoca a ferramenta de administração do controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccRunScc(
   LPVOID  pvContext,
   HWND    hWnd,
   LONG    nFiles,
   LPCSTR* lpFileNames
);
```

#### <a name="parameters"></a>Parâmetros
 pvContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 nFiles

no Número de arquivos especificados na `lpFileNames` matriz.

 lpFileNames

no Matriz de nomes de arquivo selecionados.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A ferramenta de administração do controle do código-fonte foi invocada com êxito.|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada.|
|SCC_E_INITIALIZEFAILED|Falha ao inicializar o sistema de controle do código-fonte.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção.|
|SCC_E_CONNECTIONFAILURE|Falha ao conectar ao sistema de controle do código-fonte.|
|SCC_E_FILENOTCONTROLLED|O arquivo selecionado não está no controle do código-fonte.|
|SCC_E_NONSPECIFICERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Essa função permite que o chamador acesse a gama completa de recursos do sistema de controle do código-fonte por meio de uma ferramenta de administração externa. Se o sistema de controle do código-fonte não tiver nenhuma interface do usuário, o plug-in de controle do código-fonte poderá implementar uma interface para executar as funções de administração necessárias.

 Essa função é chamada com uma contagem e uma matriz de nomes de arquivo para os arquivos selecionados no momento. Se a ferramenta de administração oferecer suporte a ela, a lista de arquivos poderá ser usada para preselecionar arquivos na interface de administração; caso contrário, a lista poderá ser ignorada.

 Essa função é normalmente invocada quando o usuário seleciona **a \<Source Control Server> inicialização** no   ->  menu **controle de origem** do arquivo. Essa opção de menu **Iniciar** pode ser sempre desabilitada ou até mesmo oculta com a definição de uma entrada de registro. Consulte [como: instalar um plug-in de controle do código-fonte](../extensibility/internals/how-to-install-a-source-control-plug-in.md) para obter detalhes. Essa função será chamada somente se [SccInitialize](../extensibility/sccinitialize-function.md) retornar o `SCC_CAP_RUNSCC` bit de recurso (consulte os [sinalizadores de capacidade](../extensibility/capability-flags.md) para obter detalhes sobre esse e outros bits de funcionalidade).

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Como instalar um plug-in de controle do código-fonte](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [Sinalizadores de capacidade](../extensibility/capability-flags.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
