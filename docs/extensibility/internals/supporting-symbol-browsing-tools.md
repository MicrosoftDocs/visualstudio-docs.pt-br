---
title: Suporte a ferramentas de navegação de símbolo | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- symbols, symbol-browsing tools
- browsers, symbol browsers
- symbol-browsing tools
- libraries
- IVsLibrary2 interface, symbol-browsing tools
- IVsSimpleLibrary2 interface, symbol-browsing tools
- symbol-browsing tools, library manager
- symbols
- libraries, symbol-browsing tools
ms.assetid: 70d8c9e5-4b0b-4a69-b3b3-90f36debe880
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 08185f64310da610253dc35e69323b17ab0177fd
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31134574"
---
# <a name="supporting-symbol-browsing-tools"></a>Suporte a ferramentas de navegação de símbolo
**Pesquisador de objetos**, **exibição de classe**, **Pesquisador de chamadas** e **localizar resultados de símbolos** ferramentas oferecem funcionalidades no Visual Studio de navegação de símbolo. Essas ferramentas exibem modos de exibição de árvore hierárquica de símbolos e mostram as relações entre os símbolos na árvore. Os símbolos podem representar namespaces, objetos, classes, membros de classe e outros elementos de linguagem contidos em vários componentes. Os componentes incluem projetos do Visual Studio, externos [!INCLUDE[dnprdnshort](../../code-quality/includes/dnprdnshort_md.md)] componentes e bibliotecas de tipos (. tlb). Para obter mais informações, consulte [Exibindo a estrutura do código](../../ide/viewing-the-structure-of-code.md).  
  
## <a name="symbol-browsing-libraries"></a>Bibliotecas de navegação de símbolo  
 Implementador de idioma, você pode estender os recursos de pesquisa de símbolo do Visual Studio criando bibliotecas que rastrear os símbolos em seus componentes e fornecem a lista de símbolos para o Gerenciador de objeto do Visual Studio por meio de um conjunto de interfaces. Uma biblioteca é descrita pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2> interface. O Gerenciador de objeto do Visual Studio responde a solicitações de novos dados das ferramentas de navegação de símbolo por obter os dados das bibliotecas e organizá-las. Posteriormente, ele preenche ou atualiza as ferramentas com os dados solicitados. Para obter uma referência para o Gerenciador de objeto do Visual Studio, <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>, passar o <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> serviço ID para o `GetService` método.  
  
 Cada biblioteca deve registrar com o Gerenciador de objeto do Visual Studio, que coleta as informações sobre todas as bibliotecas. Para registrar uma biblioteca, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> método. Dependendo de qual ferramenta inicia a solicitação, o Gerenciador de objeto do Visual Studio localiza a biblioteca apropriada e solicitações de dados. Os dados são transferidos entre as bibliotecas e o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objetos em listas de símbolos descritos pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> interface.  
  
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objeto é responsável por atualizar periodicamente ferramentas de navegação de símbolo para refletir os dados mais atuais contidos nas bibliotecas.  
  
 O diagrama a seguir contém um exemplo dos principais elementos do processo de troca de solicitações/dados entre uma biblioteca e o Gerenciador de objeto do Visual Studio. As interfaces no diagrama são parte de um aplicativo de código gerenciado.  
  
 ![Fluxo de dados entre uma biblioteca e o Gerenciador de objeto](../../extensibility/internals/media/callbrowserdiagram.gif "CallBrowserDiagram")  
  
 Para fornecer a lista de símbolos para o Gerenciador de objeto do Visual Studio, você deve primeiro registrar a biblioteca com o Gerenciador de objeto do Visual Studio ao chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> método. Depois que a biblioteca for registrada, o Gerenciador de objeto do Visual Studio solicitações certas informações sobre os recursos da biblioteca. Por exemplo, ele solicita os sinalizadores de biblioteca e suporte para categorias chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetLibFlags2%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetSupportedCategoryFields2%2A> métodos. Em algum momento, quando uma das ferramentas de solicitações de dados desta biblioteca, o Gerenciador de objeto solicita o nível superior da lista de símbolos chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetList2%2A> método. Em resposta, a biblioteca fabrica uma lista de símbolos e expõe para o Gerenciador de objeto do Visual Studio por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> interface. O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objeto determina quantos itens estão na lista chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A> método. Todas as solicitações de seguir relacionam a um determinado item na lista e fornecem o número de índice do item em cada solicitação. O Gerenciador de objeto do Visual Studio prossegue para coletar as informações sobre o tipo, a acessibilidade e outras propriedades do item ao chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A> método.  
  
 Determina o nome do item chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A> método e solicita as informações de ícone chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A> método. O ícone é exibido à esquerda do nome do item e descreve o tipo de item, a acessibilidade e outras propriedades.  
  
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] chamadas de Gerenciador de objeto de <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A> método para determinar se um determinado item de lista é expansível e tem itens filhos. Se a interface do usuário envia uma solicitação para expandir um elemento, o Gerenciador de objeto solicita a lista de filhos de símbolos chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A> método. O processo continua com diferentes partes da árvore que está sendo criada sob demanda.  
  
> [!NOTE]
>  Para implementar um provedor de símbolo de código nativo, use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibrary2> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2> interfaces.  
  
## <a name="see-also"></a>Consulte também  
 [Como: registrar uma biblioteca com o Gerenciador de objeto](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)   
 [Como: expor listas de símbolos fornecidas pela biblioteca para o Gerenciador de objeto](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)   
 [Como identificar símbolos em uma biblioteca](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)