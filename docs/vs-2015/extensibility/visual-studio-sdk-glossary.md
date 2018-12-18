---
title: Glossário do SDK do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- glossary [Visual Studio SDK]
ms.assetid: b64d432b-c39b-4904-ad18-3c3218b6e3aa
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0ec2300e8bf700deacd50a4a980e02aa4b903bae
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51758944"
---
# <a name="visual-studio-sdk-glossary"></a>Glossário do SDK do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este glossário fornece definições para termos que são usados no [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] documentação.  
  
## <a name="terms"></a>Termos  
 add-in  
 Um aplicativo de utilitário, driver ou outro software adicionadas a um aplicativo principal. No ambiente de desenvolvimento integrado do Visual Studio (IDE), um suplemento é um aplicativo baseado em automação que estende os recursos do IDE.  
  
 modelo de automação  
 O modelo de automação, conhecido nas versões anteriores do Visual Studio como o modelo de extensibilidade, é uma interface de programação que lhe dá acesso às rotinas subjacentes nessa unidade, o IDE. Suplementos, assistentes e macros usam objetos no modelo de automação para controlar ou estendem a funcionalidade do IDE.  
  
 contexto de interface do usuário do comando  
 Associação de um GUID com a visibilidade de um elemento, como uma barra de ferramentas ou um comando de interface do usuário. O contexto de interface do usuário do comando é diferente de contexto de seleção em que ele não está anexado a uma janela.  
  
 O contexto de interface do usuário do comando pode ser usado para:  
  
- Atribua um GUID para uma barra de ferramentas que aparece quando uma janela específica está ativada.  
  
- Atribua um GUID para a disponibilidade de um comando sem a necessidade de carregar ou executar um VSPackage.  
  
- Atribua um GUID para afetar a associação de chave ativa.  
  
- Atribua um GUID para ativar a gravação da macro.  
  
