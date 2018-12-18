---
title: Ações de build para arquivos
ms.date: 11/19/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-compile
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5eb4c000973afd1eef92d283e5688862413add16
ms.sourcegitcommit: f61ad0e8babec8810295f039e67629f4bdebeef0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "52002112"
---
# <a name="build-actions"></a>Ações de Build

Todos os arquivos em um projeto do Visual Studio têm uma ação de build. A ação de build controla o que acontece com o arquivo quando o projeto é compilado.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Build actions in Visual Studio for Mac](/visualstudio/mac/build-actions) (Ações de build no Visual Studio para Mac).

## <a name="set-a-build-action"></a>Definir uma ação de build

Para definir a ação de build para um arquivo, abra as propriedades do arquivo na janela **Propriedades** selecionando o arquivo no **Gerenciador de Soluções** e pressionando **Alt**+**Enter**. Ou clique com o botão direito do mouse no arquivo no **Gerenciador de Soluções** e escolha **Propriedades**. Na janela **Propriedades**, na seção **Avançado**, use a lista suspensa ao lado de **Ação de Build** para definir uma ação de build para o arquivo.

![Ações de build para um arquivo no Visual Studio](media/build-actions.png)

## <a name="build-action-values"></a>Valores de ação de build

Algumas das ações de build para arquivos de projeto do C# e Visual Basic são:

* **Nenhuma** – o arquivo não faz parte do build de nenhuma maneira. Esse valor pode ser usado para arquivos de documentação como "Leiame", por exemplo.
* **Compilar** – O arquivo é passado para o compilador como um arquivo de origem.
* **Conteúdo** – Um arquivo marcado como **Conteúdo** pode ser recuperado como um fluxo chamando <xref:System.Windows.Application.GetContentStream%2A?displayProperty=nameWithType>. Para projetos ASP.NET, esses arquivos são incluídos como parte do site quando ele for implantado.
* **Recurso inserido** – O arquivo é passado para o compilador como um recurso a ser inserido no assembly. É possível chamar <xref:System.Reflection.Assembly.GetManifestResourceStream%2A?displayProperty=fullName> para ler o arquivo do assembly.
* **AdditionalFiles** – Um arquivo de texto que não seja de origem passado para o compilador do C# ou do Visual Basic como entrada. Essa ação de build é usada principalmente para fornecer entradas para [analisadores](../code-quality/roslyn-analyzers-overview.md) referenciados por um projeto para verificar a qualidade do código. Para obter mais informações, confira [Usar arquivos adicionais](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Using%20Additional%20Files.md).

## <a name="see-also"></a>Consulte também

- [Opções do compilador do C#](/dotnet/csharp/language-reference/compiler-options/listed-alphabetically)
- [Opções do compilador do Visual Basic](/dotnet/visual-basic/reference/command-line-compiler/compiler-options-listed-alphabetically)
- [Ações de build (Visual Studio para Mac)](/visualstudio/mac/build-actions)