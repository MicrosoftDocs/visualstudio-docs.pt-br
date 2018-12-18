---
title: Define a depuração e configurações de versão | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2018
ms.technology: vs-ide-debug
ms.topic: reference
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9a65a3331c210bdfb4143ff890180fdc7d663229
ms.sourcegitcommit: a7de99f36e9ead7ea9e9bac23c88d05ddfc38b00
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52257219"
---
# <a name="set-debug-and-release-configurations-in-visual-studio"></a>Define a depuração e configurações no Visual Studio de versão

Projetos do Visual Studio tem a versão separada e configurações para o seu programa de depuração. Você compila a versão de depuração para depuração e a versão de lançamento para a distribuição da versão final.

Na configuração de depuração, o seu programa é compilado com informações de depuração simbólica e sem otimização. A otimização complica a depuração, porque a relação entre o código fonte e as instruções geradas é mais complexa.

A configuração de versão do seu programa não tem nenhuma informação de depuração simbólica e é totalmente otimizada. Depurar informações podem ser geradas em arquivos. PDB [dependendo das opções de compilador](#BKMK_symbols_release) que são usados. Criar arquivos. PDB pode ser útil se você posteriormente precisa depurar a versão de lançamento.

Para obter mais informações sobre configurações de build, consulte [Noções básicas sobre configurações de build](../ide/understanding-build-configurations.md).

Você pode alterar a configuração de compilação a **Build** menu, na barra de ferramentas ou nas páginas de propriedades do projeto. Páginas de propriedades do projeto são específicas do idioma. O procedimento a seguir mostra como alterar a configuração de build no menu e barra de ferramentas. Para obter mais informações sobre como alterar a configuração de build em projetos em linguagens diferentes, consulte o [Consulte também](#see-also) seção abaixo.

## <a name="change-the-build-configuration"></a>Alterar a configuração de build

Para alterar a configuração de compilação, ou:

* Dos **Build** menu, selecione **Configuration Manager**, em seguida, selecione **depurar** ou **versão**.

ou

* Na barra de ferramentas, escolha **Debug** ou **Release** do **configurações da solução** lista.

  ![barras de ferramentas de configuração de build](../debugger/media/toolbarbuildconfiguration.png "ToolbarBuildConfiguration")

## <a name="BKMK_symbols_release"></a>Gerar arquivos de símbolo (. PDB) para uma compilação (C#, C++, Visual Basic, F#)

Você pode optar por gerar arquivos de símbolo (. PDB) e o que depurar informações a serem incluídas. Para a maioria dos tipos de projeto, o compilador gera arquivos de símbolo por padrão para depuração e builds de versão, enquanto outras configurações padrão diferem por tipo de projeto e a versão do Visual Studio.

> [!IMPORTANT]
> O depurador carregará apenas um arquivo .pdb para um arquivo executável que corresponde exatamente ao arquivo .pdb criado quando o executável foi compilado (isto é, o .pdb deve ser o original ou uma cópia do arquivo .pdb original). Para obter mais informações, consulte [por que o Visual Studio exige arquivos de símbolo do depurador para corresponder exatamente os arquivos binários que eles foram criados?](https://blogs.msdn.microsoft.com/jimgries/2007/07/06/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with/)

Cada tipo de projeto pode ter uma maneira diferente de como definir essas opções.

### <a name="generate-symbol-files-for-a-c-aspnet-or-visual-basic-project"></a>Gerar arquivos de símbolo para um projeto c#, ASP.NET ou Visual Basic

Para obter informações detalhadas sobre as configurações de projeto para configurações de depuração em c# ou Visual Basic, consulte [configuração de depuração de configurações do projeto para um c#](../debugger/project-settings-for-csharp-debug-configurations.md) ou [deconfiguraçãodedepuraçãodeconfiguraçõesdoprojetoparaumVisualBasic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md).

1. No Gerenciador de Soluções, selecione o projeto.

2. Selecione o **propriedades** ícone (ou pressione **Alt + Enter**).

3. No painel lateral, escolha **construir** (ou **compilar** no Visual Basic).

4. No **Configuration** , escolha **Debug** ou **versão**.

5. Selecione o **Advanced** botão (ou o **opções avançadas de compilação** botão no Visual Basic).

6. No **as informações de depuração** lista (ou o **gerar informações de depuração** lista no Visual Basic), escolha **completo**, **somente Pdb**, ou **Portátil**.

   O formato portátil é o formato de plataforma cruzada mais recente para o .NET Core. Para obter mais informações sobre as opções, consulte [caixa de diálogo Configurações avançadas de compilação (c#)](../ide/reference/advanced-build-settings-dialog-box-csharp.md).

   ![Gerar PDBs para compilações em c#](../debugger/media/dbg_project_properties_pdb_csharp.png "GeneratePDBsForCSharp")

7. Criar o projeto.

   O compilador cria o arquivo de símbolo (s) na mesma pasta que o executável ou o arquivo de saída principal.

### <a name="generate-symbol-files-for-a-c-project"></a>Gerar arquivos de símbolo para um projeto do C++

1. No Gerenciador de Soluções, selecione o projeto.

2. Selecione o **propriedades** ícone (ou pressione **Alt + Enter**).

3. No **Configuration** , escolha **Debug** ou **versão**.

4. No painel lateral, escolha **vinculador > Debugging**, em seguida, selecione opções para **gerar informações de depuração**.

   Para obter informações detalhadas sobre configurações do projeto para configurações de depuração em C++, consulte [configuração de depuração de configurações do projeto para um C++](../debugger/project-settings-for-a-cpp-debug-configuration.md).

5. Configurar as opções para **gerar arquivos de banco de dados do programa**.

   Na maioria dos projetos do C++, o valor padrão é `$(OutDir)$(TargetName).pdb`, que gera arquivos. PDB na pasta de saída.

   ![Gerar PDBs para compilações em C++](../debugger/media/dbg_project_properties_pdb_cplusplus.png "GeneratePDBsforCPlusPlus")

6. Criar o projeto.

   O compilador cria o arquivo de símbolo (s) na mesma pasta que o executável ou o arquivo de saída principal.

## <a name="see-also"></a>Consulte também
 
[Especificar arquivos de símbolo (. PDB) e arquivos de origem no depurador do Visual Studio](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)<br/>
[Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)<br/>
[Configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)<br/>
[Configurações do projeto para uma configuração de depuração do c#](../debugger/project-settings-for-csharp-debug-configurations.md)<br/>
[Definições do projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)<br/>
[Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md)
