---
title: Método GetAutoInsertExtensions
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f5d88af6f24306b7b243359c9797a2cb7e7449bc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543501"
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
 Cada aplicativo para o Office a ser inserido é retornado como um nome de extensão de aplicativo do Office, que corresponde a um valor em **HKEY_CURRENT_USER \software\microsoft\office\wef\developer**. O host deve procurar esses valores no registro e, em seguida, inserir as extensões automaticamente.
