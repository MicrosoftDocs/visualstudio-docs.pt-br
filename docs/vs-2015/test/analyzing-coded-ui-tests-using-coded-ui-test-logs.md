---
title: Analisando testes de IU codificado usando logs de teste de IU codificado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7e795873-1d4b-4a13-a52a-a411d87fb759
caps.latest.revision: 15
ms.author: gewarren
manager: douge
ms.openlocfilehash: e492f3bfaf725c157060a23778e1f1725bb88ee3
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49188715"
---
# <a name="analyzing-coded-ui-tests-using-coded-ui-test-logs"></a>Analisando testes de interface de usuário codificada usando logs de teste de interface de usuário codificada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os logs de teste de IU codificado filtram e registram informações importantes sobre as execuções de teste de IU codificado.  
  
 **Requisitos**  
  
-   Visual Studio Enterprise  
  
## <a name="why-should-i-do-this"></a>Por que devo fazer isso?  
 Os logs são apresentados em um formato que permite depurar os problemas rapidamente.  
  
## <a name="how-do-i-do-this"></a>Como faço isso?  
  
### <a name="step-1-enable-logging"></a>Etapa 1: Habilitar registro em log  
 De acordo com seu cenário, use um destes métodos para habilitar o log.  
  
-   Usar a versão 4 do .NET Framework sem arquivo App.config no projeto de teste  
  
    -   Abra o arquivo **QTAgent32_40.exe.config**.  
  
         Por padrão, esse arquivo está localizado em **\<drive>:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE**.  
  
         Modifique o valor de EqtTraceLevel, informando o nível de log desejado.  
  
         Salve o arquivo.  
  
-   Usar a versão 4.5 do .NET Framework sem arquivo App.config no projeto de teste  
  
    -   Abra o arquivo **QTAgent32.exe.config**.  
  
         Por padrão, esse arquivo está localizado em **\<drive>:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE**.  
  
         Modifique o valor de EqtTraceLevel, informando o nível de log desejado.  
  
         Salve o arquivo.  
  
-   Arquivo App.config presente no projeto de teste  
  
    -   Abra o arquivo App.config no projeto.  
  
         Acrescente este código ao nó de configuração:  
  
         `<system.diagnostics>     <switches>       <add name="EqtTraceLevel" value="4" />     </switches>  </system.diagnostics>`  
  
-   Habilitar o registro em logs do próprio código de teste  
  
    -   <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.LoggerOverrideState%2A> = HtmlLoggerState.AllActionSnapshot;  
  
### <a name="step-2-run-your-coded-ui-test-and-view-the-log"></a>Etapa 2: Execute o teste de IU codificado e veja o log  
 Quando executar um teste de IU codificado com as modificações no arquivo **QTAgent32.exe.config**, você verá um link de saída nos resultados do Gerenciador de Testes. Os arquivos de log são gerados quando o teste falha e quando o nível de rastreamento dos testes bem-sucedidos está definido como "detalhado".  
  
1.  No menu **TESTE**, escolha a opção **Windows** e **Gerenciador de Testes**.  
  
2.  No menu **COMPILAR**, escolha **Compilar Solução**.  
  
3.  No Gerenciador de Testes, selecione o teste de IU codificado que você deseja executar, abra seu menu de atalho e escolha em **Executar Testes Selecionados**.  
  
     Os testes automatizados será executados e indicarão se passaram ou falharam.  
  
    > [!TIP]
    >  Para exibir o Gerenciador de Testes no **Menu de Teste**, aponte para **Windows** e escolha **Gerenciador de Testes**.  
  
4.  Clique no link **Saída** nos resultados do Gerenciador de Testes.  
  
     ![Link de saída no Gerenciador de Testes](../test/media/cuit-htmlactionlog1.png "CUIT_HTMLActionLog1")  
  
     Essa ação exibe a saída do teste, que inclui um link ao log de ações.  
  
     ![Resultados e links de saída do teste de interface do usuário codificada](../test/media/cuit-htmlactionlog2.png "CUIT_HTMLActionLog2")  
  
5.  Escolha o link UITestActionLog.html.  
  
     O log é exibido em seu navegador da Web.  
  
     ![Arquivo de log de teste de IU codificado](../test/media/cuit-htmlactionlog3.png "CUIT_HTMLActionLog3")  
  
## <a name="q--a"></a>Perguntas e respostas  
  
### <a name="q-what-happened-to-the-enablehtmllogger-key"></a>P: O que aconteceu com a chave EnableHtmlLogger?  
 Havia duas ou mais definições de configuração para habilitar o agente HTML em testes de IU codificados nas versões anteriores do Visual Studio:  
  
```  
  
<add key="EnableHtmlLogger" value="true"/>  
  
<add key="EnableSnapshotInfo" value="true"/>  
  
```  
  
 Essas duas definições foram preteridas no Visual Studio 2012. EqtTraceLevel é a única definição que precisa ser modificada para habilitar o HtmlLogger.  
  
## <a name="see-also"></a>Consulte também  
 [Usar a automação de interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)   
 [Como executar testes no Microsoft Visual Studio](http://msdn.microsoft.com/library/1a1207a9-2a33-4a1e-a1e3-ddf0181b1046)



