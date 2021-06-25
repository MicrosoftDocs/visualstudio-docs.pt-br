---
description: Essa função exibe (ou, opcionalmente, apenas verifica) as diferenças entre o arquivo atual (no disco local) e sua última versão de check-in no sistema de controle do código-fonte.
title: Função SccDiff | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccDiff
helpviewer_keywords:
- SccDiff function
ms.assetid: d49bc8c5-f631-4153-9d3c-feb3564da305
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 484d8b5e988ede9b50099e3c0376f2c3afce8317
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904650"
---
# <a name="sccdiff-function"></a>Função SccDiff
Essa função exibe (ou, opcionalmente, apenas verifica) as diferenças entre o arquivo atual (no disco local) e sua última versão de check-in no sistema de controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccDiff(
   LPVOID    pvContext,
   HWND      hWnd,
   LPCSTR    lpFileName,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>Parâmetros
 pvContext

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 Lpfilename

[in] Nome do arquivo para o qual a diferença é solicitada.

 fOptions

[in] Sinalizadores de comando. Consulte Comentários para obter detalhes.

 pvOptions

[in] Opções específicas do plug-in de controle do código-fonte.

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A cópia de trabalho e a versão do servidor são idênticas.|
|SCC_I_FILESDIFFERS|A cópia de trabalho difere da versão no controle do código-fonte.|
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|
|SCC_E_FILENOTCONTROLLED|O arquivo não está sob controle do código-fonte.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar essa operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção. Uma nova tentativa é recomendada.|
|SCC_E_NONSPECIFICERROR|Falha não específica; A diferença de arquivo não foi obtida.|
|SCC_E_FILENOTEXIST|O arquivo local não foi encontrado.|

## <a name="remarks"></a>Comentários
 Essa função atende a duas finalidades diferentes. Por padrão, ele exibe uma lista de alterações em um arquivo. O plug-in de controle do código-fonte abre sua própria janela, em qualquer formato que escolher, para exibir as diferenças entre o arquivo do usuário no disco e a versão mais recente do arquivo sob controle do código-fonte.

 Como alternativa, o IDE pode simplesmente precisar determinar se um arquivo foi alterado. Por exemplo, o IDE pode precisar determinar se é seguro fazer check-out de um arquivo sem informar o usuário. Nesse caso, o IDE passa no `SCC_DIFF_CONTENTS` sinalizador . O plug-in de controle do código-fonte deve verificar o arquivo no disco, byte byte, em relação ao arquivo controlado por origem e retornar um valor que indica se os dois arquivos são diferentes sem exibir nada para o usuário.

 Como uma otimização de desempenho, o plug-in de controle do código-fonte pode usar uma alternativa com base em uma verificação de verificação ou um timestamp em vez da comparação byte por byte chamada por : essas formas de comparação são obviamente mais rápidas, mas menos `SCC_DIFF_CONTENTS` confiáveis. Nem todos os sistemas de controle do código-fonte podem dar suporte a esses métodos de comparação alternativos e o plug-in pode ter que fazer fall back para uma comparação de conteúdo. Todos os plug-ins de controle do código-fonte devem, no mínimo, dar suporte a uma comparação de conteúdo.

> [!NOTE]
> Os sinalizadores de diferença rápida são mutuamente exclusivos. É válido não passar nenhum sinalizador, mas não é válido passar simultaneamente mais de um. `SCC_DIFF_QUICK_DIFF`, que é uma máscara que combina todos os sinalizadores, pode ser usada para testar, mas nunca deve ser passada como um parâmetro.

|`fOption`|Significado|
|---------------|-------------|
|SCC_DIFF_IGNORECASE|Comparação que não diferencia maiúsculas de minúsculas (pode ser usada para diferença rápida ou visual).|
|SCC_DIFF_IGNORESPACE|Ignora o espaço em branco (pode ser usado para uma diferença rápida ou visual).|
|SCC_DIFF_QD_CONTENTS|Compara silenciosamente o arquivo, byte byte.|
|SCC_DIFF_QD_CHECKSUM|Compara silenciosamente o arquivo por meio de uma verificação quando há suporte. Se não tiver suporte, o retornará para uma comparação de conteúdo.|
|SCC_DIFF_QD_TIME|Compara silenciosamente o arquivo por meio de seu timestamp quando há suporte. Se não tiver suporte, o retornará para uma comparação de conteúdo.|

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
