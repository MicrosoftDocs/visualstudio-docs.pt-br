---
title: Suporte a Threading no Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- multiple threads [Office development in Visual Studio]
- threading [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], threading support
- object models [Office development in Visual Studio], threading support
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5aafdad425d611d7d57c2ae8e53e505d3522ba38
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49871102"
---
# <a name="threading-support-in-office"></a>Suporte a Threading no Office
  Este artigo fornece informações sobre como threading é suportado no modelo de objeto do Microsoft Office. O modelo de objeto do Office não é thread-safe, mas é possível trabalhar com vários threads em uma solução do Office. Aplicativos do Office são servidores do modelo de objeto de componente (COM). COM permite que os clientes chamar servidores COM em threads arbitrários. Para servidores COM que não são thread-safe, COM fornece um mecanismo para serializar as chamadas simultâneas para que apenas um thread lógico seja executado no servidor a qualquer momento. Esse mecanismo é conhecido como o modelo de single-threaded apartment (STA). Porque as chamadas são serializadas, os chamadores podem ser bloqueados por períodos de tempo enquanto o servidor está ocupado ou está manipulando outras chamadas em um thread em segundo plano.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="knowledge-required-when-using-multiple-threads"></a>Necessário ao usar vários segmentos de dados de Conhecimento  
 Para trabalhar com vários threads, você deve ter conhecimento básico de pelo menos dos seguintes aspectos de multithreading:  
  
- APIs do Windows  
  
- COM os conceitos de vários threads  
  
- Concorrência  
  
- Sincronização  
  
- Marshaling  
  
  Para obter informações gerais sobre multithreading, consulte [threading gerenciado](/dotnet/standard/threading/).  
  
  Office é executado no STA principal. Noções básicas sobre as implicações disso torna possível entender como usar vários threads com o Office.  
  
## <a name="basic-multithreading-scenario"></a>Cenário básico de multithreading  
 Código em soluções do Office sempre é executado no thread da interface do usuário principal. Talvez você queira suavizar o desempenho do aplicativo, executando uma tarefa separada em um thread em segundo plano. A meta é concluir duas tarefas aparentemente ao mesmo tempo, em vez de uma tarefa seguida de outro, que deve resultar na execução mais suave (o principal motivo para usar vários threads). Por exemplo, você pode ter seu código de evento no thread principal da interface do usuário do Excel e em um thread em segundo plano, você pode executar uma tarefa que coleta dados de um servidor e atualiza as células na interface do usuário do Excel com os dados do servidor.  
  
## <a name="background-threads-that-call-into-the-office-object-model"></a>Threads em segundo plano que chamam o modelo de objeto do Office  
 Quando um thread em segundo plano faz uma chamada para o aplicativo do Office, a chamada automaticamente é realizada além do limite STA. No entanto, não há nenhuma garantia de que o aplicativo do Office pode lidar com a chamada no momento em que o thread em segundo plano torna. Existem várias possibilidades:  
  
1. O aplicativo do Office deve bomba de mensagens para a chamada para ter a oportunidade de inserir. Se ele está fazendo pesado processamento sem produzindo isso pode levar tempo.  
  
2. Se outro thread lógico já está no apartamento, não é possível inserir o novo thread. Isso geralmente acontece quando um thread lógico entra o aplicativo do Office e, em seguida, faz uma chamada reentrante para apartment do chamador. O aplicativo está bloqueado aguardando o retorno da chamada.  
  
3. Excel pode estar em um estado de modo que ele não pode tratar imediatamente uma chamada de entrada. Por exemplo, o aplicativo do Office pode estar exibindo uma caixa de diálogo modal.  
  
   Possibilidades 2 e 3, fornece COM o [IMessageFilter](/windows/desktop/api/objidl/nn-objidl-imessagefilter) interface. Se o servidor implementa, todas as chamadas inserir por meio de [HandleIncomingCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-handleincomingcall) método. Possibilidade de 2, chamadas automaticamente são rejeitadas. Possibilidade de 3, o servidor pode rejeitar a chamada, dependendo das circunstâncias. Se a chamada for rejeitada, o chamador deve decidir o que fazer. Normalmente, o implementa chamador [IMessageFilter](/windows/desktop/api/objidl/nn-objidl-imessagefilter), caso em que ele seria notificado de rejeição pela [RetryRejectedCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-retryrejectedcall) método.  
  
   No entanto, no caso de soluções criadas usando as ferramentas de desenvolvimento do Office no Visual Studio, a interoperabilidade COM converte rejeitadas todas as chamadas para um <xref:System.Runtime.InteropServices.COMException> ("o filtro de mensagens indicou que o aplicativo está ocupado"). Sempre que você faz um modelo de objeto chamada em um thread em segundo plano, você deve estar preparado para tratar essa exceção. Normalmente, que envolve tentar novamente para um determinado período de tempo e, em seguida, exibindo uma caixa de diálogo. No entanto, você também pode criar o thread em segundo plano como sendo STA e, em seguida, registrar um filtro de mensagem para esse thread lidar com isso.  
  
## <a name="start-the-thread-correctly"></a>Iniciar o thread corretamente  
 Quando você cria um novo thread STA, defina o estado de apartment para STA antes de iniciar o thread. O exemplo de código a seguir demonstra como fazer isso.  
  
 [!code-csharp[Trin_VstcoreCreatingExcel#5](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/ThisWorkbook.cs#5)]
 [!code-vb[Trin_VstcoreCreatingExcel#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/ThisWorkbook.vb#5)]  
  
 Para obter mais informações, consulte [práticas recomendadas de threading gerenciado](/dotnet/standard/threading/managed-threading-best-practices).  
  
## <a name="modeless-forms"></a>Formulários sem janela restrita  
 Um formulário sem janela restrita permite algum tipo de interação com o aplicativo, enquanto o formulário é exibido. O usuário interage com o formulário e o formulário interage com o aplicativo sem fechar. O modelo de objeto do Office dá suporte a formulários sem janela restrita gerenciados; No entanto, eles não devem ser usados em um thread em segundo plano.  
  
## <a name="see-also"></a>Consulte também  
 [Threading gerenciado](/dotnet/standard/threading/)  
 [Threading (c#)](/dotnet/csharp/programming-guide/concepts/threading/index) [Threading (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/threading/index)   
 [Use threads e threading](/dotnet/standard/threading/using-threads-and-threading)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)  
  
  