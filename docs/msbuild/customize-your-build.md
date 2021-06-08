---
title: Personalizar seu build | Microsoft Docs
description: Saiba mais sobre vários ganchos de extensibilidade que você pode usar para personalizar projetos do MSBuild que usam o processo de build padrão.
ms.custom: SEO-VS-2020
ms.date: 06/13/2019
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, transforms
- transforms [MSBuild]
ms.assetid: d0bceb3b-14fb-455c-805a-63acefa4b3ed
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 19dafcbb956634eeea5fa0ed967e93a8a8d5e546
ms.sourcegitcommit: 3fe04d5b931ae459a802a1b965f84186757cbc08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2021
ms.locfileid: "111588443"
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

As propriedades definidas em *Directory.Build.props* podem ser substituídos em outro lugar no arquivo de projeto ou em arquivos importados, portanto, você deve pensar nas configurações em *Directory.Build.props* como especificando os padrões para seus projetos.

*Directory.Build.targets* é importado de *Microsoft.Common.targets* depois de importar *arquivos .targets* de pacotes NuGet. Portanto, ele pode substituir propriedades e destinos definidos na maioria da lógica de build ou definir propriedades para todos os seus projetos, independentemente do conjunto de projetos individuais.

Quando você precisar definir uma propriedade ou definir um destino para um projeto individual que substitui as configurações anteriores, coloque essa lógica no arquivo de projeto após a importação final. Para fazer isso em um projeto no estilo SDK, primeiro você precisa substituir o atributo no estilo SDK por importações equivalentes. Consulte Como usar SDKs de projeto do [MSBuild.](how-to-use-project-sdk.md)

> [!NOTE]
> O mecanismo do MSBuild lê em todos os arquivos importados durante a avaliação, antes de iniciar a execução de build para qualquer projeto (incluindo qualquer ), portanto, esses arquivos não devem ser modificados pelo ou por qualquer outra parte do processo `PreBuildEvent` `PreBuildEvent` de build. Todas as modificações não entre em vigor até a próxima invocação *deMSBuild.exe* ou da próxima Visual Studio build.

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

Pode ser interessante ter propriedades comuns para todos os projetos *(1)*, propriedades comuns para projetos *src**(2-src)* e propriedades comuns para projetos *test**(2-test)*.

Para que o MSBuild mescle corretamente os arquivos "internos" (*2-src* e *2-test*) com o arquivo "externo" (*1*), você precisa considerar que, depois de o MSBuild localizar um arquivo *Directory.Build.props*, ele interrompe a verificação adicional. Para continuar a verificação e a mesclagem no arquivo externo, coloque este código em ambos os arquivos internos:

`<Import Project="$([MSBuild]::GetPathOfFileAbove('Directory.Build.props', '$(MSBuildThisFileDirectory)../'))" />`

Um resumo da abordagem geral do MSBuild é o seguinte:

