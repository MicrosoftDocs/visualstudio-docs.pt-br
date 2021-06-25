---
title: LPTEXTOUTPROC | Microsoft Docs
description: Saiba mais sobre o ponteiro de função LPTEXTOUTPROC. O Visual Studio IDE implementa a função para exibir o erro e o status.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- LPTEXTOUTPROC
helpviewer_keywords:
- SccMsgDataOnMessage structure
- SccMsgDataOnBeforeGetFile structure
- SccMsgDataIsCancelled structure
- LPTEXTOUTPROC callback function
- SccMsgDataOnAfterGetFile structure
ms.assetid: 2025c969-e3c7-4cf4-a5c5-099d342895ea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c313375efe8afd17dd5d76f55de4cdaf016bab40
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903093"
---
# <a name="lptextoutproc"></a>LPTEXTOUTPROC

Quando o usuário executa uma operação de controle do código-fonte de dentro do IDE (ambiente de desenvolvimento integrado), o plug-in de controle do código-fonte pode querer transmitir mensagens de erro ou status relacionadas à operação. O plug-in pode exibir suas próprias caixas de mensagem para essa finalidade. No entanto, para uma integração mais direta, o plug-in pode passar cadeias de caracteres para o IDE, que as exibe em sua maneira nativa de exibir informações de status. O mecanismo para isso é o `LPTEXTOUTPROC` ponteiro de função. O IDE implementa essa função (descrita em mais detalhes abaixo) para exibir o erro e o status.

O IDE passa para o plug-in de controle do código-fonte um ponteiro de função para essa função, como o parâmetro , ao chamar `lpTextOutProc` [o SccOpenProject](../extensibility/sccopenproject-function.md). Durante uma operação SCC, por exemplo, no meio de uma chamada para o [SccGet](../extensibility/sccget-function.md) envolvendo muitos arquivos, o plug-in pode chamar a função, passando periodicamente cadeias de caracteres para `LPTEXTOUTPROC` exibição. O IDE pode exibir essas cadeias de caracteres em uma barra de status, em uma janela de saída ou em uma caixa de mensagem separada, conforme apropriado. Opcionalmente, o IDE pode ser capaz de exibir determinadas mensagens com um **botão** Cancelar. Isso permite que o usuário cancele a operação e dá ao IDE a capacidade de passar essas informações de volta para o plug-in.

## <a name="signature"></a>Assinatura
 A função de saída do IDE tem a seguinte assinatura:

```cpp
typedef LONG (*LPTEXTOUTPROC) (
   LPSTR display_string,
   LONG mesg_type
);
```

## <a name="parameters"></a>Parâmetros

display_string

Uma cadeia de caracteres de texto a ser exibida. Essa cadeia de caracteres não deve ser encerrada com um retorno de carro ou um feed de linha.

mesg_type

O tipo de mensagem. A tabela a seguir lista os valores com suporte para esse parâmetro.

