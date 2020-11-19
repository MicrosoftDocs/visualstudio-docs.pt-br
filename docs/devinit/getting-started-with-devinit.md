---
title: Introdução com devinit
description: Guia de introdução para devinit.
ms.date: 11/18/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jillfra
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: d071a49c9996c9f7f161faf676117704fbcbbdcd
ms.sourcegitcommit: 3b9a8aec34c7e835069f4db5c133dd002028180c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2020
ms.locfileid: "94937691"
---
# <a name="getting-started-with-devinit"></a>Introdução com devinit

o devinit é uma ferramenta que você pode usar para permitir que qualquer pessoa obtenha código e seja produtivo em seu repositório executando um comando simples. Você pode usar o devinit para definir todas as dependências de todo o sistema de que seu repositório precisa de algo como o SQL Server, Node.js, Docker ou IIS. O Devinit pode invocar outras ferramentas e gerenciadores de pacotes para instalar o que o repositório precisa. Você define essas dependências em um arquivo JSON chamado [.devinit.jsem](devinit-json.md) e, em seguida, a próxima pessoa a usar seu repositório precisa apenas executar [`devinit init`](devinit-commands.md#init) para instalar todas essas dependências. Então, em vez de gastar uma integração de meia dia em um novo repositório, isso pode ser feito em minutos.

devinit não é um Gerenciador de pacotes ou uma ferramenta de configuração de VM (máquina virtual) no próprio. É um executor de tarefas para um arquivo de manifesto, chamado [.devinit.jsem](devinit-json.md), que define as dependências de todo o sistema de que seu aplicativo precisa. Para instalar essas dependências, o devinit usa ferramentas que você já deve estar usando, como [Chocolatey](https://chocolatey.org). Você pode examinar as ferramentas disponíveis na [lista completa](devinit-tool-list.md). Ao usar essas ferramentas em vez de distribuir o software diretamente, o devinit oferece a você a conveniência de usar a ferramenta de sua escolha e permitir que você use configurações existentes, por exemplo, um arquivo de [packages.config](https://chocolatey.org/docs/commands-install#packagesconfig) para Chocolatey.  

## <a name="step-1-get-devinit"></a>Etapa 1: obter devinit

Atualmente, o devinit só está disponível como parte do GitHub Codespaces ao usar o Visual Studio e é acessível a partir do terminal integrado no Visual Studio. No futuro, o devinit estará disponível como parte do Visual Studio.

## <a name="step-2-define-your-environment"></a>Etapa 2: definir seu ambiente

A etapa mais importante é definir o ambiente de ' desenvolvimento ' em um [.devinit.jsno arquivo](devinit-json.md). Esse arquivo será usado pelo devinit para criar seu ambiente quando você executar o `devinit init` .

Para esta etapa, pense nas instruções que você daria para que alguém coloque em funcionamento com um repositório de projeto. Por exemplo, eles precisam ter o SQL instalado? Uma versão específica do .NET Core? E assim por diante. Em seguida, para cada uma dessas dependências, procure uma ferramenta devinit correspondente na [lista de ferramentas](devinit-tool-list.md) e adicione-a ao arquivo do repositório `.devinit.json` .

Você também pode ver uma seleção de exemplos na documentação de [exemplos](sample-readme.md)ou conferir o [tutorial](tutorial.md).

## <a name="step-3-enjoy"></a>Etapa 3: Aproveite!

Agora, tudo o que alguém precisa fazer depois de clonar seu repositório é executado `devinit init` .

```console
devinit init
```

Se você estiver usando o [GitHub Codespaces](https://github.com/features/codespaces), poderá configurar `devinit init` para ser executado automaticamente quando o codespace for provisionado. Para saber mais, confira a documentação do [devinit e do GitHub Codespaces](devinit-and-codespaces.md).
