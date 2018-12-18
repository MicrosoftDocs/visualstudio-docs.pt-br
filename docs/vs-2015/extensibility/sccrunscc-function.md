---
title: Função SccRunScc | Microsoft Docs
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
- SccRunScc
helpviewer_keywords:
- SccRunScc function
ms.assetid: bbe7c931-b17a-4779-9cf6-59e5f9f0c172
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 67d2ad2ee783d23e3bd8c960ad5a94eac3fbd908
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51733684"
---
# <a name="sccrunscc-function"></a>Função SccRunScc
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa função chama a ferramenta de administração de controle do código-fonte.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
SCCRTN SccRunScc(  
   LPVOID  pvContext,  
   HWND    hWnd,  
   LONG    nFiles,  
   LPCSTR* lpFileNames  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 nFiles  
 [in] Número de arquivos especificados no `lpFileNames` matriz.  
  
 lpFileNames  
 [in] Matriz de nomes de arquivo selecionado.  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|A ferramenta de administração de controle do código-fonte foi invocada com êxito.|  
|SCC_I_OPERATIONCANCELED|A operação foi cancelada.|  
|SCC_E_INITIALIZEFAILED|Falha ao inicializar o sistema de controle do código-fonte.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção.|  
|SCC_E_CONNECTIONFAILURE|Falha ao conectar ao sistema de controle de origem.|  
|SCC_E_FILENOTCONTROLLED|O arquivo selecionado não está sob controle do código-fonte.|  
|SCC_E_NONSPECIFICERROR|Falha não específica.|  
  
## <a name="remarks"></a>Comentários  
 Essa função permite que o chamador acessar a gama completa de recursos do sistema de controle de origem por meio de uma ferramenta de administração externo. Se o sistema de controle do código-fonte não tem nenhuma interface do usuário, o plug-in de controle do código-fonte pode implementar uma interface para realizar funções administrativas necessárias.  
  
 Essa função é chamada com uma contagem e uma matriz de nomes de arquivo para os arquivos selecionados no momento. Se a ferramenta de administração suportá-lo, a lista de arquivos pode ser usada para selecionar antecipadamente os arquivos na interface de administração; Caso contrário, a lista pode ser ignorada.  
  
 Essa função normalmente é chamado quando o usuário seleciona o **inicie \<servidor de controle de origem >** da **arquivo** -> **controle do código-fonte** menu. Isso **inicie** opção de menu pode ser sempre desabilitada ou ocultada até mesmo, definindo uma entrada de registro. Ver [como: instalar um plug-in de controle do código-fonte](../extensibility/internals/how-to-install-a-source-control-plug-in.md) para obter detalhes. Essa função é chamada somente se [SccInitialize](../extensibility/sccinitialize-function.md) retorna o `SCC_CAP_RUNSCC` bit de recurso (consulte [sinalizadores de recurso](../extensibility/capability-flags.md) para obter detalhes sobre esse e outros bits de capacidade).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [Como: instalar um plug-in de controle do código-fonte](../extensibility/internals/how-to-install-a-source-control-plug-in.md)   
 [Sinalizadores de recurso](../extensibility/capability-flags.md)   
 [SccInitialize](../extensibility/sccinitialize-function.md)

