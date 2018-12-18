---
title: Função SccProperties | Microsoft Docs
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
- SccProperties
helpviewer_keywords:
- SccProperties function
ms.assetid: 1bed38c9-73d2-4474-9717-f9dc26a89cbe
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 045f0007aff7733e12ce46250055fe31e85d3511
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51796407"
---
# <a name="sccproperties-function"></a>Função SccProperties
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esta função exibe propriedades de controle do código-fonte para um arquivo ou projeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
SCCRTN SccProperties (  
   LPVOID pvContext,  
   HWND   hWnd,  
   LPCSTR lpFileName  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de controle de origem pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 lpFileName  
 [in] O nome de caminho totalmente qualificado do arquivo ou projeto.  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|As propriedades foram exibidas com êxito.|  
|SCC_I_RELOADFILE|O sistema de controle de versão tiver modificado as propriedades do arquivo, para que o IDE deve recarregar este arquivo.|  
|SCC_E_PROJNOTOPEN|O projeto especificado não foi aberto no controle de origem.|  
|SCC_E_NOTAUTHORIZED|O usuário não está autorizado para exibir as propriedades deste arquivo ou projeto.|  
|SCC_E_FILENOTCONTROLLED|O arquivo especificado ou o projeto não está sob controle do código-fonte.|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Ocorreu um erro desconhecido ou geral.|  
  
## <a name="remarks"></a>Comentários  
 O plug-in de controle do código-fonte exibe as propriedades em sua própria caixa de diálogo.  
  
 As propriedades são definidas pelo plug-in de controle da fonte e podem diferir de plug-in para o plug-in. Se o plug-in permite que o usuário altere as propriedades de controle de origem de um arquivo, ele deverá retornar `SCC_I_RELOAD` para sinalizar o IDE que este arquivo ou o projeto precisa ser recarregado.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API do plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)

