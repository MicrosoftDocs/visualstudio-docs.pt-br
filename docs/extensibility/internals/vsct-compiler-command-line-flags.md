---
title: Sinalizadores de linha de comando do compilador VSCT | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, compiling
- command-table file compilation (VSCT files)
ms.assetid: 9dc6c33f-e6cf-4cf2-9b05-e8f7bfac1cfb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 0cdf74d0c6c77a2c7c22829c8aaa3e238e65703a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51744884"
---
# <a name="vsct-compiler-command-line-flags"></a>Sinalizadores de linha de comando do compilador VSCT
O compilador de tabela de comando do Visual Studio (VSCT) fornece opções de linha de comando para garantir que a compilação bem-sucedida dos arquivos. VSCT.  
  
## <a name="command-line-parameters"></a>Parâmetros de linha de comando  
 Para exibir a Ajuda básica do VSCT de um [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **comando** janela, navegue até a *caminho de instalação do SDK do Visual Studio*\VisualStudioIntegration\Tools\Bin\ pasta e digite:  
  
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
>  Os caracteres - (traço) e / (barra) são ambas as notação aceito para que indica que os parâmetros de linha de comando.  
  
 Sinalizadores aceitáveis e seus significados são da seguinte maneira.  
  
|Alternar|Descrição|  
|------------|-----------------|  
|-D|Especifique todos os símbolos definidos adicionais.|  
|-I|Indicam que caminhos que devem ser usados ao resolver referências de arquivo de inclusão adicionais.|  
|-L|Especifique o <xref:System.Globalization.CultureInfo> nome de cultura, por exemplo "en-US".|  
|-E|Emitir C# objetos no namespace especificado para os itens de comando, seguido por [C&#124;H&#124;N]:*filename*em que C = C#, H = cabeçalho de C++, N = namespace. O namespace é necessário para c#.|  
|-v|Saída detalhada.|  
  
 -L switch instrui o compilador a selecionar um grupo de cadeias de caracteres para produzir o arquivo CTO já binário correspondente para o determinado <xref:System.Globalization.CultureInfo> nome da cultura. O nome da cultura especificada com o atributo de idioma de um ou mais [cadeias de caracteres de elemento](../../extensibility/strings-element.md) no arquivo. VSCT. Se um elemento de cadeias de caracteres não tem nenhum atributo de idioma, ela é herdada de recipiente [elemento CommandTable](../../extensibility/commandtable-element.md).  
  
 Um arquivo. VSCT pode ter vários elementos de cadeias de caracteres, e cada um pode ter um atributo de idioma diferente. Globalização é obtida executando o compilador VSCT várias vezes e alterando a opção – L para cada nome de cultura.  
  
 Se o nome de cultura fornecido pelo comutador -L não coincide com o atributo de idioma de qualquer elemento de cadeias de caracteres, o compilador tentará corresponder o idioma e não a região. Por exemplo, se não podem ser encontrado "en-US", o compilador tentará "en" em vez disso. Caso de falha, ele tentará a cultura atual do sistema operacional. Caso de falha, ele compilará o primeiro elemento de cadeias de caracteres que encontrar.  
  
 A opção -E pode ser usada para emitir um arquivo de cabeçalho de estilo C que contém os símbolos que são usados pela tabela de comando ou para emitir um arquivo c# que contém objetos para os símbolos de comando.  
  
 -D e - I switches têm a sintaxe dos sinalizadores de pré-processador C Cl.exe que têm o mesmo nome. -D definições que têm o formato X = Y são usadas para a expansão do baseado em XML \<definido pelo > testes no `Condition` atributos. -I incluir caminhos são usados para resolver \<Include >, \<Extern > e \<Bitmap > as referências de arquivo. Para obter mais informações, consulte o [referência de esquema de XML do VSCT](../../extensibility/vsct-xml-schema-reference.md).  
  
 O compilador VSCT também pode descompilar um arquivo binário compilado anteriormente. Para fazer isso, forneça um arquivo binário para o \<infile >.   Se o arquivo binário foi produzido pelo compilador VSCT, ele terá seus símbolos já inseridos e produzirá a saída com os nomes simbólicos em uma \<símbolos > seção da saída. Se o binário foi produzido pelo compilador CTC, a saída conterá os GUIDs e IDs de real. Se o arquivo de *.ctsym que é produzido por versões atuais do Ctc.exe estiver na mesma pasta que o arquivo binário de entrada, os símbolos serão carregados do arquivo e usados para a saída.  
  
## <a name="see-also"></a>Consulte também  
 [Tabela de comando do Visual Studio (. Arquivos de VSCT)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [Referência de esquema XML do VSCT](../../extensibility/vsct-xml-schema-reference.md)   
 [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)