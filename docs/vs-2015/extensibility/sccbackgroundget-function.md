---
title: Função SccBackgroundGet | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccBackgroundGet
helpviewer_keywords:
- SccBackgroundGet function
ms.assetid: 69817e52-b9ac-4f4d-820b-2cc9c384f0dc
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2462ca84ac2d0b902256c161e4997114489d1697
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58923998"
---
# <a name="sccbackgroundget-function"></a>Função SccBackgroundGet
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa função recupera do controle de origem cada dos arquivos especificados sem interação do usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SCCRTN SccBackgroundGet(  
   LPVOID  pContext,  
   LONG    nFiles,  
   LPCSTR* lpFileNames,  
   LONG    dwFlags,  
   LONG    dwBackgroundOperationID  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pContext  
 [in] O ponteiro de contexto de plug-in de controle do código-fonte.  
  
 nFiles  
 [in] Número de arquivos especificados no `lpFileNames` matriz.  
  
 lpFileNames  
 [no, out] Matriz de nomes de arquivos a serem recuperados.  
  
> [!NOTE]
>  Os nomes devem ser totalmente qualificado de nomes de arquivos local.  
  
 dwFlags  
 [in] Sinalizadores de comando (`SCC_GET_ALL`, `SCC_GET_RECURSIVE`).  
  
 dwBackgroundOperationID  
 [in] Um valor exclusivo associado a esta operação.  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Operação concluída com êxito.|  
|SCC_E_BACKGROUNDGETINPROGRESS|Recuperação de um plano de fundo já está em andamento (o plug-in de controle do código-fonte deve retornar isso somente se ele não oferece suporte a operações em lotes simultâneos).|  
|SCC_I_OPERATIONCANCELED|Operação foi cancelada antes de serem concluídas.|  
  
## <a name="remarks"></a>Comentários  
 Essa função sempre é chamada em um thread diferente daquele que carregar o plug-in de controle do código-fonte. Essa função não deve retornar até que ela seja feita; No entanto, ele pode ser chamado várias vezes com várias listas de arquivos, todos ao mesmo tempo.  
  
 O uso do `dwFlags` argumento for igual a [SccGet](../extensibility/sccget-function.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [SccGet](../extensibility/sccget-function.md)
