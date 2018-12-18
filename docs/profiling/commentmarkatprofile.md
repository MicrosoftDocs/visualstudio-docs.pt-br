---
title: CommentMarkAtProfile | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- CommentMarkAtProfile
- CommentMarkAtProfileA
ms.assetid: 04294ca3-bf9c-4c76-86f1-898c2140de27
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4eb29336b401b020df52d1ccaa743bb7240e1d2b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49854797"
---
# <a name="commentmarkatprofile"></a>CommentMarkAtProfile
O método `CommentMarkAtProfile` insere um valor de carimbo de data/hora, uma marca numérica e uma cadeia de caracteres de comentário no arquivo .*vsp*. O valor de carimbo de data/hora pode ser usado para sincronizar os eventos externos. Para que a marcação e o comentário sejam inseridos, a criação de perfil para o thread que contém a função CommentMarkAtProfile deve ser ON.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
PROFILE_COMMAND_STATUS PROFILERAPI CommentMarkAtProfile (  
                                   __int64 dnTimestamp,  
                                   long lMarker,  
                                   LPCTSTR szComment);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dnTimestamp`  
  
 Um inteiro de 64 bits que representa um valor de carimbo de data/hora.  
  
 `lMarker`  
  
 O marcador numérico para inserir. O marcador deve ser maior ou igual a 0 (zero).  
  
 `szComment`  
  
 Um ponteiro para a cadeia de texto para inserir. A cadeia de caracteres deve ser menor que 256 caracteres, incluindo o terminador NULO.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/valor retornado  
 A função indica êxito ou falha usando a enumeração **PROFILE_COMMAND_STATUS**. O valor de retorno pode ser um dos seguintes:  
  
|Enumerador|Descrição|  
|----------------|-----------------|  
|MARK_ERROR_MARKER_RESERVED|O parâmetro é menor ou igual a 0. Esses valores são reservados. A marca e o comentário não são registrados.|  
|MARK_ERROR_MODE_NEVER|O modo de criação de perfil foi definido para NEVER (NUNCA) quando a função foi chamada. A marca e o comentário não são registrados.|  
|MARK_ERROR_MODE_OFF|O modo de criação de perfil foi definido como OFF quando a função foi chamada. A marca e o comentário não são registrados.|  
|MARK_ERROR_NO_SUPPORT|Não há suporte de marca neste contexto. A marca e o comentário não são registrados.|  
|MARK_ERROR_OUTOFMEMORY|Não havia memória disponível para registrar o evento. A marca e o comentário não são registrados.|  
|MARK_TEXTTOOLONG|A cadeia de caracteres excede o máximo de 256 caracteres. A cadeia de caracteres de comentário é truncada e a marca e o comentário são registrados.|  
|MARK_OK|MARK_OK é retornado para indicar êxito.|  
  
## <a name="remarks"></a>Comentários  
 O estado de criação de perfil para o thread que contém a função de perfil de marca deve estar ligado quando as marcas e os comentários são inseridos com o comando Mark ou com as funções da API (CommentMarkAtProfile, CommentMarkProfile ou MarkProfile). Marcas de perfis são globais no escopo. Por exemplo, uma marca de perfil inserida em um thread pode ser usada para marcar o início ou término de um segmento de dados em um thread no arquivo .vsp.  
  
> [!IMPORTANT]
>  Os métodos CommentMarkAtProfile devem ser usados somente com a instrumentação.  
  
## <a name="net-framework-equivalent"></a>Equivalente ao .NET Framework  
 *Microsoft.VisualStudio.Profiler.dll*  
  
## <a name="function-information"></a>Informações de função  
  
|||  
|-|-|  
|**Header**|Incluir *VSPerf.h*|  
|**Library**|Usar *VSPerf.lib*|  
|**Unicode**|Implementado como CommentMarkAtProfileW (Unicode) e CommentMarkAtProfileA (ANSI).|  
  
## <a name="example"></a>Exemplo  
 O código a seguir ilustra o uso da chamada da função genérica de CommentMarkAtProfile. O exemplo pressupõe o uso de macros da cadeia de caracteres do Win32 e as configurações do compilador para ANSI para determinar se o código chama a função habilitada do ANSI.  
  
```cpp  
void ExerciseCommentMarkAtProfile(void)  
{  
    // Declare and initalize variables to pass to   
    // CommentMarkAtProfile.  The values of these   
    // parameters are assigned based on the needs   
    // of the code; and for the sake of simplicity  
    // in this example, the variables are assigned  
    // arbitrary values.  
    int64 timeStamp = 0x1111;  
    long markId = 01;  
    TCHAR * markText = TEXT("Exercising CommentMarkAtProfile...");  
  
    // Variables used to print output.  
    HRESULT hResult;  
    TCHAR tchBuffer[256];  
  
    // Declare MarkOperationResult Enumerator.    
    // Holds return value from call to CommentMarkAtProfile.  
    PROFILE_COMMAND_STATUS markResult;  
  
    markResult = CommentMarkAtProfile(  
        timeStamp,  
        markId,  
        markText);  
  
    // Format and print result.  
    LPCTSTR pszFormat = TEXT("%s %d.\0");  
    TCHAR* pszTxt = TEXT("CommentMarkAtProfile returned");  
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,   
    pszTxt, markResult);  
  
#ifdef DEBUG  
    OutputDebugString(tchBuffer);  
#endif  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API do criador de perfil do Visual Studio (nativa)](../profiling/visual-studio-profiler-api-reference-native.md)