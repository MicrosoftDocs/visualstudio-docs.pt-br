---
title: Sinalizadores de Command-Line VSCT | Microsoft Docs
description: O Visual Studio compilador de Tabela de Comando fornece opções de linha de comando para garantir a compilação bem-sucedida de arquivos .vsct.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT files, compiling
- command-table file compilation (VSCT files)
ms.assetid: 9dc6c33f-e6cf-4cf2-9b05-e8f7bfac1cfb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ce83df56e1bcfad50fe71da31291b5c43b26c47a
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898881"
---
# <a name="vsct-compiler-command-line-flags"></a>Sinalizadores de linha de comando do compilador VSCT
O compilador Visual Studio VSCT (Tabela de Comando) fornece opções de linha de comando para garantir a compilação bem-sucedida de arquivos .vsct.

## <a name="command-line-parameters"></a>Parâmetros de linha de comando
 Para exibir a ajuda básica do VSCT em uma janela Comando, navegue até o caminho de instalação do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]  *SDK* do Visual Studio \VisualStudioIntegration\Tools\Bin\ pasta e digite:

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
> Os caracteres – (traço) e /(barra) são ambas notação aceita para indicar parâmetros de linha de comando.

 Sinalizadores aceitáveis e o que eles significam são os a seguir.

|Opção|Descrição|
|------------|-----------------|
|-d|Especifique quaisquer símbolos definidos adicionais.|
|-I|Indique os caminhos de inclusão adicionais que devem ser usados ao resolver referências de arquivo.|
|-l|<xref:System.Globalization.CultureInfo>Especifique o nome da cultura, por exemplo "en-US".|
|-E|Emita objetos C# no namespace especificado para itens de comando, seguidos por [C&#124;H&#124;N]:*nome* do arquivo em que C = C#, H = C++ header, N = namespace. O namespace é necessário para C#.|
|-v|Saída detalhada.|

 A opção -L instrui o compilador a selecionar um grupo de cadeias de caracteres para produzir o arquivo .cto binário que corresponde ao nome <xref:System.Globalization.CultureInfo> de cultura determinado. O nome de cultura especificado deve corresponder ao atributo Language de um ou mais Elementos [strings](../../extensibility/strings-element.md) no arquivo .vsct. Se um elemento Strings não tiver nenhum atributo Language, ele será herdado do elemento [CommandTable que contém](../../extensibility/commandtable-element.md).

 Um arquivo .vsct pode ter vários elementos Strings e cada um pode ter um atributo Language diferente. A globalização é alcançada executando o compilador VSCT várias vezes e alterando a opção -L para cada nome de cultura.

 Se o nome da cultura dado pela opção -L não corresponder ao atributo Language de qualquer elemento Strings, o compilador tentará corresponder ao idioma e não à região. Por exemplo, se "en-US" não puder ser encontrado, o compilador tentará "en". Se isso não ocorrer, ele tentará a cultura atual do sistema operacional. Se isso não ocorrer, ele compila o primeiro elemento Strings encontrado.

 A opção -E pode ser usada para emitir um arquivo de título de estilo C que contém os símbolos usados pela tabela de comando ou para emitir um arquivo C# que contém objetos para os símbolos de comando.

 As opções -D e -I têm a sintaxe dos sinalizadores de pré-processador Cl.exe C que têm o mesmo nome. As definições de -D que têm o formato X=Y são usadas para a expansão de testes baseados em XML \<Defined> em `Condition` atributos. -Os caminhos de inclusão são usados para resolver \<Include> as referências de arquivo e \<Extern> \<Bitmap> . Para obter mais informações, consulte a Referência [de esquema XML do VSCT.](../../extensibility/vsct-xml-schema-reference.md)

 O compilador do VSCT também pode descompilar um arquivo binário compilado anteriormente. Para fazer isso, fornece um arquivo binário para o \<infile> .   Se o arquivo binário tiver sido produzido pelo compilador VSCT, ele terá seus símbolos já inseridos e produzirá a saída com os nomes simbólicos em uma seção \<Symbols> da saída. Se o binário tiver sido produzido pelo compilador CTC, a saída conterá os GUIDs e as IDs reais. Se o arquivo *.ctsym produzido pelas versões atuais do Ctc.exe estiver na mesma pasta que o arquivo de entrada binário, os símbolos serão carregados desse arquivo e usados para saída.

## <a name="see-also"></a>Confira também
- [Arquivos .Vsct (Visual Studio Command Table)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [Referência do esquema XML do VSCT](../../extensibility/vsct-xml-schema-reference.md)
- [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
