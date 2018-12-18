---
title: Registrando um personalizado de mecanismo de depuração | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- debug engines, registering
ms.assetid: 9984cd3d-d34f-4662-9ace-31766499abf5
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8ce7faf0ad538478d3291b48ac7306a39558663b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51732647"
---
# <a name="registering-a-custom-debug-engine"></a>Registrando um mecanismo de depuração personalizado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O mecanismo de depuração deve se registrar como uma fábrica de classes que segue as convenções de COM, bem como se registrar com o Visual Studio por meio da subchave do registro do Visual Studio.  
  
> [!NOTE]
>  Um exemplo de como registrar um mecanismo de depuração pode ser encontrado em uma amostra TextInterpreter, que é criado como parte do [Tutorial: Criando um depurar mecanismo usando COM ATL](http://msdn.microsoft.com/en-us/9097b71e-1fe7-48f7-bc00-009e25940c24).  
  
## <a name="dll-server-process"></a>Processo do servidor de DLL  
 Normalmente, um mecanismo de depuração é implementado em sua própria DLL como um servidor COM. Isso significa que o mecanismo de depuração deve registrar o CLSID da sua fábrica de classe com, antes que o Visual Studio pode acessá-lo. Em seguida, o mecanismo de depuração deve ser registrado com o próprio Visual Studio para estabelecer as propriedades (conhecido como métricas) de depuração dá suporte a do mecanismo. A escolha de métricas que são gravadas na subchave do registro do Visual Studio para o mecanismo de depuração depende dos recursos que o mecanismo de depuração suporta.  
  
 [Auxiliares do SDK para depuração](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) descreve não apenas os locais do Registro necessários para registrar um mecanismo de depuração; ele também descreve a biblioteca de dbgmetric.lib, que contém um número de funções úteis e declarações para os desenvolvedores de C++ que tornam manipular o registro mais fácil.  
  
### <a name="example"></a>Exemplo  
 A seguir está um exemplo típico (do exemplo TextInterpreter) que mostra como usar o `SetMetric` de função (de dbgmetric.lib), para registrar um mecanismo de depuração com o Visual Studio. As métricas que está sendo passadas também são definidas no dbgmetric.lib.  
  
> [!NOTE]
>  TextInterpreter é um mecanismo de depuração básica; ele não implementa — e, portanto, não registra — nenhum outro recurso. Um mecanismo de depuração mais completo teria uma lista completa de `SetMetric` chamadas ou seus equivalentes, uma para cada recurso, o mecanismo de depuração dá suporte.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Criando um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)   
 [Auxiliares do SDK para depuração](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [Tutorial: Criando um mecanismo de depuração usando COM ATL](http://msdn.microsoft.com/en-us/9097b71e-1fe7-48f7-bc00-009e25940c24)

