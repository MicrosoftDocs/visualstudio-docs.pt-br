---
title: Como as extensões de ida e volta
ms.date: 06/25/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 2d6cf53c-011e-4c9e-9935-417edca8c486
author: willbrown
ms.author: gregvanl
manager: justinclareburt
ms.workload:
- willbrown
ms.openlocfilehash: 826089f1018bc6156cd49bab3afb19e7bb34a47d
ms.sourcegitcommit: 1df0ae74af03bcf0244129a29fd6bd605efc9f61
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50750726"
---
# <a name="how-to-make-extensions-compatible-with-visual-studio-2017-and-visual-studio-2015"></a>Como: fazer com que as extensões compatíveis com o Visual Studio 2017 e Visual Studio 2015

Este documento explica como criar projetos de extensibilidade ida e volta entre o Visual Studio 2015 e Visual Studio 2017. Depois de concluir esta atualização, um projeto será capaz de abrir, criar, instalar e executar no Visual Studio 2015 e Visual Studio 2017. Como referência, algumas extensões que podem ida e volta entre o Visual Studio 2015 e Visual Studio 2017 podem ser encontradas na [exemplos de extensibilidade do SDK do VS](https://github.com/Microsoft/VSSDK-Extensibility-Samples).

Se você pretende criar no Visual Studio 2017, mas deseja que a saída VSIX para ser executado no Visual Studio 2015 e Visual Studio 2017, em seguida, consulte a [documento de migração de extensão](how-to-migrate-extensibility-projects-to-visual-studio-2017.md).

> [!NOTE]
> Devido a alterações no Visual Studio entre versões, algumas coisas que funcionavam em uma versão não funcionam em outro. Certifique-se de que os recursos que você está tentando acessar estão disponíveis em ambas as versões ou a extensão terá resultados inesperados.

Aqui está uma descrição das etapas que você concluirá neste documento para um VSIX de ida e volta:

1. Importe pacotes do NuGet corretos.
2. Atualize o manifesto de extensão:
    * Destino da instalação
    * Pré-requisitos
3. Atualize CSProj:
    * Atualização `<MinimumVisualStudioVersion>`.
    * Adicionar o `<VsixType>` propriedade.
    * Adicione a propriedade de depuração `($DevEnvDir)` 3 vezes.
    * Adicione condições de importação de ferramentas de build e destinos.

4. Compilar e testar

## <a name="environment-setup"></a>Configuração do ambiente

Este documento presume que você tenha os seguintes itens instalados em seu computador:

* Visual Studio 2015 com o SDK do VS instalado
* Visual Studio 2017 com a carga de trabalho de extensibilidade instalada

## <a name="recommended-approach"></a>Abordagem recomendada

É altamente recomendável iniciar essa atualização com o Visual Studio 2015, em vez do Visual Studio 2017. O principal benefício de desenvolvimento no Visual Studio 2015 é garantir que você não fizer referência a assemblies que não estão disponíveis no Visual Studio 2015. Se você fizer o desenvolvimento no Visual Studio 2017, há um risco de que você pode introduzir uma dependência em um assembly que existe somente no Visual Studio 2017.

## <a name="ensure-there-is-no-reference-to-projectjson"></a>Verifique se que não há nenhuma referência ao Project. JSON

Neste documento, podemos irá inserir instruções de importação condicional para seu **. csproj* arquivo.  Isso não funcionará se as referências de NuGet são armazenadas em *Project. JSON*. Como tal, é aconselhável para mover todas as referências de NuGet para o *Packages. config* arquivo.
Se o projeto contiver uma *Project. JSON* arquivo:

* Anote as referências no *Project. JSON*.
* Dos **Gerenciador de soluções**, exclua o *Project. JSON* arquivo do projeto. Isso exclui as *Project. JSON* de arquivo e o remove do projeto.
* Adicione que as referências de NuGet novamente para o projeto:
    * Clique com botão direito no **Solution** e escolha **gerenciar pacotes NuGet para solução**.
    * Visual Studio cria automaticamente o *Packages. config* arquivo para você.

> [!NOTE]
> Se seu projeto continha pacotes EnvDTE, eles talvez precise ser adicionados com o botão direito clicando em **referências** selecionando **adicionar referência** e adicionar a referência apropriada.  Usar pacotes do NuGet pode criar erros ao tentar compilar seu projeto.

## <a name="add-appropriate-build-tools"></a>Adicionar ferramentas de compilação apropriado

Ter certeza de que precisamos adicionar ferramentas de compilação que nos permitirá criar e depurar adequadamente. A Microsoft criou um assembly para esta chamada Microsoft.VisualStudio.Sdk.BuildTasks.

Para criar e implantar um VSIXv3 no Visual Studio 2015 e 2017, você precisará dos seguintes pacotes NuGet:

Versão | Ferramentas internas
--- | ---
Visual Studio 2015 | Microsoft.VisualStudio.Sdk.BuildTasks.14.0
Visual Studio 2017 | Microsoft.VSSDK.BuildTool

Para fazer isso:

* Adicione o pacote do NuGet Microsoft.VisualStudio.Sdk.BuildTasks.14.0 ao seu projeto.
* Se seu projeto não contiver Microsoft.VSSDK.BuildTools, adicioná-lo.
* Verifique se a versão de Microsoft.VSSDK.BuildTools é 15.x ou maior.

## <a name="update-extension-manifest"></a>Atualizar o manifesto de extensão

### <a name="1-installation-targets"></a>1. Destinos de instalação

Precisamos dizer ao Visual Studio quais versões de destino para a criação de um VSIX.  Normalmente, essas referências são a versão 14.0 (Visual Studio 2015) ou versão 15.0 (Visual Studio 2017).  Em nosso caso, queremos criar um VSIX que instalará uma extensão para ambos, portanto, precisamos ambas as versões de destino.  Se você quiser que seu VSIX para compilar e instalar em versões anteriores ao 14.0, isso pode ser feito definindo o número de versão anterior; No entanto, não há suporte para a versão 10.0 e versões anteriores.

* Abra o *vsixmanifest* arquivo no Visual Studio.
* Abra o **instalar destinos** guia.
* Alterar o **intervalo de versão** para [14.0, 16.0).  O ' [' informa ao Visual Studio para incluir 14.0 e todas as versões anteriores ele.  O ')' informa ao Visual Studio para incluir todas as versões do 15.0 até, mas não incluindo a versão 16.0.
* Salve todas as alterações e feche todas as instâncias do Visual Studio.

![Imagem de destinos de instalação](media/visual-studio-installation-targets-example.png)

### <a name="2-adding-prerequisites-to-the-extensionvsixmanifest-file"></a>2. Adicionando pré-requisitos para o *vsixmanifest* arquivo

Pré-requisitos são um novo recurso com o Visual Studio 2017.  Nesse caso, é necessário o Editor principal do Visual Studio como um pré-requisito. Uma vez que o designer do Visual Studio 2015 VSIX não lida com a nova `Prerequisites` seção, você precisará editar esta parte manualmente no código XML.  Como alternativa, você pode abrir o Visual Studio 2017 e usar o designer de manifesto atualizado para inserir os pré-requisitos.

Para fazer isso manualmente:

* Navegue até o diretório do projeto no Explorador de arquivos.
* Abra o *vsixmanifest* arquivo com um editor de texto.
* Adicione a seguinte marcação:

```xml
<Prerequisites>
    <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" DisplayName="Visual Studio core editor" />
</Prerequisites>
```

* Salve e feche o arquivo.

> [!NOTE]
> Se você optar por fazer isso com o designer VSIX no Visual Studio 2017, será preciso editar manualmente a versão do pré-requisito para garantir que ele é compatível com todas as versões do Visual Studio 2017.  Isso ocorre porque o designer irá inserir a versão mínima como sua versão atual do Visual Studio (por exemplo, 15.0.26208.0).  No entanto, desde que outros usuários podem ter uma versão anterior, você desejará editá-la manualmente para 15.0.

Neste ponto, seu arquivo de manifesto deve ser algo parecido com isto:

![Exemplo de pré-requisitos](media/visual-studio-prerequisites-example.png)

## <a name="modify-the-project-file-myprojectcsproj"></a>Modifique o arquivo de projeto (myproject.csproj)

É altamente recomendável ter uma referência a um modificado. csproj aberto enquanto realizar esta etapa.  Você pode encontrar vários exemplos [aqui](https://github.com/Microsoft/VSSDK-Extensibility-Samples).  Selecione uma amostra de extensibilidade, localize o *. csproj* para referência de arquivo e execute as seguintes etapas:

* Navegue até o diretório do projeto no **Explorador de arquivos**.
* Abra o *myproject.csproj* arquivo com um editor de texto.

### <a name="1-update-the-minimumvisualstudioversion"></a>1. Atualizar o MinimumVisualStudioVersion

* Defina a versão mínima do studio visual como `$(VisualStudioVersion)` e adicione uma instrução condicional para ele.  Adicione essas marcas se elas não existirem.  Certifique-se de que as marcas são definidas como mostrado abaixo:

```xml
<VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">14.0</VisualStudioVersion>
<MinimumVisualStudioVersion>$(VisualStudioVersion)</MinimumVisualStudioVersion>
```

### <a name="2-add-the-vsixtype-property"></a>2. Adicione a propriedade VsixType.

* Adicione a seguinte marca `<VsixType>v3</VsixType>` para um grupo de propriedades.

> [!NOTE]
> É recomendável adicionar isso abaixo o `<OutputType></OutputType>` marca.

### <a name="3-add-the-debugging-properties"></a>3. Adicionar propriedades de depuração

* Adicione o grupo de propriedades a seguir:

```xml
<PropertyGroup>
    <StartAction>Program</StartAction>
    <StartPrograms>$(DevEnvDir)devenv.exe</StartPrograms>
    <StartArguments>/rootsuffix Exp</StartArguments>
</PropertyGroup>
```

* Excluir todas as instâncias do exemplo de código a seguir do *. csproj* arquivo e qualquer *. csproj* arquivos:

```xml
<StartAction>Program</StartAction>
<StartPrograms>$(ProgramFiles)\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe</StartPrograms>
<StartArguments>/rootsuffix Exp</StartArguments>
```

### <a name="4-add-conditions-to-the-build-tools-imports"></a>4. Adicionar condições para as importações de ferramentas de compilação

* Adicionar instruções condicionais adicionais para o `<import>` marcas que têm uma referência Microsoft.VSSDK.BuildTools.  Inserir `'$(VisualStudioVersion)' != '14.0' And` na frente da instrução de condição.  Essas instruções serão exibido no cabeçalho e rodapé do arquivo csproj.

Por exemplo:

```xml
<Import Project="packages\Microsoft.VSSDK.BuildTools.15.0.26201…" Condition="'$(VisualStudioVersion)' != '14.0' And Exists(…" />
```

* Adicionar instruções condicionais adicionais para o `<import>` marcas que têm um Microsoft.VisualStudio.Sdk.BuildTasks.14.0. Inserir `'$(VisualStudioVersion)' == '14.0' And` na frente da instrução de condição. Essas instruções serão exibido no cabeçalho e rodapé do arquivo csproj.

Por exemplo:

```xml
<Import Project="packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" Condition="'$(VisualStudioVersion)' == '14.0' And Exists(…" />
```

* Adicionar instruções condicionais adicionais para o `<Error>` marcas que têm uma referência Microsoft.VSSDK.BuildTools.  Fazer isso inserindo `'$(VisualStudioVersion)' != '14.0' And` na frente da instrução de condição. Essas instruções serão exibido no rodapé do arquivo csproj.

Por exemplo:

```xml
<Error Condition="'$(VisualStudioVersion)' != '14.0' And Exists('packages\Microsoft.VSSDK.BuildTools.15.0.26201…" />
```

* Adicionar instruções condicionais adicionais para o `<Error>` marcas que têm um Microsoft.VisualStudio.Sdk.BuildTasks.14.0.  Inserir `'$(VisualStudioVersion)' == '14.0' And` na frente da instrução de condição. Essas instruções serão exibido no rodapé do arquivo csproj.

Por exemplo:

```xml
<Error Condition="'$(VisualStudioVersion)' == '14.0' And Exists('packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" />
```

* Salve o arquivo csproj e fechá-lo.

## <a name="test-the-extension-installs-in-visual-studio-2015-and-visual-studio-2017"></a>Instala a extensão de teste no Visual Studio 2015 e Visual Studio 2017

Neste ponto, seu projeto deve estar pronto para compilar um VSIXv3 que podem ser instaladas no Visual Studio 2015 e Visual Studio 2017.

* Abra seu projeto no Visual Studio 2015.
* Compile o projeto e confirme na saída de um VSIX criado corretamente.
* Navegue até o diretório do projeto.
* Abra o *\bin\Debug* pasta.
* Clique duas vezes no arquivo VSIX e instalar sua extensão no Visual Studio 2015 e Visual Studio 2017.
* Certifique-se de que você pode ver a extensão em **ferramentas** > **extensões e atualizações** no **instalado** seção.
* Tentativa de execução/usar a extensão para verificar se ele funciona.

![Localizar um VSIX](media/finding-a-VSIX-example.png)

> [!NOTE]
> Se seu projeto para de responder com a mensagem **abrindo o arquivo**, forçar o desligamento Visual Studio, navegue até o diretório do projeto, Mostrar pastas ocultas e excluir os *. VS* pasta.