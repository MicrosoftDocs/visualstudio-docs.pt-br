---
title: Fazer os testes de IU codificados aguardarem eventos específicos
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d1f077269ddfd736aa98b78c64c81170037853eb
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894762"
---
# <a name="make-coded-ui-tests-wait-for-specific-events-during-playback"></a>Fazer os testes de IU codificados aguardarem eventos específicos durante a reprodução

Na reprodução de um teste de IU codificado, é possível instruir o teste a aguardar a ocorrência de determinados eventos, como a exibição de uma janela, o desaparecimento da barra de progresso etc. Para fazer isso, use o método apropriado UITestControl.WaitForControlXXX(), conforme descrito na tabela a seguir. Para obter um exemplo de um teste de IU codificado que aguarda a habilitação de um controle usando o método <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlEnabled%2A>, confira [Passo a passo: Criando, editando e mantendo um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md).

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

**Requisitos**

Visual Studio Enterprise

> [!TIP]
> Você também pode adicionar atrasos antes de ações usando o Editor de teste de IU codificado. Para obter mais informações, confira [Como inserir um atraso antes de uma ação de interface do usuário usando o Editor de Teste de IU Codificado](editing-coded-ui-tests-using-the-coded-ui-test-editor.md#insert-a-delay-before-a-ui-action).

**Métodos UITestControl.WaitForControlXXX()**

<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlReady%2A>

Aguarda até que o controle esteja pronto para aceitar a entrada do mouse e do teclado. O mecanismo implicitamente solicita que essa API para todas as ações aguarde até que controle esteja pronto antes de realizar qualquer operação. No entanto, em determinados cenários complexos, você precisará fazer a chamada explícita.

<xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.WaitForControlEnabled%2A>

Aguarda o controle ser habilitado quando o assistente está fazendo alguma validação assíncrona da entrada ao fazer chamadas para o servidor. Por exemplo, você pode aguardar até que o botão **Avançar** do assistente esteja habilitado (). Para obter um exemplo desse método, confira [Passo a passo: Criando, editando e mantendo um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md).

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

 Todos esses métodos têm o seguinte comportamento:

 Os métodos retornarão true se a espera for bem-sucedida e false se a espera tiver falhado.

 O tempo limite implícito para a operação de espera é especificado pela propriedade <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.WaitForReadyTimeout%2A>. O valor padrão dessa propriedade é 60.000 milissegundos (um minuto).

 Os métodos têm uma sobrecarga para levar um tempo limite explícito em milissegundos. No entanto, quando a operação de espera resulta em uma pesquisa implícita para o controle ou, quando o aplicativo estiver ocupado, o tempo de espera real poderá ser maior que o tempo limite especificado.

 As funções anteriores são poderosas e flexíveis e devem atender a quase todas as condições. No entanto, caso esses métodos não atendam às suas necessidades e você precise codificar um <xref:Microsoft.VisualStudio.TestTools.UITesting.Playback.Wait%2A> ou um <xref:System.Threading.Thread.Sleep%2A> em seu código, será recomendado usar o Playback.Wait() em vez da API Thread.Sleep(). Os motivos para isso são:

 Você pode usar a propriedade <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.ThinkTimeMultiplier%2A> para modificar a duração da suspensão. Por padrão, essa variável é 1, mas você pode aumentá-la ou diminui-la para alterar o tempo de espera em todo o código. Por exemplo, se estiver testando uma rede lenta especificamente ou algum outro caso de baixo desempenho, você poderá alterar essa variável em um único lugar (ou até mesmo no arquivo de configuração) para 1,5 para adicionar 50% de espera extra em todos os locais.

 O Playback.Wait() chama Thread.Sleep() internamente (após o cálculo acima) em partes menores em um loop for durante a verificação da operação cancelar\suspender do usuário. Em outras palavras, o Playback.Wait() permite que você cancele a reprodução antes do final da espera enquanto a suspensão pode ou não lançar a exceção.

> [!TIP]
> o Editor de testes de interface de usuário codificada permite modificar facilmente os testes de IU codificados. Com o Editor de testes de interface de usuário codificada, você pode localizar, exibir e editar os métodos de teste. Também é possível editar ações de interface do usuário e seus controles associados no mapa de controles de IU. Para obter mais informações, confira [Editar testes de IU codificados usando o Editor de Teste de IU Codificado](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md).

## <a name="see-also"></a>Consulte também

- [Usar a automação de interface do usuário para testar seu código](../test/use-ui-automation-to-test-your-code.md)
- [Criar testes de IU codificados](../test/use-ui-automation-to-test-your-code.md)
- [Passo a passo: criar, editar e manter um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
- [Anatomia de um teste de IU codificado](../test/anatomy-of-a-coded-ui-test.md)
- [Configurações e plataformas compatíveis para testes de IU codificados e gravações de ação](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
- [Como inserir um atraso antes de uma ação de interface do usuário usando o editor de teste de IU codificado](editing-coded-ui-tests-using-the-coded-ui-test-editor.md#insert-a-delay-before-a-ui-action)
