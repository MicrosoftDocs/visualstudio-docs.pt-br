---
title: Carregamento de documento atrasado | Microsoft Docs
description: Saiba mais sobre o carregamento de documentos atrasados no Visual Studio e como codificar extensões para que eles não consultem elementos em um documento antes de serem carregados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: fb07b8e2-a4e3-4cb0-b04f-8eb11c491f35
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 959af31f1986a4ff670adc5d74573cfb2bb850ce
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090977"
---
# <a name="delayed-document-loading"></a>Carregamento de documento atrasado

Quando um usuário reabre uma solução do Visual Studio, a maioria dos documentos associados não é carregada imediatamente. O quadro da janela do documento é criado em um estado de inicialização pendente e um documento de espaço reservado (chamado de quadro de stub) é colocado na tabela de documentos em execução (RDT).

Sua extensão pode fazer com que os documentos do projeto sejam carregados desnecessariamente consultando elementos nos documentos antes de serem carregados, o que pode aumentar a superfície geral da memória para o Visual Studio.

## <a name="document-loading"></a>Carregamento de documentos

O quadro de stub e o documento são totalmente inicializados quando o usuário acessa o documento, por exemplo, selecionando a guia do quadro da janela. O documento também pode ser inicializado por uma extensão que solicita os dados do documento, acessando o RDT diretamente para adquirir os dados do documento ou acessando o RDT indiretamente, fazendo uma das seguintes chamadas:

- O método de quadro de janela <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> .

- O método de quadro de janela <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> em qualquer uma das seguintes propriedades:

  - [__VSFPROPID. VSFPROPID_DocView](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocView>)

  - [__VSFPROPID. VSFPROPID_ViewHelper](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_ViewHelper>)

  - [__VSFPROPID. VSFPROPID_DocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_DocData>)

  - [__VSFPROPID. VSFPROPID_AltDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_AltDocData>)

  - [__VSFPROPID. VSFPROPID_RDTDocData](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_RDTDocData>)

  - [__VSFPROPID. VSFPROPID_SPProjContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID.VSFPROPID_SPProjContext>)

- Se sua extensão usar código gerenciado, você não deverá chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> a menos que tenha certeza de que o documento não está no estado de inicialização pendente ou se deseja que o documento seja totalmente inicializado. O motivo é que o método sempre retorna o objeto de dados Doc, criando-o se necessário. Em vez disso, você deve chamar um dos métodos na `IVsRunningDocumentTable4` interface.

- Se sua extensão usar C++, você poderá passar `null` para os parâmetros que não deseja.

- Você pode evitar o carregamento de documentos desnecessários chamando um dos métodos a seguir antes de solicitar as propriedades relevantes antes de solicitar outras propriedades:

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> usando [__VSFPROPID6. VSFPROPID_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID6.VSFPROPID_PendingInitialization>).

  - <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>. Esse método retorna um <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> objeto que inclui um valor para [_VSRDTFLAGS4. RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>) se o documento ainda não foi inicializado.

Você pode descobrir quando um documento foi carregado assinando o evento RDT que é gerado quando um documento é totalmente inicializado. Há duas possibilidades:

- Se o coletor de eventos implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2> , você poderá assinar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2.OnAfterAttributeChangeEx%2A> ,

- Caso contrário, você pode assinar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterAttributeChange%2A> .

O exemplo a seguir é um cenário de acesso a documentos hipotéticos: uma extensão do Visual Studio deseja exibir algumas informações sobre documentos abertos, por exemplo, a contagem de bloqueios de edição e algo sobre os dados do documento. Ele enumera os documentos no RDT usando e, <xref:Microsoft.VisualStudio.Shell.Interop.IEnumRunningDocuments> em seguida, chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> para cada documento para recuperar os dados de documento e de contagem de bloqueios de edição. Se o documento estiver no estado de inicialização pendente, a solicitação dos dados do documento fará com que ele seja desnecessariamente inicializado.

Uma maneira mais eficiente de acessar um documento é usar <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentEditLockCount%2A> para obter a contagem de bloqueios de edição e, em seguida, usar <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A> para determinar se o documento foi inicializado. Se os sinalizadores não incluírem [_VSRDTFLAGS4. RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>), o documento já foi inicializado e a solicitação dos dados do documento com o não <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentData%2A> causa nenhuma inicialização desnecessária. Se os sinalizadores incluírem [_VSRDTFLAGS4. RDT_PendingInitialization](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4.RDT_PendingInitialization>), a extensão deve evitar solicitar os dados do documento até que o documento seja inicializado. Essa inicialização pode ser detectada no `OnAfterAttributeChange(Ex)` manipulador de eventos.

## <a name="test-extensions-to-see-if-they-force-initialization"></a>Testar extensões para ver se elas forçam a inicialização

Não há nenhuma indicação visível para indicar se um documento foi inicializado, portanto, pode ser difícil descobrir se a extensão está forçando a inicialização. Você pode definir uma chave do registro que facilita a verificação, porque ela faz com que o título de cada documento que não está totalmente inicializado tenha o texto *[stub]* no título.

Em **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0\BackgroundSolutionLoad**, defina **StubTabTitleFormatString** como *{0} [stub]*.
