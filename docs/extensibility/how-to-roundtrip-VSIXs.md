---
title: Como extensões de ida e volta
ms.date: 06/25/2017
ms.topic: how-to
ms.assetid: 2d6cf53c-011e-4c9e-9935-417edca8c486
author: willbrown
ms.author: madsk
manager: justinclareburt
ms.workload:
- willbrown
ms.openlocfilehash: ff2865080b7d36f1a7c3b8a7680d867b92ec9c08
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905781"
---
# <a name="how-to-make-extensions-compatible-with-visual-studio-20192017-and-visual-studio-2015"></a>Como: tornar as extensões compatíveis com o Visual Studio 2019/2017 e o Visual Studio 2015

Este documento explica como fazer a viagem de ida e volta dos projetos de extensibilidade entre o Visual Studio 2015 e o Visual Studio 2019 ou o Visual Studio 2017. Depois de concluir essa atualização, um projeto poderá abrir, compilar, instalar e executar o Visual Studio 2015 e o Visual Studio 2019 ou 2017. Como referência, algumas extensões que podem ser viajadas entre o Visual Studio 2015 e o Visual Studio 2019 ou 2017 podem ser encontradas nos [exemplos de extensibilidade do vs SDK](https://github.com/Microsoft/VSSDK-Extensibility-Samples).

Se você pretende apenas criar no Visual Studio 2019/2017, mas quer que o VSIX de saída seja executado no Visual Studio 2015 e no Visual Studio 2019/2017, consulte o [documento de migração de extensão](how-to-migrate-extensibility-projects-to-visual-studio-2017.md).

> [!NOTE]
> Devido a alterações no Visual Studio entre versões, algumas coisas que trabalharam em uma versão não funcionam em outra. Verifique se os recursos que você está tentando acessar estão disponíveis em ambas as versões ou se a extensão terá resultados inesperados.

Aqui está uma descrição das etapas que você concluirá neste documento para fazer uma viagem de ida e volta de um VSIX:

1. Importe pacotes NuGet corretos.
2. Atualizar manifesto de extensão:
    * Destino da instalação
    * Pré-requisitos
3. Atualizar CSProj:
    * Atualizar `<MinimumVisualStudioVersion>`.
    * Adicionar a propriedade `<VsixType>`.
    * Adicione a propriedade de depuração `($DevEnvDir)` 3 vezes.
    * Adicione condições para importar ferramentas de Build e destinos.

4. Compilar e testar

## <a name="environment-setup"></a>Configuração do ambiente

Este documento pressupõe que você tenha o seguinte instalado em seu computador:

* Visual Studio 2015 com o SDK do VS instalado
* Visual Studio 2019 ou 2017 com a carga de trabalho de extensibilidade instalada

## <a name="recommended-approach"></a>Abordagem recomendada

É altamente recomendável iniciar essa atualização com o Visual Studio 2015, em vez do Visual Studio 2019 ou 2017. O principal benefício do desenvolvimento no Visual Studio 2015 é garantir que você não referencie assemblies que não estão disponíveis no Visual Studio 2015. Se você fizer o desenvolvimento no Visual Studio 2019 ou 2017, haverá um risco de que você possa introduzir uma dependência em um assembly que existe apenas no Visual Studio 2019 ou 2017.

## <a name="ensure-there-is-no-reference-to-projectjson"></a>Verifique se não há nenhuma referência a project.js

Posteriormente neste documento, inseriremos instruções de importação condicionais no seu arquivo **. csproj* . Isso não funcionará se as referências do NuGet estiverem armazenadas no *project.jsno*. Como tal, é aconselhável mover todas as referências do NuGet para o arquivo de *packages.config* .
Se o seu projeto contiver um *project.jsno* arquivo:

* Anote as referências no *project.jsem*.
* No **Gerenciador de soluções**, exclua o *project.jsno* arquivo do projeto. Isso exclui o *project.jsno* arquivo e o Remove do projeto.
* Adicione as referências do NuGet de volta ao projeto:
  * Clique com o botão direito do mouse na **solução** e escolha **gerenciar pacotes NuGet para solução**.
  * O Visual Studio cria automaticamente o arquivo de *packages.config* para você.

> [!NOTE]
> Se o projeto contiver pacotes EnvDTE, talvez seja necessário adicioná-los clicando com o botão direito do mouse em **referências** selecionando **Adicionar referência** e adicionando a referência apropriada. O uso de pacotes NuGet pode criar erros ao tentar compilar seu projeto.

## <a name="add-appropriate-build-tools"></a>Adicionar ferramentas de compilação apropriadas

Precisamos ter certeza de adicionar ferramentas de Build que nos permitirão criar e depurar adequadamente. A Microsoft criou um assembly para isso chamado Microsoft. VisualStudio. Sdk. BuildTasks.

Para criar e implantar um VSIXv3 no Visual Studio 2015 e 2019/2017, você precisará dos seguintes pacotes NuGet:

Versão | Ferramentas criadas
--- | ---
Visual Studio 2015 | Microsoft. VisualStudio. Sdk. BuildTasks. 14.0
Visual Studio 2019 ou 2017 | Microsoft. VSSDK. BuildTool

Para fazer isso:

* Adicione o pacote NuGet Microsoft. VisualStudio. Sdk. BuildTasks. 14.0 ao seu projeto.
* Se o seu projeto não contiver Microsoft. VSSDK. BuildTools, adicione-o.
* Verifique se a versão Microsoft. VSSDK. BuildTools é 15. x ou superior.

## <a name="update-extension-manifest"></a>Atualizar manifesto de extensão

### <a name="1-installation-targets"></a>1. destinos de instalação

Precisamos dizer ao Visual Studio quais versões devem ser direcionadas para a criação de um VSIX. Normalmente, essas referências são para a versão 14,0 (Visual Studio 2015), a versão 15,0 (Visual Studio 2017) ou a versão 16,0 (Visual Studio 2019). Em nosso caso, desejamos criar um VSIX que instalará uma extensão para ambos, portanto, precisamos direcionar ambas as versões. Se você quiser que seu VSIX crie e instale em versões anteriores a 14,0, isso pode ser feito definindo o número de versão anterior; no entanto, a versão 10,0 e anteriores não são mais suportadas.

* Abra o arquivo *Source. Extension. vsixmanifest* no Visual Studio.
* Abra a guia **instalar destinos** .
* Altere o **intervalo de versão** para [14,0, 17,0). O ' [' diz ao Visual Studio para incluir 14,0 e todas as versões que o ultrapassaram. O ') ' informa ao Visual Studio para incluir todas as versões até, mas não incluindo, a versão 17,0.
* Salve todas as alterações e feche todas as instâncias do Visual Studio.

![Imagem de destinos de instalação](media/visual-studio-installation-targets-example.png)

### <a name="2-adding-prerequisites-to-the-extensionvsixmanifest-file"></a>2. adicionando pré-requisitos ao arquivo de *extensão. vsixmanifest*

Precisamos do editor principal do Visual Studio como um pré-requisito. Abra o Visual Studio e use o designer de manifesto atualizado para inserir os pré-requisitos.

Para fazer isso manualmente:

* Navegue até o diretório do projeto no explorador de arquivos.
* Abra o arquivo *extension. vsixmanifest* com um editor de texto.
* Adicione a seguinte marca:

```xml
<Prerequisites>
    <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" DisplayName="Visual Studio core editor" />
</Prerequisites>
```

* Salve e feche o arquivo.

> [!NOTE]
> Talvez seja necessário editar manualmente a versão de pré-requisito para garantir que ela seja compatível com todas as versões do Visual Studio 2019 ou 2017. Isso ocorre porque o designer irá inserir a versão mínima como sua versão atual do Visual Studio (por exemplo, 15.0.26208.0). No entanto, como outros usuários podem ter uma versão anterior, convém editá-lo manualmente para 15,0.

Neste ponto, o arquivo de manifesto deve ser semelhante a este:

![Exemplo de pré-requisitos](media/visual-studio-prerequisites-example.png)

## <a name="modify-the-project-file-myprojectcsproj"></a>Modificar o arquivo de projeto (MyProject. csproj)

É altamente recomendável ter uma referência a um. csproj aberto ao fazer esta etapa. Você pode encontrar vários exemplos [aqui](https://github.com/Microsoft/VSSDK-Extensibility-Samples). Selecione qualquer exemplo de extensibilidade, localize o arquivo *. csproj* para referência e execute as seguintes etapas:

* Navegue até o diretório do projeto no **Explorador de arquivos**.
* Abra o arquivo *MyProject. csproj* com um editor de texto.

### <a name="1-update-the-minimumvisualstudioversion"></a>1. atualizar o MinimumVisualStudioVersion

* Defina a versão mínima do Visual Studio como `$(VisualStudioVersion)` e adicione uma instrução condicional para ela. Adicione essas marcas se elas não existirem. Verifique se as marcas estão definidas como abaixo:

```xml
<VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">14.0</VisualStudioVersion>
<MinimumVisualStudioVersion>$(VisualStudioVersion)</MinimumVisualStudioVersion>
```

### <a name="2-add-the-vsixtype-property"></a>2. Adicione a propriedade Vsixtype.

* Adicione a seguinte marcação `<VsixType>v3</VsixType>` a um grupo de propriedades.

> [!NOTE]
> É recomendável adicionar isso abaixo da `<OutputType></OutputType>` marca.

### <a name="3-add-the-debugging-properties"></a>3. adicionar as propriedades de depuração

* Adicione o seguinte grupo de propriedades:

```xml
<PropertyGroup>
    <StartAction>Program</StartAction>
    <StartProgram>$(DevEnvDir)devenv.exe</StartProgram>
    <StartArguments>/rootsuffix Exp</StartArguments>
</PropertyGroup>
```

* Exclua todas as instâncias do exemplo de código a seguir do arquivo *. csproj* e de quaisquer arquivos *. csproj. User* :

```xml
<StartAction>Program</StartAction>
<StartProgram>$(ProgramFiles)\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe</StartProgram>
<StartArguments>/rootsuffix Exp</StartArguments>
```

### <a name="4-add-conditions-to-the-build-tools-imports"></a>4. Adicionar condições às importações de ferramentas de Build

* Adicione instruções condicionais adicionais às `<import>` marcas que têm uma referência Microsoft. VSSDK. BuildTools. Insira `'$(VisualStudioVersion)' != '14.0' And` na frente da instrução Condition. Essas instruções aparecerão no cabeçalho e no rodapé do arquivo csproj.

Por exemplo:

```xml
<Import Project="packages\Microsoft.VSSDK.BuildTools.15.0.26201…" Condition="'$(VisualStudioVersion)' != '14.0' And Exists(…" />
```

* Adicione instruções condicionais adicionais às `<import>` marcas que têm um Microsoft. VisualStudio. Sdk. BuildTasks. 14.0. Insira `'$(VisualStudioVersion)' == '14.0' And` na frente da instrução Condition. Essas instruções aparecerão no cabeçalho e no rodapé do arquivo csproj.

Por exemplo:

```xml
<Import Project="packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" Condition="'$(VisualStudioVersion)' == '14.0' And Exists(…" />
```

* Adicione instruções condicionais adicionais às `<Error>` marcas que têm uma referência Microsoft. VSSDK. BuildTools. Faça isso inserindo `'$(VisualStudioVersion)' != '14.0' And` na frente da instrução Condition. Essas instruções aparecerão no rodapé do arquivo csproj.

Por exemplo:

```xml
<Error Condition="'$(VisualStudioVersion)' != '14.0' And Exists('packages\Microsoft.VSSDK.BuildTools.15.0.26201…" />
```

* Adicione instruções condicionais adicionais às `<Error>` marcas que têm um Microsoft. VisualStudio. Sdk. BuildTasks. 14.0. Insira `'$(VisualStudioVersion)' == '14.0' And` na frente da instrução Condition. Essas instruções aparecerão no rodapé do arquivo csproj.

Por exemplo:

```xml
<Error Condition="'$(VisualStudioVersion)' == '14.0' And Exists('packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" />
```

* Salve o arquivo csproj e feche-o. 
  * Observe que, se você estiver usando mais de um projeto na solução, defina este projeto como projeto de inicialização usando "definir como projeto de inicialização" no menu de contexto do projeto). Isso garante que o Visual Studio reabra esse projeto depois de descarregá-lo.

## <a name="test-the-extension-installs-in-visual-studio-2015-and-visual-studio-2019-or-2017"></a>Testar as instalações de extensão no Visual Studio 2015 e no Visual Studio 2019 ou 2017

Neste ponto, seu projeto deve estar pronto para criar um VSIXv3 que possa ser instalado no Visual Studio 2015 e no Visual Studio 2017.

* Abra seu projeto no Visual Studio 2015.
* Compile seu projeto e confirme na saída que um VSIX cria corretamente.
* Navegue até o diretório do projeto.
* Abra a pasta *\bin\Debug* .
* Clique duas vezes no arquivo VSIX e instale sua extensão no Visual Studio 2015 e no Visual Studio 2019/2017.
* Verifique se você pode ver a extensão em **ferramentas**  >  **extensões e atualizações** na seção **instalada** .
* Tente executar/usar a extensão para verificar se ela funciona.

![Localizar um VSIX](media/finding-a-VSIX-example.png)

> [!NOTE]
> Se o seu projeto for suspenso com a mensagem que **abre o arquivo**, Force o desligamento do Visual Studio, navegue até o diretório do projeto, mostre pastas ocultas e exclua a pasta *. vs* .
 
