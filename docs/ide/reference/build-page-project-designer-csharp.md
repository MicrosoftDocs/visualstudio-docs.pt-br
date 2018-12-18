---
title: Página de Build, Designer de Projeto (C#)
ms.date: 06/20/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesBuild
helpviewer_keywords:
- Build options [C#]
- Project Designer, Build page
ms.assetid: 77ff1bfc-d633-4634-ba29-9afdb6d7e362
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: b003b3f965ab4f3857e2a532ae715d99533aa8e7
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38783812"
---
# <a name="build-page-project-designer-c"></a>Página de Build, Designer de Projeto (C#)
Use a página **Compilar** do **Designer de Projeto** para especificar as propriedades de configuração de build do projeto. Essa página se aplica somente a projetos do [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)].

Para acessar a página **Build**, escolha um nó do projeto (não o nó **Solução**) no **Gerenciador de Soluções**. Em seguida, escolha **Exibir**, **Páginas de Propriedade** no menu. Quando o Designer de Projeto for exibido, escolha a guia **Build**.

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="configuration-and-platform"></a>Configuração e plataforma
As opções a seguir permitem selecionar a configuração e a plataforma a ser exibida ou modificada.

> [!NOTE]
> Com configurações de build simplificadas, o sistema do projeto determina se é necessário compilar uma versão de depuração ou de liberação. Portanto, essas opções não são exibidas. Para saber mais, consulte [Como definir configurações de depuração e versão](../../debugger/how-to-set-debug-and-release-configurations.md).

**Configuração** Especifica quais definições de configuração devem ser exibidas ou modificadas. As configurações podem ser **Ativa (Depuração)** (esse é o padrão), **Depuração**, **Versão** ou **Todas as Configurações**.

**Plataforma** Especifica quais configurações de plataforma devem ser exibidas ou modificadas. A configuração padrão é **Ativo (Qualquer CPU)**. É possível alterar a plataforma ativa usando o **Configuration Manager**. Para obter mais informações, consulte [Como criar e editar configurações](../../ide/how-to-create-and-edit-configurations.md).

## <a name="general"></a>Geral
As opções a seguir permitem definir várias configurações do compilador do C#.

**Símbolos de compilação condicional** Especifica os símbolos nos quais a compilação condicional deve ser executada. Separe os símbolos com um ponto-e-vírgula (";"). Para obter mais informações, consulte [/define (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/define-compiler-option).

**Definir constante DEBUG** Define DEBUG como um símbolo em todos os arquivos de código-fonte do aplicativo. Selecionar essa opção equivale a usar a opção de linha de comando `/define:DEBUG`.

**Definir constante TRACE** Define TRACE como um símbolo em todos os arquivos de código-fonte do aplicativo. Selecionar essa opção equivale a usar a opção de linha de comando `/define:TRACE`.

**Destino da plataforma** Especifica o processador de destino do arquivo de saída. Escolha **x86** para qualquer processador compatível com Intel de 32 bits, **x64** para qualquer processador compatível com Intel de 64 bits, **ARM** para processadores ARM ou **Qualquer CPU** para especificar que qualquer processador é aceitável. **Qualquer CPU** é o valor padrão para projetos, pois permite que o aplicativo seja executado em uma ampla variedade de hardwares.

Para obter mais informações, consulte [/platform (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/platform-compiler-option).

**Preferir 32 bits** Se a caixa de seleção **Preferir 32 bits** estiver marcada, o aplicativo será executado como um aplicativo de 32 bits em versões de 32 e 64 bits do Windows. Se a caixa de seleção estiver desmarcada, o aplicativo será executado como um aplicativo de 32 bits em versões de 32 bits do Windows e como um aplicativo de 64 bits em versões de 64 bits do Windows.

Se você executar um aplicativo como um aplicativo de 64 bits, o ponteiro duplicará de tamanho e poderão ocorrer problemas de compatibilidade com outras bibliotecas que são exclusivamente de 32 bits. É útil executar um aplicativo de 64 bits somente se ele precisa de mais de 4 GB de memória ou se as instruções de 64 bits fornecem uma melhoria de desempenho significativa.

Essa caixa de seleção estará disponível somente se todas as seguintes condições forem verdadeiras:

-   Na **Página Build**, a lista **Destino da plataforma** é definida com **Qualquer CPU**.

-   Na **Página Aplicativo**, a lista **Tipo de saída** especifica que o projeto é um aplicativo.

-   Na **Página Aplicativo**, a lista **Estrutura de destino** especifica o .NET Framework 4.5.


**Permitir código inseguro** Permite que o código que usa palavra-chave [unsafe](/dotnet/csharp/language-reference/keywords/unsafe) seja compilado. Para obter mais informações, consulte [/unsafe (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/unsafe-compiler-option).

**Otimizar código** Habilita ou desabilita as otimizações executadas pelo compilador para tornar o arquivo de saída menor, mais rápido e mais eficiente. Para obter mais informações, consulte [/optimize (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/optimize-compiler-option).

## <a name="errors-and-warnings"></a>Erros e Avisos
As configurações a seguir são usadas para configurar as opções de erro e de aviso para o processo de build.

**Nível de aviso** Especifica o nível a ser exibido para os avisos do compilador. Para obter mais informações, consulte [/warn (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/warn-compiler-option).

**Suprimir avisos** Bloqueia a capacidade do compilador de gerar um ou mais avisos. Separe vários números de aviso com uma vírgula ou um ponto-e-vírgula. Para obter mais informações, consulte [/nowarn (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/nowarn-compiler-option).

## <a name="treat-warnings-as-errors"></a>Tratar Avisos como Erros
As configurações a seguir são usadas para especificar quais avisos são tratados como erros. Selecione uma das opções a seguir para indicar em quais condições um erro é retornado quando o build recebe um aviso. Para obter mais informações, consulte [/warnaserror (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/warnaserror-compiler-option).

**Nenhum** Não trata nenhum aviso como erro.

**Avisos específicos** Trata os avisos especificados como erros. Separe vários números de aviso com uma vírgula ou um ponto-e-vírgula.

**Todos** Trata todos os avisos como erros.

## <a name="output"></a>Saída
As configurações a seguir são usadas para configurar as opções de saída para o processo de build.

**Caminho de saída** Especifica o local dos arquivos de saída da configuração deste projeto. Insira o caminho da saída do build nessa caixa ou escolha o botão **Procurar** para especificar um caminho. Observe que o caminho é relativo; se você inserir um caminho absoluto, ele será salvo como relativo. O caminho padrão é bin\Debug ou bin\Release\\.

Com configurações de build simplificadas, o sistema do projeto determina se é necessário compilar uma versão de depuração ou de liberação. O comando **Build** do menu **Depurar** (F5) colocará o build no local de depuração, independentemente do **Caminho de saída** você especificar. No entanto, o comando **Build** do menu **Build** o coloca no local especificado. Para obter mais informações, consulte [Understanding Build Configurations (Noções básicas sobre configurações de build)](../../ide/understanding-build-configurations.md).

**Arquivo da documentação XML** Especifica o nome de um arquivo no qual os comentários da documentação serão processados. Para obter mais informações, consulte [/doc (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/doc-compiler-option).

**Registrar para interoperabilidade COM** Indica que o aplicativo gerenciado vai expor um objeto COM (um COM Callable Wrapper) que permite que um objeto COM interaja com o aplicativo gerenciado. A propriedade **Tipo de saída** da [página Aplicativo](../../ide/reference/application-page-project-designer-visual-basic.md) do **Designer de Projeto** desse aplicativo deve ser definida como **Biblioteca de Classes** para que a propriedade **Registrar para a interoperabilidade COM** esteja disponível. Para obter uma classe de exemplo que pode ser incluída no aplicativo [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] e exposta como um objeto COM, consulte [Classe COM de exemplo](/dotnet/csharp/programming-guide/interop/example-com-class).

**Gerar o assembly de serialização** Especifica se o compilador usará o XML Serializer Generator Tool (Sgen.exe) para criar assemblies de serialização XML. Os assemblies de serialização poderão melhorar o desempenho da inicialização de <xref:System.Xml.Serialization.XmlSerializer> se você tiver usado essa classe para serializar os tipos no código. Por padrão, essa opção é definida como **Automático**, que especifica que os assemblies de serialização serão gerados apenas se você tiver usado <xref:System.Xml.Serialization.XmlSerializer> para codificar tipos no código em XML. **Desativado** especifica que os assemblies de serialização nunca devem ser gerados, independentemente de o código usar <xref:System.Xml.Serialization.XmlSerializer>. **Ativado** especifica que os assemblies de serialização sempre devem ser gerados. Os assemblies de serialização são chamados `TypeName`.XmlSerializers.dll. Para obter mais informações, consulte [Ferramenta Geradora de Serializador XML (Sgen.exe)](/dotnet/framework/serialization/xml-serializer-generator-tool-sgen-exe).

**Avançado** Clique para exibir a caixa de diálogo [Configurações de Build Avançadas (C#)](../../ide/reference/advanced-build-settings-dialog-box-csharp.md).

## <a name="see-also"></a>Consulte também

- [Referência de Propriedades do Projeto](../../ide/reference/project-properties-reference.md)
- [Opções do compilador de C#](/dotnet/csharp/language-reference/compiler-options/index)