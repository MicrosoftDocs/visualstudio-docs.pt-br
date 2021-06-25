---
description: Essa função exibe propriedades de controle do código-fonte para um arquivo ou projeto.
title: Função SccProperties | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccProperties
helpviewer_keywords:
- SccProperties function
ms.assetid: 1bed38c9-73d2-4474-9717-f9dc26a89cbe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cd50353ab29c05e5e5db2dc2b3f363af46ca8aa7
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904185"
---
# <a name="sccproperties-function"></a>Função SccProperties
Essa função exibe propriedades de controle do código-fonte para um arquivo ou projeto.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccProperties (
   LPVOID pvContext,
   HWND   hWnd,
   LPCSTR lpFileName
);
```

#### <a name="parameters"></a>Parâmetros
 pvContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 lpFileName

no O nome do caminho totalmente qualificado do arquivo ou projeto.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|As propriedades foram exibidas com êxito.|
|SCC_I_RELOADFILE|O sistema de controle de versão modificou as propriedades do arquivo, portanto, o IDE deve recarregar esse arquivo.|
|SCC_E_PROJNOTOPEN|O projeto especificado não foi aberto no controle do código-fonte.|
|SCC_E_NOTAUTHORIZED|O usuário não está autorizado a exibir as propriedades deste arquivo ou projeto.|
|SCC_E_FILENOTCONTROLLED|O arquivo ou projeto especificado não está no controle do código-fonte.|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Ocorreu um erro desconhecido ou geral.|

## <a name="remarks"></a>Comentários
 O plug-in de controle do código-fonte exibe as propriedades em sua própria caixa de diálogo.

 As propriedades são definidas pelo plug-in de controle do código-fonte e podem ser diferentes do plug-in para o plug-in. Se o plug-in permitir que o usuário altere as propriedades de controle do código-fonte de um arquivo, ele deverá retornar `SCC_I_RELOAD` para sinalizar ao IDE que esse arquivo ou projeto precisa ser recarregado.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
