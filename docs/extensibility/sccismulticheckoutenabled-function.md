---
title: Função SccIsMultiCheckoutEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccIsMultiCheckoutEnabled
helpviewer_keywords:
- SccIsMultiCheckoutEnabled function
ms.assetid: 6721639d-e475-4766-81b5-ee40a280fc70
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e91eb566a820f4fe11ceb629643e1815dcb87a8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700577"
---
# <a name="sccismulticheckoutenabled-function"></a>Função SccIsMultiCheckoutEnabled
Essa função verifica se o plug-in de controle do código-fonte permite vários check-outs em um arquivo.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccIsMultiCheckoutEnabled(
   LPVOID pContext,
   LPBOOL pbMultiCheckout
);
```

#### <a name="parameters"></a>Parâmetros
 pContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 pbMultiCheckout

fora Especifica se vários check-outs estão habilitados para este projeto (diferente de zero significa que há suporte para vários check-outs).

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A verificação foi bem-sucedida.|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 O IDE faz duas verificações para determinar se é possível fazer check-out de arquivos simultaneamente por mais de um usuário. Primeiro, o sistema de controle do código-fonte deve dar suporte a vários check-outs. O plug-in de controle do código-fonte pode especificar esse recurso durante a inicialização especificando o `SCC_CAP_MULTICHECKOUT` . Depois disso, como uma segunda verificação, o IDE chama essa função para determinar se o projeto atual dá suporte a vários check-outs. Se houver suporte a vários check-outs para o projeto selecionado, o plug-in retornará um código de êxito e definirá `pbMultiCheckout` como diferente de zero ( `TRUE` ) ou `FALSE` .

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
