---
title: controle Indicador
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
f1_keywords:
- VST.Toolbox.Bookmark
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- bookmarks, controlling
- Bookmark control, data binding
- Bookmark control, events
- Bookmark control
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: 242a4692bc75715e661244dc8f513d30cc9480ed
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248186"
---
# <a name="bookmark-control"></a>controle Indicador
  O controle <xref:Microsoft.Office.Tools.Word.Bookmark> é um indicador que tem um nome exclusivo, expõe eventos e pode ser vinculado a dados. O indicador pode ser usado como um espaço reservado para marcar um item ou local em um documento do Microsoft Office Word. O <xref:Microsoft.Office.Tools.Word.Bookmark> controle é uma combinação de um <xref:Microsoft.Office.Interop.Word.Bookmark> objeto e um <xref:Microsoft.Office.Interop.Word.Range> objeto.

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 Em projetos de nível de documento, você pode adicionar <xref:Microsoft.Office.Tools.Word.Bookmark> controles para o documento em tempo de design ou em tempo de execução. Em projetos de suplemento do VSTO, você pode adicionar <xref:Microsoft.Office.Tools.Word.Bookmark> controles para qualquer documento aberto no tempo de execução. Confira mais informações em [Como: Adicionar controles de indicador a documentos do Word](../vsto/how-to-add-bookmark-controls-to-word-documents.md).

## <a name="bind-data-to-the-control"></a>Associar dados ao controle
 Um <xref:Microsoft.Office.Tools.Word.Bookmark> controle dá suporte à vinculação de dados simples. O indicador deve ser associado a uma fonte de dados usando o <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> propriedade. A propriedade de associação de dados padrão do indicador é o <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> propriedade.

 Se os dados no conjunto de dados associado forem atualizados, o <xref:Microsoft.Office.Tools.Word.Bookmark> controle mostra as alterações.

 Em projetos de nível de documento, você também pode associar dados aos indicadores usando o **fontes de dados** janela. Confira mais informações em [Como: Preencher documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md).

## <a name="formatting"></a>Formatação
 Formatação que pode ser aplicado a um <xref:Microsoft.Office.Interop.Word.Bookmark> pode ser aplicado a um <xref:Microsoft.Office.Tools.Word.Bookmark> controle. Essa formatação inclui fontes, recuos, espaçamento, numeração e estilos.

## <a name="assign-text-to-the-bookmark"></a>Atribuir o texto para o indicador
 Uma outra diferença entre um <xref:Microsoft.Office.Interop.Word.Bookmark?displayProperty=nameWithType> objeto e um <xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType> controle é como ele se comporta quando o texto é atribuído para o indicador. Se você atribuir o texto a um comprimento de zero <xref:Microsoft.Office.Interop.Word.Bookmark?displayProperty=nameWithType>, o texto é acrescentado à direita do indicador e o indicador permanece tem comprimento zero. No entanto, se você atribuir o texto a um comprimento de zero <xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType>, o texto é inserido no indicador e o comprimento do indicador se expande para o número total de caracteres inseridos.

 O <xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType> controle também tem o <xref:Microsoft.Office.Tools.Word.Bookmark.Text?displayProperty=nameWithType> propriedade. Essa propriedade é diferente do <xref:Microsoft.Office.Interop.Word.Range.Text?displayProperty=nameWithType> propriedade que está disponível na <xref:Microsoft.Office.Tools.Word.Bookmark.Range?displayProperty=nameWithType> propriedade de um <xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType> controle, ou o <xref:Microsoft.Office.Interop.Word.Bookmark.Range?displayProperty=nameWithType> propriedade de um <xref:Microsoft.Office.Interop.Word.Bookmark?displayProperty=nameWithType> objeto.

