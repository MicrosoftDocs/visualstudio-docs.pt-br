---
title: Como instalar o criador de perfil autônomo | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- performance tools, installing stand-alone profiler
- profiling tools, stand-alone profiler
ms.assetid: cae81c95-83cd-4ab6-8a98-84ef977a2f6d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 55c9e7c6ec4a34d59c45b2a56abedaa6d3fd2974
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942433"
---
# <a name="how-to-install-the-stand-alone-profiler"></a>Como instalar o criador de perfil autônomo
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] fornece uma linha de comando baseada no criador de perfil autônomo que pode ser executado sem instalar o IDE [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Essa situação ocorre quando um computador não tiver ou não puder ter um ambiente de desenvolvimento instalado. Por exemplo, você não deve instalar um ambiente de desenvolvimento em um servidor Web de produção.  
  
> [!NOTE]
>  Quando você está usando o criador de perfil autônomo para coletar dados de desempenho para um site ASP.NET, a ferramenta de linha de comando [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md) é recomendada em vez da [VSPerfCmd](../profiling/vsperfcmd.md).  
  
### <a name="to-install-the-stand-alone-profiler"></a>Para instalar o criador de perfil autônomo  
  
1. Localize o instalador do perfil autônomo (*vs_profiler.exe*) na mídia de instalação do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] no diretório que inclui o caminho *\Standalone Profiler* e execute-o.  
  
2. Adicione os caminhos para *vsintr.exe* e *msdis150.dll* ao caminho do sistema.  
  
   > [!NOTE]
   >  Na instalação padrão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], *vsinstr.exe* e *msdis150.dll* estão localizados em *\Program Files\Visual Studio 10\Team Tools\Performance Tools*.  
  
3. No prompt de comando, digite **VSInstr**.  
  
   > [!NOTE]
   >  Se as informações de uso para vsinstr.exe forem exibidas, tudo está configurado corretamente. Se você vir um erro que afirme vsinstr.exe ou uma de suas dependências não for encontrada, certifique-se de que você tenha seus caminhos configurados corretamente, conforme descrito na etapa 2.  
  
4. Configure o servidor de símbolos definindo sua variável **NT_SYMBOL_PATH** como **symsrv\*symsrv.dll\*c:\localcache\*http://msdl.microsoft.com/download/symbols**  
  
5. Depois de configurar o servidor de símbolo usando as variáveis de ambiente do sistema, execute as ferramentas do criador de perfil de linha de comando em um novo prompt de comando. Isso permite que as novas variáveis de ambiente entrem em vigor. Na janela de prompt de comando, digite o seguinte comando:  
  
    **start %COMSPEC%**  
  
   > [!NOTE]
   >  Para obter instruções detalhadas de como configurar o pacote do servidor de símbolos, confira [Como referenciar informações de símbolo do Windows](../profiling/how-to-reference-windows-symbol-information.md).  
  
6. Use a ferramenta [VSPerfReport](../profiling/vsperfreport.md) para serializar os símbolos no arquivo de dados (.vsp) de criação de perfil. Use a opção **VSPerfReport /summary:all /packsymbols**. Se você não tiver símbolos inseridos no arquivo de dados, certifique-se de que tenha o conjunto de variáveis de ambiente NT_SYMBOL_PATH.  
  
## <a name="see-also"></a>Consulte também  
 [Criar perfil usando a linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md)   
 [Passo a passo: criação de perfil de linha de comando usando amostragem](../profiling/walkthrough-command-line-profiling-using-sampling.md)   
 [Passo a passo: criação de perfil de linha de comando usando instrumentação](../profiling/walkthrough-command-line-profiling-using-instrumentation.md)   
 [Como referenciar informações de símbolo do Windows](../profiling/how-to-reference-windows-symbol-information.md)   
 [VSPerfReport](../profiling/vsperfreport.md)