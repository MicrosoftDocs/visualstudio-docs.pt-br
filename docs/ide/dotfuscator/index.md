---
title: Dotfuscator Community
ms.date: 03/28/2019
ms.devlang: dotnet
ms.topic: overview
keywords: Dotfuscator, Dotfuscator CE, Dotfuscator Community, PreEmptive, PreEmptive Solutions, PreEmptive Protection, proteção, community edition, ofuscação, .NET, gratuito, Visual Studio 2019, Visual Studio 2017, Visual Studio
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator CE
- Dotfuscator Community
- Dotfuscator
- obfuscation
- protection
description: Saiba como proteger os aplicativos do .NET com a cópia do Dotfuscator Community incluída gratuitamente no Visual Studio.
ms.assetid: d9550502-0a82-49a6-b005-2caa791fbe02
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 7a8602dc99ba63e6cba5035636af0fbd47263e58
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769492"
---
# <a name="dotfuscator-community"></a>Dotfuscator Community

***PreEmptive Protection – Dotfuscator*** fornece uma proteção abrangente de aplicativos .NET que pode ser adaptada facilmente ao seu ciclo de vida de desenvolvimento seguro de software.
Use-o para otimizar, proteger e remover aplicativos para desktop, móveis, servidores e incorporados, a fim de ajudar a proteger segredos comerciais e outras propriedades intelectuais (IP), reduzir a pirataria e a falsificação e proteger contra violação e depuração não autorizada.
O Dotfuscator funciona em assemblies compilados sem a necessidade de programação adicional ou até mesmo de acesso ao código-fonte.

![Proteção PreEmptive – Dotfuscator](media/header.svg)

## <a name="why-protection-matters"></a>Por que a proteção é importante

É importante **proteger sua propriedade intelectual** (IP).
O código do seu aplicativo contém detalhes de design e implementação que podem ser considerados como IP.
No entanto, os aplicativos desenvolvidos no .NET Framework [contêm metadados significativos e um código intermediário de alto nível][assemblies], facilitando a engenharia reversa apenas usando uma das muitas ferramentas automatizadas e gratuitas.
Ao interromper e parar a engenharia reversa, você pode evitar divulgação não autorizada de IP, bem como demonstrar que seu código contém segredos comerciais.
O Dotfuscator pode [ofuscar][obfuscation] seus assemblies .NET para atrapalhar a engenharia reversa, mantendo o comportamento do aplicativo original.

Também é importante **proteger a integridade do seu aplicativo**.
Além da engenharia reversa, atores mal-intencionados podem tentar piratear seu aplicativo, alterar o comportamento do aplicativo no tempo de execução ou manipular dados.
O Dotfuscator pode injetar em seu aplicativo a capacidade de [detectar usos não autorizados e responder a eles][checks], incluindo violação, depuração de terceiros e dispositivos com raiz.

Para saber mais sobre como o Dotfuscator se encaixa em um ciclo de vida de desenvolvimento seguro de software, confira a página [Proteção de aplicativo do SDL][sdl-protection] da PreEmptive Solutions.

## <a name="about-dotfuscator-community"></a>Sobre o Dotfuscator Community

Sua cópia do Microsoft Visual Studio inclui uma cópia gratuita do ***PreEmptive Protection – Dotfuscator Community*** para uso pessoal.
Esta versão gratuita era conhecida anteriormente como Dotfuscator Community Edition ou Dotfuscator CE. Para obter instruções sobre como instalar a versão do Dotfuscator Community incluída no Visual Studio, confira a [página de Instalação][install].

O Dotfuscator Community oferece uma ampla variedade de serviços de [proteção para software][software-protection] aos desenvolvedores, arquitetos e testadores.
Entre os exemplos de [ofuscação para .NET][obfuscation] e outros recursos de [Proteção do aplicativo][app-protection] incluídos no Dotfuscator Community estão:

