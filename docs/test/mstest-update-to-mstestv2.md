---
title: Atualizar para MSTestV2
description: Saiba como atualizar do MSTestV1 para o MSTestV2
ms.custom: SEO-VS-2020
ms.date: 02/26/2021
ms.topic: conceptual
f1_keywords:
- vs.UnitTest.Migrate
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ffe45c444321a7efbaee0a2eb5729850a06c5910
ms.sourcegitcommit: 99b66b0f4ced46ead0b2506a103f974f40cc0076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2021
ms.locfileid: "103366251"
---
# <a name="upgrade-from-mstestv1-to-mstestv2"></a>Atualizar do MSTestV1 para o MSTestV2

Você pode atualizar seu projeto de teste redirecionando a versão MSTest referenciada em seu *. csproj* de MSTestV1 para MSTestV2. Nem todos os recursos do MSTestV1 foram trazidos para o MSTestV2, portanto, algumas alterações podem ser necessárias para resolver erros. Consulte [recursos do MSTestV1 que não têm suporte no MSTestV2](#mstestv1-features-that-are-not-supported-in-mstestv2) para entender quais recursos não funcionarão mais. Alguns deles podem precisar ser removidos dos testes.

1. Remova a referência de assembly para Microsoft. VisualStudio. QualityTools. UnitTestFramework do seu projeto de teste de unidade.
2. Adicione referências de pacote NuGet a MSTestV2, incluindo os pacotes [MSTest. TestFrameWork](https://www.nuget.org/packages/MSTest.TestFramework) e [MSTest. TestAdapter](https://www.nuget.org/packages/MSTest.TestAdapter/) no NuGet.org. Você pode instalar pacotes no console do Gerenciador de pacotes NuGet com os seguintes comandos:

    ```console
    PM> Install-Package MSTest.TestAdapter -Version 2.1.2
    PM> Install-Package MSTest.TestFramework -Version 2.1.2
    ```

### <a name="old-style-csproj-example"></a>Exemplo de csproj de estilo antigo

Exemplo de destino de *. csproj* MSTestV1:

```xml
<Reference Include="Microsoft.VisualStudio.QualityTools.UnitTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
  <Private>False</Private>
</Reference>
```

Sample *. csproj* agora com o objetivo de MSTestV2:

```xml
<Reference Include="Microsoft.VisualStudio.TestPlatform.TestFramework, Version=14.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
  <HintPath>..\packages\MSTest.TestFramework.2.1.2\lib\net45\Microsoft.VisualStudio.TestPlatform.TestFramework.dll</HintPath>
</Reference>
```

> [!NOTE]
> Projetos de teste que são testes de interface do usuário codificados ou testes de carga da Web não são compatíveis com MSTestV2. Esses tipos de projeto foram preteridos. Leia mais sobre [substituição de teste de interface do usuário codificado](https://devblogs.microsoft.com/devops/changes-to-coded-ui-test-in-visual-studio-2019/) e [substituição de teste de carga da Web](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/).

### <a name="sdk-style-csproj-net-core-and-net-5"></a>Csproj do estilo SDK (.NET Core e .NET 5)

Se seu *. csproj* for o SDK-Style *. csproj* mais recente, você provavelmente já está usando o MSTestV2. Você pode encontrar os pacotes NuGet para [MSTestV2](https://www.nuget.org/packages/MSTest.TestFramework) e o [adaptador MSTestV2](https://www.nuget.org/packages/MSTest.TestAdapter/) no NuGet.

Exemplo:

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="16.7.1" />
  <PackageReference Include="MSTest.TestAdapter" Version="2.1.1" />
  <PackageReference Include="MSTest.TestFramework" Version="2.1.1" />
</ItemGroup>
```

## <a name="why-upgrade-to-mstestv2"></a>Por que atualizar para o MSTestV2?

Em 2016, lançamos a próxima etapa na evolução da estrutura MSTest com MSTestV2. Você pode ler mais sobre essa alteração na [postagem no blog](https://devblogs.microsoft.com/devops/taking-the-mstest-framework-forward-with-mstest-v2/)do comunicado.

* O MSTestV2 é mais facilmente adquirido e atualizado porque é entregue como um [pacote NuGet](https://www.nuget.org/packages/MSTest.TestFramework/).
* MSTestV2 é [código-fonte aberto](https://github.com/microsoft/testfx).
* Suporte uniforme a plataforma de aplicativos – o MSTestV2 é uma implementação convergida que oferece suporte uniforme à plataforma de aplicativos em .NET Framework, .NET Core, ASP.NET Core e UWP. [Leia mais](https://blogs.msdn.microsoft.com/devops/2016/09/01/announcing-mstest-v2-framework-support-for-net-core-1-0-rtm/).
* A implementação é totalmente entre plataformas (Windows, Linux e Mac). [Leia mais](https://blogs.msdn.microsoft.com/devops/2017/04/05/mstest-v2-is-open-source/).
* O MSTestV2 dá suporte ao direcionamento .NET Framework 4.5.0 e posterior, ao .NET Core 1,0 e posterior (aplicativos universais do Windows 10 +), ASP.NET Core 1,0 e posterior e .NET 5 e posterior.
* Fornece um mecanismo de extensibilidade de usuário final simples e uniforme. [Leia mais](https://blogs.msdn.microsoft.com/devops/2017/07/18/extending-mstest-v2/).
* Fornece um `DataRow` suporte uniforme para todos os projetos de teste com base em MSTest. [Leia mais](https://blogs.msdn.microsoft.com/devops/2017/02/25/mstest-v2-now-and-ahead/).
* Permite colocar o `TestCategory` atributo no nível de uma classe ou assembly. [Leia mais](https://blogs.msdn.microsoft.com/devops/2017/02/25/mstest-v2-now-and-ahead/).
* Os métodos de teste das classes base definidas em outro assembly agora são descobertos e executados da classe de teste derivada. Essa alteração leva em um comportamento consistente com tipos de classe de teste derivados. Se esse comportamento não for necessário por motivos de compatibilidade, ele poderá ser alterado novamente usando as seguintes configurações de execução:

    ```xml
    <RunSettings>    
    <MSTest> 
      <EnableBaseClassTestMethodsFromOtherAssemblies>false</EnableBaseClassTestMethodsFromOtherAssemblies> 
    </MSTest> 
    </RunSettings>
    ```

* Fornece controle mais refinado sobre a execução paralela por meio da [execução paralela em assembly](https://github.com/Microsoft/testfx-docs/blob/master/RFCs/004-In-Assembly-Parallel-Execution.md) de testes. Isso permite a execução de testes em um assembly em paralelo.
* O `TestCleanup` método em um `TestClass` é invocado mesmo se o `TestInitialize` método correspondente falhar. [Detalhes do problema](https://github.com/Microsoft/testfx/issues/250).
* O tempo gasto pelo `AssemblyInitialize` e `ClassInitialize` não é contado em direção à duração do teste. Essa alteração limita seu impacto em um tempo limite de teste.
* Testes que não são executáveis podem ser configurados para serem marcados como com falha por meio da `MapNotRunnableToFailed` marca, que faz parte do nó do adaptador no `.runsettings` arquivo.

    ```xml
    <RunSettings>    
    <MSTest> 
      <MapNotRunnableToFailed>true</MapNotRunnableToFailed> 
    </MSTest> 
    </RunSettings>
    ```

## <a name="mstestv1-features-that-are-not-supported-in-mstestv2"></a>Recursos do MSTestV1 que não têm suporte no MSTestV2

*   Os testes não podem ser incluídos em um "teste ordenado".
*   O adaptador não oferece suporte à configuração por meio de um arquivo *. testsettings* . Use o novo [arquivo *. RunSettings*](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md) para configuração de execução de teste.
*   O adaptador não dá suporte a listas de teste especificadas como um arquivo *. vsmdi* .
*   O "projeto de teste de interface do usuário codificado" e os tipos "projeto de teste de carga e desempenho da Web" não são suportados. Leia mais sobre [substituição de teste de interface do usuário codificado](https://devblogs.microsoft.com/devops/changes-to-coded-ui-test-in-visual-studio-2019/) e [substituição de teste de carga da Web](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/).

## <a name="see-also"></a>Confira também

- [Configurar execuções de teste com `.runsettings`](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)
- [Teste de unidade em seu código](../test/unit-test-your-code.md)
- [Depurar testes de unidade com o Gerenciador de Testes](../test/debug-unit-tests-with-test-explorer.md)
