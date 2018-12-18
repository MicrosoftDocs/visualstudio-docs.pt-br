---
title: Criar visualizadores de dados personalizado | Microsoft Docs
ms.custom: ''
ms.date: 11/07/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.visualizer.troubleshoot
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, visualizers
- visualizers
ms.assetid: c24c006f-f2ac-429f-89db-677fc0c6e1ea
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4c5f505bfa8032b0f7d59f348835e1e4969b2648
ms.sourcegitcommit: 6a955a2d179cd0e137942389f940d9fcbbe125de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607816"
---
# <a name="create-custom-data-visualizers"></a>Criar visualizadores de dados personalizados 
 Um *visualizer* faz parte do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] interface de usuário do depurador que exibe uma variável ou objeto de maneira apropriada para o tipo de dados. Por exemplo, um visualizador de HTML interpreta uma cadeia de caracteres HTML e exibe o resultado como seria exibido em uma janela do navegador. Um visualizador de bitmap interpreta uma estrutura de bitmap e exibe o gráfico representa. Alguns visualizadores permitem que você modifique, bem como exibir os dados.

 O [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] depurador inclui seis visualizadores padrão. O texto, HTML, XML e JSON visualizadores funcionam em objetos de cadeia de caracteres. O Visualizador de árvore do WPF exibe as propriedades de uma árvore visual de objeto do WPF. O Visualizador de dataset funciona para objetos de DataSet, DataView e DataTable. 

Visualizadores mais podem estar disponíveis para download da Microsoft, por terceiros e da comunidade. Você também pode escrever seus próprios visualizadores e instalá-los no [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] depurador.

No depurador, um visualizador é representado por um ícone de lupa ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "ícone do visualizador"). Você pode selecionar o ícone em um **DataTip**, depurador **inspeção** janela, ou **QuickWatch** caixa de diálogo e, em seguida, selecione o visualizador apropriado para o objeto correspondente.

## <a name="write-custom-visualizers"></a>Escrever visualizadores personalizados

 > [!NOTE]
 > Para criar um visualizador personalizado para código nativo, consulte o [Visualizador de depurador nativo SQLite](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/SqliteVisualizer) exemplo. Não há suporte para os visualizadores personalizados para aplicativos da UWP e Windows 8.x.

Você pode escrever um visualizador personalizado para um objeto de qualquer classe gerenciada, exceto <xref:System.Object> e <xref:System.Array>.  
  
A arquitetura de um visualizador de depurador tem duas partes:  
  
- O *do lado do depurador* é executado dentro do depurador do Visual Studio e cria e exibe a interface de usuário do visualizador.  
  
- O *lado a ser depurado* é executado dentro do processo de depuração do Visual Studio (o *ser depurado*). O objeto de dados para visualizar (por exemplo, um objeto de cadeia de caracteres) existe no processo a ser depurado. Lado a ser depurado envia o objeto ao lado do depurador, o que o exibe na interface do usuário que você cria.  

O lado do depurador recebe o objeto de dados de um *provedor do objeto* que implementa o <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> interface. Lado a ser depurado envia o objeto por meio de *origem do objeto*, que é derivado de <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource>. 

O provedor do objeto também pode enviar dados de volta para a origem do objeto, que lhe permite escrever um visualizador que pode editar dados. Você substitui o provedor do objeto para se comunicar com o avaliador de expressão e a origem do objeto.  
  
O lado a ser depurado e o lado do depurador se comunicam entre si por meio <xref:System.IO.Stream> métodos que serializar os dados de um objeto em um <xref:System.IO.Stream> e desserializar o <xref:System.IO.Stream> volta para um objeto de dados.  

Você pode escrever um visualizador para um tipo genérico somente se o tipo é um tipo aberto. Essa restrição é a mesma que a restrição ao usar o atributo `DebuggerTypeProxy`. Para obter detalhes, consulte [usar o atributo DebuggerTypeProxy](../debugger/using-debuggertypeproxy-attribute.md).  
  
Os visualizadores personalizados podem ter considerações de segurança. Ver [considerações de segurança do visualizador](../debugger/visualizer-security-considerations.md).  
  
As etapas a seguir oferecem uma visão geral da criação do visualizador. Para obter instruções detalhadas, consulte [instruções passo a passo: escrever um visualizador em C# ](../debugger/walkthrough-writing-a-visualizer-in-csharp.md) ou [passo a passo: escrever um visualizador em Visual Basic](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md).  
  
### <a name="to-create-the-debugger-side"></a>Para criar o lado do depurador  
  
Para criar a interface de usuário do visualizador no lado do depurador, você cria uma classe que herda de <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer>e substituir o <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer.Show%2A?displayProperty=fullName> método para exibir a interface. Você pode usar <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> para exibir formulários, caixas de diálogo e controles do Windows em seu visualizador.  
  
1.  Use os métodos <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> para obter o objeto visualizado no lado do depurador.  
  
1.  Crie uma classe que herda de <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer>.  
  
1.  Substitua o método <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer.Show%2A?displayProperty=fullName> para exibir sua interface. Use <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> métodos para exibir formulários, caixas de diálogo e controles do Windows em sua interface.  
  
4.  Aplique <xref:System.Diagnostics.DebuggerVisualizerAttribute>, dando a ele o visualizador para exibir (<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer>).  
  
### <a name="to-create-the-debuggee-side"></a>Para criar o lado a ser depurado  
  
Especifique o código do lado a ser depurado usando o <xref:System.Diagnostics.DebuggerVisualizerAttribute>.  
  
1.  Aplique <xref:System.Diagnostics.DebuggerVisualizerAttribute>, permitindo que você tenha um visualizador (<xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer>) e uma origem do objeto (<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource>). Se você omitir a origem do objeto, o visualizador usará uma fonte de objeto padrão.  
  
1.  Para permitir que o visualizador edite, bem como exibir os objetos de dados, substituir os `TransferData` ou `CreateReplacementObject` métodos de <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource>.   
  
## <a name="see-also"></a>Consulte também
  
 [Passo a passo: escrever um visualizador em C#](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)  

 [Passo a passo: escrever um visualizador em Visual Basic](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)  
  
 [Como instalar um visualizador](../debugger/how-to-install-a-visualizer.md)  
  
 [Como testar e depurar um visualizador](../debugger/how-to-test-and-debug-a-visualizer.md)  
  
 [Referência de API do visualizador](../debugger/visualizer-api-reference.md)  
  
 [Exibir dados no depurador](../debugger/viewing-data-in-the-debugger.md)