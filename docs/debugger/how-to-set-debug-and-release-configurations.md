---
title: Definir configurações de depuração e versão | Microsoft Docs
ms.date: 10/05/2018
ms.topic: how-to
f1_keywords:
- vs.debug.builds
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- configurations, release
- build configurations, release
- projects [Visual Studio], release configurations
- debugging [Visual Studio], release configurations
- release builds, changing settings
- debug builds
- debug builds, switching to release build
- debug builds, changing configuration settings
- debugging [Visual Studio], debug configurations
- projects [Visual Studio], debug configurations
- build configurations, debug
- debug configurations
- release builds, switching to debug build
- Visual Basic projects, debug and release builds
ms.assetid: 57b6bbb7-f2af-48f7-8773-127d75034ed2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 458e6cb4ebf882d2d9e331823cc4955143e7d5b7
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349153"
---
# <a name="set-debug-and-release-configurations-in-visual-studio"></a>Definir configurações de depuração e versão no Visual Studio

Os projetos do Visual Studio têm configurações separadas de versão e depuração para seu programa. Você cria a versão de depuração para depuração e a versão de lançamento para a distribuição de versão final.

Em configuração de depuração, seu programa compila com informações de depuração simbólicas completas e sem otimização. A otimização complica a depuração, porque a relação entre o código fonte e as instruções geradas é mais complexa.

A configuração de versão do programa não tem informações de depuração simbólicas e é totalmente otimizada. Para código gerenciado e código C++, as informações de depuração podem ser geradas em arquivos. pdb, [dependendo das opções de compilador](#BKMK_symbols_release) usadas. A criação de arquivos. pdb pode ser útil se você precisar depurar a versão de lançamento posteriormente.

Para obter mais informações sobre configurações de build, consulte [Noções básicas sobre configurações de build](../ide/understanding-build-configurations.md).

Você pode alterar a configuração de Build no menu **Compilar** , na barra de ferramentas ou nas páginas de propriedades do projeto. As páginas de propriedades do projeto são específicas do idioma. O procedimento a seguir mostra como alterar a configuração de Build no menu e na barra de ferramentas. Para obter mais informações sobre como alterar a configuração de compilação em projetos em idiomas diferentes, consulte a seção [Consulte também](#see-also) abaixo.

## <a name="change-the-build-configuration"></a>Alterar a configuração da compilação

Para alterar a configuração da compilação, seja:

* No menu **Compilar** , selecione **Configuration Manager**e, em seguida, selecione **depurar** ou **liberar**.

ou

* Na barra de ferramentas, escolha **depurar** ou **liberar** na lista de **configurações da solução** .

  ![configuração da compilação de barras de ferramentas](../debugger/media/toolbarbuildconfiguration.png "ToolbarBuildConfiguration")

## <a name="generate-symbol-pdb-files-for-a-build-c-c-visual-basic-f"></a><a name="BKMK_symbols_release"></a>Gerar arquivos de símbolo (. pdb) para uma compilação (C#, C++, Visual Basic, F #)

Você pode optar por gerar arquivos de símbolo (. pdb) e quais informações de depuração incluir. Para a maioria dos tipos de projeto, o compilador gera arquivos de símbolo por padrão para compilações de depuração e versão, enquanto outras configurações padrão diferem por tipo de projeto e versão do Visual Studio.

> [!IMPORTANT]
> O depurador carregará apenas um arquivo .pdb para um arquivo executável que corresponde exatamente ao arquivo .pdb criado quando o executável foi compilado (isto é, o .pdb deve ser o original ou uma cópia do arquivo .pdb original). Para obter mais informações, consulte [por que o Visual Studio exige arquivos de símbolo do depurador para corresponder exatamente aos arquivos binários com os quais eles foram criados?](https://blogs.msdn.microsoft.com/jimgries/2007/07/06/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with/).

Cada tipo de projeto pode ter uma maneira diferente de definir essas opções.

### <a name="generate-symbol-files-for-a-c-aspnet-or-visual-basic-project"></a>Gerar arquivos de símbolo para um projeto em C#, ASP.NET ou Visual Basic

Para obter informações detalhadas sobre configurações de projeto para configurações de depuração em C# ou Visual Basic, consulte [configurações de projeto para uma configuração de depuração em c#](../debugger/project-settings-for-csharp-debug-configurations.md) ou [configurações de projeto para uma configuração de depuração de Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md).

1. No Gerenciador de Soluções, selecione o projeto.

2. Selecione o ícone de **Propriedades** (ou pressione **ALT + Enter**).

3. No painel lateral, escolha **Compilar** (ou **Compilar** em Visual Basic).

4. Na lista **configuração** , escolha **depurar** ou **liberar**.

5. Selecione o botão **avançado** (ou o botão **Opções avançadas de compilação** em Visual Basic).

6. Na lista **informações de depuração** (ou na lista **gerar informações de depuração** no Visual Basic), escolha **completo**, **somente PDB**ou **portátil**.

   O formato portátil é o formato de plataforma cruzada mais recente para o .NET Core. Para obter mais informações sobre opções, consulte [caixa de diálogo Configurações avançadas de compilação (C#)](../ide/reference/advanced-build-settings-dialog-box-csharp.md).

   ![Gerar PDBs para compilações em C #](../debugger/media/dbg_project_properties_pdb_csharp.png "GeneratePDBsForCSharp")

7. Compile o projeto.

   O compilador cria os arquivos de símbolo na mesma pasta que o executável ou o arquivo de saída principal.

### <a name="generate-symbol-files-for-a-c-project"></a>Gerar arquivos de símbolo para um projeto C++

1. No Gerenciador de Soluções, selecione o projeto.

2. Selecione o ícone de **Propriedades** (ou pressione **ALT + Enter**).

3. Na lista **configuração** , escolha **depurar** ou **liberar**.

4. No painel lateral, escolha **vinculador > depuração**e, em seguida, selecione opções para **gerar informações de depuração**.

   Para obter informações detalhadas sobre configurações de projeto para configurações de depuração em C++, consulte [configurações de projeto para uma configuração de depuração do c++](../debugger/project-settings-for-a-cpp-debug-configuration.md).

5. Configurar opções para **gerar arquivos de banco de dados do programa**.

   Na maioria dos projetos em C++, o valor padrão é `$(OutDir)$(TargetName).pdb` , que gera arquivos. pdb na pasta de saída.

   ![Gerar PDBs para Builds em C++](../debugger/media/dbg_project_properties_pdb_cplusplus.png "GeneratePDBsforCPlusPlus")

6. Compile o projeto.

   O compilador cria os arquivos de símbolo na mesma pasta que o executável ou o arquivo de saída principal.

## <a name="see-also"></a><a name="see-also"></a>Consulte também

- [Especificar arquivos de símbolo (. pdb) e arquivos de origem no depurador do Visual Studio](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)<br/>
- [Configurações e preparação do depurador](../debugger/debugger-settings-and-preparation.md)<br/>
- [Configurações do projeto para uma configuração de depuração do C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)<br/>
- [Configurações de projeto para uma configuração de depuração em C#](../debugger/project-settings-for-csharp-debug-configurations.md)<br/>
- [Configurações de projeto para uma configuração de depuração de Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)<br/>
- [Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md)
