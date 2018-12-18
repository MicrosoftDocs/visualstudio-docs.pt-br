---
title: Criar um plug-in de teste de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
f1_keywords:
- vs.test.load.loadtestplugin
helpviewer_keywords:
- code, load tests
- plug-ins, load test
- load tests, plug-ins
ms.assetid: 27806972-1b15-4388-833d-6d0632816f1f
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: ce3e85965aa8823aa12102fff41401cf24eef6a7
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896725"
---
# <a name="how-to-create-a-load-test-plug-in"></a>Como criar um plug-in de teste de carga

Você pode criar um plug-in de teste de carga para executar o código em momentos diferentes com o teste de carga em execução. Você cria um plug-in para expandir ou modificar a funcionalidade interna do teste de carga. Por exemplo, você pode codificar um plug-in de teste de carga para modificar o padrão do teste de carga com o teste de carga em execução. Para fazer isso, você deve criar uma classe que herde a interface <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>. Essa classe deve implementar o método <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin.Initialize*> dessa interface. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>.

> [!NOTE]
> Você também pode criar plug-ins para testes de desempenho na Web. Para obter mais informações, confira [Como criar um plug-in de teste de desempenho Web](../test/how-to-create-a-web-performance-test-plug-in.md)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-create-a-load-test-plug-in-by-using-visual-c"></a>Para criar um plug-in de teste de carga usando o Visual C#

1.  Abra um projeto de teste de carga e de desempenho na Web contendo um teste de desempenho na Web.

2.  Adicione um teste de carga ao projeto de teste e configure-o para executar um teste de desempenho na Web.

     Para obter mais informações, consulte [Início rápido: criar um projeto de teste de carga](../test/quickstart-create-a-load-test-project.md).

3.  No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução, selecione **Adicionar** e, em seguida, escolha **Novo Projeto**.

     A caixa de diálogo **Adicionar Novo Projeto** é exibida.

4.  Em **Modelos Instalados**, selecione **Visual C#**.

5.  Na lista de modelos, selecione **Biblioteca de Classes**.

6.  Na caixa de texto **Nome**, digite um nome para a classe.

7.  Escolha **OK**.

8.  O novo projeto da biblioteca de classes é adicionado ao **Gerenciador de Soluções** e a nova classe é exibida no **Editor de Códigos**.

9. No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **Referências** da nova biblioteca de classes e selecione **Adicionar Referência**.

10. A caixa de diálogo **Adicionar Referência** é exibida.

11. Escolha a guia **.NET**, role para baixo e selecione **Microsoft.VisualStudio.QualityTools.LoadTestFramework**.

12. Escolha **OK**.

     A referência a **Microsoft.VisualStudio.QualityTools.LoadTestFramework** é adicionada à pasta **Referência** do **Gerenciador de Soluções**.

13. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó superior do projeto de teste de carga e de desempenho Web que contém o teste de carga ao qual você deseja adicionar o plug-in de teste de carga e selecione **Adicionar Referência**.

14. A **caixa de diálogo Adicionar Referência é exibida**.

15. Escolha a guia **Projetos** e selecione o projeto da biblioteca de classes.

16. Escolha **OK**.

17. No **Editor de Códigos**, adicione uma instrução `using` ao namespace <xref:Microsoft.VisualStudio.TestTools.LoadTesting>.

18. Implemente a interface <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin> da classe que foi criada no projeto da biblioteca de classes. Consulte a seção Exemplo a seguir para obter uma implementação de exemplo.

19. Depois de gravar o código, compile o novo projeto.

20. Clique com o botão direito do mouse no nó superior do teste de carga e escolha **Adicionar Plug-in de Teste de Carga**.

     A caixa de diálogo **Adicionar Plug-in de Teste de Carga** é exibida.

21. Em **Selecionar um plug-in**, selecione a classe de plug-in do teste de carga.

22. No painel **Propriedades do plug-in selecionado**, defina os valores iniciais a serem usados pelo plug-in em tempo de execução.

    > [!NOTE]
    > Você pode expor quantas propriedades quiser de seus plug-ins; apenas torne-os públicos, definíveis e de um tipo de base como Inteiro, Booliano ou Cadeia de Caracteres. Altere também as propriedades do plug-in de teste de desempenho Web posteriormente usando a janela **Propriedades**.

23. Escolha **OK**.

     O plug-in é adicionado à pasta **Plug-ins de teste de carga**.

    > [!WARNING]
    > Você talvez receba um erro semelhante ao seguinte quando executar um teste de desempenho na Web ou um teste de carga usando seu plug-in:
    >
    > **Falha na solicitação: exceção em \<plug-in> evento: não foi possível carregar arquivo ou assembly '\<"Nome do plug-in".dll arquivo>, versão =\<n.n.n. n >, Culture=neutral, PublicKeyToken=null' ou uma de suas dependências. O sistema não pode localizar o arquivo especificado.**
    >
    > Isso acontecerá se você fizer alterações no código de qualquer um de seus plug-ins e criar uma nova versão de DLL **(versão=0.0.0.0)**, mas o plug-in ainda estiver referenciando a versão original do plug-in. Para corrigir esse problema, siga estas etapas:
    >
    > 1.  Em seu projeto de teste de carga e desempenho na Web, você verá um aviso em referências. Remova e adicione novamente a referência à DLL do plug-in.
    > 2.  Remova o plug-in do teste ou do local apropriado e adicione-o de volta.

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

-   <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestStarting>

-   <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestFinished>

-   <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestWarmupComplete>

-   <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.TestStarting>

-   <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.TestFinished>

-   <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.ThresholdExceeded>

-   <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.Heartbeat>

-   <xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest.LoadTestAborted>

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>
- [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [Como criar um plug-in de teste de desempenho Web](../test/how-to-create-a-web-performance-test-plug-in.md)