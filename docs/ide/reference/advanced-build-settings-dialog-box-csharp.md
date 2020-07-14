---
title: Caixa de diálogo Configurações de Build Avançadas (C#)
ms.date: 08/05/2019
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- cs.AdvancedBuildSettings
helpviewer_keywords:
- Build options [C#], advanced
ms.assetid: 141f2dee-1563-4ce6-ba37-32920b082519
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 917ef4ff685c243fa271a0966a931151cb12ed2b
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418841"
---
# <a name="advanced-build-settings-dialog-box-c"></a>Caixa de diálogo Configurações avançadas de compilação (C#)

Use a caixa de diálogo **Configurações de Build Avançadas** do **Designer de Projeto** para especificar as propriedades de configuração de build avançadas do projeto. Essa caixa de diálogo se aplica somente a projetos C#.

## <a name="general"></a>Geral

As opções a seguir permitem definir configurações gerais avançadas.

**Versão do idioma**

::: moniker range=">=vs-2019"

Links para [/langversion (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/langversion-compiler-option), que fornece informações sobre como uma versão de idioma padrão é escolhida com base na estrutura de destino de um projeto.

::: moniker-end

::: moniker range="vs-2017"

Especifica a versão da linguagem a ser usada. O conjunto de recursos é diferente em cada versão e, portanto, essa opção pode ser usada para forçar o compilador a permitir somente um subconjunto dos recursos implementados ou permitir somente os recursos compatíveis com um padrão existente.

O valor padrão é C# 7,0.

::: moniker-end

**Relatório de erros do compilador interno**

Especifica se os erros do compilador são relatados à Microsoft. Se for definido como **prompt** (o padrão), você receberá um prompt se ocorrer um erro interno do compilador, fornecendo a opção de enviar um relatório de erro eletronicamente à Microsoft. Se for definido como **send**, um relatório de erros será enviado automaticamente. Se for definido como **queue**, relatórios de erros serão colocados na fila. Se for definido como **none**, o erro será relatado somente na saída de texto do compilador. Para obter mais informações, consulte [/errorreport (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/errorreport-compiler-option).

**Verificar estouro/estouro negativo aritmético**

Especifica se uma instrução de aritmética de números inteiros, que não está no escopo das palavras-chave [marcadas](/dotnet/csharp/language-reference/keywords/checked) ou [desmarcadas](/dotnet/csharp/language-reference/keywords/unchecked) e que resulta em um valor fora do intervalo do tipo de dados, causará uma exceção de tempo de execução. Para obter mais informações, consulte [/checked (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/checked-compiler-option).

**Não referenciar mscorlib.dll**

Especifica se mscorlib.dll será importado para o programa, definindo todo o namespace <xref:System>. Marque essa caixa se desejar definir ou criar seus próprios objetos e namespace <xref:System>. Para obter mais informações, consulte [/nostdlib (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/nostdlib-compiler-option).

## <a name="output"></a>Saída

As opções a seguir permitem especificar opções de saída avançadas.

**Informações de depuração**

Especifica o tipo de informações de depuração geradas pelo compilador. Para obter informações sobre como configurar o desempenho de depuração de um aplicativo, consulte [Facilitando a depuração de uma imagem](/dotnet/framework/debug-trace-profile/making-an-image-easier-to-debug). Essa configuração tem as seguintes opções:

- **nenhum**

   Especifica que nenhuma informação de depuração será gerada.

- **completo**

   Permite anexar um depurador ao programa em execução.

- **pdbonly**

   Permite a depuração de código-fonte quando o programa é iniciado no depurador, mas apenas exibirá o assembler quando o programa em execução estiver anexado ao depurador.

- **portátil**

   Produz um arquivo PDB, um arquivo de símbolo portátil e não específico da plataforma que fornece outras ferramentas, especialmente depuradores, informações sobre o que está no arquivo executável principal e como ele foi produzido. Consulte [PDB portátil](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md) para obter mais informações.

- **incorporado**

   Incorpora informações de símbolo portátil no assembly. Nenhum arquivo PDB externo é produzido.

Para obter mais informações, consulte [/debug (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option).

**Alinhamento de Arquivo**

Especifica o tamanho das seções no arquivo de saída. Os valores válidos são **512**, **1024**, **2048**, **4096**e **8192**. Esses valores são medidos em bytes. Cada seção será alinhada em um limite que é um múltiplo desse valor, afetando o tamanho do arquivo de saída. Para obter mais informações, consulte [/filealign (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/filealign-compiler-option).

**Endereço básico da biblioteca**

Especifica o endereço básico preferencial no qual uma DLL será carregada. O endereço básico padrão de uma DLL é definido pelo Common Language Runtime do .NET Framework. Para obter mais informações, consulte [/BaseAddress (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/baseaddress-compiler-option).

## <a name="see-also"></a>Veja também

- [Opções do compilador de C#](/dotnet/csharp/language-reference/compiler-options/index)
- [Página de compilação, designer de projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md)
