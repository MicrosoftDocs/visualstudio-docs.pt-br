---
title: Caixa de diálogo Configurações de Build Avançadas (C#)
ms.date: 06/20/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- cs.AdvancedBuildSettings
helpviewer_keywords:
- Build options [C#], advanced
ms.assetid: 141f2dee-1563-4ce6-ba37-32920b082519
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: cf4fd5b48dc3bfcfbfe1809eebe656a5b8f2079d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49928276"
---
# <a name="advanced-build-settings-dialog-box-c"></a>Caixa de diálogo Configurações de Build Avançadas (C#)

Use a caixa de diálogo **Configurações de Build Avançadas** do **Designer de Projeto** para especificar as propriedades de configuração de build avançadas do projeto. Essa caixa de diálogo se aplica somente a projetos [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)].

## <a name="general"></a>Geral

As opções a seguir permitem definir configurações gerais avançadas.

**Versão da Linguagem**

Especifica a versão da linguagem a ser usada. O conjunto de recursos é diferente em cada versão e, portanto, essa opção pode ser usada para forçar o compilador a permitir somente um subconjunto dos recursos implementados ou permitir somente os recursos compatíveis com um padrão existente. Essa configuração tem as seguintes opções:

- **default**

   Define a versão atual como destino.

- **ISO-1** e **ISO-2**

   Define como destino os recursos padrão ISO-1 e ISO-2, respectivamente.

- **C# [número de versão]**

   Define como destino uma versão específica do C#. Para obter mais informações, consulte [/langversion (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/langversion-compiler-option).

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

- **none**

   Especifica que nenhuma informação de depuração será gerada.

- **full**

   Permite anexar um depurador ao programa em execução.

- **pdbonly**

   Permite a depuração de código-fonte quando o programa é iniciado no depurador, mas apenas exibirá o assembler quando o programa em execução estiver anexado ao depurador.

-  **portátil**

   Produz um arquivo PDB, um arquivo de símbolo portátil e não específico da plataforma que fornece outras ferramentas, especialmente depuradores, informações sobre o que está no arquivo executável principal e como ele foi produzido. Consulte [PDB portátil](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md) para obter mais informações.

- **inserido**

   Incorpora informações de símbolo portátil no assembly. Nenhum arquivo PDB externo é produzido.

Para obter mais informações, consulte [/debug (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option).

**Alinhamento de Arquivo**

Especifica o tamanho das seções no arquivo de saída. Os valores válidos são **512**, **1024**, **2048**, **4096** e **8192**. Esses valores são medidos em bytes. Cada seção será alinhada em um limite que é um múltiplo desse valor, afetando o tamanho do arquivo de saída. Para obter mais informações, consulte [/filealign (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/filealign-compiler-option).

**Endereço básico da biblioteca**

Especifica o endereço básico preferencial no qual uma DLL será carregada. O endereço básico padrão para uma DLL é definido pelo Common Language Runtime de [!INCLUDE[dnprdnshort](../../code-quality/includes/dnprdnshort_md.md)]. Para obter mais informações, consulte [/baseaddress (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/baseaddress-compiler-option).

## <a name="see-also"></a>Consulte também

- [Opções do compilador de C#](/dotnet/csharp/language-reference/compiler-options/index)
- [Página de Build, Designer de Projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md)