|Valor|Descrição|
|-----------|-----------------|
|`SCC_MSG_INFO, SCC_MSG_WARNING, SCC_MSG_ERROR`|A mensagem é considerada Informações, Aviso ou Erro.|
|`SCC_MSG_STATUS`|A mensagem mostra o status e pode ser exibida na barra de status.|
|`SCC_MSG_DOCANCEL`|Enviado sem nenhuma cadeia de caracteres de mensagem.|
|`SCC_MSG_STARTCANCEL`|Começa a exibir um **botão** Cancelar.|
|`SCC_MSG_STOPCANCEL`|Para de exibir um **botão** Cancelar.|
|`SCC_MSG_BACKGROUND_IS_CANCELLED`|Pergunta ao IDE se a operação em segundo plano deve ser cancelada: O IDE retorna se a operação `SCC_MSG_RTN_CANCEL` foi cancelada; caso contrário, retorna `SCC_MSG_RTN_OK` . O `display_string` parâmetro é cast como uma estrutura [SccMsgDataIsCancelled,](#LinkSccMsgDataIsCancelled) que é fornecida pelo plug-in de controle do código-fonte.|
|`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`|Informa o IDE sobre um arquivo antes de ser recuperado do controle de versão. O `display_string` parâmetro é cast como uma estrutura [SccMsgDataOnBeforeGetFile,](#LinkSccMsgDataOnBeforeGetFile) que é fornecida pelo plug-in de controle do código-fonte.|
|`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`|Informa o IDE sobre um arquivo depois que ele foi recuperado do controle de versão. O `display_string` parâmetro é cast como uma estrutura [SccMsgDataOnAfterGetFile,](#LinkSccMsgDataOnAfterGetFile) que é fornecida pelo plug-in de controle do código-fonte.|
|`SCC_MSG_BACKGROUND_ON_MESSAGE`|Informa o IDE do status atual de uma operação em segundo plano. O `display_string` parâmetro é cast como uma estrutura [SccMsgDataOnMessage,](#LinkSccMsgDataOnMessage) que é fornecida pelo plug-in de controle do código-fonte.|

## <a name="return-value"></a>Valor retornado

|Valor|Descrição|
|-----------|-----------------|
|SCC_MSG_RTN_OK|A cadeia de caracteres foi exibida ou a operação foi concluída com êxito.|
|SCC_MSG_RTN_CANCEL|O usuário deseja cancelar a operação.|

## <a name="example"></a>Exemplo
 Suponha que o IDE chama [o SccGet com](../extensibility/sccget-function.md) vinte nomes de arquivo. O plug-in de controle do código-fonte deseja impedir o cancelamento da operação no meio de um arquivo get. Depois de obter cada arquivo, ele chama , passando as informações de status em cada arquivo e envia uma mensagem se ele não `lpTextOutProc` tiver nenhum status para `SCC_MSG_DOCANCEL` relatar. Se a qualquer momento o plug-in receber um valor de retorno do IDE, ele cancelará a operação get imediatamente, para que nenhum arquivo mais `SCC_MSG_RTN_CANCEL` seja recuperado.

## <a name="structures"></a>Estruturas

### <a name="sccmsgdataiscancelled"></a><a name="LinkSccMsgDataIsCancelled"></a> SccMsgDataIsCancelled

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
} SccMsgDataIsCancelled;
```

 Essa estrutura é enviada com a `SCC_MSG_BACKGROUND_IS_CANCELLED` mensagem . Ele é usado para comunicar a ID da operação em segundo plano que foi cancelada.

### <a name="sccmsgdataonbeforegetfile"></a><a name="LinkSccMsgDataOnBeforeGetFile"></a> SccMsgDataOnBeforeGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
} SccMsgDataOnBeforeGetFile;
```

 Essa estrutura é enviada com a `SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE` mensagem . Ele é usado para comunicar o nome do arquivo prestes a ser recuperado e a ID da operação em segundo plano que está fazendo a recuperação.

### <a name="sccmsgdataonaftergetfile"></a><a name="LinkSccMsgDataOnAfterGetFile"></a> SccMsgDataOnAfterGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
   SCCRTN sResult;
} SccMsgDataOnAfterGetFile;
```

 Essa estrutura é enviada com a `SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE` mensagem . Ele é usado para comunicar o resultado da recuperação do arquivo especificado, bem como a ID da operação em segundo plano que fez a recuperação. Consulte os valores de retorno para [o SccGet](../extensibility/sccget-function.md) para o que pode ser dado como resultado.

### <a name="sccmsgdataonmessage"></a><a name="LinkSccMsgDataOnMessage"></a> SccMsgDataOnMessage

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szMessage;
   BOOL bIsError;
} SccMsgDataOnMessage;
```

 Essa estrutura é enviada com a `SCC_MSG_BACKGROUND_ON_MESSAGE` mensagem . Ele é usado para comunicar o status atual de uma operação em segundo plano. O status é expresso como uma cadeia de caracteres a ser exibida pelo IDE e indica a severidade da mensagem ( para uma mensagem de erro; para um aviso ou para uma mensagem `bIsError` `TRUE` `FALSE` informacional). A ID da operação em segundo plano que envia o status também é dada.

## <a name="code-example"></a>Exemplo de código
 Aqui está um breve exemplo de chamada para enviar a mensagem, mostrando como lançar a `LPTEXTOUTPROC` `SCC_MSG_BACKGROUND_ON_MESSAGE` estrutura para a chamada.

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

## <a name="see-also"></a>Confira também
- [Funções de retorno de chamada implementadas pelo IDE](../extensibility/callback-functions-implemented-by-the-ide.md)
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
