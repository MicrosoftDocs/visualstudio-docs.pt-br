---
title: Arquitetura do Visualizador | Microsoft Docs
description: Um visualizador exibe um tipo específico de elemento de dados e também pode permitir a edição. Saiba mais sobre a arquitetura de um visualizador.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 6aad395f-7170-4d9e-b2b8-a5faf453380e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9df1dfa1912c54d30c5c428ec59de9432fe68051
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99884241"
---
# <a name="visualizer-architecture"></a>Arquitetura do visualizador
A arquitetura de um visualizador de depurador tem duas partes:

- O *lado do depurador* é executado no depurador do Visual Studio. O código do lado depurador cria e exibe a interface do usuário para o visualizador.

- O *lado a ser depurado* é executado dentro do processo que o Visual Studio está depurando (o *lado a ser depurado*).

  Um visualizador é um componente de depurador que permite que o depurador exiba (*visualize*) o conteúdo de um objeto de dados em um formato significativo e legível. Alguns visualizadores também dão suporte à edição do objeto de dados. Ao escrever visualizadores personalizados, você poderá estender o depurador para lidar com seus próprios tipos de dados personalizados.

  O objeto de dados a ser visualizado reside no processo que você estiver depurando (o processo *a ser depurado*). A interface do usuário que exibirá os dados é criada no processo a ser depurado do Visual Studio:

|Processo do depurador|Processo a ser depurado|
|----------------------|----------------------|
|Interface de usuário do depurador (DataTips, janela de inspeção, QuickWatch)|Objeto de dados a ser visualizado|

 Para visualizar o objeto de dados dentro da interface do depurador, você precisará do código para comunicar entre os dois processos. Consequentemente, a arquitetura do visualizador consiste em duas partes: código do *lado do depurador* e código do *lado a ser depurado*.

 O código do lado do depurador cria sua própria interface do usuário, que pode ser invocada a partir da interface do depurador, como um DataTip, janela de inspeção ou QuickWatch. A interface do visualizador é criada usando a classe <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> e a interface <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService>. Como todas as APIs do visualizador, DialogDebuggerVisualizer e IDialogVisualizerService estão localizadas no namespace <xref:Microsoft.VisualStudio.DebuggerVisualizers>.

|O lado do depurador|O lado a ser depurado|
|-------------------|-------------------|
|Classe DialogDebuggerVisualizer<br /><br /> Interface de IDialogVisualizerService|Objeto de dados|

 A interface do usuário obtém os dados a serem visualizados de um Provedor do Objeto, que existe no lado do depurador:

|O lado do depurador|O lado a ser depurado|
|-------------------|-------------------|
|Classe DialogDebuggerVisualizer<br /><br /> Interface de IDialogVisualizerService|Objeto de dados|
|Provedor do Objeto (implementa <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider>)||

 Há um objeto correspondente no lado a ser depurado chamado de Origem do Objeto:

|O lado do depurador|O lado a ser depurado|
|-------------------|-------------------|
|Classe DialogDebuggerVisualizer<br /><br /> Interface de IDialogVisualizerService|Objeto de dados|
|Provedor do Objeto (implementa <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider>)|Origem do Objeto (derivada de <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource>)|

 O Provedor do Objeto fornece os dados do objeto que devem ser visualizado na interface do usuário do visualizador. O Provedor do Objeto obtém os dados do objeto da Origem do Objeto. O Provedor do Objeto e a Origem do Objeto fornecem APIs para comunicar dados de objeto entre o lado do depurador e o lado a ser depurado.

 Cada visualizador deve obter o objeto de dados a ser visualizado. A tabela a seguir mostra as APIs correspondentes que o Provedor do Objeto e a Origem do Objeto usam para esse propósito:

|Provedor do Objeto|Origem do Objeto|
|---------------------|-------------------|
|<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A><br /><br /> — ou —<br /><br /> <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A>|<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.GetData%2A>|

 Observe que o provedor do objeto pode usar <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A> ou <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A>. Qualquer API resulta em uma chamada para <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.GetData%2A> na Origem do Objeto. Uma chamada para <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.GetData%2A?displayProperty=fullName> preenche um <xref:System.IO.Stream?displayProperty=fullName>, que representa um formato serializado do objeto que está sendo visualizado.

 O <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A?displayProperty=fullName> desserializa os dados de volta no formato do objeto, que você pode exibir na interface do usuário que cria com <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer>. O <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A?displayProperty=fullName> preenche os dados como `Stream`bruto, que você deve desserializar. O <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A?displayProperty=fullName> funciona chamando <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A?displayProperty=fullName> para obter o `Stream` serializado, em seguida, desserializando os dados. Use <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A?displayProperty=fullName> quando o objeto não for serializável pelo .NET e não exigir serialização personalizada. Nesse caso, você também deve substituir o método <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.Serialize%2A?displayProperty=fullName>.

 Se você estiver criando um visualizador somente leitura, a comunicação unidirecional com <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetData%2A> ou <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.GetObject%2A> será suficiente. Se você estiver criando um visualizador que dá suporte à edição de objetos de dados, será necessário fazer mais. Você também deve poder enviar um objeto de dados do Provedor de Objeto de volta para a Origem do Objeto. A tabela a seguir mostra as APIs do Provedor do Objeto e a Origem do Objeto usadas para esse propósito:

|Provedor do Objeto|Origem do Objeto|
|---------------------|-------------------|
|<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceData%2A><br /><br /> — ou —<br /><br /> <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceObject%2A>|<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.CreateReplacementObject%2A>|

 Observe, novamente, que há duas APIs que o Provedor do Objeto pode usar. Os dados são enviados sempre do Provedor do Objeto para a Origem do Objeto como `Stream`, mas <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceData%2A> exige que você serialize o objeto em um `Stream`.

 O <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceObject%2A> usa o objeto que você fornece, serializa-o em um `Stream` e, em seguida, chama o <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.ReplaceData%2A> para enviar o `Stream` para o <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.CreateReplacementObject%2A>.

 Usar um dos métodos de substituir cria um novo objeto de dados no lado a ser depurado que substitui o objeto que está sendo visualizado. Se você quiser alterar o conteúdo do objeto original sem substituí-lo, use um dos métodos de transferência mostrados na tabela a seguir. Essas APIs transferem dados em ambas as direções ao mesmo tempo, sem substituir o objeto que está sendo visualizado:

|Provedor do Objeto|Origem do Objeto|
|---------------------|-------------------|
|<xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.TransferData%2A><br /><br /> — ou —<br /><br /> <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider.TransferObject%2A>|<xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource.TransferData%2A>|

## <a name="see-also"></a>Confira também
- [Como escrever um visualizador](create-custom-visualizers-of-data.md)
- [Walkthrough: escrevendo um visualizador em C #](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)
- [Instruções passo a passo: escrevendo um visualizador no Visual Basic](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)
- [Instruções passo a passo: escrevendo um visualizador no Visual Basic](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)
- [Considerações de segurança do Visualizador](../debugger/visualizer-security-considerations.md)