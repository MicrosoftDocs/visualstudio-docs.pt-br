---
title: Como suprimir avisos do compilador | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 31827b17-f933-413d-b28a-b19f903b64ca
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: aeb404c479edec5dec89f28e80584d435f5c370a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670651"
---
# <a name="how-to-suppress-compiler-warnings"></a>Como suprimir avisos do compilador

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode melhorar a organização de um log de build especificando um ou mais tipos de avisos do compilador que você não deseja que ele contenha. Por exemplo, você pode usar essa técnica para examinar algumas, mas não todas as informações que são geradas automaticamente ao definir o detalhamento do log de build como Normal, Detalhado ou Diagnóstico. Para obter mais informações sobre detalhes, consulte [como exibir, salvar e configurar arquivos de log de compilação](../ide/how-to-view-save-and-configure-build-log-files.md).

### <a name="to-suppress-specific-warnings-for-visual-c-or-f"></a>Para suprimir avisos específicos para o Visual C# ou F\#

1. No **Gerenciador de Soluções**, escolha o projeto no qual você deseja suprimir avisos.

2. Na barra de menus, escolha **Exibir**, **Páginas de Propriedade**.

3. Escolha a página **Build**.

4. Na caixa **Suprimir avisos**, especifique os códigos de erro dos avisos que deseja suprimir, separados por ponto e vírgula, e recompile a solução.

### <a name="to-suppress-specific-warnings-for-visual-c"></a>Para suprimir avisos específicos para o Visual C++

1. No **Gerenciador de Soluções**, escolha o projeto ou arquivo de origem no qual deseja suprimir avisos.

2. Na barra de menus, escolha **Exibir**, **Páginas de Propriedade**.

3. Escolha a categoria **Propriedades de Configuração**, escolha a categoria **C++** e escolha a página **Avançado**.

4. Execute uma das seguintes etapas:

    - Na caixa **Desabilita Avisos Específicos**, especifique os códigos de erro dos avisos que deseja suprimir, separados por ponto e vírgula.

    - Na caixa **Desabilita Avisos Específicos**, escolha **Editar** para exibir mais opções.

5. Escolha o botão **OK** e recompile a solução.

## <a name="suppressing-warnings-for-visual-basic"></a>Suprimindo avisos para o Visual Basic

Você pode ocultar avisos de compilador específicos para Visual Basic editando o arquivo .vbproj para o projeto. Você também pode usar a [Página Compilação, Designer de Projeto](../ide/reference/compile-page-project-designer-visual-basic.md) para suprimir os avisos por categoria. Para obter mais informações, consulte [Configurando avisos no Visual Basic](../ide/configuring-warnings-in-visual-basic.md).

#### <a name="to-suppress-specific-warnings-for-visual-basic"></a>Para suprimir avisos específicos para o Visual Basic

1. No **Gerenciador de Soluções**, escolha o projeto no qual você deseja suprimir avisos.

2. Na barra de menus, escolha **Projeto**, **Descarregar Projeto**.

3. No **Gerenciador de Soluções**, abra o menu de atalho do projeto Proxies e escolha **Editar**_ProjectName_**.vbproj**.

    O arquivo de projeto é aberto no editor de códigos.

4. Localize o elemento `<NoWarn></NoWarn>` na configuração de build com o qual você está compilando.

    A exemplo a seguir mostra o elemento `<NoWarn></NoWarn>` em negrito para a configuração de build de depuração em uma plataforma x86:

   ```xml
   <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x86' ">
       <PlatformTarget>x86</PlatformTarget>
       <DebugSymbols>true</DebugSymbols>
       <DebugType>full</DebugType>
       <Optimize>false</Optimize>
       <OutputPath>bin\Debug\</OutputPath>
       <DefineDebug>true</DefineDebug>
       <DefineTrace>true</DefineTrace>
       <ErrorReport>prompt</ErrorReport>
       <NoWarn></NoWarn>
       <WarningLevel>1</WarningLevel>
     </PropertyGroup>
   ```

5. Adicione um ou mais números de aviso como o valor do elemento `<NoWarn>`. Se você especificar vários números de aviso, separe-os com uma vírgula, como mostra o exemplo a seguir.

   ```xml
   <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x86' ">
       <PlatformTarget>x86</PlatformTarget>
       <DebugSymbols>true</DebugSymbols>
       <DebugType>full</DebugType>
       <Optimize>false</Optimize>
       <OutputPath>bin\Debug\</OutputPath>
       <DefineDebug>true</DefineDebug>
       <DefineTrace>true</DefineTrace>
       <ErrorReport>prompt</ErrorReport>
       <NoWarn>40059,42024</NoWarn>
       <WarningLevel>1</WarningLevel>
     </PropertyGroup>
   ```

6. Salve as alterações no arquivo .vbproj.

7. Na barra de menus, escolha **Projeto**, **Recarregar Projeto**.

8. Na barra de menus, escolha **Compilar**, **Recompilar Solução**.

    A janela **Saída** não mostra mais os avisos especificados.

   Para obter mais informações, consulte [/nowarn](https://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83).

## <a name="see-also"></a>Consulte Também

- [Passo a passo: criando um aplicativo](../ide/walkthrough-building-an-application.md)
- [Como exibir, salvar e configurar arquivos de log de compilação](../ide/how-to-view-save-and-configure-build-log-files.md)
- [Compilando e criando](../ide/compiling-and-building-in-visual-studio.md)
