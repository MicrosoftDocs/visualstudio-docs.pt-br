---
title: Tutorial
description: Tutorial para devinit.
ms.date: 11/18/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 5fc53a534b592b4f6a4799100ce16b1d45049457
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104671794"
---
# <a name="tutorial"></a>Tutorial

> [!IMPORTANT]
> A partir de 12 de abril de 2021, a conexão ao GitHub Codespaces do Visual Studio 2019 não será mais suportada e essa versão prévia privada terá sido concluída. Estamos concentrados em experiências em evolução para um loop interno baseado em nuvem e soluções de VDI otimizadas para um amplo conjunto de cargas de trabalho do Visual Studio. Incentivamos você a estar envolvido em nosso fórum da comunidade de desenvolvedores para Visual Studio para obter informações sobre versões futuras e informações de roteiro.

Neste tutorial, vamos explorar a configuração do [repositório eShopOnWeb](https://github.com/andysterland/eShopOnWeb) com Devinit e Codespaces. Este tutorial pressupõe que o devinit já está disponível, conforme descrito na [página de introdução](getting-started-with-devinit.md).

## <a name="step-1-determining-setup-steps"></a>Etapa 1: determinando as etapas de instalação

Conforme mencionado na [página de introdução](getting-started-with-devinit.md), a primeira etapa é sempre determinar quais dependências e etapas de configuração seu projeto tem. Isso irá variar com base no projeto específico, mas há algumas perguntas a serem consideradas:

- Em quais tempos de execução ou SDKs seu projeto depende?
- Seu projeto requer pacotes (por exemplo, de Chocolatey)?
- O processo de instalação requer que todas as ações sejam executadas (por exemplo, executando um script)?
- Seu projeto tem dependências implícitas em qualquer coisa instalada junto com o Visual Studio?
  - Nesse caso, é uma boa ideia incluí-los na configuração do devinit também. Dessa forma, você pode evitar o acoplamento à instalação do Visual Studio.

Uma das melhores maneiras de determinar essas informações é explorar as etapas de configuração manual que você tem atualmente para o repositório. Para eShopOnWeb, há algumas coisas que precisamos manipular:

- Instalando a versão mais recente do SDK do .NET Core
- Instalando a versão mais recente da CLI do .NET Entity Framework Core Tools
- Instalando o SQL Server 2019 Express
- Usando a CLI do .NET Entity Framework para atualizar o banco de dados local para a migração mais recente

Em seguida, exploraremos como fazer tudo isso no contexto de devinit.

## <a name="step-2-the-devinitjson"></a>Etapa 2: a .devinit.jsem

Primeiro, desejamos construir um [.devinit.jsno arquivo](devinit-json.md) e colocá-lo na raiz do nosso repositório. Esse arquivo incluirá uma série de etapas que serão executadas posteriormente como parte de um `devinit init` comando. Para determinar o que deve ser incluído no `.devinit.json` arquivo, podemos pegar nossa lista de etapas de configuração e comparar com a lista de [ferramentas de devinit](devinit-tool-list.md). Vamos fazer isso agora com as etapas de configuração acima.

| Etapa                                                              | Devinit pode lidar com isso para nós?                                                                        |
| :---------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------  |
| Instalar o SDK do .NET Core mais recente                                      | **Sim**! Podemos usar a [ `require-dotnetcoresdk` ferramenta](tool-require-dotnetcoresdk.md)                  |
| Instalar a CLI das ferramentas do .NET Entity Framework Core                      | **Sim**! Podemos usar a [ `dotnet-toolinstall` ferramenta](tool-dotnet-toolinstall.md)                        |
| Instalar o SQL Server 2019 Express                                   | **Sim**! Podemos usar a [ `choco-install` ferramenta](tool-choco-install.md)                                  |
| Atualizar o banco de dados local usando o .NET Entity Framework                 | **Não**, mas ainda fazemos isso combinando devinit com um script!                               |

Agora que imaginamos isso, vamos começar com um básico `.devinit.json` . Incluiremos uma referência ao [ `.devinit.json` esquema](https://json.schemastore.org/devinit.schema-2.0)e uma `run` seção vazia:

```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-2.0",
  "run": []
}
```

Agora, vamos adicionar algumas ferramentas!

Primeiro, vamos adicionar [`require-dotnetcoresdk`](tool-require-dotnetcoresdk.md) . Na documentação dessa ferramenta, podemos ver que o comportamento padrão é instalar a versão mais recente do SDK. Isso é exatamente o que queremos, então vamos adicioná-lo ao nosso `.devinit.json` :

```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-2.0",
  "run": [
    {
      "comments": "Install the latest version of the .NET Core SDK.",
      "tool": "require-dotnetcoresdk"
    }
  ]
}
```

Em segundo lugar, vamos adicionar [`dotnet-toolinstall`](tool-dotnet-toolinstall.md) para instalar a `dotnet-ef` ferramenta globalmente. Na documentação, vemos que podemos usar o `input` campo para especificar o nome da ferramenta e o `additionalOptions` campo para especificar o escopo global:

```json
{
  "run": [
    {
      "comments": "Install the latest version of the .NET Core SDK.",
      "tool": "require-dotnetcoresdk"
    },
    {
      "comments": "Install latest version of the .NET Entity Framework Core Tools CLI.",
      "tool": "dotnet-toolinstall",
      "input": "dotnet-ef",
      "additionalOptions": "--global"
    }
  ]
}
```

Por fim, adicionaremos [`choco-install`](tool-choco-install.md) para instalar o `sql-server-express` pacote.

```json
{
  "run": [
    {
      "comments": "Install the latest version of the .NET Core SDK.",
      "tool": "require-dotnetcoresdk"
    },
    {
      "comments": "Install latest version of the .NET Entity Framework Core Tools CLI.",
      "tool": "dotnet-toolinstall",
      "input": "dotnet-ef",
      "additionalOptions": "--global"
    },
    {
      "comments": "Install SQL Server 2019 Express",
      "tool": "choco-install",
      "input": "sql-server-express"
    }
  ]
}
```

Agora que o nosso `.devinit.json` está concluído, podemos trabalhar em um script de instalação que cuidará da execução do devinit e da atualização do banco de dados local.

## <a name="step-3-the-setup-script"></a>Etapa 3: o script de instalação

Para lidar com a execução de devinit e a atualização do banco de dados local, criaremos um script que executa os comandos necessários. Vamos criar um script do PowerShell vazio em nossa raiz do repositório, chamado `PostCloneSetup.ps1` . Primeiro, adicionaremos uma chamada para `devinit init` :

```powershell
devinit init
```

Quando executado, `devinit init` o executará todas as ferramentas definidas na `run` seção de nosso `.devinit.json` .

Por fim, queremos invocar `dotnet ef database update` para atualizar o banco de dados local:

```powershell
devinit init
dotnet ef database update -c catalogcontext -p src\Infrastructure\Infrastructure.csproj -s src\Web\Web.csproj
dotnet ef database update -c appidentitydbcontext -p src\Infrastructure\Infrastructure.csproj -s src\Web\Web.csproj
```

Agora que o nosso script de instalação foi concluído, precisamos adicionar um `.devcontainer.json` arquivo que o executará durante a instalação do codespace.

## <a name="step-4-the-devcontainerjson"></a>Etapa 4: a .devcontainer.jsem

Para garantir que nosso script de instalação seja executado durante a criação de nosso codespace, usaremos um `.devcontainer.json` arquivo. Da mesma forma que os outros arquivos, isso deve ser colocado na raiz do repositório.

No `.devcontainer.json` arquivo, precisamos apenas chamar nosso script de instalação como parte do `postCreateCommand` . Isso será executado como parte do processo de criação de codespace:

```json
{
  "postCreateCommand": "Powershell.exe -ExecutionPolicy unrestricted -File .\\PostCloneSetup.ps1"
}
```

Pronto!

## <a name="step-5-trying-it-out"></a>Etapa 5: experimentando

Agora que nossas etapas de configuração estão em vigor, vamos testar isso em um codespace ao vivo usando o [repositório real](https://github.com/andysterland/eShopOnWeb).

Primeiro, vamos criar um codespace usando o Visual Studio:

:::image type="content" source="media/eshoponweb-github-codespaces-prompt.png" alt-text="Criando um codespace":::

Depois que a criação de codespace for iniciada, podemos observar o progresso do nosso processo de instalação no `C:\.vsonline\.vsoshared\vmTerminal.dat` :

:::image type="content" source="media/eshoponweb-watching-progress.png" alt-text="Observando o progresso da instalação":::

Após a conclusão, vamos executar o aplicativo por meio do `Web.csproj` para verificar se tudo está funcionando corretamente:

:::image type="content" source="media/eshoponweb-csproj.png" alt-text="Executando o projeto":::

Depois que o aplicativo é criado e iniciado, podemos ver a loja em nosso navegador da Web:

:::image type="content" source="media/eshoponweb-live.png" alt-text="Exibindo o site":::

Portanto, nosso processo de instalação funcionou corretamente e agora estamos prontos para desenvolver no projeto eShopOnWeb!
