---
title: CommentMarkProfile | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- CommentMarkProfile
- CommentMarkProfileA
ms.assetid: 33ccff45-c33a-4672-b41f-5b317b848cd1
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 750ce3cbcae593aee315998ec8b205a71e004d41
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543034"
---
# <a name="commentmarkprofile"></a>CommentMarkProfile
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A `CommentMarkProfile` função insere um marcador numérico e uma cadeia de texto no arquivo .vsp. Para que a marcação e o comentário sejam inseridos, a criação de perfil para o thread que contém a função `CommentMarkProfile` deve ser ON.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
PROFILE_COMMAND_STATUS PROFILERAPI CommentMarkProfile(  
                                   long lMarker,   
                                   LPCTSTR szComment);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `lMarker`  
  
 Marcador numérico para inserir. O marcador deve ser maior ou igual a 0 (zero).  
  
 `szComment`  
  
 Ponteiro para a cadeia de texto para inserir. A cadeia de caracteres deve ser menor que 256 caracteres, incluindo o terminador NULO.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
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
 O estado de criação de perfil para o thread que contém a função de perfil de marca deve estar ligado quando as marcas e os comentários são inseridos com o comando VSInstr Mark ou com as funções (CommentMarkAtProfile, CommentMarkProfile ou MarkProfile).  
  
 Marcas de perfis são globais no escopo. Por exemplo, uma marca de perfil inserida em um thread pode ser usada para marcar o início ou término de um segmento de dados em um thread no arquivo .vsp.  
  
> [!IMPORTANT]
> O método CommentMarkProfile só pode ser usado com a instrumentação.  
  
## <a name="net-framework-equivalent"></a>Equivalente ao .NET Framework  
 Microsoft.VisualStudio.Profiler.dll  
  
## <a name="function-information"></a>Informações de Função  
  
|Item|Valor|  
|-|-|  
|**Cabeçalho**|Inclui VSPerf.h|  
|**Biblioteca**|Use VSPerf.lib|  
|**Unicode**|Implementado como `CommentMarkProfileW` (Unicode) e `CommentMarkProfileA` (ANSI).|  
  
## <a name="example"></a>Exemplo  
 O código a seguir ilustra a chamada da função CommentMarkProfile. O exemplo pressupõe o uso de macros de cadeia de caracteres do Win32 e as configurações do compilador de Unicode para determinar se o código chama a chamada da função [!INCLUDE[vcpransi](../includes/vcpransi-md.md)].  
  
```  
void ExerciseCommentMarkProfile()  
{  
    // Declare and initalize variables to pass to   
    // CommentMarkProfile.  The values of these   
    // parameters are assigned based on the needs   
    // of the code; and for the sake of simplicity  
    // in this example, the variables are assigned  
    // arbitrary values.  
    long markId = 01;  
    TCHAR * markText = TEXT("Exercising CommentMarkProfile...");  
  
    // Variables used to print output.  
    HRESULT hResult;  
    TCHAR tchBuffer[256];  
  
    // Declare MarkOperationResult Enumerator.    
    // Holds return value from call to CommentMarkProfile.  
    PROFILE_COMMAND_STATUS markResult;  
  
    markResult = CommentMarkProfile(  
        markId,  
        markText);  
  
    // Format and print result.  
    LPCTSTR pszFormat = TEXT("%s %d.\0");  
    TCHAR* pszTxt = TEXT("CommentMarkProfile returned");  
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,   
        pszTxt, markResult);  
  
#ifdef DEBUG  
    OutputDebugString(tchBuffer);  
#endif  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do criador de perfil do Visual Studio (nativo)](../profiling/visual-studio-profiler-api-reference-native.md)
