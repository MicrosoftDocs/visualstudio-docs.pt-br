---
description: Essa função permite que o usuário procure arquivos que já estão no sistema de controle do código-fonte e, posteriormente, faça com que esses arquivos façam parte do projeto atual.
title: Função SccAddFromScc | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccAddFromScc
helpviewer_keywords:
- SccAddFromScc function
ms.assetid: 902e764d-200e-46e1-8c42-4da7b037f9a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 48560f135d73c4e53ba132845f4c768cdf4ac982
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904870"
---
# <a name="sccaddfromscc-function"></a>Função SccAddFromScc
Essa função permite que o usuário procure arquivos que já estão no sistema de controle do código-fonte e, posteriormente, faça com que esses arquivos façam parte do projeto atual. Por exemplo, essa função pode obter um arquivo de header comum para o projeto atual sem copiar o arquivo. A matriz de retorno de arquivos, `lplpFileNames` , contém a lista de arquivos que o usuário deseja adicionar ao projeto do IDE.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccAddFromScc (
   LPVOID   pvContext,
   HWND     hWnd,
   LPLONG   lpnFiles,
   LPCSTR** lplpFileNames
);
```

### <a name="parameters"></a>Parâmetros
 pvContext

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 lpnFiles

[in, out] Um buffer para o número de arquivos que estão sendo adicionados. (Isso se `NULL` a memória apontada por deve ser `lplpFileNames` liberada. Consulte Comentários para obter detalhes.)

 lplpFileNames

[in, out] Uma matriz de ponteiros para todos os nomes de arquivo sem caminhos de diretório. Essa matriz é alocada e liberada pelo plug-in de controle do código-fonte. Se = 1 e não for , o primeiro nome na `lpnFiles` matriz apontada por `lplpFileNames` `NULL` `lplpFileNames` conterá a pasta de destino.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Os arquivos foram localizados e adicionados com êxito ao projeto.|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada sem efeito.|
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|

## <a name="remarks"></a>Comentários
 O IDE chama essa função. Se o plug-in de controle do código-fonte dá suporte à especificação de uma pasta de destino local, o IDE passa = 1 e passa o `lpnFiles` nome da pasta local para `lplpFileNames` .

 Quando a chamada para a função retorna, o plug-in atribuiu valores a e , alocando a memória para a matriz de nomes de arquivo conforme `SccAddFromScc` necessário (observe que essa alocação substitui o ponteiro `lpnFiles` `lplpFileNames` em `lplpFileNames` ). O plug-in de controle do código-fonte é responsável por colocar todos os arquivos no diretório do usuário ou na pasta de designação especificada. Em seguida, o IDE adiciona os arquivos ao projeto do IDE.

 Por fim, o IDE chama essa função uma segunda vez, passando `NULL` para `lpnFiles` . Isso é interpretado como um sinal especial pelo plug-in de controle do código-fonte para liberar a memória alocada para a matriz de nome de arquivo no `lplpFileNames``.`

 `lplpFileNames` é um `char ***` ponteiro. O plug-in de controle do código-fonte coloca um ponteiro para uma matriz de ponteiros para nomes de arquivo, passando assim a lista da maneira padrão para essa API.

> [!NOTE]
> As versões iniciais da API do VSSCI não forneceram uma maneira de indicar o projeto de destino para os arquivos adicionados. Para acomodar isso, a semântica do parâmetro foi aprimorada para torná-lo um parâmetro `lplpFIleNames` de entrada/saída em vez de um parâmetro de saída. Se apenas um único arquivo for especificado, ou seja, o valor apontado por = 1, o primeiro `lpnFiles` elemento de `lplpFileNames` conterá a pasta de destino. Para usar essas novas semânticas, o IDE chama `SccSetOption` a função com o parâmetro definido como `nOption` `SCC_OPT_SHARESUBPROJ` . Se um plug-in de controle do código-fonte não dá suporte à semântica, ele retorna `SCC_E_OPTNOTSUPPORTED` . Isso desabilita o uso do recurso **Adicionar do Controle do Código-Fonte.** Se um plug-in for compatível **com o recurso Adicionar do Controle do** Código-Fonte ( ), ele deverá dar suporte à nova `SCC_CAP_ADDFROMSCC` semântica e retornar `SCC_I_SHARESUBPROJOK` .

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