- Atribua um GUID para ativar o modo de depuração ou para alternar entre o design e modo de execução em um editor.  
  
  componente  
  Parte do software que pode ser feito parte da funcionalidade de um aplicativo sem ter qualquer pré-existente informações sobre a implementação do software aplicativo. A comunicação entre um componente e um aplicativo é unicamente por meio de interfaces de estilo do OLE.  
  
  Gerenciador de componentes  
  Um serviço, `SOleComponentManager`, que fornece serviços de coordenação de interface de não usuário para componentes de nível superior. O `SOleComponentManager` de serviço implementa o `IOleComponentManager` interface.  
  
  Gerenciador de componentes de interface do usuário  
  Um serviço, `SOleComponentUIManager`, que fornece serviços de coordenação de interface do usuário. O `SOleComponentUIManager` de serviço implementa as `IOleComponentUIManager` e `IOleInPlaceComponentUIManager` interfaces.  
  
  recipiente de contexto  
  Um `IVsUserContext` (objeto COM) do objeto anexado a um componente do ambiente. Esse objeto contém palavras-chave de pesquisa, palavras-chave de F1 e atributos relacionados ao componente. Além disso, recipientes de contexto apontam para qualquer recipientes de subcontexto que estão vinculados a eles.  
  
  provedor de contexto  
  Um componente do IDE que tenha um conjunto de contexto associado a ele. Esses componentes incluem uma janela de ferramentas, editor ou hierarquia do projeto.  
  
  designer  
  Uma interface de programação que permite aos usuários manipular elementos de interface do usuário (formulários, botões e outros controles).  
  
  DocData  
  Um objeto COM que encapsula os dados subjacentes de um documento em um mundo onde há separação de documento/exibição (por exemplo, no caso do editor de texto, isso seria o buffer de texto subjacente a todas as exibições do editor de texto). Se EditorFactory não fornecer a esse objeto, o IDE produzirá um em seu nome. A responsabilidade desse objeto é gerenciar a persistência de dados e a semântica de compartilhamento para vários modos de exibição sobre isso mesmo `DocData`. Se o `DocData` objeto dá suporte a `IOleCommandTarget` interface, ele será incluído no roteamento de comando da UIShell.  
  
  DocObject  
  Tecnologia usada para hospedar a interface do usuário em um intervalo fornecido pelo host. Mais especificamente, este termo se refere à qualquer inserção que dá suporte a `IOleDocument` e das interfaces relacionadas. Essa tecnologia tem muitos aplicativos potenciais, como um detalhe de implementação de documentos COM, janelas de ferramentas no Visual Basic 5.0, designers do ActiveX no Visual Basic 6.0 e assim por diante.  
  
  documento  
  Usado para se referir genericamente ao documento como um todo — tanto a `DocData` e o `DocView`. Por exemplo, um DocumentFrame contém um `DocView`, mas ele também mantém uma referência ao `DocData` para lidar com a persistência.  
  
  DocView  
  O DocObject/incorporação/WindowPane com a qual o usuário interage para exibir e manipular subjacente `DocData`. Observe que os usuários não tiram proveito da separação de documento/exibição que faz parte do `DocObject` design da interface. Os usuários usar um DocObject inteira para atuar como um modo de exibição em vez de usar uma noção mais abstrata (e menos formalizado) dos dados subjacentes, conhecidos como `DocData`. `DocView` objetos sempre são inseridos com objetos de quadro (janelas MDI filho) do documento do IDE.  
  
  DTE  
  O `DTE` objeto (extensibilidade de ferramentas de desenvolvimento) é o ponto de acesso mais alto no modelo de automação do Visual Studio, que lhe permite automatizar e estender o IDE programaticamente.  
  
  Janela de ajuda dinâmica  
  Janela de ferramenta que é implementada pelo IDE e exibe uma lista de tópicos da Ajuda F1 ou de palavra-chave de pesquisa.  
  
  editor  
  Código (CLSID classe) que implementa o `DocView`. Ele também implementa `DocData` se a separação de dados do modo de exibição é compatível.  
  
  extensão  
  Um recurso que modifica, personaliza ou adiciona a um IDE. Você criar extensões usando o modelo de automação ou VSPackages.  
  
  editor externo  
  Um editor que não é específico para o IDE, como o Microsoft Word. Ele foi registrado por meio de seus próprios mecanismos e pode ser usado fora do IDE. Se este editor pode ser inserido, ele será exibido dentro de uma janela no IDE. Se ele não pode ser inserido, uma janela de nível superior separada será criada.  
  
  hierarquia  
  Árvore de nós, cada nó associado a um conjunto de propriedades.  
  
  componente de nível superior independente  
  Um componente que usa uma janela de nível superior sem janela restrita e pode operar efetivamente como uma janela de aplicativo autônomo, mas é implementado como um objeto em processo. Portanto, um componente independente de nível superior deve coordenar modalidade e serviços de loop de mensagem com o IDE. Objetos em processo não tem seu próprio loop de mensagem.  
  
  provedor de informações  
  O provedor de informações é um módulo que pode pesquisar palavras-chave e retornar uma lista de tópicos, na forma de `IVsUserContextItem` objetos. Para fornecer itens de palavra-chave F1 e pesquisa para o provedor de informações, registrar o seu arquivo de Ajuda compilado (. Nos formatos HxS) com o sistema. Os tópicos da Ajuda nesses arquivos são usados para fornecer a lista de tópicos exibidos na janela Ajuda dinâmica e mostra se um usuário pressiona F1.  
  
  no local componente  
  Um objeto de VSPackage que implementa o `IOleInPlaceComponent` interface para gerenciar uma janela que visualmente está contida dentro de uma janela de documentos pertencente a IDE. Componentes no local não participam padrão OLE-mesclagem de menu; em vez disso, eles integram seus elementos de interface do usuário do IDE.  
  
  Há dois tipos de componentes no local: conectada in-loco componentes e controles de componente.  
  
  Conectada in-loco componentes têm menus, barras de ferramentas e comandos que são totalmente integrados a interface do usuário do IDE, que aparecem como se eles foram criados diretamente no IDE.  
  
  Controles de componente não tem qualquer um dos seus próprios elementos de interface do usuário integrados ao IDE; em vez disso, use as barras de ferramentas, comandos e menus do IDE. Por exemplo, o comando de negrito pode ser usado como uma palavra selecionada em um controle rich text inserido em um formulário de negrito. No entanto, os controles de componente podem solicitar que os elementos de interface do usuário específicos do componente instalados dinamicamente seja exibido.  
  
  serviço de linguagem  
  Um conjunto de objetos que permite aos desenvolvedores de VSPackage implementar recursos de editores de código de idioma do computador, como o texto de marcação e colorir.  
  
  Projeto arquivos diversos  
  Projeto usado para arquivos abertos de casa que não estão em qualquer projeto. A lista de itens neste projeto não é persistente.  
  
  projeto  
  Projetos são compostos de objetos da hierarquia, ou COM objetos que implementam o `IVsHierarchy` interface.  
  
  designer de projeto específico ou editor  
  Um designer que não pode ser usado independentemente do tipo de projeto. Todos os designers específicos do projeto devem inserir suas informações de fábrica de Editor no registro. O IDE, em seguida, pode instanciar o designer sempre que um determinado tipo de arquivo é aberto em um projeto específico.  
  
  janela de tipo de projeto  
  Uma janela que rastreia constantemente a hierarquia do projeto ativo no momento e o item do contexto de seleção global. Tipo de projeto windows usa o `SVsTrackSelectionEx` serviço para o IDE das alterações de alerta e exibir comentários para o usuário. Gerenciador de soluções é um exemplo de uma janela do tipo de projeto.  
  
  Janela de Propriedades  
  Anteriormente conhecido como navegador de propriedade.  
  
  Projetos de referência  
  Projeto que não exigem que os arquivos para o projeto estar no mesmo diretório. Em vez disso, referências aos arquivos de outros diretórios não relacionados são armazenadas e mantidas pelo próprio projeto.  
  
  tabela de documento em execução  
  Estrutura interna pela qual o IDE mantém a lista de todos os documentos abertos no momento. Essa lista inclui todos os documentos abertos na memória, independentemente se os documentos estão sendo editados. Um documento é qualquer item que é salvo, incluindo procedimentos armazenados abertos em um editor, arquivos em um projeto ou arquivo de projeto principal (por exemplo, *. vcproj arquivo).  
  
  Contexto de seleção  
  Dados que faz parte dos detalhes de cada janela no IDE e são usados para controlar as seleções de Active Directory. Contexto de seleção consiste em:  
  