|Propriedade de texto|Descrição|
|-------------------|-----------------|
|<xref:Microsoft.Office.Tools.Word.Bookmark.Text?displayProperty=nameWithType>|Use essa propriedade para exibir o texto dentro do indicador e deixar o indicador no documento. A atribuição de texto para o indicador expande o intervalo do indicador e não exclui o indicador.<br /><br /> Por exemplo, `Bookmark1.Text = "Hello world"` insere o texto do indicador e deixa o indicador intacto.|
|<xref:Microsoft.Office.Interop.Word.Range.Text?displayProperty=nameWithType>|Use essa propriedade para exibir o texto no local do indicador e exclui automaticamente o indicador. Por exemplo, `Bookmark1.Range.Text = "Hello world"` insere o texto do indicador e exclui o indicador.|

## <a name="rename-the-control-at-design-time"></a>Renomeie o controle em tempo de design
 Em projetos de nível de documento, quando você arrasta uma <xref:Microsoft.Office.Tools.Word.Bookmark> controlar do **caixa de ferramentas** ao seu documento, o Visual Studio gera automaticamente um nome para o controle. Você pode alterar o nome do controle na **propriedades** janela.

## <a name="overlapping-controls"></a>Sobrepondo controles
 Controles de indicador podem se sobrepor uns aos outros. O mesmo texto pode ser compartilhado por mais de um indicador. Quando você atribui um novo texto a um dos indicadores sobrepostos, ele contém apenas o novo texto e os indicadores de não se sobrepõem. O outro marcador agora contém apenas o texto que não era compartilhado entre os indicadores de sobreposição originais.

 A tabela a seguir mostra como a frase "Este é o texto de exemplo". é compartilhado por dois indicadores sobrepostos:

|Indicador|Texto|
|--------------|----------|
|Sobreposição de indicadores|[Esta é a amostra {] texto.}|
|Bookmark1|Este é exemplo|
|Bookmark2|texto de exemplo.|

 Se você atribuir o novo texto "Esta é uma substituição." para Bookmark1, os indicadores não se sobrepõem e Bookmark2 retém apenas o texto que originalmente não era parte do Bookmark1.

|Indicador|Texto|
|--------------|----------|
|Dois indicadores separados|[Esta é a substituição] {text}.|
|Bookmark1|Esse é o substituto|
|Bookmark2|Texto.|

Se você alterar o texto de um indicador que contém outro indicador, o indicador de interno não é excluído. No entanto, o indicador interno torna-se um indicador vazio e move para o fim do indicador externo.

A tabela a seguir mostra como a frase "Este é o texto de exemplo". é compartilhado por um indicador que está contido dentro de outro indicador:

|Indicador|Texto|
|--------------|----------|
|Sobreposição de indicadores|[Este é o texto de {exemplo}].|
|Bookmark1|Este é o texto de exemplo.|
|Bookmark2|exemplo|

 Se você atribuir o novo texto "Esta é uma substituição." para Bookmark1, os indicadores não são sobrepostas e Bookmark2 torna-se um indicador vazio que está localizado no final da Bookmark1.

|Indicador|Texto|
|--------------|----------|
|Dois indicadores separados|[Esta é uma substituição.]{}|
|Bookmark1|Esse é o substituto.|
|Bookmark2|*\<vazio >*|

## <a name="events"></a>Eventos

Os eventos a seguir estão disponíveis para o <xref:Microsoft.Office.Tools.Word.Bookmark> controle:

-   <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeDoubleClick>

-   <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeRightClick>

-   <xref:Microsoft.Office.Tools.Word.Bookmark.BindingContextChanged>

-   <xref:Microsoft.Office.Tools.Word.Bookmark.Deselected>

-   <xref:System.ComponentModel.IComponent.Disposed>

-   <xref:Microsoft.Office.Tools.Word.Bookmark.Selected>

-   <xref:Microsoft.Office.Tools.Word.Bookmark.SelectionChange>

## <a name="see-also"></a>Consulte também

- [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)
- [Como: Adicionar controles de indicador a documentos do Word](../vsto/how-to-add-bookmark-controls-to-word-documents.md)
- [Passo a passo: Criar menus de atalho para indicadores](../vsto/walkthrough-creating-shortcut-menus-for-bookmarks.md)
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)