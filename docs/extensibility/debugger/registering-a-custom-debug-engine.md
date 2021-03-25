---
title: Registrando um mecanismo de depuração personalizado | Microsoft Docs
description: Saiba como o mecanismo de depuração se registra como uma fábrica de classes, seguindo as convenções COM, bem como registrando-se no Visual Studio por meio do registro.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, registering
ms.assetid: 9984cd3d-d34f-4662-9ace-31766499abf5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 04e4e8de875cb66ed285e610950baa1c5bf4ef3f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070655"
---
# <a name="register-a-custom-debug-engine"></a>Registrar um mecanismo de depuração personalizado
O mecanismo de depuração deve se registrar como uma fábrica de classes, seguindo as convenções COM, bem como registrar com o Visual Studio por meio da subchave do registro do Visual Studio.

> [!NOTE]
> Você pode encontrar um exemplo de como registrar um mecanismo de depuração no exemplo do textintérprete, que é criado como parte do [tutorial: Criando um mecanismo de depuração usando com ATL](/previous-versions/bb147024(v=vs.90)).

## <a name="dll-server-process"></a>Processo do servidor DLL
 Um mecanismo de depuração normalmente é configurado em sua própria DLL como um servidor COM. Como tal, o mecanismo de depuração deve registrar o CLSID de sua fábrica de classes com com, antes que o Visual Studio possa acessá-lo. Em seguida, o mecanismo de depuração deve se registrar com o Visual Studio para estabelecer quaisquer propriedades (também conhecidas como métricas) que o mecanismo de depuração suporta. A escolha das métricas gravadas na subchave do registro do Visual Studio depende dos recursos aos quais o mecanismo de depuração dá suporte.

 [Auxiliares de SDK para depuração](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) descreve não apenas os locais de registro necessários para registrar um mecanismo de depuração; Ele também descreve a biblioteca *dbgmetric. lib* , que contém uma série de funções e declarações úteis para desenvolvedores de C++ que facilitam a manipulação do registro.

### <a name="example"></a>Exemplo
 O exemplo a seguir (do exemplo textintérprete) mostra como usar a `SetMetric` função (de *dbgmetric. lib*) para registrar um mecanismo de depuração com o Visual Studio. As métricas que estão sendo passadas também são definidas em *dbgmetric. lib*.

> [!NOTE]
> Textintérprete é um mecanismo de depuração básico; Ele não é configurado — e, portanto, não se registra — quaisquer outros recursos. Um mecanismo de depuração mais completo teria uma lista completa de `SetMetric` chamadas ou seu equivalente, um para cada recurso compatível com o mecanismo de depuração.

```
// Define base registry subkey to Visual Studio.
static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0";

HRESULT CTextInterpreterModule::RegisterServer(BOOL bRegTypeLib, const CLSID * pCLSID)
{
    SetMetric(metrictypeEngine, __uuidof(Engine), metricName, L"Text File", false, strRegistrationRoot);
    SetMetric(metrictypeEngine, __uuidof(Engine), metricCLSID, CLSID_Engine, false, strRegistrationRoot);
    SetMetric(metrictypeEngine, __uuidof(Engine), metricProgramProvider, CLSID_MsProgramProvider, false, strRegistrationRoot);

    return base::RegisterServer(bRegTypeLib, pCLSID);
}
```

## <a name="see-also"></a>Confira também
- [Criando um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)
- [Auxiliares do SDK para depuração](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [Tutorial: Criando um mecanismo de depuração usando o COM ATL](/previous-versions/bb147024(v=vs.90))