- Ponteiro para o `IVsHierarchy` interface da hierarquia do projeto  
  
- Identificador do item do item de projeto.  
  
- Ponteiro para o `ISelectionContainer` interface fornecendo acesso às propriedades dos objetos do Active Directory.  
  
- Matriz de valores de elemento.  
  
  serviço  
  Um contrato para um conjunto de interfaces COM que residem em um único objeto COM. Quando você cria um serviço, que é identificado por um GUID, você pode definir o conjunto de interfaces COM que executa o serviço. Objetos COM usam serviços para se comunicar entre si.  
  
  Solução  
  Grupo de projetos relacionados com o qual um usuário trabalha.  
  
  designer padrão  
  Um designer que pode ser usado independentemente do tipo de projeto. Todos os designers padrão Insira suas informações de fábrica de Editor do registro. O IDE, em seguida, pode instanciar o designer sempre que um arquivo com uma extensão específica é aberto. Os dados devem persistir em um arquivo.  
  
  editor padrão  
  Editor que pode ser usada independentemente de qualquer tipo de projeto específico. Esses editores têm EditorFactories registrada no registro. Isso permite que o IDE localizar e invocar o editor.  
  
  editor padrão do sistema operacional  
  Não é Visual Studio de incorporação específico. Ele é registrado usando as teclas de Win32 bem conhecidas (por exemplo, o Gerenciador de Win32 sabe como chamar). Se tal um editor pode ser inserido, o editor ainda aparecerá em seu lugar no IDE. Caso contrário, uma janela de nível superior separada é criada para esses editores.  
  
  recipiente de subcontexto  
  Um `IVsUserContext` objeto vinculado a um recipiente de contexto. Esse objeto contém palavras-chave de pesquisa, palavras-chave de F1 e atributos de uma seleção dentro de um componente do IDE. Exemplos de subcontexto incluem um comando em uma janela de ferramentas ou uma palavra-chave em um editor.  
  
  Lista de tarefas  
  Janela de ferramenta que é implementada pelo IDE e exibe uma lista de tarefas ativas.  
  
  Buffer de texto  
  Nome comum do objeto `VSTextBuffer`.  
  
  Exibição de texto  
  Nome comum do objeto `VSTextView`.  
  
  componente de nível superior da ferramenta  
  Um componente que opera como uma janela pop-up sem janela restrita, coordenação intimamente com a interface do usuário do IDE. Como componentes independentes de nível superior, os componentes de nível superior da ferramenta também devem coordenar modalidade e serviços de loop de mensagem com o IDE.  
  
  componente de nível superior  
  Um objeto de VSPackage que gerencia uma janela de nível superior sem janela restrita, em vez de área de cliente de uma janela do IDE. Componentes de nível superior é implementar o `IOleComponent` interface para tirar proveito dos serviços de loop de mensagem, como o acesso para o tempo ocioso.  
  
  Interface do usuário do Active Directory  
  Um objeto de VSPackage que é visível e tem foco no momento.  
  
  Hierarquia de interface do usuário  
  Um objeto COM que implementa o `IVsUIHierarchy` interface para permitir a exibição de uma hierarquia. A janela de hierarquia de interface do usuário implementa o `ISelectionContainer` de interface para atualizar a janela Propriedades; outras janelas do tipo de projeto podem usar essa implementação, se desejado.  
  
  VSCT  
  Tabela de comando do Visual Studio. O arquivo. VSCT contém informações sobre o posicionamento e comportamentos de menus, barras de ferramentas e comandos no formato XML.  
  
  VSPackage  
  Um componente instalável de software que estende o IDE do Visual Studio, contribuindo com um ou mais dos seguintes: interface do usuário, serviços, tipos de projeto ou designer do editor. Um VSPackage consiste em um objeto COM que implementa o `IVsPackage` interface e um ou mais outros objetos COM que implementam outras interfaces para dar suporte a seleção e outros recursos. Além disso, um VSPackage possui requisitos de registro específico.