* *[Renomeação][renaming]* de identificadores para dificultar a engenharia reversa de assemblies compilados.
* *[Antiadulteração][tamper]* para detectar a execução de aplicativos adulterados e encerrar as sessões adulteradas ou responder a elas.
* *[Antidepuração][debug]* para detectar a anexação de um depurador a um aplicativo em execução e encerrar as sessões depuradas ou responder a elas.
* *[Proteção contra dispositivos com raiz][root]* para detectar se o aplicativo está em execução em um dispositivo Android com raiz e encerrar as sessões nesses dispositivos ou responder a elas.
* *[Comportamentos de expiração do aplicativo][shelflife]* que codificam uma data de "fim da vida útil" e encerram as sessões expiradas do aplicativo.

Para obter detalhes sobre esses recursos, incluindo como eles se encaixam em sua estratégia de proteção do aplicativo, confira a [página Funcionalidades][capabilities].

O Dotfuscator Community oferece proteção básica pronta para uso.
Há ainda mais medidas de proteção do aplicativo disponíveis para usuários registrados do Dotfuscator Community e para os usuários do ***PreEmptive Protection – Dotfuscator Professional***, o principal [ofuscador para .NET][net-obfuscator] do mundo.
Para saber mais sobre como melhorar o Dotfuscator, confira a [página Atualizações][upgrades].

## <a name="getting-started"></a>Introdução

::: moniker range="vs-2019"

Para começar a usar o Dotfuscator Community no Visual Studio, digite `dotfuscator` na **caixa de pesquisa** (Ctrl+Q).

* Se já instalou o Dotfuscator Community, a **caixa de pesquisa** mostrará a opção para iniciar o Dotfuscator Community, abaixo do título *Menus*. Para obter detalhes, confira [a página de Introdução do Guia completo do usuário do Dotfuscator Community][get-started].
* Se ainda não instalou o Dotfuscator Community, a **caixa de pesquisa** mostrará a opção **Instalar o PreEmptive Protection – Dotfuscator**, abaixo do título *Componentes individuais*. Confira a [página de Instalação][install] para obter detalhes.

::: moniker-end

::: moniker range="vs-2017"

Para começar a usar o Dotfuscator Community no Visual Studio, digite `dotfuscator` na barra de pesquisa de **Início Rápido** (Ctrl+Q).

* Se já instalou o Dotfuscator Community, o **Início Rápido** exibirá a opção *Menu* para iniciar a interface do usuário do Dotfuscator Community. Para obter detalhes, confira [a página de Introdução do Guia completo do usuário do Dotfuscator Community][get-started].
* Se ainda não instalou o Dotfuscator Community, o **Início Rápido** exibirá a opção *Instalar* relevante. Confira a [página de Instalação][install] para obter detalhes.

::: moniker-end

Também é possível obter a **versão mais recente** do Dotfuscator Community na [página de Downloads do Dotfuscator em preemptive.com][download].

## <a name="full-documentation"></a>Documentação completa

Esta página e as respectivas subpáginas fornecem uma visão geral de alto nível dos recursos do Dotfuscator Community, bem como [instruções para instalar a ferramenta][install].

Confira [o Guia do Usuário Completo do Dotfuscator Community em preemptive.com][full] para obter instruções de uso detalhadas, inclusive [como começar a usar a interface do usuário do Dotfuscator Community][get-started].

<!-- Copyright © 2019 PreEmptive Solutions, LLC -->

[assemblies]:  /dotnet/standard/assembly-format
[software-protection]:  https://www.preemptive.com/software-protection
[obfuscation]:  https://www.preemptive.com/obfuscation
[app-protection]:  https://www.preemptive.com/application-protection
[sdl-protection]:  https://www.preemptive.com/solutions/SDL-App-Protection
[net-obfuscator]:  https://www.preemptive.com/products/dotfuscator/overview
[download]:  https://www.preemptive.com/products/dotfuscator/downloads

[install]:  install.md
[capabilities]:  capabilities.md
[upgrades]:  upgrades.md

[get-started]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_getstarted.html

[renaming]:  https://www.preemptive.com/dotfuscator/ce/docs/help/obfuscation_renaming.html

[checks]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_overview.html
[tamper]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_tamper.html
[debug]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_debug.html
[root]: https://www.preemptive.com/dotfuscator/ce/docs/help/checks_root.html
[shelflife]:  https://www.preemptive.com/dotfuscator/ce/docs/help/checks_shelflife.html

[full]:  https://www.preemptive.com/dotfuscator/ce/docs/help/index.html
