---
title: Erro-a depuração de modo misto para processos x64 tem suporte apenas ao usar o Microsoft .NET Framework 4 ou superior | Microsoft Docs
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
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 9f30fe9b729df84506f6717e5fd895297390dea6
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460631"
---
# <a name="error-mixed-mode-debugging-for-x64-processes-is-supported-only-when-using-microsoft-net-framework-4-or-greater"></a>Erro: depuração de modo misto para processos x64 só é suportada durante o uso do Microsoft .NET Framework 4 ou superior
Para depurar código nativo e gerenciado Misto em um processo de 64 bits, você deve ter .NET Framework versão 4. Não há suporte para a depuração de modo misto de processos de 64 bits com versões .NET Framework anteriores a 4.

### <a name="to-correct-this-error"></a>Para corrigir este erro

- Execute uma das seguintes etapas:

  - Atualize seu .NET Framework para a versão 4.

  - Crie uma versão de 32 bits do aplicativo para depuração.

## <a name="see-also"></a>Veja também
- [Depuração remota](../debugger/remote-debugging.md)