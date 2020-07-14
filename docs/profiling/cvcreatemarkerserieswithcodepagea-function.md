---
title: Função CvCreateMarkerSeriesWithCodePageA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmakers/CvCreateMarkerSeriesWithCodePageA
helpviewer_keywords:
- CvCreateMarkerSeriesWithCodePageA method
ms.assetid: 3d7ed601-2222-4be9-a557-f217db008753
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e17083c48db1ba1aa6b7ff45ee467ac97900e101
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332431"
---
# <a name="cvcreatemarkerserieswithcodepagea-function"></a>Função CvCreateMarkerSeriesWithCodePageA
Cria a série de marcador para determinado provedor e uma página de código especificada. Essa função pode ser usada para especificar a página de código explicitamente para o texto gravado por funções ANSI da API do marcador. Configurar a página de código pode ser útil caso o rastreamento seja capturado e então analisado em diferentes computadores com diferentes localidades/idiomas. Por padrão, a página de código retornada pela função GetACP() é usada.

## <a name="syntax"></a>Sintaxe

```C
HRESULT CvCreateMarkerSeriesWithCodePageA(
   _In_ PCV_PROVIDER pProvider,
   _In_ LPCSTR pSeriesName,
   _In_ UINT nTextCodePage,
   _Out_ PCV_MARKERSERIES* ppMarkerSeries
);
```

#### <a name="parameters"></a>Parâmetros
 `pProvider` Objeto do provedor inicializado anteriormente por CvInitProvider. Não pode ser NULL.

 `pSeriesName` Nome da série de marcador. Não pode ser NULL, mas uma cadeia de caracteres vazia é permitida.

 `nTextCodePage` Página de código válida.

 `ppMarkerSeries` Endereço de uma variável de saída que armazenará o contexto de série de marcador. Não pode ser NULL.

## <a name="return-value"></a>Valor retornado
 S_OK quando a série de marcador é criada com êxito ou código de erro no caso de erros. Use as macros SUCCEEDED/FAILED para verificar a condição de erro.

## <a name="requirements"></a>Requisitos
 **Cabeçalho:** *cvmarkers.h*

## <a name="see-also"></a>Veja também
- [Referência da biblioteca C++](../profiling/cpp-library-reference.md)