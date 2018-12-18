---
title: Analisando testes de interface de usuário codificada usando logs de teste de interface de usuário codificada
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 9c31dd90981cf39f1de296b2c96d6064afc730b4
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896673"
---
# <a name="analyzing-coded-ui-tests-using-coded-ui-test-logs"></a>Analisando testes de IU codificados usando logs de teste de IU codificado

Os logs de teste de IU codificado filtram e registram informações importantes sobre as execuções de teste de IU codificado. Os logs são apresentados em um formato que permite depurar os problemas rapidamente.

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="step-1-enable-logging"></a>Etapa 1: Habilitar registro em log

De acordo com seu cenário, use um destes métodos para habilitar o log:

- Use a versão 4 do .NET Framework sem arquivo *App.config* no projeto de teste:

   1. Abra o arquivo *QTAgent32_40.exe.config*. Por padrão, esse arquivo fica localizado em *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE*.

   2. Modifique o valor de EqtTraceLevel, informando o nível de log desejado.

   3. Salve o arquivo.

- Use a versão 4.5 do .NET Framework sem arquivo *App.config* no projeto de teste:

   1. Abra o arquivo *QTAgent32.exe.config*. Por padrão, esse arquivo fica localizado em *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE*.

   2. Modifique o valor de EqtTraceLevel, informando o nível de log desejado.

   3. Salve o arquivo.

- O arquivo *App.config* está presente no projeto de teste:

    - Abra o arquivo *App.config* no projeto e adicione o seguinte código sob o nó de configuração:

      ```xml
      <system.diagnostics>
        <switches>
          <add name="EqtTraceLevel" value="4" />
        </switches>
      </system.diagnostics>`
      ```

- Habilitar registro em log do próprio código de teste:

   <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.LoggerOverrideState%2A> = HtmlLoggerState.AllActionSnapshot;

## <a name="step-2-run-your-coded-ui-test-and-view-the-log"></a>Etapa 2: Execute o teste de IU codificado e veja o log

Ao executar um teste de IU codificado com as modificações no arquivo *QTAgent32.exe.config* em vigor, você verá um link de saída nos resultados do **Gerenciador de Testes**. Os arquivos de log são gerados não apenas quando o teste falha, mas também quando o nível de rastreamento está definido como "detalhado" e os testes são bem-sucedidos.

1.  No menu **Teste**, escolha a opção **Windows** e selecione **Gerenciador de Testes**.

2.  No menu **Compilar**, escolha **Compilar Solução**.

3.  No **Gerenciador de Testes**, selecione o teste de IU codificado que você deseja executar, abra seu menu de atalho e escolha em **Executar Testes Selecionados**.

     Os testes automatizados são executados e indicam se passaram ou falharam.

    > [!TIP]
    > Para exibir o **Gerenciador de Testes**, escolha **Teste** > **Windows** e escolha **Gerenciador de Testes**.

4.  Clique no link **Saída** nos resultados do **Gerenciador de Testes**.

     ![Link de saída no Gerenciador de Testes](../test/media/cuit_htmlactionlog1.png)

     Essa ação exibe a saída do teste, que inclui um link ao log de ações.

     ![Resultados e links de saída do teste de IU codificado](../test/media/cuit_htmlactionlog2.png)

5.  Escolha o link *UITestActionLog.html*.

     O log é exibido em seu navegador da Web.

     ![Arquivo de log do teste de IU codificado](../test/media/cuit_htmlactionlog3.png)

## <a name="see-also"></a>Consulte também

- [Usar a automação de interface do usuário para testar seu código](../test/use-ui-automation-to-test-your-code.md)
- [Como executar testes no Microsoft Visual Studio](https://msdn.microsoft.com/Library/1a1207a9-2a33-4a1e-a1e3-ddf0181b1046)