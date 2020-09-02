---
title: Como especificar locais de arquivo de símbolo na linha de comando | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 8aa067bb-e8bf-4081-aff0-cfbcf65934a0
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: f9238c922b8adda3ce7d99571182d4b5ce91f35f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "85329023"
---
# <a name="how-to-specify-symbol-file-locations-from-the-command-line"></a>Como especificar locais de arquivo de símbolo por meio da linha de comando
Para exibir informações de símbolo como nomes de função e números de linha, a ferramenta de linha de comando VSPerfReport precisa ter acesso aos arquivos de símbolo (.*pdb*) dos componentes analisados e aos arquivos do sistema do Windows. Os arquivos de símbolo são criados quando um componente é compilado. Para obter mais informações, confira [VSPerfReport](../profiling/vsperfreport.md). A VSPerfReport procura arquivos de símbolo automaticamente nos seguintes locais:

- Caminhos especificados na opção **/SymbolPath** ou na variável de ambiente **_NT_SYMBOL_PATH**.

- O caminho local exato em que um componente foi compilado.

- O diretório que contém o arquivo de dados de criação de perfil (.*vsp* ou .*vsps*).

  A Microsoft fornece os arquivos .*pdb* online para muitos de seus produtos em um servidor de símbolos. Se o computador que você está usando para relatórios está conectado à Internet, a VSPerfReport conecta-se ao servidor do símbolos online para pesquisar informações de símbolo automaticamente e salvar os arquivos em um repositório local.

  Você pode especificar o local dos arquivos de símbolo e do repositório do servidor de símbolos da Microsoft das seguintes maneiras:

- Definir a variável de ambiente **_NT_SYMBOL_PATH**.

- Adicionar a opção **/SymbolPath** à linha de comando da VSPerfReport.

  Você também pode usar ambos os métodos.

> [!NOTE]
> Se o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] estiver instalado no computador local, um local para os arquivos de símbolo do Windows já foi provavelmente especificado. Para obter mais informações, confira [Como referenciar informações de símbolo do Windows](../profiling/how-to-reference-windows-symbol-information.md). Você ainda precisa configurar o VSPerfReport para que ele use o local e o servidor, conforme descrito mais adiante neste tópico.

## <a name="specify-windows-symbol-files"></a>Especificar arquivos de símbolo do Windows

#### <a name="to-configure-the-use-of-the-windows-symbol-server"></a>Para configurar o uso do servidor de símbolos do Windows

1. Se necessário, crie um diretório para armazenar localmente os arquivos de símbolo.

2. Use a sintaxe a seguir para definir a variável de ambiente **_NT_SYMBOL_PATH** ou a opção /SymbolPath da VSPerfReport:

    `srv*<LocalStore>*https://msdl.microsoft.com/download/symbols`

    em que *<LocalStore>* é o caminho do diretório local que você criou.

## <a name="specify-component-symbol-files"></a>Especificar arquivos de símbolo de componente
 As Ferramentas de Criação de Perfil pesquisam os arquivos .*pdb* dos componentes que você deseja analisar em seus locais originais, que são armazenados nos componentes ou na pasta que contém o arquivo de dados de criação de perfil. Você pode especificar outros locais para pesquisa, adicionando um ou mais caminhos à **_NT_SYMBOL_PATH** ou à opção **/SymbolPath**. Separe caminhos com ponto e vírgula.

## <a name="example"></a>Exemplo
 A linha de comando a seguir define a variável de ambiente **_NT_SYMBOL_PATH** para o servidor de símbolos do Windows e o diretório local para **C:\Symbols**.

 ```cmd
  set  _NT_SYMBOL_PATH=srv*C:\symbols*https://msdl.microsoft.com/download/symbols
 ```

 A linha de comando VSPerfReport a seguir adiciona o diretório *C:\Projects\Symbols* ao caminho de pesquisa usando a opção **/SymbolPath** .

 **VSPerfReport**  *MyApp* **.exe /SymbolPath:C:\Projects\Symbols /summary:all**
