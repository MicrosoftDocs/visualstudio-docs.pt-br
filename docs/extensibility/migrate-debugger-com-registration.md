---
title: Migrar o registro de classe do depurador de 64 bits COM | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 45cfcee6-7a68-4d4f-b3f6-e2d8a0fa066a
author: gregg-miskelly
ms.author: greggm
manager: douge
ms.workload:
- greggm
ms.openlocfilehash: 6c7578ddbdf84a1520a732fb64380bb53e5359f9
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39637845"
---
# <a name="migrate-64-bit-debugger-com-class-registration"></a>Migrar o registro de classe COM de depurador de 64 bits

Para extensões de depurador que registre-se COM as classes em HKEY_CLASSES_ROOT usando regasm, regsvr32, ou escrevendo diretamente no registro e carregado no *msvsmon.exe* (o depurador remoto), agora é possível fornecer isso registro do msvsmon sem a necessidade de escrever para HKEY_CLASSES_ROOT. Isso afeta herdados avaliadores de expressão do depurador .NET ou mecanismos de depuração que são configurados para carregar na *msvsmon.exe* processo.

## <a name="msvsmon-comclass-def"></a>o msvsmon-comclass-def

Para usar essa técnica, adicione uma  **.msvsmon-comclass-def.json* arquivo ao lado do msvsmon (InstallDir:* \Common7\IDE\Remote Debugger\x64*).

Aqui está um exemplo de arquivo de definição de comclass msvsmon que registra um gerenciado e uma classe nativa:

Nome do arquivo: *MyCompany.MyExample.msvsmon-comclass-def.json*

```json
{
  "managedCOMClasses": [
    {
      "clsid": "{C9F48B25-36ED-4B22-8210-98BC5BE4D1E7}",
      "assemblyName": "MyCompany.MyAssembly",
      "className": "MyCompany.MyNamespace.MyClass"
    }
  ],
  "nativeCOMClasses": [
    {
      "clsid": "{42A476E9-8FA7-44D5-ADFE-216AD371EEC9}",
      "dllPath": "MyExample.dll"
    }
  ]
}
```
