---
title: Funcionalidades do Dotfuscator
ms.date: 03/28/2019
ms.devlang: dotnet
ms.topic: conceptual
keywords: Dotfuscator, Dotfuscator Community, Dotfuscator CE, PreEmptive, PreEmptive Solutions, PreEmptive Protection, proteção, community edition, ofuscação, .NET, gratuito, Visual Studio 2017, Visual Studio 2019, Visual Studio
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator Community
- Dotfuscator CE
- Dotfuscator
- obfuscation
- protection
description: Conheça as funcionalidades da cópia gratuita do Dotfuscator Community, incluída no Visual Studio 2017.
ms.assetid: 0ee89c58-c900-48fc-a6a2-65ace00e8bab
author: Joe-Sewell-PreEmptive
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 5bf42ec3c706282adf2752d21c0c121f89c2ed5f
ms.sourcegitcommit: 40393347a36779230d128f2355a911632a8d458e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58866631"
---
# <a name="capabilities-of-dotfuscator"></a>Funcionalidades do Dotfuscator

Esta página apresenta as funcionalidades do Dotfuscator Community com algumas referências às opções avançadas disponíveis por meio de [atualizações][upgrades].

O Dotfuscator Community é um sistema *pós-build* para aplicativos .NET.
Com ele, os usuários do Visual Studio podem [ocultar assemblies][obfuscation] e injetar [medidas de defesa ativa no aplicativo][checks]. Tudo sem que o Dotfuscator precise acessar o código-fonte original.
O Dotfuscator protege seu aplicativo de várias maneiras, criando uma estratégia de proteção em camadas.

O Dotfuscator Community dá suporte a uma ampla variedades de tipos de assembly e de aplicativo do .NET, incluindo [UWP (Plataforma Universal do Windows)][uwp] e [Xamarin][xamarin].

## <a name="intellectual-property-protection"></a>Proteção de propriedade intelectual

O design, o comportamento e a implementação do aplicativo são formas de IP (propriedade intelectual).
No entanto, os aplicativos criados para o .NET Framework são basicamente manuais abertos; é muito fácil executar engenharia reversa dos assemblies do .NET, [pois eles contêm metadados de alto nível e código intermediário][assemblies].

O Dotfuscator Community inclui a [ofuscação do .NET][obfuscation] básica na forma de [renomeação][renaming].
A ofuscação do código com o Dotfuscator reduz o risco de acesso não autorizado ao código-fonte por meio de engenharia reversa, já que informações importantes de nomenclatura deixarão de ser públicas.
A ofuscação também mostra um esforço de sua parte em proteger o código contra o exame – uma etapa importante em estabelecer que sua IP é legalmente protegida como segredo comercial.

Muitos dos [recursos de proteção de integridade do aplicativo](#application-integrity-protection) do Dotfuscator Community impedem ainda mais a engenharia reversa.
Por exemplo, um ator mal-intencionado pode tentar anexar um depurador a uma instância em execução do aplicativo para entender a lógica do programa.
O Dotfuscator pode injetar um [comportamento antidepuração][debug] no aplicativo para impedir isso.

## <a name="application-integrity-protection"></a>Proteção de integridade do aplicativo

Além de proteger o código-fonte, também é importante garantir que o aplicativo seja usado como projetado.
Os invasores podem tentar sequestrar o aplicativo para contornar políticas de licenciamento (ou seja, pirataria de software), roubar ou manipular dados confidenciais tratados pelo aplicativo ou alterar o comportamento do aplicativo.

O Dotfuscator Community pode injetar um [código de validação do aplicativo][checks] nos assemblies, incluindo medidas [contra adulteração][tamper], [contra depuração][debug] e [contra dispositivos com raiz][root].
Quando um estado de aplicativo inválido é detectado, o código de validação pode [chamar o código do aplicativo para resolver a situação de maneira apropriada][check-app].
Ou, se preferir não gravar o código para manipular usos inválidos do aplicativo, o Dotfuscator também poderá injetar comportamentos de [resposta][check-action] sem precisar modificar o código-fonte.

Muitos desses mesmos métodos também podem ser usados para impor [datas limite de fim da vida útil][shelflife] para avaliação ou software de avaliação.

## <a name="see-also"></a>Consulte também

[Este tópico no Guia completo do usuário do Dotfuscator Community][full]

<!-- Copyright © 2019 PreEmptive Solutions, LLC -->

[assemblies]:  https://docs.microsoft.com/dotnet/standard/assembly-format
[uwp]:  https://www.preemptive.com/blog/article/856-uwp-applications-in-dotfuscator-ce/91-dotfuscator-ce
[xamarin]:  https://www.preemptive.com/obfuscating-xamarin-with-dotfuscator

[upgrades]:  upgrades.md

[obfuscation]:  https://www.preemptive.com/dotfuscator/ce/docs/help/obfuscation_overview.html
[renaming]:  https://www.preemptive.com/dotfuscator/ce/docs/help/obfuscation_renaming.html

[checks]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_overview.html
[check-app]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_overview.html#app-notification
[check-action]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_overview.html#action

[tamper]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_tamper.html
[debug]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_debug.html
[root]: https://www.preemptive.com/dotfuscator/ce/docs/help/checks_root.html
[shelflife]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_shelflife.html

[full]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_capabilities.html
