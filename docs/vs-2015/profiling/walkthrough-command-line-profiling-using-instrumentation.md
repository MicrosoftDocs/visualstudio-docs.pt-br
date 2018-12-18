---
title: 'Passo a passo: Criação de perfil de linha de comando usando instrumentação | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- profiling tools, walkthroughs
- performance tools, walkthroughs
- performance tools, command-line tools
ms.assetid: 1c6f1586-3d6a-431f-bedf-c54088e280ba
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1b670ef29ca2edcc96ed8886b82dd5d7c6cb416b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741460"
---
# <a name="walkthrough-command-line-profiling-using-instrumentation"></a>Instruções passo a passo: criação de perfil de linha de comando usando instrumentação
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo leva você pela criação de perfil de um aplicativo autônomo [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] Para coletar dados detalhados de tempo e contagem de chamadas usando o método de instrumentação das ferramentas de criação de perfil. Nesta explicação passo a passo, você concluirá as seguintes tarefas:  
  
-   Use a ferramenta de linha de comando [VSInstr](../profiling/vsinstr.md) para gerar binários instrumentados.  
  
-   Use a ferramenta [VSPerfCLREnv](../profiling/vsperfclrenv.md) para definir as variáveis de ambiente para coletar dados de criação de perfil do .NET.  
  
-   Use a ferramenta [VSPerfCmd](../profiling/vsperfcmd.md) para coletar dados de criação de perfil.  
  
-   Use a ferramenta [VSPerfReport](../profiling/vsperfreport.md) para gerar relatórios com base em arquivo dos dados de criação de perfil.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   [!INCLUDE[vsprvsts](../includes/vsprvsts-md.md)]  
  
-   Noções intermediárias do C#  
  
-   Compreensão intermediária de como trabalhar com ferramentas de linha de comando  
  
-   Uma cópia de [amostra do PeopleTrax](../profiling/peopletrax-sample-profiling-tools.md)  
  
-   Para trabalhar com as informações fornecidas pela criação de perfil, é bom ter as informações de símbolo de depuração disponíveis. Para obter mais informações, consulte [Como fazer referência a informações de símbolo do Windows](../profiling/how-to-reference-windows-symbol-information.md).  
  
## <a name="command-line-profiling-using-the-instrumentation-method"></a>Criação de perfil da linha de comando usando o método de instrumentação  
 A instrumentação é um método de criação de perfil pelo qual versões especialmente projetadas de binários com perfil contêm funções de teste que coletam informações de tempo na entrada e saída para funções em um módulo instrumentado. Como esse método de criação de perfil é mais invasivo do que a amostragem, resulta em maior quantidade de sobrecarga. Binários instrumentados também são maiores do que os binários de depuração ou liberação e não são destinados a implantação.  
  
> [!NOTE]
>  Não envie binários instrumentados aos seus clientes. Binários instrumentados podem conter vários riscos. Os binários incluem informações que facilitam a engenharia reversa de seus aplicativos e aumentam os riscos de segurança.  
  
#### <a name="to-profile-the-peopletrax-application-by-using-the-instrumentation-method"></a>Para analisar o aplicativo PeopleTrax usando o método de instrumentação  
  
1.  Instale o aplicativo de exemplo PeopleTrax e compile a versão de lançamento.  
  
2.  Abra uma janela de prompt de comando e adicione o diretório **Ferramentas de criação de perfil** à variável de ambiente Path local.  
  
3.  Altere o diretório de trabalho para o diretório que contém os binários de PeopleTrax.  
  
4.  Crie um diretório para conter os relatórios baseados em arquivo. Digite o seguinte comando:  
  
    ```  
    md Reports  
    ```  
  
5.  Use a ferramenta de linha de comando VSInstr para instrumentar binários no aplicativo. Digite os seguintes comandos em linhas de comando separadas:  
  
    ```  
    VSInstr PeopleTrax.exe  
    VSInstr PeopleTrax.exe  
    VSInstr People.dll  
    VSInstr Person.dll  
    VSInstr Operation.dll  
    ```  
  
     **Observação** por padrão, VSInstr salva um backup não instrumentado do arquivo original. O nome do arquivo de backup tem a extensão .orig. Por exemplo, a versão original do "MyApp.exe" deve ser salva como "MyApp.exe.orig".  
  
6.  Digite o comando a seguir para definir as variáveis de ambiente apropriadas:  
  
    ```  
    VsPerfCLREnv /traceon  
    ```  
  
7.  Para iniciar o criador de perfil, digite o seguinte comando:  
  
    ```  
    VsPerfCmd /start:trace /output:Reports\Report.vsp  
    ```  
  
8.  Depois de iniciar o criador de perfil no modo de rastreamento, execute a versão instrumentada do processo PeopleTrax.exe para coletar dados.  
  
     A janela do aplicativo **PeopleTrax** é exibida.  
  
9. Clique em **Get People**.  
  
     A grade de dados do PeopleTrax é preenchida com os dados.  
  
10. Clique em **Exportar Dados**.  
  
     O bloco de notas é iniciado e exibe um novo arquivo que contém uma lista de pessoas do aplicativo **PeopleTrax**.  
  
11. Feche o bloco de notas e, em seguida, feche o aplicativo **PeopleTrax**.  
  
12. Desligue o criador de perfil. Digite o seguinte comando:  
  
    ```  
    VSPerfCmd /shutdown  
    ```  
  
13. Digite o comando a seguir para redefinir as variáveis de ambiente:  
  
    ```  
    VSPerfCLREnv /off  
    ```  
  
14. Use a ferramenta VSPerfReport para gerar ou arquivos de relatório de valores separados por vírgulas (.csv). Tipo:  
  
    ```  
    VSPerfReport Reports\Report.vsp /output:Reports /summary:all  
    ```  
  
     Você pode analisar os relatórios gerados em um programa de planilha ou pode usar o IDE [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para analisar os dados de criação de perfil no arquivo Report.vsp. Para obter mais informações, consulte [Analisando dados de ferramentas de desempenho](../profiling/analyzing-performance-tools-data.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral da sessão de desempenho](../profiling/performance-session-overview.md)   
 [Criando perfil na linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Noções básicas sobre valores de dados de amostragem](../profiling/understanding-sampling-data-values.md)   
 [Exibições de relatório de desempenho](../profiling/performance-report-views.md)



