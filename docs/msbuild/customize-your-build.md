---
title: Personalizar seu build | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, transforms
- transforms [MSBuild]
ms.assetid: d0bceb3b-14fb-455c-805a-63acefa4b3ed
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 31856366712da0a2287f73906c6e3a5f81f63a00
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49857582"
---
# <a name="customize-your-build"></a>Personalizar seu build

Os projetos do MSBuild que usam o processo de build padrão (importando *Microsoft.Common.props* e *Microsoft.Common.targets*) têm vários ganchos de extensibilidade que você pode usar para personalizar o processo de build.

## <a name="add-arguments-to-command-line-msbuild-invocations-for-your-project"></a>Adicionar argumentos para invocações de linha de comando do MSBuild para o seu projeto

Um arquivo *Directory.Build.rsp* no diretório de origem ou acima dele será aplicado aos builds de linha de comando do projeto. Para obter detalhes, confira [Arquivos de resposta do MSBuild](../msbuild/msbuild-response-files.md#directorybuildrsp).

## <a name="directorybuildprops-and-directorybuildtargets"></a>Directory.Build.props e Directory.Build.targets

Antes do MSBuild versão 15, se você quisesse fornecer uma propriedade nova e personalizada para os projetos da solução, precisaria adicionar manualmente uma referência a essa propriedade para cada arquivo de projeto na solução. Ou você precisava definir a propriedade em um arquivo *.props* e, em seguida, explicitamente, importar o arquivo *.props* em todos os projetos na solução, entre outras coisas.

No entanto, agora você pode adicionar uma nova propriedade a todos os projetos em uma única etapa, definindo-a em um único arquivo chamado *Directory.Build.props* na pasta raiz que contém sua fonte. Quando o MSBuild é executado, o *Microsoft.Common.props* pesquisa sua estrutura de diretório pelo arquivo *Directory.Build.props* (e o *Microsoft.Common.targets* procura o *Directory.Build.targets*). Se ele encontrar um, ele importa a propriedade. *Directory.Build.props* é um arquivo definido pelo usuário que fornece personalizações de projetos em um diretório.

> [!NOTE]
> Sistemas de arquivos baseados em Linux diferenciam maiúsculas de minúsculas. Verifique se a capitalização do nome do arquivo Directory.Build.props possui uma correspondência exata ou não será detectado durante o processo de compilação.
>
> Consulte mais informações sobre [este problema de GitHub](https://github.com/dotnet/core/issues/1991#issue-368441031).

### <a name="directorybuildprops-example"></a>Exemplo de Directory.Build.props

Por exemplo, se você desejasse habilitar todos os seus projetos para acessar o novo recurso **/deterministic** do Roslyn (que é exposto no destino `CoreCompile` do Roslyn pela propriedade `$(Deterministic)`), poderia fazer o seguinte.

1. Crie um novo arquivo na raiz do seu repositório chamado *Directory.Build.props*.
2. Adicione o XML a seguir ao arquivo.

   ```xml
   <Project>
    <PropertyGroup>
      <Deterministic>true</Deterministic>
    </PropertyGroup>
   </Project>
   ```
3. Execute o MSBuild. As importações do *Microsoft.Common.props* e *Microsoft.Common.targets* existentes do projeto encontram o arquivo e o importam.

### <a name="search-scope"></a>Escopo da pesquisa

Ao pesquisar um arquivo *Directory.Build.props*, o MSBuild percorre a estrutura de diretórios para cima de seu local de projeto (`$(MSBuildProjectFullPath)`), parando depois de localizar o arquivo *Directory.Build.props*. Por exemplo, se seu `$(MSBuildProjectFullPath)` for *c:\usuários\nomedeusuário\código\teste\caso1*, o MSBuild deve iniciar a pesquisa aí e depois pesquisar a estrutura do diretório para cima até localizar um arquivo *Directory.Build.props*, como na estrutura de diretório a seguir.

```
c:\users\username\code\test\case1
c:\users\username\code\test
c:\users\username\code
c:\users\username
c:\users
c:\
```

O local do arquivo de solução é irrelevante para o *Directory.Build.props*.

### <a name="import-order"></a>Ordem de importação

O *Directory.Build.props* é importado muito no início no *Microsoft.Common.props* e as propriedades definidas posteriormente não ficam disponíveis para ele. Portanto, evite referenciar propriedades que ainda não foram definidas (e que serão avaliadas como vazias).

O *Directory.Build.targets* é importado do *Microsoft.Common.targets* depois de importar os arquivos *.targets* dos pacotes do NuGet. Portanto, ele pode substituir as propriedades e os destinos definidos na maior parte da lógica de build, mas, às vezes, talvez seja necessário personalizar o arquivo de projeto após a importação final.

### <a name="use-case-multi-level-merging"></a>Caso de uso: mesclagem de vários níveis

Suponha que você tenha essa estrutura de solução padrão:

```
\
  MySolution.sln
  Directory.Build.props     (1)
  \src
    Directory.Build.props   (2-src)
    \Project1
    \Project2
  \test
    Directory.Build.props   (2-test)
    \Project1Tests
    \Project2Tests
```

Pode ser interessante ter propriedades comuns para todos os projetos *(1)*, propriedades comuns para projetos *src* *(2-src)* e propriedades comuns para projetos *test* *(2-test)*.

Para que o MSBuild mescle corretamente os arquivos "internos" (*2-src* e *2-test*) com o arquivo "externo" (*1*), você precisa considerar que, depois de o MSBuild localizar um arquivo *Directory.Build.props*, ele interrompe a verificação adicional. Para continuar a verificação e a mesclagem no arquivo externo, coloque este código em ambos os arquivos internos:

`<Import Project="$([MSBuild]::GetPathOfFileAbove('Directory.Build.props', '$(MSBuildThisFileDirectory)../'))" />`

Um resumo da abordagem geral do MSBuild é o seguinte:

- Para qualquer projeto, o MSBuild localiza o primeiro *Directory.Build.props* para cima na estrutura da solução, mescla-o com padrões e interrompe o exame adicional
- Se você quiser que vários níveis sejam encontrados e mesclados, então [`<Import...>`](../msbuild/property-functions.md#msbuild-getpathoffileabove) (mostrado acima) o arquivo "externo" do arquivo "interno"
- Se o arquivo "externo" também não importar nada acima dele, a verificação será interrompida aqui
- Para controlar o processo de exame/mesclagem, use `$(DirectoryBuildPropsPath)` e `$(ImportDirectoryBuildProps)`

Ou, de maneira mais simples: o primeiro *Directory.Build.props* que não importar nada é o local em que o MSBuild para.

## <a name="msbuildprojectextensionspath"></a>MSBuildProjectExtensionsPath

Por padrão, *Microsoft.Common.props* importa `$(MSBuildProjectExtensionsPath)$(MSBuildProjectFile).*.props` e *Microsoft.Common.targets* importa `$(MSBuildProjectExtensionsPath)$(MSBuildProjectFile).*.targets`. O valor padrão de `MSBuildProjectExtensionsPath` é `$(BaseIntermediateOutputPath)`, `obj/`. O NuGet usa esse mecanismo para se referir à lógica de build entregue com pacotes; ou seja, no momento da restauração, ele cria arquivos `{project}.nuget.g.props` que se referem ao conteúdo do pacote.

Desabilite esse mecanismo de extensibilidade definindo a propriedade `ImportProjectExtensionProps` como `false` em um *Directory.Build.props* ou antes de importar *Microsoft.Common.props*.

> [!NOTE]
> Desabilitar importações de MSBuildProjectExtensionsPath impedirá que a lógica de build fornecida em pacotes do NuGet se aplique ao seu projeto. Alguns pacotes do NuGet exigem que a lógica de build execute a função deles e eles se tornarão inúteis quando essa opção estiver desabilitada.

## <a name="user-file"></a>Arquivo .user

O *Microsoft.Common.CurrentVersion.targets* importa `$(MSBuildProjectFullPath).user` se ele existe; portanto, você pode criar um arquivo ao lado do projeto com essa extensão adicional. Para alterações de longo que você planeja verificar no controle do código-fonte, alterar o projeto propriamente dito, para que os mantenedores futuros não precisem saber sobre esse mecanismo de extensão.

## <a name="msbuildextensionspath-and-msbuilduserextensionspath"></a>MSBuildExtensionsPath e MSBuildUserExtensionsPath

> [!WARNING]
> Com o uso desses mecanismos de extensão, é mais difícil obter builds repetíveis entre computadores. Tente usar uma configuração cujo check-in possa ser feito em seu sistema de controle do código-fonte e compartilhado entre todos os desenvolvedores de sua base de código.

Por convenção, muitos arquivos de lógica de build principais são importados

```xml
$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\{TargetFileName}\ImportBefore\*.targets
```

antes dos respectivos conteúdos, e

```xml
$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\{TargetFileName}\ImportAfter\*.targets
```

depois. Isso permite que os SDKs instalados ampliem a lógica de build dos tipos comuns de projeto.

A mesma estrutura de diretório é pesquisada em `$(MSBuildUserExtensionsPath)`, que é a pasta por usuário *%LOCALAPPDATA%\Microsoft\MSBuild*. Arquivos colocados nessa pasta serão importados para todos os builds do tipo de projeto correspondente executados sob as credenciais do usuário. Desabilite as extensões de usuário definindo as propriedades nomeadas como o arquivo de importação no padrão `ImportUserLocationsByWildcardBefore{ImportingFileNameWithNoDots}`. Por exemplo, definir `ImportUserLocationsByWildcardBeforeMicrosoftCommonProps` para `false` impediria a importação de `$(MSBuildUserExtensionsPath)\$(MSBuildToolsVersion)\Imports\Microsoft.Common.props\ImportBefore\*`.

## <a name="customize-the-solution-build"></a>Personalizar o build de solução

> [!IMPORTANT]
> A personalização do build de solução dessa maneira aplica-se apenas a builds de linha de comando com o *MSBuild.exe*. Isso **não** se aplica a builds dentro do Visual Studio.

Quando o MSBuild compila um arquivo de solução, ele primeiro se converte internamente em um arquivo de projeto e, em seguida, compila isso. O arquivo de projeto gerado importa `before.{solutionname}.sln.targets` antes de definir quaisquer destinos e `after.{solutionname}.sln.targets` após importar destinos, incluindo destinos instalados nos diretórios `$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\SolutionFile\ImportBefore` e `$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\SolutionFile\ImportAfter`.

Por exemplo, você pode definir um novo destino para gravar uma mensagem de log personalizada depois de compilar *MyCustomizedSolution.sln* criando um arquivo no mesmo diretório chamado *after.MyCustomizedSolution.sln.targets* que contém

```xml
<Project>
 <Target Name="EmitCustomMessage" AfterTargets="Build">
   <Message Importance="High" Text="The solution has completed the Build target" />
 </Target>
</Project>
```

## <a name="see-also"></a>Consulte também

[Conceitos do MSBuild](../msbuild/msbuild-concepts.md)

[Referência do MSBuild](../msbuild/msbuild-reference.md)
