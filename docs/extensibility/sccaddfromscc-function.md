---
description: Essa função permite que o usuário procure arquivos que já estão no sistema de controle do código-fonte e, posteriormente, torne esses arquivos parte do projeto atual.
title: Função SccAddFromScc | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: be67fd18c6cac7217da0d79aaef766e942e15fb9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085670"
---
# <a name="sccaddfromscc-function"></a>Função SccAddFromScc
Essa função permite que o usuário procure arquivos que já estão no sistema de controle do código-fonte e, posteriormente, torne esses arquivos parte do projeto atual. Por exemplo, essa função pode obter um arquivo de cabeçalho comum no projeto atual sem copiar o arquivo. A matriz de retorno de arquivos, `lplpFileNames` , contém a lista de arquivos que o usuário deseja adicionar ao projeto do IDE.

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

no A estrutura de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 lpnFiles

[entrada, saída] Um buffer para o número de arquivos que estão sendo adicionados. ( `NULL` Se a memória apontada pelo `lplpFileNames` for ser lançada. Consulte comentários para obter detalhes.)

 lplpFileNames

[entrada, saída] Uma matriz de ponteiros para todos os nomes de arquivo sem caminhos de diretório. Essa matriz é alocada e liberada pelo plug-in de controle do código-fonte. Se `lpnFiles` = 1 e `lplpFileNames` não for `NULL` , o primeiro nome na matriz apontado pelo `lplpFileNames` contém a pasta de destino.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Os arquivos foram localizados e adicionados ao projeto com êxito.|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada sem nenhum efeito.|
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|

## <a name="remarks"></a>Comentários
 O IDE chama essa função. Se o plug-in de controle do código-fonte der suporte à especificação de uma pasta de destino local, o IDE passará `lpnFiles` = 1 e passará o nome da pasta local para `lplpFileNames` .

 Quando a chamada para a `SccAddFromScc` função retorna, o plug-in atribuiu valores para `lpnFiles` e `lplpFileNames` , alocando a memória para a matriz de nome de arquivo conforme necessário (Observe que essa alocação substitui o ponteiro em `lplpFileNames` ). O plug-in de controle do código-fonte é responsável por colocar todos os arquivos no diretório do usuário ou na pasta de designação especificada. O IDE, em seguida, adiciona os arquivos ao projeto do IDE.

 Por fim, o IDE chama essa função uma segunda vez, passando `NULL` para `lpnFiles` . Isso é interpretado como um sinal especial pelo plug-in de controle do código-fonte para liberar a memória alocada para a matriz de nome de arquivo em `lplpFileNames``.`

 `lplpFileNames` é um `char ***` ponteiro. O plug-in de controle do código-fonte coloca um ponteiro em uma matriz de ponteiros para nomes de arquivos, passando assim a lista da forma padrão para essa API.

> [!NOTE]
> As versões iniciais da API do VSSCI não forneceram uma maneira de indicar o projeto de destino para os arquivos adicionados. Para acomodar isso, a semântica do `lplpFIleNames` parâmetro foi aprimorada para torná-lo um parâmetro in/out em vez de um parâmetro de saída. Se apenas um único arquivo for especificado, ou seja, o valor apontado por `lpnFiles` = 1, o primeiro elemento de `lplpFileNames` conterá a pasta de destino. Para usar essas novas semânticas, o IDE chama a `SccSetOption` função com o `nOption` parâmetro definido como `SCC_OPT_SHARESUBPROJ` . Se um plug-in de controle do código-fonte não oferecer suporte à semântica, ele retornará `SCC_E_OPTNOTSUPPORTED` . Isso desabilita o uso do recurso **Adicionar do controle do código-fonte** . Se um plug-in der suporte ao recurso **Adicionar do controle do código-fonte** ( `SCC_CAP_ADDFROMSCC` ), ele deverá dar suporte à nova semântica e retorno `SCC_I_SHARESUBPROJOK` .

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
