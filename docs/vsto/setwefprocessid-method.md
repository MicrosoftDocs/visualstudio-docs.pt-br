---
title: Método SetWefProcessId
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
ms.openlocfilehash: 13a6748e2e3b66f581a3c72c1f847e0329189e64
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537326"
---
# <a name="setwefprocessid-method"></a>Método SetWefProcessId
  Fornece o identificador do processo que executará o conteúdo do WEF (Web Extensions Framework).

## <a name="syntax"></a>Sintaxe

```csharp
HRESULT SetWefProcessId(
    [in] DWORD dwProcessId
);
```

#### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---------------|-----------------|
|*dwProcessId*|O identificador do processo que será usado para executar o conteúdo do WEF.|

## <a name="return-value"></a>Retornar valor
 Um valor HRESULT que indica se o método foi concluído com êxito.

## <a name="remarks"></a>Comentários
 Esse método deve ser chamado depois que o processo de conteúdo WEF é criado, mas antes de qualquer conteúdo de WEF ser executado.

 Se você quiser que o ambiente de desenvolvimento anexe um depurador ao processo de conteúdo do WEF, o ambiente deverá executar essa operação em sua implementação desse método.
