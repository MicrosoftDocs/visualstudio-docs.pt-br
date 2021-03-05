---
description: Para depurar código nativo e gerenciado Misto em um processo de 64 bits, você deve ter .NET Framework versão 4.
title: Há suporte para a depuração de modo misto para processos x64 somente ao usar o Microsoft .NET Framework 4 ou superior | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.interop_unsupported_x64
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 31ae6b1c4a80f7d28cdbbdd2c4d944cddf15227d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146945"
---
# <a name="error-mixed-mode-debugging-for-x64-processes-is-supported-only-when-using-microsoft-net-framework-4-or-greater"></a>Erro: depuração de modo misto para processos x64 só é suportada durante o uso do Microsoft .NET Framework 4 ou superior
Para depurar código nativo e gerenciado Misto em um processo de 64 bits, você deve ter .NET Framework versão 4. Não há suporte para a depuração de modo misto de processos de 64 bits com versões .NET Framework anteriores a 4.

### <a name="to-correct-this-error"></a>Para corrigir este erro

- Execute uma das seguintes etapas:

  - Atualize seu .NET Framework para a versão 4.

  - Crie uma versão de 32 bits do aplicativo para depuração.

## <a name="see-also"></a>Confira também
- [Depuração remota](../debugger/remote-debugging.md)
