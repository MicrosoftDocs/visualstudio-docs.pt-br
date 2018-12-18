---
title: Preparar para depurar os serviços do Windows | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], Windows services
- Windows Service applications, debugging
ms.assetid: ac0a99f7-ec3d-4a20-b17f-698a817fdcc2
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 86a80c6c24fdba594a5bfb5c11650b69eb2de693
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53065004"
---
# <a name="debugging-preparation-windows-services"></a>Preparação de depuração: Serviços Windows
Um serviço do Windows é um programa executado em segundo plano no Microsoft Windows. Os exemplos incluem o serviço de Telnet e o serviço de tempo do Windows, que atualiza o relógio visível do computador. Um serviço do Windows não pode ser executados no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]; ele deve ser executado no contexto do Gerenciador de Controle de Serviços. Para obter mais informações, confira [Criando serviços do Windows](/dotnet/framework/windows-services/how-to-create-windows-services), [Depurando aplicativos de serviço Windows](/dotnet/framework/windows-services/how-to-debug-windows-service-applications) e [Aplicativos de serviço Windows](/dotnet/framework/windows-services/index).  
  
## <a name="see-also"></a>Consulte também  
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)   
 [Tipos de projeto do C#, F# e Visual Basic](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [Configurações do projeto para configurações de depuração de C#](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Configurações do projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [Como: Depurar o método OnStart](../debugger/how-to-debug-the-onstart-method.md)