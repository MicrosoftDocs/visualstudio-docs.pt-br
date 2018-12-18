---
title: LPTEXTOUTPROC | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- LPTEXTOUTPROC
helpviewer_keywords:
- SccMsgDataOnMessage structure
- SccMsgDataOnBeforeGetFile structure
- SccMsgDataIsCancelled structure
- LPTEXTOUTPROC callback function
- SccMsgDataOnAfterGetFile structure
ms.assetid: 2025c969-e3c7-4cf4-a5c5-099d342895ea
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2d8439d706dbe8c84d807fb445eda272b96ad589
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49822872"
---
# <a name="lptextoutproc"></a>LPTEXTOUTPROC
Quando o usuário executa uma operação de controle do código-fonte dentro do ambiente de desenvolvimento integrado (IDE), o plug-in de controle do código-fonte talvez queira transmitir mensagens de status ou erro relacionadas à operação. O plug-in pode exibir suas próprias caixas de mensagem para essa finalidade. No entanto, para obter mais integração perfeita, o plug-in pode passar cadeias de caracteres para o IDE, o que, em seguida, exibe-os em sua maneira nativa de exibir informações de status. O mecanismo para isso é o `LPTEXTOUTPROC` ponteiro de função. O IDE implementa essa função (descrita mais detalhadamente abaixo) para exibir o status e erros.  
  
 O IDE passa para o controle de fonte plug-in um ponteiro de função para essa função, como o `lpTextOutProc` parâmetro, ao chamar o [SccOpenProject](../extensibility/sccopenproject-function.md). Durante uma operação de SCC, por exemplo, no meio de uma chamada para o [SccGet](../extensibility/sccget-function.md) envolvendo muitos arquivos, o plug-in pode chamar o `LPTEXTOUTPROC` função, periodicamente passar cadeias de caracteres para exibir. O IDE pode exibir essas cadeias de caracteres em uma barra de status em uma janela de saída, ou em uma caixa de mensagem separada, conforme apropriado. Opcionalmente, o IDE pode ser capaz de exibir determinadas mensagens com um **Cancelar** botão. Isso permite que o usuário cancelar a operação, e ele permite que o IDE para transmitir essas informações para o plug-in.  
  
## <a name="signature"></a>Assinatura  
 O IDE saída função tem a seguinte assinatura:  
  
