---
title: Função SccCheckin | Microsoft Docs
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
- SccCheckin
helpviewer_keywords:
- SccCheckin function
ms.assetid: e3f26ac2-6163-42e1-a764-22cfea5a3bc6
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 26daf5fcd3ee4ec14b0801c828a6e536a65150d8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51797995"
---
# <a name="scccheckin-function"></a>Função SccCheckin
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa função faz check-in anteriormente arquivos com check-out para o sistema de controle do código-fonte, armazenar as alterações e criar uma nova versão. Essa função é chamada com uma contagem e uma matriz de nomes dos arquivos para check-in.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
SCCRTN SccCheckin (  
   LPVOID    pvContext,  
   HWND      hWnd,  
   LONG      nFiles,  
   LPSTR*    lpFileNames,  
   LPCSTR    lpComment,  
   LONG      fOptions,  
   LPCMDOPTS pvOptions  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 pvContext  
 [in] A estrutura de contexto de plug-in de controle de origem.  
  
 hWnd  
 [in] Um identificador para a janela do IDE que o plug-in de SCC pode usar como um pai para todas as caixas de diálogo que ele oferece.  
  
 nFiles  
 [in] Número de arquivos selecionados para fazer check-in.  
  
 lpFileNames  
 [in] Matriz de nomes de caminho local totalmente qualificado dos arquivos para check-in.  
  
 lpComment  
 [in] Comentário a ser aplicado a cada um dos arquivos selecionados em check-in. Isso é `NULL` se solicitará que o plug-in de controle do código-fonte para um comentário.  
  
 fOptions  
 [in] Sinalizadores de comando, 0 ou `SCC_KEEP_CHECKEDOUT`.  
  
 pvOptions  
 [in] Opções de plug-in específico de SCC.  
  
## <a name="return-value"></a>Valor de retorno  
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_OK|Arquivos foi verificado com êxito.|  
|SCC_E_FILENOTCONTROLLED|O arquivo selecionado não está sob controle do código-fonte.|  
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. É recomendável uma nova tentativa.|  
|SCC_E_NONSPECIFICERROR|Falha não específica. Arquivo não foi aprovado.|  
|SCC_E_NOTCHECKEDOUT|O usuário não tem check-out do arquivo, portanto, não é possível fazer check-in.|  
|SCC_E_CHECKINCONFLICT|Fazer check-in não pôde ser realizada porque:<br /><br /> -Outro usuário fez check-in em frente e `bAutoReconcile` era falsa.<br /><br /> -ou-<br /><br /> -A mesclagem automática não pode ser feita (por exemplo, quando os arquivos são binários).|  
|SCC_E_VERIFYMERGE|Arquivo tiver sido mesclada automaticamente, mas não foi verificado aguardam a verificação de usuário.|  
|SCC_E_FIXMERGE|Arquivo tiver sido mesclada automaticamente, mas não foi verificado devido a um conflito de mesclagem que deve ser resolvido manualmente.|  
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|  
|SCC_I_OPERATIONCANCELED|Operação foi cancelada antes da conclusão.|  
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|  
|SCC_E_FILENOTEXIST|Arquivo local não foi encontrado.|  
  
## <a name="remarks"></a>Comentários  
 O comentário se aplica a todos os arquivos em check-in. O argumento de comentário pode ser um `null` de cadeia de caracteres, caso em que o plug-in de controle do código-fonte pode solicitar ao usuário uma cadeia de caracteres de comentário para cada arquivo.  
  
 O `fOptions` argumento pode ser fornecido um valor da `SCC_KEEP_CHECKEDOUT` sinalizador para indicar a intenção do usuário para o arquivo de check-in e check-out novamente.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de API do plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)

