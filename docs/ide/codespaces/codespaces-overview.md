---
title: Visão geral do GitHub Codespaces (versão prévia)
description: Saiba mais sobre o GitHub Codespaces com o Visual Studio e como ele pode ajudar a estender seu ambiente de desenvolvimento para a nuvem.
ms.topic: overview
ms.date: 09/04/2020
author: gregvanl
ms.author: gregvanl
manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: vs-2019
ms.openlocfilehash: ab50c3c2df2cfad6d489d800f47624503844dc9d
ms.sourcegitcommit: a667ce8394a800906d633737f4fcbc77f0fcba7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/30/2021
ms.locfileid: "108298737"
---
# <a name="what-is-github-codespaces-preview"></a>O que é o GitHub Codespaces? (Visualização)

> [!Important]
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Incentivamos você a estar envolvido em nosso [Fórum da comunidade de desenvolvedores](https://developercommunity.visualstudio.com/home) para Visual Studio para obter informações sobre versões futuras e informações de roteiro.

Bem-vindo ao Codespaces! Estamos felizes por você estar aqui.

O GitHub Codespaces fornece um ambiente de desenvolvimento baseado em nuvem para qualquer atividade, seja um projeto de longo prazo ou uma tarefa de curto prazo, como revisar uma solicitação de pull.

Além disso, o GitHub Codespaces traz muitos dos benefícios do DevOps, como a repetição e &mdash; a confiabilidade que normalmente foram reservadas para cargas de trabalho de produção &mdash; em um ambiente de desenvolvimento. Você também pode personalizar o GitHub Codespaces para que as ferramentas, os processos e as configurações que você preferir e que dependem também estejam lá.

Este documento explicará os principais conceitos e apresentará os recursos do Codespaces. Se você pretende começar, confira [usar o Visual Studio com um codespace](use-visual-studio-with-codespaces.md).

## <a name="concepts-and-features"></a>Conceitos e funcionalidades

Os recursos do GitHub Codespaces são criados com base em alguns conceitos fundamentais. Esta seção aborda esses conceitos e oferece um breve tour pelos recursos.

### <a name="remote-development"></a>Desenvolvimento remoto

Atualmente, muitos desenvolvedores tentam codificar em instalações remotas ou VMs configuradas com o desenvolvimento e as pilhas de tempo de execução específicas. Eles fazem isso porque é muito difícil, com muita interrupção e, em alguns casos, quase impossível configurar esses ambientes de desenvolvimento localmente. Além disso, os indivíduos desejam experimentar novas tecnologias ou novas estruturas sem o medo de "bagunçar" as máquinas necessárias para o trabalho diário.

Embora o uso de ambientes remotos e ferramentas com capacidade remota capacita os desenvolvedores, geralmente há a sobrecarga do gerenciamento de máquinas. A configuração do ambiente geralmente complica a integração e a alternância de contexto. O GitHub Codespaces remove as barreiras para a integração rápida e a alternância de contexto, permitindo que muitos ambientes existam simultaneamente.

O GitHub Codespaces fornece soluções gerenciadas que permitem que você se concentre na produtividade da instalação. O GitHub Codespaces conceitualmente e tecnicamente estende o Visual Studio 2019 para desenvolvimento remoto.

### <a name="about-codespaces"></a>Sobre o codespaces

Um codespace é a metade do "back-end" do Codespaces do GitHub. É onde ocorre toda a computação associada ao desenvolvimento de software: Compilando, Depurando, restaurando, etc. A criação de um codespace prepara tudo o que você precisa para concluir uma tarefa, examinar uma PR ou iniciar um novo projeto. Codespaces configure o tempo de execução, o compilador, o depurador, o editor, as configurações de dotfile personalizadas e o código-fonte necessário para trabalhar em um projeto.

Os codespaces hospedados na nuvem oferecem os seguintes benefícios:

- Eles são rápidos de criar e descartáveis. Crie quantas forem necessárias (até os limites de conta) e descarte-as quando terminar.
- Eles são gerenciados, o que reduz a manutenção geral para você.
- Eles têm preços previsíveis e você só paga pelo que usar. E, há uma suspensão interna para eliminar custos de fuga.
- Eles salvam recursos de computação. Quando você move sua carga de trabalho de desenvolvimento para a nuvem, ela libera os recursos limitados em seu computador pessoal.

## <a name="custom-configuration"></a>Configuração personalizada

O GitHub Codespaces foi criado para acomodar a maior variedade de projetos ou tarefas. Você pode começar com recursos de configuração inteligente que fornecem padrões comuns ou ajustar um codespace com [configuração personalizada](customize-codespaces.md).

A configuração flexível permite que os desenvolvedores se integrem rapidamente a projetos com configuração e requisitos exclusivos que são difíceis de aplicar em um computador local. Além disso, rereproduzível codespaces eliminar problemas de "trabalhos em meu computador".

## <a name="personal-configuration"></a>Configuração pessoal

Sabemos que preservar as preferências pessoais é essencial para fazer o desenvolvimento em um codespace hospedado na nuvem se sentir familiar e natural. O GitHub Codespaces camadas individualizadas personalizações sobre uma configuração de codespace. As preferências pessoais e a configuração para editores e terminais são suportadas pelo GitHub Codespaces.

Um codespace pode ser criado com uma coleção específica do usuário de [dotfiles personalizados](https://docs.github.com/github/developing-online-with-codespaces/personalizing-codespaces-for-your-account) (por exemplo,,, `.bashrc` `.gitconfig` etc.), e o GitHub Codespaces sincroniza automaticamente sua identidade, temas e configurações do git, de forma que cada codespace que você criar tenha a aparência desejada, independentemente dos recursos de ambiente específicos do projeto.

## <a name="see-also"></a>Confira também

* [Como usar o Visual Studio com um codespace](use-visual-studio-with-codespaces.md)
* [Como personalizar um codespace](customize-codespaces.md)
* [Recursos do Visual Studio com suporte](supported-features-codespaces.md)