```cpp  
typedef LONG (*LPTEXTOUTPROC) (  
   LPSTR display_string,  
   LONG mesg_type  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 display_string  
 Uma cadeia de caracteres de texto para exibir. Essa cadeia de caracteres não deve ser terminada com um carro de retorno ou uma alimentação de linha.  
  
 mesg_type  
 O tipo de mensagem. A tabela a seguir lista os valores com suporte para esse parâmetro.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`SCC_MSG_INFO, SCC_MSG_WARNING, SCC_MSG_ERROR`|A mensagem é considerada informações, aviso ou erro.|  
|`SCC_MSG_STATUS`|A mensagem mostra o status e pode ser exibida na barra de status.|  
|`SCC_MSG_DOCANCEL`|Enviado com nenhuma cadeia de caracteres de mensagem.|  
|`SCC_MSG_STARTCANCEL`|Começa exibindo uma **Cancelar** botão.|  
|`SCC_MSG_STOPCANCEL`|Interrompe a exibição de um **Cancelar** botão.|  
|`SCC_MSG_BACKGROUND_IS_CANCELLED`|Solicita que o IDE se a operação em segundo plano deve ser cancelada: IDE retorna `SCC_MSG_RTN_CANCEL` se a operação foi cancelada; caso contrário, retornará `SCC_MSG_RTN_OK`. O `display_string` parâmetro é convertido como um [SccMsgDataIsCancelled](#LinkSccMsgDataIsCancelled) estrutura, que é fornecida pelo plug-in de controle do código-fonte.|  
|`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`|Informa o IDE sobre um arquivo antes de serem recuperado do controle de versão. O `display_string` parâmetro é convertido como um [SccMsgDataOnBeforeGetFile](#LinkSccMsgDataOnBeforeGetFile) estrutura, que é fornecida pelo plug-in de controle do código-fonte.|  
|`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`|Informa o IDE sobre um arquivo depois que ele tiver sido recuperado do controle de versão. O `display_string` parâmetro é convertido como um [SccMsgDataOnAfterGetFile](#LinkSccMsgDataOnAfterGetFile) estrutura, que é fornecida pelo plug-in de controle do código-fonte.|  
|`SCC_MSG_BACKGROUND_ON_MESSAGE`|Informa o IDE do status atual de uma operação em segundo plano. O `display_string` parâmetro é convertido como um [SccMsgDataOnMessage](#LinkSccMsgDataOnMessage) estrutura, que é fornecida pelo plug-in de controle do código-fonte.|  
  
## <a name="return-value"></a>Valor retornado  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SCC_MSG_RTN_OK|A cadeia de caracteres foi exibida ou a operação foi concluída com êxito.|  
|SCC_MSG_RTN_CANCEL|O usuário deseja cancelar a operação.|  
  
## <a name="example"></a>Exemplo  
 Suponha que o IDE chama o [SccGet](../extensibility/sccget-function.md) com vinte nomes de arquivo. O plug-in de controle do código-fonte quer impedir que cancelar a operação no meio de um get de arquivo. Depois de obter cada arquivo, ele chama `lpTextOutProc`, passando as informações de status em cada arquivo e envia um `SCC_MSG_DOCANCEL` da mensagem se ele tiver nenhum status a ser relatado. Se a qualquer momento o plug-in recebe um valor de retorno de `SCC_MSG_RTN_CANCEL` do IDE, ele cancela a operação imediatamente, para que não há mais arquivos são recuperados.  
  
## <a name="structures"></a>Estruturas  
  
###  <a name="LinkSccMsgDataIsCancelled"></a> SccMsgDataIsCancelled  
  
```cpp  
typedef struct {  
   DWORD dwBackgroundOperationID;  
} SccMsgDataIsCancelled;  
```  
  
 Essa estrutura é enviada com o `SCC_MSG_BACKGROUND_IS_CANCELLED` mensagem. Ele é usado para comunicar a ID da operação em segundo plano que foi cancelada.  
  
###  <a name="LinkSccMsgDataOnBeforeGetFile"></a> SccMsgDataOnBeforeGetFile  
  
```cpp  
typedef struct {  
   DWORD dwBackgroundOperationID;  
   PCSTR szFile;  
} SccMsgDataOnBeforeGetFile;  
```  
  
 Essa estrutura é enviada com o `SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE` mensagem. Ele é usado para comunicar-se o nome do arquivo que está prestes a ser recuperado e a ID da operação em segundo plano que está fazendo a recuperação.  
  
###  <a name="LinkSccMsgDataOnAfterGetFile"></a> SccMsgDataOnAfterGetFile  
  
```cpp  
typedef struct {  
   DWORD dwBackgroundOperationID;  
   PCSTR szFile;  
   SCCRTN sResult;  
} SccMsgDataOnAfterGetFile;  
```  
  
 Essa estrutura é enviada com o `SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE` mensagem. Ele é usado para comunicar-se o resultado de recuperar o arquivo especificado, bem como a ID da operação de plano de fundo que fazia a recuperar. Consulte os valores retornados para o [SccGet](../extensibility/sccget-function.md) para o que pode ser fornecido como resultado.  
  
###  <a name="LinkSccMsgDataOnMessage"></a> SccMsgDataOnMessage  
 [C++]  
  
```cpp  
typedef struct {  
   DWORD dwBackgroundOperationID;  
   PCSTR szMessage;  
   BOOL bIsError;  
} SccMsgDataOnMessage;  
```  
  
 Essa estrutura é enviada com o `SCC_MSG_BACKGROUND_ON_MESSAGE` mensagem. Ele é usado para comunicar o status atual de uma operação em segundo plano. O status é expresso como uma cadeia de caracteres a ser exibido pelo IDE, e `bIsError` indica a severidade da mensagem (`TRUE` para uma mensagem de erro; `FALSE` para um aviso ou uma mensagem informativa). Também recebe a ID da operação em segundo plano, o status de envio.  
  
## <a name="code-example"></a>Exemplo de código  
 Aqui está um breve exemplo de chamada `LPTEXTOUTPROC` para enviar o `SCC_MSG_BACKGROUND_ON_MESSAGE` mensagem, que mostra como converter a estrutura para a chamada.  
  
```cpp  
LONG SendStatusMessage(  
    LPTEXTOUTPROC pTextOutProc,  
    DWORD         dwBackgroundID,  
    LPCTSTR       pStatusMsg,  
    BOOL          bIsError)  
{  
    SccMsgDataOnMessage msgData = { 0 };  
    LONG                result  = 0;  
  
    msgData.dwBackgroundOperationID = dwBackgroundID;  
    msgData.szMessage               = pStatusMsg;  
    msgData.bIsError                = bIsError;  
  
    result = pTextOutProc(reinterpret_cast<LPCTSTR>(&msgData), SCC_MSG_BACKGROUND_ON_MESSAGE);  
    return result;  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de retorno de chamada implementadas pelo IDE](../extensibility/callback-functions-implemented-by-the-ide.md)   
 [Plug-ins de controle de origem](../extensibility/source-control-plug-ins.md)