---
title: Segurança
ms.date: 06/01/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio], applications
- application design, securability
ms.assetid: 7d32c4cf-8bec-4307-a2a8-42f0ceddf3eb
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 87e9cb7e9400253713caab17da04c44eb11f5ed1
ms.sourcegitcommit: ce154aee5b403d5c1c41da42302b896ad3cf8d82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34843904"
---
# <a name="secure-applications"></a>Proteger aplicativos

Você deve considerar a segurança em todos os aspectos do desenvolvimento do aplicativo, do design à implantação. Comece executando o Visual Studio com a máxima segurança possível. Confira [Permissões de usuário](../ide/user-permissions-and-visual-studio.md).

Para que você desenvolva aplicativos efetivamente seguros, é preciso ter um entendimento básico dos conceitos e dos recursos de segurança das plataformas para as quais você está desenvolvendo. Também é preciso entender as técnicas de codificação segura.

## <a name="code-for-security"></a>Codificar com segurança

A maioria dos erros de codificação que resultam em vulnerabilidades de segurança ocorrem porque os desenvolvedores fazem suposições incorretas ao trabalhar com a entrada do usuário ou porque eles não têm um entendimento completo da plataforma para a qual estão desenvolvendo.

- [Diretrizes de codificação segura](/dotnet/standard/security/secure-coding-guidelines) descreve as diferentes maneiras em que o código .NET pode ser projetado para trabalhar com o sistema de segurança.
- [Práticas recomendadas de segurança para C++](/cpp/top/security-best-practices-for-cpp) contém informações sobre as ferramentas de segurança e as práticas recomendadas para desenvolvedores de C++.

## <a name="build-for-security"></a>Compilar com segurança

A segurança também é uma consideração importante no processo de compilação. Algumas etapas adicionais podem melhorar a segurança de um aplicativo implantado e ajudar a evitar engenharia reversa não autorizada, falsificação ou outros ataques:

- [Dotfuscator](dotfuscator/index.md) é gratuito e ajuda a proteger assemblies .NET contra engenharia reversa e uso não autorizado, como depuração não autorizada.
- [Assinatura de nome forte](managing-assembly-and-manifest-signing.md) pode ser usada para identificar os componentes de software com exclusividade e evitar falsificação de nome.

## <a name="see-also"></a>Consulte também

- [Segurança no .NET Framework](/dotnet/standard/security/index)
- [Segurança do Azure](/azure/security/)
- [Guia de segurança do Windows 10 Mobile](/windows/security/threat-protection/windows-10-mobile-security-guide)
- [Recursos de segurança da plataforma Apache Cordova](/visualstudio/cross-platform/tools-for-cordova/security/best-practices?view=toolsforcordova-2017)
- [Segurança do ASP.NET Core](/aspnet/core/security/?view=aspnetcore-2.1)
- [Segurança do Windows Forms](/dotnet/framework/winforms/windows-forms-security)