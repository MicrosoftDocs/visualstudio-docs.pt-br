---
title: Sinalizadores de Command-Line do compilador VSCT | Microsoft Docs
description: O compilador de tabela de comandos do Visual Studio fornece opções de linha de comando para garantir a compilação bem-sucedida de arquivos. vsct.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, compiling
- command-table file compilation (VSCT files)
ms.assetid: 9dc6c33f-e6cf-4cf2-9b05-e8f7bfac1cfb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 20c078d65af6224c65c2c574471b046deaf0cc92
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069290"
---
# <a name="vsct-compiler-command-line-flags"></a>Sinalizadores de linha de comando do compilador VSCT
O compilador de tabela de comando do Visual Studio (VSCT) fornece opções de linha de comando para garantir a compilação bem-sucedida de arquivos. vsct.

## <a name="command-line-parameters"></a>Parâmetros de linha de comando
 Para exibir a ajuda básica do VSCT em uma janela de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **comando** , navegue até o *caminho de instalação do SDK do Visual Studio*\VisualStudioIntegration\Tools\Bin\ pasta e digite:

```
vsct /?
```

 Isso retorna:

```
Microsoft (R) Visual Studio (R) Command Table Compiler Version 3.00.2000

Syntax: vsct <infile> [<outfile>] [-S[symbols file]] [-D<preprocessor-define>]*
[-I<include-path>]* [-L<language>] [-E[C|H|N]:<name>]

  -D    Specify any additional preprocessor defines
  -I    Indicate what additional include paths to send to the preprocessor
  -L    Specify the language to use when selecting strings
  -E    Emit C# objects in the specified namespace for command items,
        followed by [L|F|H|N]:<value>
        F = Name of the file to emit (used if -EL is provided)
        L = Name of a language providing a CodeDOM provider
        N = namespace (required if -EL is provided)
        H = C++ header
  -c    Clean build skipping dependency checks
  -v    Verbose output
```

> [!NOTE]
> Os caracteres-(traço) e/(barra invertida) são notação aceita para indicar os parâmetros de linha de comando.

 Os sinalizadores aceitáveis e o que significam são os seguintes.

|Opção|Descrição|
|------------|-----------------|
|-d|Especifique quaisquer símbolos definidos adicionais.|
|-I|Indique os caminhos de inclusão adicionais que devem ser usados ao resolver referências de arquivo.|
|-l|Especifique o <xref:System.Globalization.CultureInfo> nome da cultura, por exemplo, "en-US".|
|-E|Emita objetos C# no namespace especificado para itens de comando, seguidos de [C&#124;H&#124;N]:*nome de arquivo* em que C = C#, h = cabeçalho C++, N = namespace. O namespace é necessário para C#.|
|-v|Saída detalhada.|

 A opção-L instrui o compilador a selecionar um grupo de cadeias de caracteres para produzir o arquivo binário. CTO que corresponde ao <xref:System.Globalization.CultureInfo> nome de cultura fornecido. O nome de cultura especificado deve corresponder ao atributo de idioma de um ou mais [elementos de cadeia de caracteres](../../extensibility/strings-element.md) no arquivo. vsct. Se um elemento de cadeia de caracteres não tiver nenhum atributo language, ele será herdado do [elemento commandtable](../../extensibility/commandtable-element.md)que o contém.

 Um arquivo. vsct pode ter vários elementos de cadeia de caracteres e cada um deles pode ter um atributo de idioma diferente. A globalização é obtida executando o compilador VSCT várias vezes e alterando a opção-L para cada nome de cultura.

 Se o nome de cultura fornecido pela opção-L não corresponder ao atributo language de qualquer elemento de cadeia de caracteres, o compilador tentará corresponder ao idioma e não à região. Por exemplo, se "en-US" não for encontrado, o compilador tentará "en" em vez disso. Falhando, ele tentará a cultura atual do sistema operacional. Falhando, ele compilará o primeiro elemento de cadeia de caracteres que encontrar.

 A opção-E pode ser usada para emitir um arquivo de cabeçalho em estilo C que contém os símbolos que são usados pela tabela de comandos ou para emitir um arquivo C# que contém objetos para os símbolos de comando.

 As opções-D e-I têm a sintaxe dos sinalizadores de pré-processador do Cl.exe C que têm o mesmo nome. -D as definições que têm o formato X = Y são usadas para a expansão de testes baseados em XML \<Defined> em `Condition` atributos. -I inclui caminhos que são usados para \<Include> resolver \<Extern> e \<Bitmap> referências de arquivo. Para obter mais informações, consulte a [referência de esquema XML do vsct](../../extensibility/vsct-xml-schema-reference.md).

 O compilador VSCT também pode descompilar um arquivo binário compilado anteriormente. Para fazer isso, forneça um arquivo binário para o \<infile> .   Se o arquivo binário foi produzido pelo compilador VSCT, ele terá seus símbolos já inseridos e produzirá a saída com os nomes simbólicos em uma \<Symbols> seção da saída. Se o binário foi produzido pelo compilador CTC, a saída conterá os GUIDs e as IDs reais. Se o arquivo *. ctsym produzido pelas versões atuais do Ctc.exe estiver na mesma pasta que o arquivo de entrada binário, os símbolos serão carregados desse arquivo e usados para saída.

## <a name="see-also"></a>Confira também
- [Arquivos .Vsct (Visual Studio Command Table)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [Referência do esquema XML do VSCT](../../extensibility/vsct-xml-schema-reference.md)
- [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
