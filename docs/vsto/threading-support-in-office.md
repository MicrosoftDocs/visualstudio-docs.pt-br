---
title: Suporte a Threading no Office
description: O threading tem suporte no modelo de objeto Microsoft Office. O modelo de objeto do Office não é thread-safe, mas pode trabalhar com vários threads em uma solução do Office.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- multiple threads [Office development in Visual Studio]
- threading [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], threading support
- object models [Office development in Visual Studio], threading support
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: dce8bb0667cecbe073c734595d341f9c7b7ccac9
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826077"
---
# <a name="threading-support-in-office"></a>Suporte a Threading no Office
  Este artigo fornece informações sobre como o threading tem suporte no modelo de objeto Microsoft Office. O modelo de objeto do Office não é thread-safe, mas é possível trabalhar com vários threads em uma solução do Office. Os aplicativos do Office são servidores Component Object Model (COM). O COM permite que os clientes chamem servidores COM em threads arbitrários. Para servidores COM que não são thread-safe, COM fornece um mecanismo para serializar chamadas simultâneas para que apenas um thread lógico seja executado no servidor a qualquer momento. Esse mecanismo é conhecido como modelo STA (single-threaded apartment). Como as chamadas são serializadas, os chamadores podem ser bloqueados por períodos de tempo enquanto o servidor está ocupado ou manipulando outras chamadas em um thread em segundo plano.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="knowledge-required-when-using-multiple-threads"></a>Conhecimento necessário ao usar vários threads
 Para trabalhar com vários threads, você deve ter pelo menos o conhecimento básico dos seguintes aspectos do multithreading:

- APIs do Windows

- Conceitos de multithread COM

- Simultaneidade

- Synchronization

- Marshaling

  Para obter informações gerais sobre multithreading, consulte [Threading gerenciado](/dotnet/standard/threading/).

  O Office é executado no STA principal. Entender as implicações disso torna possível entender como usar vários threads com o Office.

## <a name="basic-multithreading-scenario"></a>Cenário básico de multithread
 O código nas soluções do Office sempre é executado no thread da interface do usuário principal. Talvez você queira suavizar o desempenho do aplicativo executando uma tarefa separada em um thread em segundo plano. O objetivo é concluir duas tarefas aparentemente de uma só vez em vez de uma tarefa seguida pela outra, o que deve resultar em uma execução mais suave (o principal motivo para usar vários threads). Por exemplo, você pode ter o código do evento no thread principal da interface do usuário do Excel e, em um thread em segundo plano, você pode executar uma tarefa que coleta dados de um servidor e atualiza células na interface do usuário do Excel com os dados do servidor.

## <a name="background-threads-that-call-into-the-office-object-model"></a>Threads em segundo plano que chamam o modelo de objeto do Office
 Quando um thread em segundo plano faz uma chamada para o aplicativo do Office, a chamada é automaticamente empacotada em todo o limite de STA. No entanto, não há nenhuma garantia de que o aplicativo do Office possa lidar com a chamada no momento em que o thread de segundo plano o fizer. Há várias possibilidades:

1. O aplicativo do Office deve bombear mensagens para que a chamada tenha a oportunidade de entrar. Se estiver fazendo processamento intenso sem gerar isso pode levar algum tempo.

2. Se outro thread lógico já estiver no apartamento, o novo thread não poderá entrar. Isso geralmente acontece quando um thread lógico entra no aplicativo do Office e, em seguida, faz uma chamada reentrante de volta para o apartamento do chamador. O aplicativo é bloqueado aguardando que a chamada seja retornada.

3. O Excel pode estar em um estado de modo que não possa tratar imediatamente de uma chamada de entrada. Por exemplo, o aplicativo do Office pode estar exibindo uma caixa de diálogo modal.

   Para as possibilidades 2 e 3, COM fornece a interface [IMessageFilter](/windows/desktop/api/objidl/nn-objidl-imessagefilter) . Se o servidor implementá-lo, todas as chamadas entrarão por meio do método [HandleIncomingCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-handleincomingcall) . Para a possibilidade 2, as chamadas são rejeitadas automaticamente. Para a possibilidade 3, o servidor pode rejeitar a chamada, dependendo das circunstâncias. Se a chamada for rejeitada, o chamador deverá decidir o que fazer. Normalmente, o chamador implementa [IMessageFilter](/windows/desktop/api/objidl/nn-objidl-imessagefilter), caso em que seria notificado da rejeição pelo método [RetryRejectedCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-retryrejectedcall) .

   No entanto, no caso de soluções criadas usando as ferramentas de desenvolvimento do Office no Visual Studio, a interoperabilidade COM converte todas as chamadas rejeitadas em um <xref:System.Runtime.InteropServices.COMException> ("o filtro de mensagem indicou que o aplicativo está ocupado"). Sempre que você fizer uma chamada de modelo de objeto em um thread em segundo plano, deverá estar preparado para lidar com essa exceção. Normalmente, isso envolve a repetição de um determinado período de tempo e a exibição de uma caixa de diálogo. No entanto, você também pode criar o thread em segundo plano como STA e, em seguida, registrar um filtro de mensagem para esse thread para lidar com esse caso.

## <a name="start-the-thread-correctly"></a>Iniciar o thread corretamente
 Quando você cria um novo thread STA, defina o estado apartment para STA antes de iniciar o thread. O exemplo de código a seguir demonstra como fazer isso.

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/ThisWorkbook.cs" id="Snippet5":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/ThisWorkbook.vb" id="Snippet5":::

 Para obter mais informações, consulte [práticas recomendadas de Threading gerenciadas](/dotnet/standard/threading/managed-threading-best-practices).

## <a name="modeless-forms"></a>Formulários sem janela restrita
 Um formulário sem janela restrita permite algum tipo de interação com o aplicativo enquanto o formulário é exibido. O usuário interage com o formulário e o formulário interage com o aplicativo sem fechar. O modelo de objeto do Office dá suporte a formulários gerenciados sem janela restrita; no entanto, eles não devem ser usados em um thread em segundo plano.

## <a name="see-also"></a>Consulte também
- [Threading (C#)](/dotnet/csharp/programming-guide/concepts/threading/index)
- [Threading (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/threading/index)
- [Usar threads e threading](/dotnet/standard/threading/using-threads-and-threading)
- [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)
