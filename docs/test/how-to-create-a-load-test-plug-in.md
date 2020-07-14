---
title: Criar um plug-in de teste de carga
ms.date: 10/19/2016
ms.topic: how-to
f1_keywords:
- vs.test.load.loadtestplugin
helpviewer_keywords:
- code, load tests
- plug-ins, load test
- load tests, plug-ins
ms.assetid: 27806972-1b15-4388-833d-6d0632816f1f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0abcc3865c21a4f4673331377af8d17b223c7875
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288020"
---
# <a name="how-to-create-a-load-test-plug-in"></a>Como criar um plug-in de teste de carga

Você pode criar um plug-in de teste de carga para executar o código em momentos diferentes com o teste de carga em execução. Você cria um plug-in para expandir ou modificar a funcionalidade interna do teste de carga. Por exemplo, você pode codificar um plug-in de teste de carga para modificar o padrão do teste de carga com o teste de carga em execução. Para fazer isso, você deve criar uma classe que herde a interface <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>. Essa classe deve implementar o método <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin.Initialize*> dessa interface. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>.

> [!TIP]
> Você também pode criar plug-ins para testes de desempenho na Web. Para obter mais informações, consulte [como: criar um plug-in de teste de desempenho da Web](../test/how-to-create-a-web-performance-test-plug-in.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

<!-- markdownlint-disable MD003 MD020 -->
## <a name="to-create-a-load-test-plug-in-in-c"></a>Como criar um plug-in de teste de carga em C#
<!-- markdownlint-enable MD003 MD020 -->

1. Abra um projeto de teste de carga e de desempenho na Web contendo um teste de desempenho na Web.

2. Adicione um teste de carga ao projeto de teste e configure-o para executar um teste de desempenho na Web.

     Para obter mais informações, consulte [Início rápido: criar um projeto de teste de carga](../test/quickstart-create-a-load-test-project.md).

3. Adicione um novo projeto de **Biblioteca de Classes** à solução. (Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução e selecione **Adicionar** e escolha **novo projeto**.)

4. Em **Gerenciador de soluções**, clique com o botão direito do mouse na pasta **referências** na nova biblioteca de classes e selecione **Adicionar referência**.

   A caixa de diálogo **Adicionar Referência** é exibida.

5. Escolha a guia **.NET**, role para baixo e selecione **Microsoft.VisualStudio.QualityTools.LoadTestFramework**.

6. Escolha **OK**.

   A referência a **Microsoft. VisualStudio. QualityTools. LoadTestFramework** é adicionada à pasta de **referência** em **Gerenciador de soluções**.

7. No **Gerenciador de soluções**, clique com o botão direito do mouse no nó superior do projeto de teste de carga e desempenho na Web que contém o teste de carga ao qual você deseja adicionar o plug-in de teste de carga e selecione **Adicionar referência**.

   A **caixa de diálogo Adicionar referência é exibida**.

8. Escolha a guia **Projetos** e selecione o projeto da biblioteca de classes.

9. Escolha **OK**.

10. No **Editor de Códigos**, adicione uma instrução `using` ao namespace <xref:Microsoft.VisualStudio.TestTools.LoadTesting>.

11. Implemente a interface <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin> da classe que foi criada no projeto da biblioteca de classes. Consulte a seção Exemplo a seguir para obter uma implementação de exemplo.

12. Depois de gravar o código, compile o novo projeto.

13. Clique com o botão direito do mouse no nó superior do teste de carga e escolha **Adicionar Plug-in de Teste de Carga**.

     A caixa de diálogo **Adicionar Plug-in de Teste de Carga** é exibida.

14. Em **Selecionar um plug-in**, selecione a classe de plug-in do teste de carga.

15. No painel **Propriedades do plug-in selecionado**, defina os valores iniciais a serem usados pelo plug-in em tempo de execução.

    > [!NOTE]
    > Você pode expor quantas propriedades quiser de seus plug-ins; apenas torne-os públicos, definíveis e de um tipo de base como Inteiro, Booliano ou Cadeia de Caracteres. Você também pode alterar as propriedades de plug-in de teste de desempenho da Web mais tarde usando a janela **Propriedades** .

16. Escolha **OK**.

     O plug-in é adicionado à pasta **Plug-ins de teste de carga**.

    > [!WARNING]
    > Você talvez receba um erro semelhante ao seguinte quando executar um teste de desempenho na Web ou um teste de carga usando seu plug-in:
    >
    > **Falha na solicitação: exceção no \<plug-in> evento: não foi possível carregar o arquivo ou assembly ' \<"Plug-in name".dll file> , versão = \<n.n.n.n> , cultura = neutral, PublicKeyToken = null ' ou uma de suas dependências. O sistema não pode localizar o arquivo especificado.**
    >
    > Isso acontecerá se você fizer alterações no código de qualquer um de seus plug-ins e criar uma nova versão de DLL **(versão=0.0.0.0)**, mas o plug-in ainda estiver referenciando a versão original do plug-in. Para corrigir esse problema, siga estas etapas:
    >
    > 1. Em seu projeto de teste de carga e desempenho na Web, você verá um aviso em referências. Remova e adicione novamente a referência à DLL do plug-in.
    > 2. Remova o plug-in do teste ou do local apropriado e adicione-o de volta.

## <a name="example"></a>Exemplo

O código a seguir mostra um plug-in de teste de carga que executa um código personalizado depois que ocorre um evento LoadTestFinished. Se esse código for executado em um agente de teste em um computador remoto e o agente de teste não tiver um serviço SMTP localhost, o teste de carga permanecerá no estado "Em andamento" porque uma caixa de mensagem será aberta.

> [!NOTE]
> O código a seguir exige que você adicione uma referência a System.Windows.Forms.

```csharp
using System;
using Microsoft.VisualStudio.TestTools.LoadTesting;
using System.Net.Mail;
using System.Windows.Forms;

namespace LoadTestPluginTest
{
    public class MyLoadTestPlugin : ILoadTestPlugin
    {
        LoadTest myLoadTest;

        public void Initialize(LoadTest loadTest)
        {
            myLoadTest = loadTest;
            myLoadTest.LoadTestFinished += new
                EventHandler(myLoadTest_LoadTestFinished);
        }

        void myLoadTest_LoadTestFinished(object sender, EventArgs e)
        {
            try
            {
                // place custom code here
                MailAddress MyAddress = new MailAddress("someone@example.com");
                MailMessage MyMail = new MailMessage(MyAddress, MyAddress);
                MyMail.Subject = "Load Test Finished -- Admin Email";
                MyMail.Body = myLoadTest..Name + " has finished.";

                SmtpClient MySmtpClient = new SmtpClient("localhost");
                MySmtpClient.Send(MyMail);
            }

            catch (SmtpException ex)
            {
                MessageBox.Show(ex.InnerException.Message +
                    ".\r\nMake sure you have a valid SMTP.", "LoadTestPlugin", MessageBoxButtons.OK, MessageBoxIcon.Warning, MessageBoxDefaultButton.Button1);
            }
        }
    }
}
```

Oito eventos são associados a um teste de carga que pode ser identificado no plug-in de teste de carga para executar um código personalizado com o teste de carga. Esta é uma lista dos eventos que dão acesso a períodos diferentes da execução do teste de carga:

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestStarting>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestFinished>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestWarmupComplete>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.TestStarting>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.TestFinished>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.ThresholdExceeded>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.Heartbeat>

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestAborted>

## <a name="see-also"></a>Veja também

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>
- [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [Como: criar um plug-in de teste de desempenho na Web](../test/how-to-create-a-web-performance-test-plug-in.md)
