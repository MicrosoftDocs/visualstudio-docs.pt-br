---
title: MarkProfile | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- MarkProfile
ms.assetid: 54dac8c8-c8ee-4023-af27-b25466e3a6ec
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 98530a790963d1c7fc60742dda4bb16e14a28ab4
ms.sourcegitcommit: 269b55b413d2c82e6aa56c6ab8e53da7926fb2e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35238154"
---
# <a name="markprofile"></a>MarkProfile
O método `MarkProfile` insere uma marca de perfil no arquivo .*vsp*. A criação de perfil para o thread que contém a função `MarkProfile` deve ser ON para a marca a ser inserida.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
PROFILE_COMMAND_STATUS PROFILERAPI MarkProfile( long lMarker );  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `lMarker`  
  
 O marcador a inserir. O marcador deve ser maior ou igual a 0 (zero).  
  
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
 O valor de marca é inserido no arquivo .*vsp* sempre que o código é executado quando está sendo criado o perfil do thread que contém a função MarkProfile. Você pode chamar MarkProfile várias vezes.  
  
 Marcas de perfis são globais no escopo. Por exemplo, uma marca de perfil inserida em um thread pode ser usada para marcar o início ou término de um segmento de dados em um thread no arquivo .*vsp*.  
  
 O estado de criação de perfil para o thread que contém a função de perfil de marca deve estar ligado quando as marcas e os comentários são inseridos com o comando Mark ou com as funções da API (CommentMarkAtProfile, CommentMarkProfile ou MarkProfile).  
  
> [!IMPORTANT]
>  O método MarkProfile deve ser usado somente com criação de perfil por instrumentação.  
  
## <a name="net-framework-equivalent"></a>Equivalente ao .NET Framework  
 *Microsoft.VisualStudio.Profiler.dll*  
  
## <a name="function-information"></a>Informações de função  
 Cabeçalho: declarado em *VSPerf.h*  
  
 Biblioteca de importação: *VSPerf.lib*  
  
## <a name="example"></a>Exemplo  
 O código a seguir ilustra a função MarkProfile.  
  
```cpp  
void ExerciseMarkProfile()  
{  
    // Declare and initialize variables to pass to   
    // MarkProfile.  The values of these parameters   
    // are assigned based on the needs of the code;  
    // and for the sake of simplicity in this example,   
    // the variables are assigned arbitrary values.  
    int markId = 03;  
  
    // Declare enumeration to hold return value of   
    // call to MarkProfile.  
    PROFILE_COMMAND_STATUS markResult;  
  
    // Variables used to print output.  
    HRESULT hResult;  
    TCHAR tchBuffer[256];  
  
    markResult = MarkProfile(markId);  
  
    // Format and print result.  
    LPCTSTR pszFormat = TEXT("%s %d.\0");  
    TCHAR* pszTxt = TEXT("MarkProfile returned");  
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,   
        pszTxt, markResult);  
  
#ifdef DEBUG  
    OutputDebugString(tchBuffer);  
#endif  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API do criador de perfil do Visual Studio (nativo)](../profiling/visual-studio-profiler-api-reference-native.md)