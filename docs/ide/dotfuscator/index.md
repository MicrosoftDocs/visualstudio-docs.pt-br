---
title: Dotfuscator Community Edition (CE)
ms.date: 10/10/2017
ms.devlang: dotnet
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
keywords: Dotfuscator, Dotfuscator CE, PreEmptive, PreEmptive Solutions, PreEmptive Protection, proteção, community edition, ofuscação, .NET, gratuito, Visual Studio 2017
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator CE
- Dotfuscator
- obfuscation
- protection
description: Saiba como você pode proteger seus aplicativos .NET com o Dotfuscator Community Edition incluído gratuitamente no Visual Studio 2017.
ms.assetid: d9550502-0a82-49a6-b005-2caa791fbe02
author: Joe-Sewell-PreEmptive
ms.author: gewarren
manager: douge
ms.openlocfilehash: d6cac51aaa73053dc0e1f306288d8198fdacccfd
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219051"
---
# <a name="dotfuscator-community-edition-ce"></a>Dotfuscator Community Edition (CE)

*PreEmptive Protection – Dotfuscator* fornece uma proteção abrangente de aplicativos .NET que pode ser adaptada facilmente ao seu ciclo de vida de desenvolvimento seguro de software.
Use-o para otimizar, proteger e remover aplicativos para desktop, móveis, servidores e incorporados, a fim de ajudar a proteger segredos comerciais e outras propriedades intelectuais (IP), reduzir a pirataria e a falsificação e proteger contra violação e depuração não autorizada.
O Dotfuscator funciona em assemblies compilados sem a necessidade de programação adicional ou até mesmo de acesso ao código-fonte.

![Proteção PreEmptive – Dotfuscator](media/header.svg)

## <a name="why-protection-matters"></a>Por que a proteção é importante

É importante **proteger sua propriedade intelectual** (IP).
O código do seu aplicativo contém detalhes de design e implementação que podem ser considerados como IP.
No entanto, os aplicativos criados no .NET Framework [contêm metadados significativos e um código intermediário de alto nível][assemblies], facilitando a engenharia reversa apenas usando uma das muitas ferramentas automatizadas e gratuitas.
Ao interromper e parar a engenharia reversa, você pode evitar divulgação não autorizada de IP, bem como demonstrar que seu código contém segredos comerciais.
O Dotfuscator pode [ofuscar][obfuscation] seus assemblies .NET para atrapalhar a engenharia reversa, mantendo o comportamento do aplicativo original.

Também é importante **proteger a integridade do seu aplicativo**.
Além da engenharia reversa, atores ruins podem tentar piratear seu aplicativo, alterar o comportamento do aplicativo no tempo de execução ou manipular dados.
O Dotfuscator pode injetar em seu aplicativo a capacidade de [detectar e responder a usos não autorizados][checks], incluindo violação, depuração de terceiros e dispositivos com raiz.

Para saber mais sobre como o Dotfuscator se encaixa em um ciclo de vida de desenvolvimento seguro de software, veja a página [Proteção de aplicativo do SDL][sdl-protection] da PreEmptive Solutions.

## <a name="about-dotfuscator-ce"></a>Sobre o Dotfuscator CE

Sua cópia do Microsoft Visual Studio 2017 inclui uma cópia do **_PreEmptive Protection – Dotfuscator_ Community Edition**, também conhecido como Dotfuscator CE, gratuito para uso pessoal.
Para obter instruções sobre como instalar a versão do Dotfuscator CE incluída no Visual Studio 2017, veja a [página Instalação][install].

O Dotfuscator CE oferece uma ampla variedade de [sistemas de proteção de serviços para software][software-protection] aos desenvolvedores, arquitetos e testadores.
Exemplos de [ofuscação de .NET][obfuscation] e outros recursos de [Proteção de aplicativo][app-protection] incluídos no Dotfuscator CE:

* *[Renomeação][renaming]* de identificadores para dificultar a engenharia reversa de assemblies compilados.
* *[Antiviolação][tamper]* para detectar a execução de aplicativos violados e encerrar ou responder às sessões violadas.
* *[Antidepuração][debug]* para detectar a anexação de um depurador a um aplicativo em execução e encerrar ou responder às sessões depuradas.
* *[Proteção contra dispositivos com raiz][root]* para detectar se o aplicativo está em execução em um dispositivo Android com raiz e encerrar ou responder às sessões nesses dispositivos.
* *[Comportamentos de expiração do aplicativo][shelflife]* que codificam uma data de "fim da vida útil" e encerram as sessões do aplicativo que expirou.

Para obter detalhes sobre esses recursos, incluindo como eles se encaixam em sua estratégia de proteção do aplicativo, veja a [página Recursos][capabilities].

O Dotfuscator CE oferece proteção básica de forma nativa.
Há ainda mais medidas de proteção do aplicativo disponíveis para usuários registrados do Dotfuscator CE e para os usuários do *PreEmptive Protection - Dotfuscator* Professional Edition, o principal [Ofuscador .NET][net-obfuscator] do mundo.
Para saber mais sobre como melhorar o Dotfuscator, veja a [página Atualizações][upgrades].

## <a name="getting-started"></a>Introdução

Para começar a usar o Dotfuscator CE no Visual Studio, digite `dotfuscator` na barra de pesquisa **Início Rápido** (Ctrl+Q).

* Se o Dotfuscator CE já estiver instalado, o **Início Rápido** abrirá a opção *Menu* para iniciar a interface do usuário do Dotfuscator CE. Para obter detalhes, consulte [a página de Introdução do Guia do usuário completo do CE Dotfuscator][get-started].
* Se o Dotfuscator CE ainda não estiver instalado, o **Início Rápido** abrirá a opção *Instalar* relevante. Consulte a [página Instalação][install] para obter detalhes.

Você também pode obter a **versão mais recente** do Dotfuscator CE na [página de Downloads do Dotfuscator em preemptive.com][download].

## <a name="full-documentation"></a>Documentação completa

Esta página e suas subpáginas fornecem uma visão geral de alto nível dos recursos do Dotfuscator CE, bem como [instruções para instalar a ferramenta][install].

Veja [o guia de usuário completo do Dotfuscator CE em preemptive.com][full] para obter instruções detalhadas de uso, incluindo [como começar a usar a interface do usuário do Dotfuscator CE][get-started].

<!-- Copyright © 2017 PreEmptive Solutions, LLC -->

[assemblies]:  https://docs.microsoft.com/dotnet/standard/assembly-format
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
