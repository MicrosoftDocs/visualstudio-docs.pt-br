---
description: Essa função exibe o histórico dos arquivos especificados.
title: Função SccHistory | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccHistory
helpviewer_keywords:
- SccHistory function
ms.assetid: a636d9d3-47c1-4b48-ac6b-bcfde19d6cf9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5b7e1cd6fa6d5b9b3a5ab42cd1b4cafec215deca
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102220567"
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

no A estrutura de contexto do plug-in de controle do código-fonte.

 `hWnd`

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 `nFiles`

no Número de arquivos especificados na `lpFileName` matriz.

 `lpFileName`

no Matriz de nomes totalmente qualificados de arquivos.

 `fOptions`

no Sinalizadores de comando (atualmente não usados).

 `pvOptions`

no Opções específicas de plug-ins de controle do código-fonte.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O histórico de versão foi obtido com êxito.|
|SCC_I_RELOADFILE|O sistema de controle do código-fonte realmente modificou o arquivo no disco ao buscar o histórico (por exemplo, obtendo uma versão antiga dele), portanto, o IDE deve recarregar esse arquivo.|
|SCC_E_FILENOTCONTROLLED|O arquivo não está no controle do código-fonte.|
|SCC_E_OPNOTSUPPORTED|O sistema de controle do código-fonte não oferece suporte a essa operação.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. Uma nova tentativa é recomendada.|
|SCC_E_PROJNOTOPEN|O projeto não foi aberto.|
|SCC_E_NONSPECIFICERROR|Falha não específica. Não foi possível obter o histórico de arquivos.|

## <a name="remarks"></a>Comentários
 O plug-in de controle do código-fonte pode exibir sua própria caixa de diálogo para mostrar o histórico de cada arquivo, usando `hWnd` como a janela pai. Como alternativa, a função de retorno de chamada de saída de texto opcional fornecida para o [SccOpenProject](../extensibility/sccopenproject-function.md) pode ser usada, se houver suporte.

 Observe que, em determinadas circunstâncias, o arquivo que está sendo examinado pode ser alterado durante a execução dessa chamada. Por exemplo, o [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] comando de histórico dá ao usuário a oportunidade de obter uma versão antiga do arquivo. Nesse caso, o plug-in de controle do código-fonte retorna `SCC_I_RELOAD` para avisar o IDE de que ele precisa para recarregar o arquivo.

> [!NOTE]
> Se o plug-in de controle do código-fonte não oferecer suporte a essa função para uma matriz de arquivos, somente o histórico de arquivos do primeiro arquivo poderá ser exibido.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
