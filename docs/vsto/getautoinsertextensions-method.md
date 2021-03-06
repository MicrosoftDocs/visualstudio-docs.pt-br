---
description: Obtém informações sobre os aplicativos para o Office que devem ser inseridos automaticamente durante a depuração.
title: Método GetAutoInsertExtensions
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c4a49942f50a79db604d2363cf2d85762c5ddce5
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223427"
---
# <a name="getautoinsertextensions-method"></a>Método GetAutoInsertExtensions
  Obtém informações sobre os aplicativos para o Office que devem ser inseridos automaticamente durante a depuração.

 Este método está reservado para uso futuro.

## <a name="syntax"></a>Sintaxe

```csharp
HRESULT GetAutoInsertExtensions(
    [out, retval] SAFEARRAY(BSTR)* psaExtensionNames
);
```

### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---------------|-----------------|
|*psaExtensionNames*|Os nomes de extensão dos aplicativos para o Office.|

## <a name="return-value"></a>Retornar valor
 Um valor HRESULT que indica se o método foi concluído com êxito.

## <a name="remarks"></a>Comentários
 Cada aplicativo para o Office a ser inserido é retornado como um nome de extensão de aplicativo do Office, que corresponde a um valor em **HKEY_CURRENT_USER\Software\Microsoft\Office\WEF\Developer**. O host deve procurar esses valores no registro e, em seguida, inserir as extensões automaticamente.
