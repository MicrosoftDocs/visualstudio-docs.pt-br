---
description: Essa função inicializa o plug-in de controle do código-fonte e fornece recursos e limites para o IDE (ambiente de desenvolvimento integrado).
title: Função SccInitialize | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccInitialize
helpviewer_keywords:
- SccInitialize function
ms.assetid: 5bc0d28b-2c68-4d43-9e51-541506a8f76e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 633e8909febd758df455a9375f735a93e3407c77
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902521"
---
# <a name="sccinitialize-function"></a>Função SccInitialize
Essa função inicializa o plug-in de controle do código-fonte e fornece recursos e limites para o IDE (ambiente de desenvolvimento integrado).

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccInitialize (
   LPVOID* ppvContext,
   HWND    hWnd,
   LPCSTR  lpCallerName,
   LPSTR   lpSccName,
   LPLONG  lpSccCaps,
   LPSTR   lpAuxPathLabel,
   LPLONG  pnCheckoutCommentLen,
   LPLONG  pnCommentLen
);
```

#### <a name="parameters"></a>Parâmetros
 `ppvContext`

no O plug-in de controle do código-fonte pode posicionar um ponteiro para sua estrutura de contexto aqui.

 `hWnd`

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 `lpCallerName`

no O nome do programa que chama o plug-in de controle do código-fonte.

 `lpSccName`

[entrada, saída] O buffer em que o plug-in de controle do código-fonte coloca seu próprio nome (não para exceder `SCC_NAME_LEN` ).

 `lpSccCaps`

fora Retorna os sinalizadores de capacidade do plug-in de controle do código-fonte.

 `lpAuxPathLabel`

[entrada, saída] O buffer em que o plug-in de controle do código-fonte coloca uma cadeia de caracteres que descreve o `lpAuxProjPath` parâmetro retornado pelo [SccOpenProject](../extensibility/sccopenproject-function.md) e o [SccGetProjPath](../extensibility/sccgetprojpath-function.md) (não para exceder `SCC_AUXLABEL_LEN` ).

 `pnCheckoutCommentLen`

fora Retorna o comprimento máximo permitido para um comentário de check-out.

 `pnCommentLen`

fora Retorna o comprimento máximo permitido para outros comentários.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Inicialização do controle do código-fonte bem-sucedida.|
|SCC_E_INITIALIZEFAILED|Não foi possível inicializar o sistema.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar a operação especificada.|
|SCC_E_NONSPECFICERROR|Falha não específica; o sistema de controle do código-fonte não foi inicializado.|

## <a name="remarks"></a>Comentários
 O IDE chama essa função quando carrega pela primeira vez o plug-in de controle do código-fonte. Ele permite que o IDE passe determinadas informações, como o nome do chamador, para o plug-in. O IDE também retorna determinadas informações, como o comprimento máximo permitido para comentários e os recursos do plug-in.

 O `ppvContext` aponta para um `NULL` ponteiro. O plug-in de controle do código-fonte pode alocar uma estrutura para seu próprio uso e armazenar um ponteiro para essa estrutura no `ppvContext` . O IDE passará esse ponteiro para todas as outras funções da API VSSCI, permitindo que o plug-in tenha informações de contexto disponíveis sem recorrer ao armazenamento global e para dar suporte a várias instâncias do plug-in. Essa estrutura deve ser desalocada quando o [SccUninitialize](../extensibility/sccuninitialize-function.md) é chamado.

 Os `lpCallerName` `lpSccName` parâmetros e habilitam o IDE e o plug-in de controle do código-fonte para nomes do Exchange. Esses nomes podem ser usados simplesmente para distinguir entre várias instâncias ou podem realmente aparecer em menus ou caixas de diálogo.

 O `lpAuxPathLabel` parâmetro é uma cadeia de caracteres usada como um comentário para identificar o caminho do projeto auxiliar que é armazenado no arquivo de solução e passado para o plug-in de controle do código-fonte em uma chamada para o [SccOpenProject](../extensibility/sccopenproject-function.md). [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] usa a cadeia de caracteres "SourceSafe Project:"; outros plug-ins de controle do código-fonte devem evitar o uso dessa cadeia de caracteres específica.

 O `lpSccCaps` parâmetro fornece ao plug-in de controle do código-fonte um local para armazenar bitflags indicando os recursos do plug-in. (Para obter uma lista completa de funcionalidades bitflags, consulte [sinalizadores de capacidade](../extensibility/capability-flags.md)). Por exemplo, se o plug-in planeja gravar resultados em uma função de retorno de chamada fornecida pelo chamador, o plug-in definiria o bit de recurso SCC_CAP_TEXTOUT. Isso sinalizaria ao IDE para criar uma janela para resultados de controle de versão.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [Sinalizadores de capacidade](../extensibility/capability-flags.md)
