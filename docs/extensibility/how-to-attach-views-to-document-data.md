---
title: Como anexar exibições a dados de documentos | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - attach views to document data
ms.assetid: f92c0838-45be-42b8-9c55-713e9bb8df07
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d5437e3a5d4fb0d6d33d570eb4d8923245cb287b
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905895"
---
# <a name="how-to-attach-views-to-document-data"></a>Como anexar exibições aos dados do documento
Se você tiver uma nova exibição de documento, poderá anexá-la a um objeto de dados de documento existente.

## <a name="to-determine-if-you-can-attach-a-view-to-an-existing-document-data-object"></a>Para determinar se você pode anexar uma exibição a um objeto de dados de documento existente

1. Implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>.

2. Na sua implementação do `IVsEditorFactory::CreateEditorInstance` , chame `QueryInterface` no objeto de dados de documento existente quando o IDE chama sua `CreateEditorInstance` implementação.

    `QueryInterface`A chamada permite que você examine o objeto de dados de documento existente, que é especificado no `punkDocDataExisting` parâmetro.

    No entanto, as interfaces exatas que você deve consultar dependem do editor que está abrindo o documento, conforme descrito na etapa 4.

3. Se você não encontrar as interfaces apropriadas no objeto de dados de documento existente, retorne um código de erro para o editor indicando que o objeto de dados do documento é incompatível com seu editor.

    Na implementação do IDE do <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> , uma caixa de mensagem notifica que o documento está aberto em outro editor e pergunta se você deseja fechá-lo.

4. Se você fechar este documento, o Visual Studio chamará a fábrica do editor por uma segunda vez. Nessa chamada, o `DocDataExisting` parâmetro é igual a NULL. A implementação de fábrica do editor pode abrir o objeto de dados do documento em seu próprio editor.

   > [!NOTE]
   > Para determinar se você pode trabalhar com um objeto de dados de documento existente, você também pode usar o conhecimento privado da implementação da interface ao converter um ponteiro para a [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] classe real de sua implementação privada. Por exemplo, todos os editores padrão implementam `IVsPersistFileFormat` , que herdam de <xref:Microsoft.VisualStudio.OLE.Interop.IPersist> . Assim, você pode chamar `QueryInterface` for <xref:Microsoft.VisualStudio.OLE.Interop.IPersist.GetClassID%2A> e, se a ID da classe no objeto de dados do documento existente corresponder à ID de classe da implementação, você poderá trabalhar com o objeto de dados do documento.

## <a name="robust-programming"></a>Programação robusta
 Quando o Visual Studio chama a implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método, ele passa de volta um ponteiro para o objeto de dados de documento existente no `punkDocDataExisting` parâmetro, se houver. Examine o objeto de dados do documento retornado em `punkDocDataExisting` para determinar se o objeto de dados do documento é apropriado para seu editor, conforme descrito na observação na etapa 4 do procedimento neste tópico. Se for apropriado, a fábrica do editor deverá fornecer uma segunda exibição para os dados, conforme descrito em suporte a [vários modos](../extensibility/supporting-multiple-document-views.md)de exibição de documento. Caso contrário, ele deverá exibir uma mensagem de erro apropriada.

## <a name="see-also"></a>Confira também
- [Suporte a exibições de vários documentos](../extensibility/supporting-multiple-document-views.md)
- [Dados de documento e exibição de documento em editores personalizados](../extensibility/document-data-and-document-view-in-custom-editors.md)
