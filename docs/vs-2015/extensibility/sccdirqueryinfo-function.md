---
title: Função SccDirQueryInfo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SccDirQueryInfo
helpviewer_keywords:
- SccDirQueryInfo function
ms.assetid: 459e2d99-573d-47c4-b834-6d82c5e14162
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: f2df4dd52ff9984059eb28f21edf49b9db741358
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51784891"
---
# <a name="sccdirqueryinfo-function"></a>Função SccDirQueryInfo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa função examina uma lista de diretórios totalmente qualificados para o seu status atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
SCCRTN SccDirQueryInfo(  
LPVOID  pContext,  
LONG    nDirs,  
LPCSTR* lpDirNames,  
LPLONG  lpStatus  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 nDirs  
 [in] O número de diretórios selecionados para serem consultados.  
  
 lpDirNames  
 [in] Uma matriz de caminhos totalmente qualificados dos diretórios a serem consultadas.  
  
 lpStatus  
 [no, out] Uma estrutura de matriz para o plug-in para retornar os sinalizadores de status de controle de origem (consulte [código de Status do diretório](../extensibility/directory-status-code-enumerator.md) para obter detalhes).  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|A consulta foi bem-sucedida.|  
|SCC_E_OPNOTSUPPORTED|O sistema de controle do código-fonte não oferece suporte a essa operação.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. É recomendável uma nova tentativa.|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Falha não específica.|  
  
## <a name="remarks"></a>Comentários  
 A função preenche a matriz de retornada com uma máscara de bits de bits do `SCC_DIRSTATUS` família (consulte [código de Status do diretório](../extensibility/directory-status-code-enumerator.md)), uma entrada para cada diretório fornecido. A matriz de status é alocada pelo chamador.  
  
 O IDE usa essa função antes de um diretório é renomeado para verificar se o diretório está sob controle do código-fonte, consultando se ele tem um projeto correspondente. Se o diretório não está sob controle de origem, o IDE pode fornecer o aviso apropriado para o usuário.  
  
> [!NOTE]
>  Se um plug-in de controle do código-fonte optar por não implementar uma ou mais dos valores de status, o bits não implementadas devem ser definidos como zero.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [Código de status do diretório](../extensibility/directory-status-code-enumerator.md)

