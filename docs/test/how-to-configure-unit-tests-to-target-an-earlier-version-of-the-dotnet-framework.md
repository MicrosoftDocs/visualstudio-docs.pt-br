---
title: Configurar testes de unidade para que sejam direcionados para uma versão anterior do .NET Framework no Visual Studio
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
author: gewarren
ms.openlocfilehash: dad7589e09ded8994a5e687c4f4cf95283887324
ms.sourcegitcommit: 495bba1d8029646653f99ad20df2f80faad8d58b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39380636"
---
# <a name="how-to-configure-unit-tests-to-target-an-earlier-version-of-the-net-framework"></a>Como configurar testes de unidade para usar uma versão anterior do .NET Framework como destino

Quando você cria um projeto de teste no Microsoft Visual Studio, a versão mais recente do .NET Framework é definida como destino, por padrão. Além disso, se você atualizar projetos de teste de versões anteriores do Visual Studio, eles são atualizados para destinar-se à versão mais recente do .NET Framework. Ao editar as propriedades do projeto, é possível redirecionar explicitamente o projeto para versões anteriores do .NET Framework.

Você pode criar projetos de teste de unidade que se destinam a versões específicas do .NET Framework. A versão de destino deve ser 3.5 ou posterior e não pode ser uma versão de cliente. O Visual Studio permite o seguinte suporte básico para testes de unidade que se direcionam a versões específicas:

- Você pode criar projetos de teste de unidade e destiná-las a uma versão específica do .NET Framework.

- Você pode executar testes de unidade direcionados a uma versão específica do .NET Framework no Visual Studio no computador local.

- Você pode executar testes de unidade direcionados a uma versão específica do .NET Framework usando o *MSTest.exe* no prompt de comando.

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

## <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-visual-basic-unit-test-projects"></a>Redirecionando para uma versão específica do .NET Framework para projetos de teste de unidade do Visual Basic

1.  Crie um novo projeto de teste de unidade do Visual Basic. No menu **Arquivo**, escolha **Novo** e, em seguida, clique em **Projeto**.

     A caixa de diálogo **Novo Projeto** é exibida.

2.  Em **Modelos Instalados**, expanda **Visual Basic**. Selecione **Testar** e, em seguida, selecione o modelo de **Projeto de Teste**.

3.  Na caixa de texto **Nome**, digite um nome para o projeto de teste do Visual Basic e, em seguida, escolha **OK**.

4.  No **Gerenciador de Soluções**, escolha **Propriedades** no menu de atalho do novo projeto de teste do Visual Basic.

     As propriedades do seu projeto de teste do Visual Basic são exibidas.

5.  Na guia **Compilar** escolha **Opções de Compilação Avançadas** conforme mostrado na ilustração a seguir.

     ![Opções compiladas avançadas](../test/media/howtoconfigureunittest35frameworka.png)

6.  Use a lista suspensa **Estrutura de destino (todas as configurações)** para alterar a estrutura de destino para **.NET Framework 3.5** ou uma versão posterior, conforme mostrado no texto explicativo B na ilustração a seguir. Não especifique uma versão de cliente.

     ![Lista suspensa da estrutura de destino](../test/media/howtoconfigureunitest35frameworkstepb.png)

## <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-visual-c-unit-test-projects"></a>Redirecionando para uma versão específica do .NET Framework para projetos de teste de unidade do Visual C#

1.  Crie um novo projeto de teste de unidade do Visual C#. No menu **Arquivo**, escolha **Novo** e, em seguida, clique em **Projeto**.

     A caixa de diálogo **Novo Projeto** é exibida.

2.  Em **Modelos Instalados**, expanda **Visual C#**. Selecione **Testar** e, em seguida, selecione o modelo de **Projeto de Teste**.

3.  Na caixa de texto **Nome**, digite um nome para o projeto de teste do Visual C# e, em seguida, escolha **OK**.

4.  No **Gerenciador de Soluções**, escolha **Propriedades** no menu de atalho do novo projeto de teste do Visual C#.

     As propriedades do seu projeto de teste do Visual C# são exibidas.

5.  Na guia **Aplicativo**, escolha **Estrutura de destino**. Na lista suspensa, escolha **.NET Framework 3.5** ou uma versão posterior, conforme mostra a ilustração a seguir. Não especifique uma versão de cliente.

     ![Lista suspensa da estrutura de destino](../test/media/howtoconfigureunittest35frameworkcsharp.png)

## <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-ccli-unit-test-projects"></a>Redirecionando para uma versão específica do .NET Framework para projetos de teste de unidade do C++/da CLI

1.  Crie um novo projeto de teste de unidade do C++. No menu **Arquivo**, selecione **Novo** e, em seguida, clique em **Projeto**.

     A caixa de diálogo **Novo Projeto** é exibida.

    > [!WARNING]
    > Para compilar testes de unidade do C++/CLI para uma versão anterior do .NET Framework para o Visual C++, é necessário usar a versão correspondente do Visual Studio. Por exemplo, para direcionar para o .NET Framework 3.5, é necessário instalar o Visual Studio 2008 e o Visual Studio 2008 Service Pack 1.

2.  Em **Modelos Instalados**, expanda **Visual C++**. Selecione **Testar** e, em seguida, selecione o modelo de **Projeto de Teste**.

3.  Na caixa de texto **Nome**, digite um nome para o projeto de teste do Visual C++ e, em seguida, clique em **OK**.

4.  No **Gerenciador de Soluções**, escolha **Descarregar Projeto** do novo projeto de teste do Visual C++.

5.  No **Gerenciador de Soluções**, escolha o projeto de teste descarregado do Visual C++ e, em seguida, escolha **Editar \<nome do projeto>.vcxproj**.

     O arquivo *.vcxproj* é aberto no editor.

6.  Defina o `TargetFrameworkVersion` para a versão 3.5 ou posterior no `PropertyGroup` rotulado `"Globals"`. Não especifique uma versão de cliente:

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

7.  Salve e feche o arquivo *.vcxproj*.

8.  No **Gerenciador de Soluções**, escolha **Recarregar Projeto** no menu de atalho do novo projeto de teste do Visual C++.

## <a name="see-also"></a>Consulte também

- [Criar soluções do SharePoint](../sharepoint/create-sharepoint-solutions.md)
- [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [Caixa de diálogo Configurações avançadas do compilador (Visual Basic)](../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md)
