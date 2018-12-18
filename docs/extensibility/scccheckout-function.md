---
title: Função SccCheckout | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccCheckout
helpviewer_keywords:
- SccCheckout function
ms.assetid: 06e9ecd7-fc09-40c1-9dd1-2b56c622c80b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1ba80df71dce70ad4a6a0953d37f8f87bd487e12
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49908516"
---
# <a name="scccheckout-function"></a>Função SccCheckout
Dada uma lista de nomes de arquivo totalmente qualificado, essa função verifica-los para a unidade local. O comentário se aplica a todos os arquivos que está sendo extraídos. O argumento de comentário pode ser um `null` cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SCCRTN SccCheckout (  
   LPVOID    pvContext,  
   HWND      hWnd,  
   LONG      nFiles,  
   LPCSTR*   lpFileNames,  
   LPCSTR    lpComment,  
   LONG      fOptions,  
   LPCMDOPTS pvOptions  
);  
```  
  
### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 nFiles  
 [in] Número de arquivos selecionados para fazer check-out.  
  
 lpFileNames  
 [in] Matriz de nomes de caminho local totalmente qualificado dos arquivos para fazer check-out.  
  
 lpComment  
 [in] Comentário a ser aplicado a cada um dos arquivos selecionados que está sendo extraídos.  
  
 fOptions  
 [in] Sinalizadores de comando (consulte [sinalizadores de bit usados por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md)).  
  
 pvOptions  
 [in] Opções de plug-in específico de controle de origem.  
  
## <a name="return-value"></a>Valor retornado  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Check-out foi bem-sucedida.|  
|SCC_E_FILENOTCONTROLLED|O arquivo selecionado não está sob controle do código-fonte.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. É recomendável uma nova tentativa.|  
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|  
|SCC_E_NONSPECIFICERROR|Falha não específica. O arquivo não foi extraído.|  
|SCC_E_ALREADYCHECKEDOUT|O usuário já tiver o arquivo de check-out.|  
|SCC_E_FILEISLOCKED|O arquivo está bloqueado, proibindo a criação de novas versões.|  
|SCC_E_FILEOUTEXCLUSIVE|Outro usuário tenha feito um check-out exclusivo nesse arquivo.|  
|SCC_I_OPERATIONCANCELED|A operação foi cancelada antes da conclusão.|  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in da controle de origem](../extensibility/source-control-plug-in-api-functions.md)   
 [Sinalizadores de bit usados por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md)