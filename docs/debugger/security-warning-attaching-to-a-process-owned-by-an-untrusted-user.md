---
description: Essa caixa de diálogo de aviso é exibida quando você anexa a um processo que contém o código parcialmente confiável ou seja de propriedade de um usuário não confiável imediatamente antes de ocorrer a anexação.
title: 'Aviso de segurança: A anexação a um processo pertencente a um usuário não confiável pode ser perigosa. Se as informações a seguir parecerem suspeitas ou se você não tiver certeza, não anexe a este processo | Microsoft Docs'
ms.date: 1/15/2021
ms.topic: conceptual
f1_keywords:
- vs.debug.attachsecuritywarning
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 52246c1e-a371-40a0-b756-a435cc51876f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9fe65e753a0e825eed0c09fdefc4e93168d27ecb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160310"
---
# <a name="security-warning-attaching-to-a-process-owned-by-an-untrusted-user-can-be-dangerous-if-the-following-information-looks-suspicious-or-you-are-unsure-do-not-attach-to-this-process"></a>Aviso de segurança: A anexação a um processo pertencente a um usuário não confiável pode ser perigosa. Se as informações a seguir parecerem suspeitas ou, se você não tiver certeza, não anexe a esse processo

Essa caixa de diálogo de aviso é exibida quando você anexa a um processo que contém o código parcialmente confiável ou seja de propriedade de um usuário não confiável imediatamente antes de ocorrer a anexação. Um processo não confiável que contém o código mal-intencionado tem o potencial de danificar o computador que faz a depuração. Se você tiver razão para desconfiar do processo, clique em **Cancelar** para evitar a depuração.

Em cenários do IIS, você poderá ver esse aviso se usar um pool de aplicativos personalizado, que não é confiável.

Para suprimir este aviso ao depurar um cenário legítimo:

1. Feche o Visual Studio.

1. Defina o valor da `DisableAttachSecurityWarning` chave do registro como 1.

   Localize ou crie a chave em `HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\<version>\Debugger` e defina-a como 1.

   A partir do Visual Studio 2017, se você quiser exibir as configurações completas do registro, será necessário carregar o hive do registro privado. Para obter mais informações, consulte [como examinar o registro do Visual Studio 2017](https://github.com/microsoft/VSProjectSystem/blob/master/doc/overview/examine_registry.md). Certifique-se de descarregar o hive do registro privado antes de iniciar o Visual Studio.

1. Reinicie o Visual Studio.

1. Depois de concluir a depurar do cenário, redefina o valor como 0 e reinicie o Visual Studio.

Os “Usuários confiáveis” incluem você, mais um conjunto de usuários padrão que são definidos normalmente em computadores que têm o .NET Framework instalado, por exemplo, `aspnet`, `localsystem`, `networkservice` e `localservice`.

## <a name="uielement-list"></a>Lista de elementos de interface do usuário

 Nome do nome do assembly solicitado para depurar

 Usuário atual usuário

 Anexar Pressione para continuar a depuração anexando

 Não anexar ao processo

## <a name="see-also"></a>Confira também
- [Anexar aos processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [Segurança do depurador](../debugger/debugger-security.md)
