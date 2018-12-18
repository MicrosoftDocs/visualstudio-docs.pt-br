---
title: Atualizar um aplicativo existente para o MSBuild 15 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4da159ae0fcb4347052efcea5d0dbd24d5ccd8f1
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219231"
---
# <a name="update-an-existing-application-for-msbuild-15"></a>Atualizar um aplicativo existente para o MSBuild 15

Em versões do MSBuild anteriores à 15.0, o MSBuild era carregado do GAC (cache de assembly global) e extensões do MSBuild eram instaladas no registro. Isso garantia que todos os aplicativos usassem a mesma versão do MSBuild e tivessem acesso aos mesmos conjuntos de ferramentas, mas impedia instalações lado a lado de diferentes versões do Visual Studio.

Para dar suporte a uma instalação mais rápida, menor e lado a lado, o Visual Studio 2017 não coloca mais o MSBuild no GAC ou modifica o registro. Infelizmente, isso significa que aplicativos que desejam usar a API do MSBuild para avaliar ou criar projetos não podem contar implicitamente com a instalação do Visual Studio.

## <a name="use-msbuild-from-visual-studio"></a>Usar o MSBuild no Visual Studio

Para garantir que builds programáticos de seu aplicativo correspondam àqueles feitos no Visual Studio ou no *MSBuild.exe*, carregue assemblies do MSBuild no Visual Studio e use os SDKs disponíveis dentro do Visual Studio. O pacote NuGet Microsoft.Build.Locator simplifica esse processo.

## <a name="use-microsoftbuildlocator"></a>Usar Microsoft.Build.Locator

Se você redistribuir *Microsoft.Build.Locator.dll* com seu aplicativo, não precisará distribuir outros assemblies do MSBuild.

Atualizar um projeto para usar o MSBuild 15 e a API de localizador requer algumas alterações no seu projeto, descritas abaixo. Para ver um exemplo das alterações necessárias para atualizar um projeto, consulte [As confirmações feitas em um projeto de exemplo no repositório do MSBuildLocator](https://github.com/Microsoft/MSBuildLocator/commits/example-updating-to-msbuild-15).

### <a name="change-msbuild-references"></a>Alterar as referências do MSBuild

Para garantir que o MSBuild seja carregado de um local central, não distribua seus assemblies com seu aplicativo.

O mecanismo para alterar o projeto para evitar carregar o MSBuild de um local central depende de como você faz referência ao MSBuild.

#### <a name="use-nuget-packages-preferred"></a>Usar pacotes NuGet (preferencial)

Essas instruções pressupõem que você esteja usando [referências de NuGet de estilo PackageReference](https://docs.microsoft.com/nuget/consume-packages/package-references-in-project-files).

Altere os arquivos de projeto para fazer referência a assemblies de MSBuild de seus pacotes NuGet. Especifique `ExcludeAssets=runtime` para informar ao NuGet que os assemblies são necessários somente no momento da compilação, e não devem ser copiados para o diretório de saída.

As versões principal e secundária dos pacotes do MSBuild devem ser menores ou iguais à versão mínima do Visual Studio a que você deseja dar suporte. Se quiser dar suporte a qualquer versão do Visual Studio 2017, faça referência à versão do pacote `15.1.548`.

Por exemplo, você pode usar este XML:

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.Build" Version="15.1.548" ExcludeAssets="runtime" />
  <PackageReference Include="Microsoft.Build.Utilities" Version="15.1.548" ExcludeAssets="runtime" />
</ItemGroup>
```

#### <a name="use-extension-assemblies"></a>Usar assemblies de extensão

Se você não puder usar pacotes NuGet, poderá fazer referência aos assemblies do MSBuild distribuídos com o Visual Studio. Se você fizer referência ao MSBuild diretamente, certifique-se de que ele não seja copiado para o diretório de saída por meio da definição de `Copy Local` como `False`. No arquivo de projeto, essa configuração seria semelhante ao seguinte código:

```xml
    <Reference Include="Microsoft.Build, Version=15.1.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
      <Private>False</Private>
    </Reference>
```

#### <a name="binding-redirects"></a>Redirecionamentos de associação

Faça referência ao pacote do Microsoft.Build.Locator para assegurar que seu aplicativo use automaticamente os redirecionamentos de associação necessários de todas as versões de assemblies do MSBuild para a versão `15.1.0.0`.

### <a name="ensure-output-is-clean"></a>Garantir uma saída limpa

Compile o projeto e inspecione o diretório de saída para ter certeza de que ele não contenha assemblies *Microsoft.Build.\*.dll* diferentes de *Microsoft.Build.Locator.dll*, adicionado na próxima etapa.

### <a name="add-package-reference"></a>Adicionar referência de pacote

Adicione uma referência de pacote NuGet para [Microsoft.Build.Locator](https://www.nuget.org/packages/Microsoft.Build.Locator/).

```xml
    <PackageReference Include="Microsoft.Build.Locator">
      <Version>1.0.7-preview-ge60d679b53</Version>
    </PackageReference>
```

### <a name="register-instance-before-calling-msbuild"></a>Registre a instância antes de chamar o MSBuild

Adicione uma chamada à API do localizador antes de chamar qualquer método que usa o MSBuild.

A maneira mais simples de adicionar a chamada à API do localizador é adicionar uma chamada

```csharp
MSBuildLocator.RegisterDefaults();
```

no código de inicialização do aplicativo.

Se quiser ter um controle mais refinado sobre o carregamento do MSBuild, você poderá selecionar um resultado de `MSBuildLocator.QueryVisualStudioInstances()` para passar para `MSBuildLocator.RegisterInstance()` manualmente, mas geralmente isso não é necessário.
