---
title: Função SccDirDiff | Microsoft Docs
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
- SccDirDiff
helpviewer_keywords:
- SccDirDiff function
ms.assetid: 26c9ba92-e3b9-4dd2-bd5e-76b17745e308
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 7d2c45773a9d45c69cfed4f773bc5cdfcfa1c305
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51791183"
---
# <a name="sccdirdiff-function"></a>Função SccDirDiff
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esta função exibe as diferenças entre o diretório local atual no disco do cliente e o projeto correspondente sob controle do código-fonte.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
SCCRTN SccDirDiff(  
   LPVOID    pContext,  
   HWND      hWnd,  
   LPCSTR    lpDirName,  
   LONG      dwFlags,  
   LPCMDOPTS pvOptions  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 lpDirName  
 [in] Caminho totalmente qualificado para o diretório local para o qual mostram uma diferença de visual.  
  
 dwFlags  
 [in] Sinalizadores de comando (consulte comentários seção).  
  
 pvOptions  
 [in] Opções de plug-in específico de controle de origem.  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|O diretório em disco é o mesmo que o projeto no controle do código fonte.|  
|SCC_I_FILESDIFFER|O diretório no disco é diferente do projeto no controle do código fonte.|  
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|  
|SCC_E_FILENOTCONTROLLED|O diretório não está sob controle do código-fonte.|  
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. É recomendável uma nova tentativa.|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Falha não específica.|  
|SCC_E_FILENOTEXIST|Não foi possível encontrar o diretório local.|  
  
## <a name="remarks"></a>Comentários  
 Essa função é usada para instruir o controle de fonte de plug-in para exibir ao usuário uma lista de alterações para um diretório especificado. O plug-in abre sua própria janela, em um formato de sua escolha, para exibir as diferenças entre o diretório do usuário no disco e o projeto correspondente sob controle de versão.  
  
 Se uma comparação dá suporte a plug-in de diretórios em todas, ele deve oferecer suporte a comparação dos diretórios em uma base de nome de arquivo, mesmo se não há suporte para as opções "diff rápido".  
  
|`dwFlags`|Interpretação|  
|---------------|--------------------|  
|SCC_DIFF_IGNORECASE|Comparação diferencia maiusculas de minúsculas (pode ser usado para comparação rápida ou visual).|  
|SCC_DIFF_IGNORESPACE|Ignora o espaço em branco (pode ser usado para comparação rápida ou visual).|  
|SCC_DIFF_QD_CONTENTS|Se houver suporte a plug-in de controle do código-fonte, compara silenciosamente o diretório, byte por byte.|  
|SCC_DIFF_QD_CHECKSUM|Se compatível com o plug-in, silenciosamente compara o diretório por meio de uma soma de verificação ou, se não tiver suporte, voltará a SCC_DIFF_QD_CONTENTS.|  
|SCC_DIFF_QD_TIME|Se compatível com o plug-in, silenciosamente compara o diretório por meio de seu carimbo de hora ou, se não tiver suporte, recai em SCC_DIFF_QD_CHECKSUM ou SCC_DIFF_QD_CONTENTS.|  
  
> [!NOTE]
>  Essa função usa os mesmos sinalizadores de comando como o [SccDiff](../extensibility/sccdiff-function.md). No entanto, um plug-in de controle do código-fonte pode optar por não oferece suporte à operação "diff rápido" para diretórios.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API do plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)