- Para qualquer projeto, o MSBuild localiza o primeiro *Directory.Build.props* para cima na estrutura da solução, mescla-o com padrões e interrompe o exame adicional
- Se você quiser que vários níveis sejam encontrados e mesclados, (mostrado acima) o arquivo [`<Import...>`](../msbuild/property-functions.md#msbuild-getpathoffileabove) "externo" do arquivo "interno"
- Se o arquivo "externo" também não importar nada acima dele, a verificação será interrompida aqui
- Para controlar o processo de exame/mesclagem, use `$(DirectoryBuildPropsPath)` e `$(ImportDirectoryBuildProps)`

Ou, de maneira mais simples: o primeiro *Directory.Build.props* que não importar nada é o local em que o MSBuild para.

### <a name="choose-between-adding-properties-to-a-props-or-targets-file"></a>Escolha entre adicionar propriedades a um arquivo .props ou .targets

O MSBuild depende da ordem de importação, e a última definição de uma propriedade (ou uma `UsingTask` ou um destino) é a definição usada.

Ao usar importações explícitas, você pode importar de um arquivo *.props* ou *.targets* a qualquer momento. Veja a seguir a convenção mais amplamente usada:

- Os arquivos *.props* são importados no início na ordem de importação.

- Os arquivos *.targets* são importados no final na ordem de compilação.

Essa convenção é imposta pelas importações `<Project Sdk="SdkName">` (isto é, a importação de *Sdk.props* vem primeiro, antes de todos os conteúdos do arquivo, e *Sdk.targets* vem por último, depois de todos os conteúdos do arquivo).

Ao decidir onde colocar as propriedades, use as seguintes diretrizes gerais:

- Para muitas propriedades, não importa onde elas são definidas porque elas não são substituídas e serão lidas somente no tempo de execução.

- Para o comportamento que pode ser personalizado em um projeto individual, defina padrões em arquivos *.props*.

- Evite definir propriedades dependentes em arquivos *.props* lendo o valor de uma propriedade possivelmente personalizada, pois a personalização não acontecerá até que o MSBuild leia o projeto do usuário.

- Defina propriedades dependentes em arquivos *.targets*, pois eles selecionarão as personalizações em projetos individuais.

- Se você precisar substituir as propriedades, faça isso em um arquivo *.targets*, depois que todas as personalizações de projeto do usuário tiverem tido uma chance de entrar em vigor. Tenha cuidado ao usar propriedades derivadas, pois elas também podem precisar ser substituídas.

- Inclua itens em arquivos *.props* (condicionados em uma propriedade). Todas as propriedades são consideradas antes de qualquer item, portanto, as personalizações de propriedade do projeto do usuário são captadas, o que dá ao projeto do usuário a oportunidade de `Remove` ou `Update` qualquer item inserido pela importação.

- Defina os destinos nos arquivos *.targets*. No entanto, se o arquivo *.targets* for importado por um SDK, lembre-se de que esse cenário torna a substituição do destino mais difícil porque o projeto do usuário não tem um lugar para substituí-lo por padrão.

- Se possível, prefira propriedades de personalização no tempo de avaliação às propriedades de alteração dentro de um destino. Essa diretriz torna mais fácil carregar um projeto e entender o que ele está fazendo.

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

depois. Essa convenção permite que SDKs instalados ampliem a lógica da compilação de tipos de projeto comuns.

A mesma estrutura de diretório é pesquisada em `$(MSBuildUserExtensionsPath)`, que é a pasta por usuário *%LOCALAPPDATA%\Microsoft\MSBuild*. Arquivos colocados nessa pasta serão importados para todos os builds do tipo de projeto correspondente executados sob as credenciais do usuário. Desabilite as extensões de usuário definindo as propriedades nomeadas como o arquivo de importação no padrão `ImportUserLocationsByWildcardBefore{ImportingFileNameWithNoDots}`. Por exemplo, definir `ImportUserLocationsByWildcardBeforeMicrosoftCommonProps` para `false` impediria a importação de `$(MSBuildUserExtensionsPath)\$(MSBuildToolsVersion)\Imports\Microsoft.Common.props\ImportBefore\*`.

## <a name="customize-the-solution-build"></a>Personalizar o build de solução

> [!IMPORTANT]
> A personalização do build de solução dessa maneira aplica-se apenas a builds de linha de comando com o *MSBuild.exe*. Isso **não** se aplica a builds dentro do Visual Studio. Por esse motivo, não é recomendável colocar a personalização no nível da solução. Uma alternativa melhor para personalizar todos os projetos em uma solução é usar *arquivos Directory.Build.props* e *Directory.build.targets* na pasta da solução, conforme discutido em outro lugar neste artigo.

Quando o MSBuild compila um arquivo de solução, ele primeiro se converte internamente em um arquivo de projeto e, em seguida, compila isso. O arquivo de projeto gerado importa `before.{solutionname}.sln.targets` antes de definir quaisquer destinos e `after.{solutionname}.sln.targets` após importar destinos, incluindo destinos instalados nos diretórios `$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\SolutionFile\ImportBefore` e `$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\SolutionFile\ImportAfter`.

Por exemplo, você pode definir um novo destino para gravar uma mensagem de log personalizada depois de compilar *MyCustomizedSolution.sln* criando um arquivo no mesmo diretório chamado *after.MyCustomizedSolution.sln.targets* que contém

```xml
<Project>
 <Target Name="EmitCustomMessage" AfterTargets="Build">
   <Message Importance="High" Text="The solution has completed the Build target" />
 </Target>
</Project>
```

O build da solução é separado dos builds do projeto, portanto, as configurações aqui não afetam os builds do projeto.

## <a name="customize-all-net-builds"></a>Personalizar todos os builds do .NET

Ao manter um servidor de build, talvez seja necessário definir as configurações do MSBuild globalmente para todos os builds no servidor.  Em princípio, você pode modificar os arquivos *globais Microsoft.Common.Targets* ou *Microsoft.Common.Props,* mas há uma maneira melhor. Você pode afetar todos os builds de um determinado tipo de projeto (como todos os projetos C#) usando determinadas propriedades do MSBuild e adicionando determinados arquivos `.targets` e `.props` personalizados.

Para afetar todos os builds C# ou Visual Basic regidos por uma instalação do MSBuild ou Visual Studio, crie um arquivo *Custom.Before.Microsoft.Common.Targets* ou *Custom.After.Microsoft.Common.Targets* com destinos que serão executados antes ou depois de *Microsoft.Common.targets* ou um arquivo *Custom.Before.Microsoft.Common.Props* ou *Custom.After.Microsoft.Common.Props* com propriedades que serão processadas antes ou depois de *Microsoft.Common.props.*

Você pode especificar os locais desses arquivos usando as seguintes propriedades do MSBuild:

- CustomBeforeMicrosoftCommonProps
- CustomBeforeMicrosoftCommonTargets
- CustomAfterMicrosoftCommonProps
- CustomAfterMicrosoftCommonTargets
- CustomBeforeMicrosoftCSharpTargets
- CustomBeforeMicrosoftVisualBasicTargets
- CustomAfterMicrosoftCSharpTargets
- CustomAfterMicrosoftVisualBasicTargets

As *versões* comuns dessas propriedades afetam os projetos C# e Visual Basic. Você pode definir essas propriedades na linha de comando do MSBuild.

```cmd
msbuild /p:CustomBeforeMicrosoftCommonTargets="C:\build\config\Custom.Before.Microsoft.Common.Targets" MyProject.csproj
```

A melhor abordagem depende do seu cenário. Usando Visual Studio extensibilidade, você pode personalizar o sistema de build e fornecer um mecanismo para instalar e gerenciar as personalizações.

Se você tiver um servidor de build dedicado e quiser garantir que determinados destinos sempre executem em todos os builds do tipo de projeto apropriado que são executados nesse servidor, o uso de um arquivo ou personalizado global faz `.targets` `.props` sentido.  Se você quiser que os destinos personalizados só serão executados quando determinadas condições se aplicarem, use outro local do arquivo e de definido o caminho para esse arquivo definindo a propriedade apropriada do MSBuild na linha de comando do MSBuild somente quando necessário.

> [!WARNING]
> Visual Studio usa os arquivos personalizados ou se os encontra na pasta `.targets` MSBuild sempre que cria qualquer projeto do `.props` tipo correspondente. Isso pode ter consequências não intencionais e, se for feito incorretamente, pode desabilitar a capacidade de Visual Studio criar no computador.

## <a name="customize-c-builds"></a>Personalizar builds do C++

Para projetos C++, os arquivos .targets e *.props* *personalizados mencionados* anteriormente não podem ser usados da mesma maneira para substituir as configurações padrão. *Directory.Build.props* é importado por *Microsoft.Common.props,* que é importado no enquanto a maioria dos padrões é definida em `Microsoft.Cpp.Default.props` *Microsoft.Cpp.props* e, para várias propriedades, uma condição "se ainda não definida" não pode ser usada, pois a propriedade já está definida, mas o padrão precisa ser diferente para propriedades de projeto específicas definidas com (consulte estrutura de arquivo `PropertyGroup` `Label="Configuration"` [.vcxproj e .props](/cpp/build/reference/vcxproj-file-structure)).

No entanto, você pode usar as seguintes propriedades para especificar *arquivos .props* a serem importados automaticamente antes/depois dos *arquivos \* Microsoft.Cpp:*

- ForceImportAfterCppDefaultProps
- ForceImportBeforeCppProps
- ForceImportAfterCppProps
- ForceImportBeforeCppTargets
- ForceImportAfterCppTargets

Para personalizar os valores padrão de propriedades para todos os builds do C++, crie outro *arquivo .props* (digamos, *MyProps.props*) e defina a propriedade ao apontar `ForceImportAfterCppProps` para `Directory.Build.props` ele:

<PropertyGroup><ForceImportAfterCppProps>$(MsbuildThisFileDirectory)\MyProps.props<ForceImportAfterCppProps>
</PropertyGroup>

*MyProps.props* será importado automaticamente no final do *Microsoft.Cpp.props.*

## <a name="customize-all-c-builds"></a>Personalizar todos os builds do C++

A personalização da instalação do Visual Studio não é recomendada, pois não é fácil acompanhar essas personalizações, mas se você estiver estendendo o Visual Studio para personalizar builds do C++ para uma plataforma específica, poderá criar arquivos para cada plataforma e coloque-os nas pastas de importação apropriadas para essas plataformas como parte de uma extensão `.targets` Visual Studio.

O `.targets` arquivo para a plataforma Win32, *Microsoft.Cpp.Win32.targets,* contém o seguinte `Import` elemento:

```xml
<Import Project="$(VCTargetsPath)\Platforms\Win32\ImportBefore\*.targets"
        Condition="Exists('$(VCTargetsPath)\Platforms\Win32\ImportBefore')"
/>
```

Há um elemento semelhante próximo ao final do mesmo arquivo:

```xml
<Import Project="$(VCTargetsPath)\Platforms\Win32\ImportAfter\*.targets"
        Condition="Exists('$(VCTargetsPath)\Platforms\Win32\ImportAfter')"
/>
```

Elementos de importação semelhantes existem para outras plataformas de destino em *%ProgramFiles32%\MSBuild\Microsoft.Cpp\v{version}\Platforms. \*

Depois de colocar o arquivo na pasta apropriada de acordo com a plataforma, o MSBuild importa seu arquivo para cada `.targets` `ImportAfter` build do C++ para essa plataforma. Você pode colocar vários `.targets` arquivos lá, se necessário. 

Usando Visual Studio extensibilidade, outras personalizações são possíveis, como a definição de uma nova plataforma. Para obter mais informações, consulte [Extensibilidade do projeto C++.](../extensibility/visual-cpp-project-extensibility.md)

### <a name="specify-a-custom-import-on-the-command-line"></a>Especificar uma importação personalizada na linha de comando

Para personalizado que você deseja incluir para um build específico de um projeto C++, de definir uma ou ambas as propriedades e `.targets` `ForceImportBeforeCppTargets` na linha de `ForceImportAfterCppTargets` comando.

```cmd
msbuild /p:ForceImportBeforeCppTargets="C:\build\config\Custom.Before.Microsoft.Cpp.Targets" MyCppProject.vcxproj
```

Para uma configuração global (para afetar, digamos, todos os builds do C++ para uma plataforma em um servidor de build), há dois métodos. Primeiro, você pode definir essas propriedades usando uma variável de ambiente do sistema que é sempre definida. Isso funciona porque o MSBuild sempre lê o ambiente e cria (ou substitui) propriedades para todas as variáveis de ambiente.

## <a name="see-also"></a>Confira também

- [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)

- [Referência do MSBuild](../msbuild/msbuild-reference.md)
