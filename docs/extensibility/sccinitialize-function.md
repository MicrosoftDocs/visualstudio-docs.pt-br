---
title: Função SccInitialize | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- SccInitialize
helpviewer_keywords:
- SccInitialize function
ms.assetid: 5bc0d28b-2c68-4d43-9e51-541506a8f76e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 136978a6d1dc19a414079ba424ebcd5d50f6840a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49934568"
---
# <a name="sccinitialize-function"></a>Função SccInitialize
Essa função inicializa o plug-in de controle do código-fonte e fornece recursos e limites para o ambiente de desenvolvimento integrado (IDE).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SCCRTN SccInitialize (  
   LPVOID* ppvContext,  
   HWND    hWnd,  
   LPCSTR  lpCallerName,  
   LPSTR   lpSccName,  
   LPLONG  lpSccCaps,  
   LPSTR   lpAuxPathLabel,  
   LPLONG  pnCheckoutCommentLen,  
   LPLONG  pnCommentLen  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppvContext`  
 [in] Aqui, o plug-in de controle de origem pode colocar um ponteiro para sua estrutura de contexto.  
  
 `hWnd`  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 `lpCallerName`  
 [in] O nome do programa plug-in de controle de fonte de chamada.  
  
 `lpSccName`  
 [no, out] O buffer no qual o plug-in de controle do código-fonte coloca seu próprio nome (não deve exceder `SCC_NAME_LEN`).  
  
 `lpSccCaps`  
 [out] Retorna o controle do código-fonte sinalizadores de recurso do plug-in.  
  
 `lpAuxPathLabel`  
 [no, out] O buffer no qual o plug-in de controle do código-fonte coloca uma cadeia de caracteres que descreve o `lpAuxProjPath` parâmetro retornado pela [SccOpenProject](../extensibility/sccopenproject-function.md) e o [SccGetProjPath](../extensibility/sccgetprojpath-function.md) (não deve exceder `SCC_AUXLABEL_LEN`).  
  
 `pnCheckoutCommentLen`  
 [out] Retorna o comprimento máximo permitido para um comentário de check-out.  
  
 `pnCommentLen`  
 [out] Retorna o comprimento máximo permitido para outros comentários.  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Inicialização de controle de origem foi bem-sucedida.|  
|SCC_E_INITIALIZEFAILED|Não foi possível inicializar o sistema.|  
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar a operação especificada.|  
|SCC_E_NONSPECFICERROR|Falha não específica; sistema de controle do código-fonte não foi inicializado.|  
  
## <a name="remarks"></a>Comentários  
 O IDE chama esta função ao carregar o plug-in de controle do código-fonte pela primeira vez. Ele permite que o IDE passar a certas informações, como o nome do chamador, para o plug-in. O IDE também obtém de volta determinadas informações como o comprimento máximo permitido para comentários e recursos do plug-in.  
  
 O `ppvContext` aponta para um `NULL` ponteiro. O plug-in de controle do código-fonte pode alocar uma estrutura para seu próprio uso e armazenar um ponteiro para essa estrutura no `ppvContext`. O IDE passará este ponteiro para todas as outras funções API VSSCI, permitindo que o plug-in para ter informações de contexto disponíveis sem recorrer a armazenamento global e para dar suporte a várias instâncias do plug-in. Essa estrutura deve ser desalocada quando o [SccUninitialize](../extensibility/sccuninitialize-function.md) é chamado.  
  
 O `lpCallerName` e `lpSccName` parâmetros permitem que o IDE e o plug-in de controle do código-fonte para nomes do exchange. Esses nomes podem ser usados simplesmente para distinguir entre várias instâncias ou, na verdade, eles podem aparecer nos menus ou caixas de diálogo.  
  
 O `lpAuxPathLabel` parâmetro é uma cadeia de caracteres usada como um comentário para identificar o caminho do projeto auxiliar que é armazenado no arquivo de solução e passado para o controle do código-fonte plug-in em uma chamada para o [SccOpenProject](../extensibility/sccopenproject-function.md). [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] usa a cadeia de caracteres "projeto do SourceSafe:"; outros plug-ins de controle do código-fonte deverá evitar usar essa cadeia de caracteres específica.  
  
 O `lpSccCaps` parâmetro fornece controle de fonte de plug-in um local para armazenar os sinalizadores de bit que indica os recursos do plug-in. (Para obter uma lista completa dos sinalizadores de bit de recurso, consulte [sinalizadores de recurso](../extensibility/capability-flags.md)). Por exemplo, se os planos de plug-in para gravar os resultados em uma função de retorno de chamada fornecido pelo chamador, o plug-in definiria a capacidade de bit SCC_CAP_TEXTOUT. Isso seria sinalizar o IDE para criar uma janela de resultados de controle de versão.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)   
 [SccUninitialize](../extensibility/sccuninitialize-function.md)   
 [SccOpenProject](../extensibility/sccopenproject-function.md)   
 [Sinalizadores de recurso](../extensibility/capability-flags.md)