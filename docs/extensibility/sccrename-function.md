---
title: Função SccRename | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccRename
helpviewer_keywords:
- SccRename function
ms.assetid: b467ade6-a1db-4c0b-b60f-7850ec4f79eb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 92c19e47f680d4feb6c4a4acd6de358c1a6191ab
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49841221"
---
# <a name="sccrename-function"></a>Função SccRename
Essa função renomeia um arquivo no sistema de controle de origem.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SCCRTN SccRename(  
   LPVOID pvContext,  
   HWND   hWnd,  
   LPCSTR lpFileName,  
   LPCSTR lpNewName  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 lpFileName  
 [in] O nome de arquivo totalmente qualificado do arquivo que está sendo renomeado.  
  
 lpNewName  
 [in] O novo nome totalmente qualificado. Se o caminho do diretório é diferente, o arquivo foi movido de um subdiretório para outro.  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|A operação de renomeação foi concluída com êxito.|  
|SCC_E_PROJNOTOPEN|O projeto não está aberto no controle de origem.|  
|SCC_E_FILENOTCONTROLLED|O arquivo não está sob controle de origem.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção.|  
|SCC_E_NOTAUTHORIZED|O usuário não está autorizado para concluir esta operação.|  
|SCC_E_COULDNOTCREATEPROJECT|O projeto não pôde ser criado como parte do processo de renomeação.|  
|SCC_E_OPNOTPERFORMED|A operação não foi executada.|  
|SCC_E_NONSPECIFICERROR|Ocorreu um erro não especificado ou geral.|  
  
## <a name="remarks"></a>Comentários  
 Essa função pode ser usada para renomear um arquivo ou movê-lo de um local para outro no sistema de controle de origem. O plug-in de controle do código-fonte não deve tentar acessar o arquivo no disco. É responsabilidade do IDE para renomear o arquivo local.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API do plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)