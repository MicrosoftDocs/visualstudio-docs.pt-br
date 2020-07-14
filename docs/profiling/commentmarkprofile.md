---
title: CommentMarkProfile | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CommentMarkProfile
- CommentMarkProfileA
ms.assetid: 33ccff45-c33a-4672-b41f-5b317b848cd1
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 2972f9d470bebe3a65b7d525aa2b358d68ad5f1c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546582"
---
# <a name="commentmarkprofile"></a>CommentMarkProfile
A função `CommentMarkProfile` insere um marcador numérico e uma cadeia de caracteres de texto no arquivo .*vsp*. Para que a marcação e o comentário sejam inseridos, a criação de perfil para o thread que contém a função `CommentMarkProfile` deve ser ON.

## <a name="syntax"></a>Sintaxe

```cpp
PROFILE_COMMAND_STATUS PROFILERAPI CommentMarkProfile(
                                   long lMarker,
                                   LPCTSTR szComment);
```

#### <a name="parameters"></a>Parâmetros
 `lMarker`

 Marcador numérico para inserir. O marcador deve ser maior ou igual a 0 (zero).

 `szComment`

 Ponteiro para a cadeia de texto para inserir. A cadeia de caracteres deve ser menor que 256 caracteres, incluindo o terminador NULO.

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
 O estado de criação de perfil para o thread que contém a função de perfil de marca deve estar ligado quando as marcas e os comentários são inseridos com o comando VSInstr Mark ou com as funções (CommentMarkAtProfile, CommentMarkProfile ou MarkProfile).

 Marcas de perfis são globais no escopo. Por exemplo, uma marca de perfil inserida em um thread pode ser usada para marcar o início ou o fim de um segmento de dados em qualquer thread no. arquivo *VSP* .

> [!IMPORTANT]
> O método CommentMarkProfile só pode ser usado com a instrumentação.

## <a name="net-framework-equivalent"></a>Equivalente ao .NET Framework
 Microsoft.VisualStudio.Profiler.dll

## <a name="function-information"></a>Informações de função

|Item|Valor|
|-|-|
|**Cabeçalho**|Inclui VSPerf.h|
|**Biblioteca**|Use VSPerf.lib|
|**Unicode**|Implementado como `CommentMarkProfileW` (Unicode) e `CommentMarkProfileA` (ANSI).|

## <a name="example"></a>Exemplo
 O código a seguir ilustra a chamada da função CommentMarkProfile. O exemplo pressupõe o uso de macros de cadeia de caracteres do Win32 e as configurações do compilador de Unicode para determinar se o código chama a chamada da função [!INCLUDE[vcpransi](../profiling/includes/vcpransi_md.md)].

```cpp
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

## <a name="see-also"></a>Confira também
- [Referência da API do criador de perfil do Visual Studio (nativo)](../profiling/visual-studio-profiler-api-reference-native.md)
