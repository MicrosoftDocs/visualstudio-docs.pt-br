---
description: Essa função exibe o histórico dos arquivos especificados.
title: Função SccHistory | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccHistory
helpviewer_keywords:
- SccHistory function
ms.assetid: a636d9d3-47c1-4b48-ac6b-bcfde19d6cf9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1208bd0cb13661f1aa60bb9f97c9e4502e517e6d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902534"
---
# <a name="scchistory-function"></a>Função SccHistory
Essa função exibe o histórico dos arquivos especificados.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccHistory(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>Parâmetros
 `pvContext`

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 `hWnd`

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 `nFiles`

[in] Número de arquivos especificados na `lpFileName` matriz.

 `lpFileName`

[in] Matriz de nomes totalmente qualificados de arquivos.

 `fOptions`

[in] Sinalizadores de comando (atualmente não usados).

 `pvOptions`

[in] Opções específicas do plug-in de controle do código-fonte.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O histórico de versão foi obtido com êxito.|
|SCC_I_RELOADFILE|O sistema de controle do código-fonte realmente modificou o arquivo no disco ao buscar o histórico (por exemplo, ao obter uma versão antiga dele), de modo que o IDE deve recarregar esse arquivo.|
|SCC_E_FILENOTCONTROLLED|O arquivo não está sob controle do código-fonte.|
|SCC_E_OPNOTSUPPORTED|O sistema de controle do código-fonte não dá suporte a essa operação.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar essa operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção. Uma nova tentativa é recomendada.|
|SCC_E_PROJNOTOPEN|O projeto não foi aberto.|
|SCC_E_NONSPECIFICERROR|Falha não específica. Não foi possível obter o histórico de arquivos.|

## <a name="remarks"></a>Comentários
 O plug-in de controle do código-fonte pode exibir sua própria caixa de diálogo para mostrar o histórico de cada arquivo, usando `hWnd` como a janela pai. Como alternativa, a função de retorno de chamada de saída de texto opcional fornecida ao [SccOpenProject](../extensibility/sccopenproject-function.md) poderá ser usada, se tiver suporte.

 Observe que, em determinadas circunstâncias, o arquivo que está sendo examinado pode mudar durante a execução dessa chamada. Por exemplo, o [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] comando de histórico dá ao usuário a oportunidade de obter uma versão antiga do arquivo. Nesse caso, o plug-in de controle do código-fonte retorna para avisar o IDE de que ele `SCC_I_RELOAD` precisa recarregar o arquivo.

> [!NOTE]
> Se o plug-in de controle do código-fonte não dá suporte a essa função para uma matriz de arquivos, somente o histórico de arquivos para o primeiro arquivo pode ser exibido.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
