---
title: Como configurar testes de unidade para direcionar a uma versão anterior do .NET Framework | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: adb6c011-5abd-41d2-8ead-08cd7579bf37
caps.latest.revision: 14
ms.author: gewarren
manager: douge
ms.openlocfilehash: 978f4e3edeb83d5980d793d74cf209e8e8f7205e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49892779"
---
# <a name="how-to-configure-unit-tests-to-target-an-earlier-version-of-the-net-framework"></a>Como configurar testes de unidade para direcionar uma versão anterior do .NET Framework
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você cria um projeto de teste no Microsoft Visual Studio, a versão mais recente do .NET Framework é definida como destino, por padrão. Além disso, se você atualizar projetos de teste de versões anteriores do Visual Studio, eles são atualizados para destinar-se à versão mais recente do .NET Framework. Ao editar as propriedades do projeto, é possível redirecionar explicitamente o projeto para versões anteriores do .NET Framework.  
  
 Você pode criar projetos de teste de unidade que se destinam a versões específicas do .NET Framework. A versão de destino deve ser 3.5 ou posterior e não pode ser uma versão de cliente. O Visual Studio permite o seguinte suporte básico para testes de unidade que se direcionam a versões específicas:  
  
- Você pode criar projetos de teste de unidade e destiná-las a uma versão específica do .NET Framework.  
  
- Você pode executar testes de unidade direcionados a uma versão específica do .NET Framework no Visual Studio no computador local.  
  
- Você pode executar testes de unidade direcionados a uma versão específica do .NET Framework usando o MSTest.exe no prompt de comando.  
  
