---
title: Dando suporte a exibições de vários documentos | Microsoft Docs
description: Saiba como fornecer mais de uma exibição de um documento usando dados de documento separados e objetos de exibição de documento para seu editor personalizado no SDK do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - multiple document views
ms.assetid: c7ec2366-91c4-477f-908d-e89068bdb3e3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e54ee028c6a7db2d5d2ea1ab609be6c2887c9829
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056201"
---
# <a name="supporting-multiple-document-views"></a>Dando suporte a várias exibições de documento
Você pode fornecer mais de uma exibição de um documento criando dados de documento separados e objetos de exibição de documento para seu editor. Alguns casos em que uma exibição de documento adicional seria útil são:

- Novo suporte à janela: você deseja que o editor forneça duas ou mais exibições do mesmo tipo, para que um usuário que já tenha uma janela aberta no editor possa abrir uma nova janela selecionando o comando **nova janela** no menu **janela** .

- Suporte para exibição de formulário e código: você quer que seu editor forneça exibições de tipos diferentes. [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], por exemplo, fornece uma exibição de formulário e uma exibição de código.

  Para obter mais informações sobre isso, consulte o procedimento CreateEditorInstance no arquivo EditorFactory. cs no projeto de editor personalizado criado pelo modelo de pacote do Visual Studio. Para obter mais informações sobre este projeto, consulte [passo a passos: Criando um editor personalizado](../extensibility/walkthrough-creating-a-custom-editor.md).

## <a name="synchronizing-views"></a>Sincronizando exibições
 Quando você implementa vários modos de exibição, o objeto de dados do documento é responsável por manter todas as exibições sincronizadas com os dados. Você pode usar as interfaces de manipulação de eventos no <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> para sincronizar vários modos de exibição com os dados.

 Se você não usar o <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> objeto para sincronizar várias exibições, deverá implementar seu próprio sistema de eventos para lidar com as alterações feitas no objeto de dados do documento. Você pode usar diferentes níveis de granularidade para manter várias exibições atualizadas. Com uma configuração de granularidade máxima, conforme você digita em uma exibição, as outras exibições são atualizadas imediatamente. Com a granularidade mínima, outras exibições não são atualizadas até que sejam ativadas.

## <a name="determining-whether-document-data-is-already-open"></a>Determinando se os dados do documento já estão abertos
 A tabela de documentos em execução (RDT) no ambiente de desenvolvimento integrado (IDE) ajuda a controlar se os dados de um documento já estão abertos, conforme mostrado no diagrama a seguir.

 ![Gráfico DocDataView](../extensibility/media/docdataview.gif "Docdataview") Várias exibições

 Por padrão, cada exibição (objeto de exibição de documento) está contida em seu próprio quadro de janela ( <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> ). Como já observado, no entanto, os dados do documento podem ser exibidos em vários modos de exibição. Para habilitar isso, o Visual Studio verifica o RDT para determinar se o documento em questão já está aberto em um editor. Quando o IDE chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> para criar o editor, um valor não nulo retornado no `punkDocDataExisting` parâmetro indica que o documento já está aberto em outro editor. Para obter mais informações sobre como as funções RDT, consulte [executando a tabela de documentos](../extensibility/internals/running-document-table.md).

 Em sua <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> implementação, examine o objeto de dados do documento retornado `punkDocDataExisting` para determinar se os dados do documento são apropriados para o seu editor. (Por exemplo, somente dados HTML devem ser exibidos por um editor de HTML.) Se for apropriado, a fábrica do editor deverá fornecer uma segunda exibição para os dados. Se o `punkDocDataExisting` parâmetro não for `NULL` , é possível que o objeto de dados do documento esteja aberto em outro editor ou, mais provavelmente, que os dados do documento já estejam abertos em um modo de exibição diferente com o mesmo editor. Se os dados do documento estiverem abertos em um editor diferente para o qual a fábrica do editor não oferece suporte, o Visual Studio não abrirá a fábrica do editor. Para obter mais informações, consulte [como anexar exibições a dados de documentos](../extensibility/how-to-attach-views-to-document-data.md).
