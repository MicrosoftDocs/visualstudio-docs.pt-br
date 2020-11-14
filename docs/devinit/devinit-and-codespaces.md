---
title: devinit e Codespaces do GitHub
description: Saiba como personalizar um codespace para o Visual Studio usando o devinit.
ms.date: 08/28/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jillfra
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 929be4682465494738d859f9fe8144b5e26aaf4f
ms.sourcegitcommit: c1cc3d8e1673c52fbfddc86b089b4a3d46bb3e59
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2020
ms.locfileid: "94626164"
---
# <a name="devinit-and-github-codespaces"></a>devinit e Codespaces do GitHub

devinit é um ótimo complemento para o [GitHub Codespaces](https://github.com/features/codespaces) e o devinit pode ser usado para obter uma configuração de codespace para que os colaboradores possam criar, executar e depurar imediatamente.

> [!IMPORTANT]
> Antes de integrar o devinit com seu codespace, primeiro você precisa verificar se tem um `.devinit.json` arquivo que define suas dependências. Para obter mais informações sobre como criar um `.devinit.json` , leia a [documentação do guia de introdução](getting-started-with-devinit.md).

Dentro de um codespace do GitHub, seu aplicativo é compilado e executado na nuvem. Estar na nuvem significa que seu aplicativo não tem acesso aos recursos locais em seus computadores. Isso inclui ferramentas ou programas que você instalou localmente. Se seu aplicativo precisar de qualquer dependência em todo o sistema para ser instalado ou configurado, ele precisará ser feito em cada codespace. A maneira mais fácil de conseguir isso é usar um `.devinit.json` arquivo.

Para garantir que um codespace seja criado com as dependências de que seu aplicativo precisa, `devinit` precisa ser executado quando o codespace é criado. Isso pode ser feito chamando `devinit init` a partir do `postCreateCommand` definido em um `.devcontainer.json` arquivo colocado na raiz do repositório. As cadeias de caracteres em `postCreateCommand` são executadas no shell padrão, depois que o repositório é clonado no codespace. Você pode ler mais sobre `postCreateCommand` na [documentação de personalização](https://docs.github.com/github/developing-online-with-codespaces/configuring-codespaces-for-your-project)do GitHub Codespaces. Para adicionar o `devinit` comando, você pode adicionar `devinit init` ao `postCreateCommand` conforme mostrado nos exemplos abaixo.

Você também pode executar `devinit init -f <path to .devinit.json>` a partir do terminal integrado do Visual Studio uma vez conectado ao seu codespace.

## <a name="examples"></a>Exemplos

Nos dois exemplos abaixo, o `.devinit.json` está na raiz do repositório junto com `.devcontainer.json` .

### <a name="with-a-devcontainerjson-file"></a>Com um .devcontainer.jsno arquivo

Neste exemplo, o `.devcontainer.json` arquivo abaixo é colocado na raiz do repositório junto com o `.devinit.json` arquivo. Os arquivos também podem ser colocados em um `.devcontainer` diretório.

```json
{
  "postCreateCommand": "devinit init"
}
```

Quando o `.devinit.json` estiver em outro diretório, o sinalizador-f poderá ser usado.

```json
{
  "postCreateCommand": "devinit init -f path\\to\\.devinit.json"
}

```

```json
{
  "postCreateCommand": ["<some other command>", "devinit init"]
}
```

Você pode encontrar mais exemplos de como usar o devinit em nossa [documentação](sample-all-tool.md) e no GitHub no [exemplo do .net Core](https://github.com/microsoft/devinit-example-dotnet-core) eNode.js repositórios de [ exemplo](https://github.com/microsoft/devinit-example-nodejs) .

### <a name="as-commands"></a>Comandos do as

Neste exemplo, o `.devcontainer.json` arquivo abaixo é colocado na raiz do repositório e `devinit run` está sendo chamado diretamente da linha de comando para executar uma ferramenta individual.  

```json
{
  "postCreateCommand": ["devinit run –t require-dotnetcoresdk"]
}
```

### <a name="from-a-terminal-prompt"></a>De um prompt de terminal

Quando o diretório de trabalho atual contém um `.devinit.json` arquivo.

```console
devinit init
```

Quando o `.devinit.json` está em outro diretório.

```console
devinit init -f path/to/.devinit.json
```
