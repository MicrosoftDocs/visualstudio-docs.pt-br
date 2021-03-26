---
title: Suporte a ferramentas de Symbol-Browsing | Microsoft Docs
description: O Visual Studio fornece recursos de navegação de símbolos no Visual Studio. Saiba como estender esses recursos com bibliotecas para os símbolos em seus componentes.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d54f56ae3bc5fd5956f67400d84edfd4c8c9e55c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080561"
---
# <a name="supporting-symbol-browsing-tools"></a>Suporte a ferramentas de navegação de símbolo
As ferramentas **pesquisador de objetos**, **modo de exibição de classe**, **pesquisador de chamadas** e **Localizar resultados de símbolos** fornecem recursos de navegação de símbolos no Visual Studio. Essas ferramentas exibem modos de exibição de árvore hierárquica de símbolos e mostram as relações entre os símbolos na árvore. Os símbolos podem representar namespaces, objetos, classes, membros de classe e outros elementos de linguagem contidos em vários componentes. Os componentes incluem projetos do Visual Studio, componentes de .NET Framework externos e bibliotecas de tipo (. tlb). Para obter mais informações, consulte [exibindo a estrutura do código](../../ide/viewing-the-structure-of-code.md).

## <a name="symbol-browsing-libraries"></a>Bibliotecas de Symbol-Browsing
 Como um implementador de linguagem, você pode estender os recursos de navegação de símbolo do Visual Studio criando bibliotecas que acompanham os símbolos em seus componentes e fornecem as listas de símbolos para o Gerenciador de objetos do Visual Studio por meio de um conjunto de interfaces. Uma biblioteca é descrita pela <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2> interface. O Gerenciador de objetos do Visual Studio responde a solicitações de novos dados das ferramentas de navegação de símbolos, obtendo os dados das bibliotecas e organizando-os. Em seguida, ele preenche ou atualiza as ferramentas com os dados solicitados. Para obter uma referência ao Gerenciador de objetos do Visual Studio, <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2> , passe a <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> ID do serviço para o `GetService` método.

 Cada biblioteca deve ser registrada com o Gerenciador de objetos do Visual Studio, que coleta as informações em todas as bibliotecas. Para registrar uma biblioteca, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> método. Dependendo de qual ferramenta inicia a solicitação, o Gerenciador de objetos do Visual Studio localiza os dados de biblioteca e solicitações apropriados. Os dados trafegam entre as bibliotecas e o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objetos em listas de símbolos descritos pela <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> interface.

 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objetos é responsável por atualizar periodicamente as ferramentas de navegação de símbolo para refletir os dados mais atuais contidos nas bibliotecas.

 O diagrama a seguir contém um exemplo de elementos-chave do processo de solicitações/troca de dados entre uma biblioteca e o Gerenciador de objetos do Visual Studio. As interfaces no diagrama fazem parte de um aplicativo de código gerenciado.

 ![Fluxo de dados entre uma biblioteca e o Gerenciador de objetos](../../extensibility/internals/media/callbrowserdiagram.gif "CallBrowserDiagram")

 Para fornecer as listas de símbolos para o Gerenciador de objetos do Visual Studio, você deve primeiro registrar a biblioteca com o Gerenciador de objetos do Visual Studio chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> método. Depois que a biblioteca é registrada, o Gerenciador de objetos do Visual Studio solicita determinadas informações sobre os recursos da biblioteca. Por exemplo, ele solicita os sinalizadores de biblioteca e as categorias com suporte chamando os <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetLibFlags2%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetSupportedCategoryFields2%2A> métodos e. Em algum momento, quando uma das ferramentas solicita dados dessa biblioteca, o Gerenciador de objetos solicita a lista de símbolos de nível superior chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetList2%2A> método. Em resposta, a biblioteca fabrica uma lista de símbolos e a expõe para o Gerenciador de objetos do Visual Studio por meio da <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> interface. O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objetos determina quantos itens estão na lista chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A> método. Todas as solicitações a seguir estão relacionadas a um determinado item na lista e fornecem o número de índice do item em cada solicitação. O Gerenciador de objetos do Visual Studio prossegue a coletar as informações sobre o tipo, a acessibilidade e outras propriedades do item chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A> método.

 Ele determina o nome do item chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A> método e solicita as informações do ícone chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A> método. O ícone é exibido à esquerda do nome do item e descreve o tipo do item, a acessibilidade e outras propriedades.

 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objetos chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A> método para determinar se um determinado item de lista é expansível e tem itens filhos. Se a interface do usuário enviar uma solicitação para expandir um elemento, o Gerenciador de objetos solicitará a lista de símbolos filho chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A> método. O processo continua com diferentes partes da árvore que está sendo criada sob demanda.

> [!NOTE]
> Para implementar um provedor de símbolo de código nativo, use as <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibrary2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2> interfaces e.

## <a name="see-also"></a>Confira também
- [Como registrar uma biblioteca com o Gerenciador de Objetos](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [Como expor listas de símbolos fornecidos pela biblioteca ao Gerenciador de Objetos](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
- [Como identificar símbolos em uma biblioteca](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)
