---
title: Como instalar o criador de perfil autônomo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- performance tools, installing stand-alone profiler
- profiling tools, stand-alone profiler
ms.assetid: cae81c95-83cd-4ab6-8a98-84ef977a2f6d
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 950927510d4c7acd77db22e80dff59946c0d6c20
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330140"
---
# <a name="how-to-install-the-stand-alone-profiler"></a>Como instalar o criador de perfil autônomo
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] fornece uma linha de comando baseada no criador de perfil autônomo que pode ser executado sem instalar o IDE [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Essa situação ocorre quando um computador não tiver ou não puder ter um ambiente de desenvolvimento instalado. Por exemplo, você não deve instalar um ambiente de desenvolvimento em um servidor Web de produção.

> [!NOTE]
> Quando você está usando o criador de perfil autônomo para coletar dados de desempenho para um site ASP.NET, a ferramenta de linha de comando [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md) é recomendada em vez da [VSPerfCmd](../profiling/vsperfcmd.md).

### <a name="to-install-the-stand-alone-profiler"></a>Para instalar o criador de perfil autônomo

1. Baixe as [Ferramentas de Desempenho do Visual Studio](https://visualstudio.microsoft.com/downloads/?q=performance+tools#performance-tools-for-visual-studio).

1. Localize o instalador do perfil independente (*vs_standaloneprofiler.exe*) no qual você baixou as ferramentas de desempenho e execute-o.

2. Adicione o caminho para *vsinstr.exe* ao caminho do sistema.

   > [!NOTE]
   > Para obter o caminho para as ferramentas de criação de perfil, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md). Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de Prompt de Comando ou adicioná-lo ao próprio comando.

3. No prompt de comando, digite **VSInstr**.

   > [!NOTE]
   > Se as informações de uso para vsinstr.exe forem exibidas, tudo está configurado corretamente. Se você vir um erro que afirme vsinstr.exe ou uma de suas dependências não for encontrada, certifique-se de que você tenha seus caminhos configurados corretamente, conforme descrito na etapa 2.

4. Configure o servidor de símbolos definindo sua variável **NT_SYMBOL_PATH** como **symsrv\*symsrv.dll\*c:\localcache\*https://msdl.microsoft.com/download/symbols**

5. Depois de configurar o servidor de símbolo usando as variáveis de ambiente do sistema, execute as ferramentas do criador de perfil de linha de comando em um novo prompt de comando. Isso permite que as novas variáveis de ambiente entrem em vigor. Na janela de prompt de comando, digite o seguinte comando:

    **start %COMSPEC%**

   > [!NOTE]
   > Para obter instruções detalhadas sobre como configurar o pacote do servidor de símbolos, consulte [como fazer referência a informações de símbolo do Windows](../profiling/how-to-reference-windows-symbol-information.md).

6. Use a ferramenta [VSPerfReport](../profiling/vsperfreport.md) para serializar os símbolos no arquivo de dados (.vsp) de criação de perfil. Use a opção **VSPerfReport /summary:all /packsymbols**. Se você não tiver símbolos inseridos no arquivo de dados, certifique-se de que tenha o conjunto de variáveis de ambiente NT_SYMBOL_PATH.

## <a name="see-also"></a>Veja também
- [Criar perfil da linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md)
- [Walkthrough: criação de perfil de linha de comando usando instrumentação](command-line-profiling-of-stand-alone-applications.md)
- [Como: consultar informações de símbolo do Windows](../profiling/how-to-reference-windows-symbol-information.md)
- [VSPerfReport](../profiling/vsperfreport.md)
