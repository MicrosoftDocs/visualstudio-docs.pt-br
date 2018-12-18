---
title: ResumeProfile | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- ResumeProfile
ms.assetid: 876f145b-ec07-4240-ade6-4f6e44baadce
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b15c57766c2deadc65e0d2d7d2b41baa50bf50e5
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35668130"
---
# <a name="resumeprofile"></a>ResumeProfile
O método `ResumeProfile` diminui o contador de suspender/retomar para o nível de criação de perfil especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
PROFILE_COMMAND_STATUS PROFILERAPI ResumeProfile(  
                       PROFILE_CONTROL_LEVEL Level,   
                       unsigned int dwId);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `Level`  
  
 Indica o nível de perfil de desempenho que pode ser aplicado a coleta de dados. Os enumeradores seguintes **PROFILE_CONTROL_LEVEL** podem ser usados para indicar um dos três níveis de desempenho aos quais a coleta de dados pode ser aplicada:  
  
|Enumerador|Descrição|  
|----------------|-----------------|  
|PROFILE_GLOBALLEVEL|A configuração de nível global afeta todos os processos e threads na execução da criação de perfil.|  
|PROFILE_PROCESSLEVEL|A configuração de nível de processo afeta todos os threads que fazem parte do processo especificado.|  
|PROFILE_THREADLEVEL|A configuração do nível de criação de perfil do thread afeta o thread especificado.|  
  
 `dwId`  
  
 O identificador de processo ou thread gerado pelo sistema.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/valor retornado  
 A função indica êxito ou falha usando a enumeração **PROFILE_COMMAND_STATUS**. O valor de retorno pode ser um dos seguintes:  
  
|Enumerador|Descrição|  
|----------------|-----------------|  
|PROFILE_ERROR_ID_NOEXIST|A ID de elemento de criação de perfil não existe.|  
|PROFILE_ERROR_LEVEL_NOEXIST|O nível de criação de perfil especificado não existe.|  
|PROFILE_ERROR_MODE_NEVER|O modo de criação de perfil foi definido para NUNCA quando a função foi chamada.|  
|PROFILE_ERROR_NOT_YET_IMPLEMENTED|A chamada de função de criação de perfil, o nível de criação de perfil ou combinação de chamada e nível ainda não foi implementada.|  
|PROFILE_OK|A chamada foi bem-sucedida.|  
  
## <a name="remarks"></a>Comentários  
 O valor inicial do contador Suspender/Retomar é 0. Cada chamada para SuspendProfile adiciona 1 à contagem de Suspender/Retomar; cada chamada para ResumeProfile subtrai 1.  
  
 Quando a contagem de suspender/retomar for maior que 0, o estado de Suspensão/retomar para o nível é OFF. Quando a contagem for menor ou igual a 0, o estado de Suspensão/retomar é ON.  
  
 Quando o estado de Iniciar/Parar e o estado de Suspender/Retomar estiverem em ON, o estado de criação de perfil para o nível será ON. Para um thread ter seu perfil criado, os estados de nível global, processo e de thread para o thread devem estar em ON.  
  
## <a name="net-framework-equivalent"></a>Equivalente ao .NET Framework  
 *Microsoft.VisualStudio.Profiler.dll*  
  
## <a name="function-information"></a>Informações de função  
 Cabeçalho: declarado em *VSPerf.h*  
  
 Biblioteca de importação: *VSPerf.lib*  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra a função ResumeProfile. O exemplo supõe que uma chamada para o método SuspendProfile foi feita para o mesmo thread ou processo identificado por [PROFILE_CURRENTID](../profiling/profile-currentid.md).  
  
```cpp  
void ExerciseResumeProfile()  
{  
    // The initial value of the Suspend/Resume counter is 0.   
    // Each call to SuspendProfile adds 1 to the Suspend/Resume   
    // count; each call to ResumeProfile subtracts 1.   
  
    // Variables used to print output.  
    HRESULT hResult;  
    TCHAR tchBuffer[256];  
  
    // Declare enumeration to hold result of call to ResumeProfile  
    PROFILE_COMMAND_STATUS profileResult;  
  
    profileResult = ResumeProfile(  
        PROFILE_GLOBALLEVEL,  
        PROFILE_CURRENTID);  
  
    // Format and print result.  
    LPCTSTR pszFormat = TEXT("%s %d.\0");  
    TCHAR* pszTxt = TEXT("ResumeProfile returned");  
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,   
        pszTxt, profileResult);  
  
#ifdef DEBUG  
    OutputDebugString(tchBuffer);  
#endif  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API do criador de perfil do Visual Studio (nativo)](../profiling/visual-studio-profiler-api-reference-native.md)