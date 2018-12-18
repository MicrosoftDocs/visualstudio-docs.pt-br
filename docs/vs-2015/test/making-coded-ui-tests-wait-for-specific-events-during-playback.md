---
title: Fazendo testes de IU codificado aguardar eventos específicos durante a reprodução | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 41981ad6-673e-492e-b739-9863b14157b1
caps.latest.revision: 26
ms.author: gewarren
manager: douge
ms.openlocfilehash: 0042be9e22b4143021b78cb96b6032144bd624f5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49941003"
---
# <a name="making-coded-ui-tests-wait-for-specific-events-during-playback"></a>Fazendo testes de IU codificado aguardar eventos específicos durante a reprodução
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na reprodução de um teste de IU codificado, é possível instruir o teste a aguardar a ocorrência de determinados eventos, como a exibição de uma janela, o desaparecimento da barra de progresso etc. Para fazer isso, use o método apropriado UITestControl.WaitForControlXXX(), conforme descrito na tabela a seguir. Para obter um exemplo de um teste de IU codificado que espera um controle ser habilitado usando o método <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlEnabled%2A>, consulte [Instruções passo a passo: criando, editando e mantendo um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md).  
  
 **Requisitos**  
  
 Visual Studio Enterprise  
  
> [!TIP]
>  Você também pode adicionar atrasos antes de ações usando o Editor de teste de IU codificado. Para obter mais informações, consulte [How to: Insert a Delay Before a UI Action Using the Coded UI Test Editor](http://msdn.microsoft.com/library/509f8ef7-e105-4049-b11b-d64549e055b0) (Como inserir um atraso antes de uma ação de interface do usuário usando o Editor de teste de IU codificado).  
  
 **Métodos UITestControl.WaitForControlXXX()**  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlReady%2A>  
  
 Aguarda até que o controle esteja pronto para aceitar a entrada do mouse e do teclado. O mecanismo implicitamente solicita que essa API para todas as ações aguarde até que controle esteja pronto antes de realizar qualquer operação. No entanto, em determinados cenários complexos, você precisará fazer a chamada explícita.  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlEnabled%2A>  
  
 Aguarda o controle ser habilitado quando o assistente está fazendo alguma validação assíncrona da entrada ao fazer chamadas para o servidor. Por exemplo, você pode aguardar até que o botão **Avançar** do assistente esteja habilitado (). Para obter um exemplo desse método, consulte [Instruções passo a passo: criando, editando e mantendo um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md).  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlExist%2A>  
  
 Aguarda até que o controle apareça na interface do usuário. Por exemplo, você está esperando uma caixa de diálogo de erro depois que o aplicativo fez a validação dos parâmetros. O tempo necessário para a validação é variável. Você pode usar esse método para aguardar a caixa de diálogo de erro.  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlNotExist%2A>  
  
 Aguarda até que o controle desapareça da interface do usuário. Por exemplo, você pode aguardar até que a barra de progresso desapareça.  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlPropertyEqual%2A>  
  
 Aguarda até que propriedade especificada do controle tenha o valor especificado. Por exemplo, você aguarda até que o texto de status seja alterado para **Concluído**.  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlPropertyNotEqual%2A>  
  
 Aguarda até que a propriedade especificada do controle tenha o oposto do valor especificado. Por exemplo, você aguarda até que a caixa de edição não seja somente leitura, isto é, editável.  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlCondition%2A>  
  
 Aguarda até que o predicado especificado volte a ser `true`. Isso pode ser usado em operações de espera complexas (como condições OR) em um determinado controle. Por exemplo, você pode aguardar até que o texto de status seja **Êxito** ou **Falha**, conforme mostrado no código a seguir:  
  
```csharp  
  
// Define the method to evaluate the condition   
private static bool IsStatusDone(UITestControl control)   
{   
    WinText statusText = control as WinText;   
    return statusText.DisplayText == "Succeeded" || statusText.DisplayText == "Failed";   
}   
  
// In test method, wait till the method evaluates to true   
statusText.WaitForControlCondition(IsStatusDone);  
  
```  
  
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForCondition%2A>  
  
 Todos os métodos anteriores são métodos de instância de UITestControl. Esse método é um método estático. Esse método também espera que o predicado especificado seja `true`, mas ele pode ser usado em operações de espera complexas (como condições OR) em vários controles. Por exemplo, você pode aguardar até que o texto de status seja **Êxito** ou até que uma mensagem de erro apareça, conforme mostrado no código a seguir:  
  
```csharp  
  
// Define the method to evaluate the condition   
private static bool IsStatusDoneOrError(UITestControl[] controls)   
{   
    WinText statusText = controls[0] as WinText;   
    WinWindow errorDialog = controls[1] as WinWindow;   
    return statusText.DisplayText == "Succeeded" || errorDialog.Exists;   
}   
  
// In test method, wait till the method evaluates to true   
UITestControl.WaitForCondition<UITestControl[]>(new UITestControl[] { statusText, errorDialog }, IsStatusDoneOrError);  
  
```  
  
 Todos esses métodos têm o comportamento a seguir:  
  
 Os métodos retornarão true se a espera for bem-sucedida e false se a espera tiver falhado.  
  
 O tempo limite implícito para a operação de espera é especificado pela propriedade <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.WaitForReadyTimeout%2A>. O valor padrão dessa propriedade é 60.000 milissegundos (um minuto).  
  
 Os métodos têm uma sobrecarga para levar um tempo limite explícito em milissegundos. No entanto, quando a operação de espera resulta em uma pesquisa implícita para o controle ou, quando o aplicativo estiver ocupado, o tempo de espera real poderá ser maior que o tempo limite especificado.  
  
 As funções anteriores são poderosas e flexíveis e devem atender a quase todas as condições. No entanto, caso esses métodos não atendam às suas necessidades e você precise codificar um <xref:Microsoft.VisualStudio.TestTools.UITesting.Playback.Wait%2A> ou um <xref:System.Threading.Thread.Sleep%2A> em seu código, será recomendado usar o Playback.Wait() em vez da API Thread.Sleep(). Os motivos para isso são:  
  
 Você pode usar a propriedade <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.ThinkTimeMultiplier%2A> para modificar a duração da suspensão. Por padrão, essa variável é 1, mas você pode aumentá-la ou diminui-la para alterar o tempo de espera em todo o código. Por exemplo, se estiver testando uma rede lenta especificamente ou algum outro caso de baixo desempenho, você poderá alterar essa variável em um único lugar (ou até mesmo no arquivo de configuração) para 1,5 para adicionar 50% de espera extra em todos os locais.  
  
 O Playback.Wait() chama Thread.Sleep() internamente (após o cálculo acima) em partes menores em um loop for durante a verificação da operação cancelar\suspender do usuário. Em outras palavras, o Playback.Wait() permite que você cancele a reprodução antes do final da espera enquanto a suspensão pode ou não lançar a exceção.  
  
> [!TIP]
>  o Editor de testes de interface de usuário codificada permite modificar facilmente os testes de IU codificados. Com o Editor de testes de interface de usuário codificada, você pode localizar, exibir e editar os métodos de teste. Também é possível editar ações de interface do usuário e seus controles associados no mapa de controles de IU. Para obter mais informações, consulte [Editing Coded UI Tests Using the Coded UI Test Editor](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md) (Editando testes de IU codificada usando o Editor de teste de IU codificado).  
  
 **Diretrizes**  
  
 Para obter informações, consulte [Teste para entrega contínua com o Visual Studio 2012 – Capítulo 5: Automatizando os testes de sistema](http://go.microsoft.com/fwlink/?LinkID=255196)  
  
## <a name="see-also"></a>Consulte também  
 [Usar a automação de interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)   
 [Criando testes de IU codificados](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)   
 [Instruções passo a passo: Criando, editando e mantendo um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)   
 [Anatomia de um teste de IU codificado](../test/anatomy-of-a-coded-ui-test.md)   
 [Configurações e plataformas com suporte para testes de IU codificados e gravações das ações](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)   
 [Como inserir um atraso antes de uma ação de interface do usuário usando o Editor de teste de IU codificado](http://msdn.microsoft.com/library/509f8ef7-e105-4049-b11b-d64549e055b0)



