---
title: Atraso de carregamento do documento | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fb07b8e2-a4e3-4cb0-b04f-8eb11c491f35
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 94d79af00fced81dc7da38f323598ade926d26f4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755481"
---
# <a name="delayed-document-loading"></a>Atraso no carregamento de documentos
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Quando um usuário é reaberto em uma solução do Visual Studio, a maioria dos documentos associados não é carregada imediatamente. O quadro de janela do documento é criado em um estado pendente de inicialização, e um documento de espaço reservado (chamado de um quadro de stub) é colocado na tabela de documento em execução (RDT).  
  
 Sua extensão pode causar a documentos do projeto para ser carregado desnecessariamente consultando elementos nos documentos antes que eles sejam carregados. Isso pode aumentar o espaço de memória geral para o Visual Studio.  
  
## <a name="document-loading"></a>Carregamento do documento  
 O quadro de stub e o documento estão totalmente inicializados quando o usuário acessa o documento, por exemplo, selecionando a guia do quadro da janela. O documento também pode ser inicializado por uma extensão que solicita os dados do documento, acessando o RDT diretamente para adquirir os dados do documento ou acessar o RDT indiretamente, fazendo uma das seguintes chamadas:  
  
- O método show do quadro de janela: <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>.  
  
- Método GetProperty do quadro de janela <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> em qualquer uma das seguintes propriedades:  
  
  -   <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  -   <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  -   <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  -   <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  -   <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  -   <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>  
  
  Se sua extensão usar código gerenciado, você não deve chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> , a menos que você tiver certeza de que o documento não está no estado pendente de inicialização, ou você deseja que o documento seja totalmente inicializada... Isso ocorre porque esse método sempre retorna o documento de objeto de dados, criá-lo se necessário. Em vez disso, você deve chamar um dos métodos na interface IVsRunningDocumentTable4.  
  
  Se sua extensão usar C++, você pode passar `null` para os parâmetros que você não deseja.  
  
  Você pode evitar o carregamento do documento desnecessárias chamando um dos métodos a seguir antes de você perguntar para as propriedades relevantes: antes de você perguntar para outras propriedades.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> usando <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID6>.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A>. Esse método retorna um <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> objeto que inclui um valor para <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4> se o documento ainda não foi inicializado.  
  
  Você pode descobrir quando um documento foi carregado por assinatura do evento RDT que é gerado quando um documento está totalmente inicializado. Há duas possibilidades:  
  
- Se o coletor de eventos implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2>, você pode assinar <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents2.OnAfterAttributeChangeEx%2A>,  
  
- Caso contrário, você pode assinar <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterAttributeChange%2A>.  
  
  Este é um cenário de acesso do documento hipotético. Uma extensão que deseja exibir algumas informações sobre como abrir documentos do Visual Studio, por exemplo Editar Bloquear contagem e algo sobre os dados do documento. Enumera os documentos usando o RDT <xref:Microsoft.VisualStudio.Shell.Interop.IEnumRunningDocuments>, em seguida, chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.GetDocumentInfo%2A> para cada documento para recuperar os dados de documento e de contagem de bloqueio editar. Se o documento estiver no estado pendente de inicialização, solicita os dados de documento faz com que ele seja inicializada desnecessariamente.  
  
  Uma maneira mais eficiente de fazer isso é usar <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentEditLockCount%2A> para obter a contagem de bloqueio de edição e, em seguida, use <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentFlags%2A> para determinar se o documento foi inicializado. Se não incluir os sinalizadores <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4>, o documento já foi inicializado e solicita os dados de documento com <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable4.GetDocumentData%2A> não faz com que qualquer inicialização desnecessária. Se os sinalizadores de incluir <xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS4>, a extensão deve evitar solicita os dados de documento até que o documento seja inicializado. Isso pode ser detectado no manipulador de eventos OnAfterAttributeChange(Ex).  
  
## <a name="testing-extensions-to-see-if-they-force-initialization"></a>Testando extensões para ver se eles forçam a inicialização  
 Não há nenhuma indicação visível para indicar se um documento foi inicializado, portanto, pode ser difícil descobrir se sua extensão está forçando a inicialização. Você pode definir uma chave do registro que facilita a verificação, porque ele faz com que o título de todos os documentos que não esteja totalmente inicializado para ter o texto `[Stub]` no título.  
  
 Na **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0\BackgroundSolutionLoad]**, defina **StubTabTitleFormatString** para  **{0} [Stub]**.