- Você pode executar testes de unidade em um agente de build como parte de um build.  
  
  **Testar aplicativos de SharePoint**  
  
  Os recursos listados acima também permitem gravar testes de unidade e testes de integração de aplicativos do SharePoint usando o Visual Studio. [!INCLUDE[crabout](../includes/crabout-md.md)] como desenvolver aplicativos do SharePoint usando o Visual Studio, consulte [Criar soluções do SharePoint](http://msdn.microsoft.com/library/4bfb1e59-97c9-4594-93f8-3068b4eb9631), [Criação e depuração de soluções do SharePoint](http://msdn.microsoft.com/library/c9e7c9ab-4eb3-40cd-a9b9-6c2a896f70ae) e [Verificando e depurando o código do SharePoint](http://msdn.microsoft.com/library/b5f3bce2-6a51-41b1-a292-9e384bae420c).  
  
  **Limitações**  
  
  As seguintes limitações se aplicam quando você redireciona projetos de teste para usar versões anteriores do .NET Framework:  
  
- No .NET Framework 3.5, há suporte para multiplataforma para projetos de teste que contenham somente testes de unidade. O .NET Framework 3.5 não oferece suporte a nenhum outro tipo de teste, como o teste de carga ou teste da interface do usuário codificada. O redirecionamento está bloqueado para tipos de teste diferentes de testes de unidade.  
  
- A execução de testes que são destinados a uma versão anterior do .NET Framework só tem suporte no adaptador do host padrão. Não há suporte no adaptador do host do ASP.NET. Os aplicativos ASP.NET que precisam ser executados no contexto do ASP.NET Development Server devem ser compatíveis com a versão atual do .NET Framework.  
  
- O suporte à coleta de dados é desabilitado quando você executa testes que oferecem suporte a multiplataforma do .NET Framework 3.5. Você pode executar a cobertura de código usando as ferramentas de linha de comando do Visual Studio.  
  
- Não é possível executar testes de unidade que usam o .NET Framework 3.5 em um computador remoto.  
  
- Você não pode direcionar testes de unidade a versões de cliente anteriores do Framework.  
  
### <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-visual-basic-unit-test-projects"></a>Redirecionar para uma versão específica do .NET Framework para projetos de teste de unidade do Visual Basic  
  
1.  Crie um novo projeto de teste de unidade do Visual Basic. No menu **Arquivo**, escolha **Novo** e, em seguida, clique em **Projeto**.  
  
     A caixa de diálogo **Novo Projeto** é exibida.  
  
2.  Em **Modelos Instalados**, expanda **Visual Basic**. Selecione **Testar** e, em seguida, selecione o modelo de **Projeto de Teste**.  
  
3.  Na caixa de texto **Nome**, digite um nome para o projeto de teste do Visual Basic e, em seguida, escolha **OK**.  
  
4.  No Gerenciador de Soluções, escolha **Propriedades** no menu de atalho do novo projeto de teste do Visual Basic.  
  
     As propriedades do seu projeto de teste do Visual Basic são exibidas.  
  
5.  Na guia **Compilar** escolha **Opções de Compilação Avançadas** conforme mostrado na ilustração a seguir.  
  
     ![Opções de compilação Avançadas](../test/media/howtoconfigureunittest35frameworka.png "HowToConfigureUnitTest35FrameworkA")  
  
6.  Use a lista suspensa **Estrutura de destino (todas as configurações)** para alterar a estrutura de destino para **.NET Framework 3.5** ou uma versão posterior, conforme mostrado no texto explicativo B na ilustração a seguir. Não especifique uma versão de cliente.  
  
     ![Lista de lista suspensa de estrutura de destino](../test/media/howtoconfigureunitest35frameworkstepb.png "HowToConfigureUniTest35FrameworkStepB")  
  
### <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-visual-c-unit-test-projects"></a>Redirecionar para uma versão específica do .NET Framework para projetos de teste de unidade do Visual C#  
  
1.  Crie um novo projeto de teste de unidade do Visual C#. No menu **Arquivo**, escolha **Novo** e, em seguida, clique em **Projeto**.  
  
     A caixa de diálogo **Novo Projeto** é exibida.  
  
2.  Em **Modelos Instalados**, expanda **Visual C#**. Selecione **Testar** e, em seguida, selecione o modelo de **Projeto de Teste**.  
  
3.  Na caixa de texto **Nome**, digite um nome para o projeto de teste do Visual C# e, em seguida, escolha **OK**.  
  
4.  No Gerenciador de Soluções, escolha **Propriedades** no menu de atalho do seu novo projeto de teste do Visual C#.  
  
     As propriedades do seu projeto de teste do Visual C# são exibidas.  
  
5.  Na guia **Aplicativo** escolha **Estrutura de destino** e, em seguida, escolha **.NET Framework 3.5** ou uma versão posterior na lista suspensa para alterar a estrutura de destino conforme mostrado na ilustração a seguir. Não especifique uma versão de cliente.  
  
     ![Lista de lista suspensa de estrutura de destino](../test/media/howtoconfigureunittest35frameworkcsharp.png "HowToConfigureUnitTest35FrameworkCSharp")  
  
### <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-ccli-unit-test-projects"></a>Redirecionar para uma versão específica do .NET Framework para projetos de teste de unidade do C++/CLI  
  
1.  Crie um novo projeto de teste de unidade do C++. No menu **Arquivo**, selecione **Novo** e, em seguida, clique em **Projeto**.  
  
     A caixa de diálogo **Novo Projeto** é exibida.  
  
    > [!WARNING]
    >  Para compilar testes de unidade do C++/CLI para uma versão anterior do .NET Framework para o Visual C++, é necessário usar a versão correspondente do Visual Studio. Por exemplo, para direcionar para o .NET Framework 3.5, é necessário instalar o [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] e o [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] Service Pack 1.  
  
2.  Em **Modelos Instalados**, expanda **Visual C++**. Selecione **Testar** e, em seguida, selecione o modelo de **Projeto de Teste**.  
  
3.  Na caixa de texto **Nome**, digite um nome para o projeto de teste do Visual C++ e, em seguida, clique em **OK**.  
  
4.  No Gerenciador de Soluções, escolha **Descarregar Projeto** do seu novo projeto de teste do Visual C++.  
  
5.  No Gerenciador de Soluções, escolha o projeto de teste descarregado do Visual C++ e, em seguida, escolha **Editar \<nome do projeto>.vcxproj**.  
  
     O arquivo .vcxproj é aberto no editor.  
  
6.  Defina o `TargetFrameworkVersion` para a versão 3.5 ou posterior no `PropertyGroup` rotulado `"Globals"`. Não especifique uma versão de cliente:  
  
    ```  
    <PropertyGroup Label="Globals">  
        <TargetName>DefaultTest</TargetName>  
        <ProjectTypes>{3AC096D0-A1C2-E12C-1390-A8335801FDAB};{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}</ProjectTypes>  
        <ProjectGUID>{CE16D77A-E364-4ACD-948B-1EB6218B0EA3}</ProjectGUID>  
        <TargetFrameworkVersion>3.5</TargetFrameworkVersion>  
        <Keyword>ManagedCProj</Keyword>  
        <RootNamespace>CPP_Test</RootNamespace>  
      </PropertyGroup>  
  
    ```  
  
7.  Salve e feche o arquivo .vcxproj.  
  
8.  No Gerenciador de Soluções, escolha **Recarregar Projeto** no menu de atalho do seu novo projeto de teste do Visual C++.  
  
## <a name="see-also"></a>Consulte também  
 [Criar e Executar Testes de Unidade para Código Existente](http://msdn.microsoft.com/en-us/e8370b93-085b-41c9-8dec-655bd886f173)   
 [Criar soluções do SharePoint](http://msdn.microsoft.com/library/4bfb1e59-97c9-4594-93f8-3068b4eb9631)   
 [Compilando e depurando soluções do SharePoint](http://msdn.microsoft.com/library/c9e7c9ab-4eb3-40cd-a9b9-6c2a896f70ae)   
 [Caixa de diálogo Configurações de Compilador Avançadas (Visual Basic)](../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md)



