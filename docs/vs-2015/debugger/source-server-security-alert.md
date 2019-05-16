---
title: Alerta de segurança do servidor de origem | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.sourceserver.enablewarning
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 8451c281-6914-469c-b80c-6271cc3f3d17
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3f8b122deab5dbdc30b129bce221a804f8c53aa3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65699321"
---
# <a name="source-server-security-alert"></a>Alerta de segurança do servidor de origem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao usar o Servidor de Origem, use somente os arquivos de símbolo que forem de um local conhecido e confiável.  
  
 Este aviso aparece quando você ativa o suporte do servidor de origem. Os comandos do servidor de origem são inseridos nos arquivos de símbolo de depuração (arquivos de PDB). Verifique se você sabe de onde vêm seus arquivos PDB.  
  
> [!IMPORTANT]
> As seguintes ameaças potenciais de segurança devem ser levadas em conta ao usar o servidor de origem: Comandos arbitrários podem ser inseridos no arquivo PDB do aplicativo, portanto, certifique-se de que colocar somente aqueles que deseja executar no arquivo SRCSRV. ini. Qualquer tentativa de executar um comando que não esteja no arquivo srcsvr.ini fará com que uma caixa de diálogo de confirmação seja exibida. Para obter mais informações, consulte [aviso de segurança: O depurador deve executar o comando não confiável](../debugger/security-warning-debugger-must-execute-untrusted-command.md). Nenhuma validação é feita em parâmetros de comando, portanto, tenha cuidado com comandos confiáveis. Por exemplo, se você confiar no cmd.exe, um usuário mal-intencionado pode especificar parâmetros que tornariam o comando perigoso.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Servidor de Origem](https://msdn.microsoft.com/library/windows/desktop/ms680641.aspx)
