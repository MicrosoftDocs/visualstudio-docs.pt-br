---
title: Testes de unidade direcionados a uma versão anterior do .NET Framework
ms.date: 11/04/2016
ms.topic: how-to
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
author: mikejo5000
ms.openlocfilehash: 670ec672c55d591496e26435db5a3112c345a44d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288163"
---
# <a name="how-to-configure-unit-tests-to-target-an-earlier-version-of-the-net-framework"></a>Como configurar testes de unidade para usar uma versão anterior do .NET Framework como destino

Quando você cria um projeto de teste no Microsoft Visual Studio, a versão mais recente do .NET Framework é definida como destino, por padrão. Além disso, se você atualizar projetos de teste de versões anteriores do Visual Studio, eles são atualizados para destinar-se à versão mais recente do .NET Framework. Ao editar as propriedades do projeto, é possível redirecionar explicitamente o projeto para versões anteriores do .NET Framework.

Você pode criar projetos de teste de unidade que se destinam a versões específicas do .NET Framework. A versão de destino deve ser 3.5 ou posterior e não pode ser uma versão de cliente. O Visual Studio permite o seguinte suporte básico para testes de unidade que se direcionam a versões específicas:

- Você pode criar projetos de teste de unidade e destiná-las a uma versão específica do .NET Framework.

- Você pode executar testes de unidade direcionados a uma versão específica do .NET Framework no Visual Studio no computador local.

- Você pode executar testes de unidade direcionados a uma versão específica do .NET Framework usando *MSTest.exe* do prompt de comando.

- Você pode executar testes de unidade em um agente de build como parte de um build.

**Testar aplicativos de SharePoint**

Os recursos listados acima também permitem gravar testes de unidade e testes de integração de aplicativos do SharePoint usando o Visual Studio. Para obter mais informações sobre como desenvolver aplicativos do SharePoint usando o Visual Studio, confira [Criar soluções do SharePoint](../sharepoint/create-sharepoint-solutions.md), [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md) e [Verificar e depurar um código do SharePoint](../sharepoint/verifying-and-debugging-sharepoint-code.md).

**Limitações**

As seguintes limitações se aplicam quando você redireciona projetos de teste para usar versões anteriores do .NET Framework:

- No .NET Framework 3.5, há suporte para multiplataforma para projetos de teste que contenham somente testes de unidade. O .NET Framework 3.5 não oferece suporte a nenhum outro tipo de teste, como o teste de carga ou teste da interface do usuário codificada. O redirecionamento está bloqueado para tipos de teste diferentes de testes de unidade.

- A execução de testes que são destinados a uma versão anterior do .NET Framework só tem suporte no adaptador do host padrão. Não há suporte no adaptador do host do ASP.NET. Os aplicativos ASP.NET que precisam ser executados no contexto do ASP.NET Development Server devem ser compatíveis com a versão atual do .NET Framework.

- O suporte à coleta de dados é desabilitado quando você executa testes que oferecem suporte a multiplataforma do .NET Framework 3.5. Você pode executar a cobertura de código usando as ferramentas de linha de comando do Visual Studio.

- Não é possível executar testes de unidade que usam o .NET Framework 3.5 em um computador remoto.

- Você não pode direcionar testes de unidade a versões de cliente anteriores do Framework.

## <a name="retargeting-for-visual-basic-unit-test-projects"></a>Redirecionando para projetos de teste de unidade do Visual Basic

1. Crie um **projeto de teste de unidade** do Visual Basic.

2. No **Gerenciador de Soluções**, escolha **Propriedades** no menu aberto ao clicar com o botão direito do mouse do novo projeto de teste do Visual Basic.

     As propriedades do seu projeto de teste do Visual Basic são exibidas.

3. Na guia **Compilar** escolha **Opções de Compilação Avançadas** conforme mostrado na ilustração a seguir.

     ![Opções compiladas avançadas](../test/media/howtoconfigureunittest35frameworka.png)

4. Use a lista suspensa **Estrutura de destino (todas as configurações)** para alterar a estrutura de destino para **.NET Framework 3.5** ou uma versão posterior, conforme mostrado no texto explicativo B na ilustração a seguir. Não especifique uma versão de cliente.

     ![Lista suspensa da estrutura de destino](../test/media/howtoconfigureunitest35frameworkstepb.png)

## <a name="retargeting-for-c-unit-test-projects"></a>Redirecionando para projetos de teste de unidade do C#

1. Crie um novo projeto de **projeto de teste de unidade** em C#.

2. No **Gerenciador de Soluções**, escolha **Propriedades** no menu aberto ao clicar com o botão direito do mouse do novo projeto de teste do C#.

   As propriedades do seu projeto de teste do C# são exibidas.

3. Na guia **Aplicativo**, escolha **Estrutura de destino**. Na lista suspensa, escolha **.NET Framework 3.5** ou uma versão posterior, conforme mostra a ilustração a seguir. Não especifique uma versão de cliente.

   ![Lista suspensa da estrutura de destino](../test/media/howtoconfigureunittest35frameworkcsharp.png)

## <a name="retargeting-for-ccli-unit-test-projects"></a>Redirecionando para projetos de teste de unidade do C++/CLI

1. Crie um **projeto de teste de unidade** do C++.

   > [!WARNING]
   > Para compilar testes de unidade do C++/CLI para uma versão anterior do .NET Framework para o Visual C++, é necessário usar a versão correspondente do Visual Studio.

2. No **Gerenciador de Soluções**, escolha **Descarregar Projeto** do novo projeto de teste do C++.

3. Em **Gerenciador de soluções**, escolha o projeto de teste do C++ descarregado e, em seguida, escolha **Editar \<project name> . vcxproj**.

   O arquivo *. vcxproj* é aberto no editor.

4. Defina o `TargetFrameworkVersion` para a versão 3.5 ou posterior no `PropertyGroup` rotulado `"Globals"`. Não especifique uma versão de cliente:

    ```xml
    <PropertyGroup Label="Globals">
        <TargetName>DefaultTest</TargetName>
        <ProjectTypes>{3AC096D0-A1C2-E12C-1390-A8335801FDAB};{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}</ProjectTypes>
        <ProjectGUID>{CE16D77A-E364-4ACD-948B-1EB6218B0EA3}</ProjectGUID>
        <TargetFrameworkVersion>3.5</TargetFrameworkVersion>
        <Keyword>ManagedCProj</Keyword>
        <RootNamespace>CPP_Test</RootNamespace>
      </PropertyGroup>
    ```

5. Salve e feche o arquivo *. vcxproj* .

6. No **Gerenciador de Soluções**, escolha **Recarregar Projeto** no menu aberto ao clicar com o botão direito do mouse do novo projeto de teste do C++.

## <a name="see-also"></a>Veja também

- [Criar soluções do SharePoint](../sharepoint/create-sharepoint-solutions.md)
- [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [Caixa de diálogo Configurações avançadas do compilador (Visual Basic)](../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md)
