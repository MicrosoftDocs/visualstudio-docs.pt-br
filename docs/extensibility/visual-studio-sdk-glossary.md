---
title: Visual Studio do Glossário do SDK | Microsoft Docs
description: Este glossário fornece definições para termos que são usados na documentação Visual Studio SDK.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- glossary [Visual Studio SDK]
ms.assetid: b64d432b-c39b-4904-ad18-3c3218b6e3aa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 49e91a64220882eea196819a1860052dc871bec4
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905417"
---
# <a name="visual-studio-sdk-glossary"></a>Visual Studio glossário do SDK
Este glossário fornece definições para termos que são usados na [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] documentação.

## <a name="terms"></a>Termos
 add-in Um aplicativo utilitário, driver ou outro software adicionado a um aplicativo primário. No Visual Studio IDE (ambiente de desenvolvimento integrado), um complemento é um aplicativo baseado em Automação que estende os recursos do IDE.

 modelo de automação O modelo de automação, conhecido nas versões anteriores do Visual Studio como o modelo de extensibilidade, é uma interface de programação que fornece acesso às rotinas subjacentes que impulsionam o IDE. Os complementos, assistentes e macros usam objetos no modelo de automação para controlar ou estender a funcionalidade do IDE.

 contexto da interface do usuário do comando Associação de um GUID com a visibilidade de um comando ou elemento de interface do usuário, como uma barra de ferramentas. O contexto da interface do usuário do comando é diferente do contexto de seleção, já que ele não está anexado a uma janela.

 O contexto da interface do usuário de comando pode ser usado para:

- Atribua um GUID a uma barra de ferramentas que aparece quando uma janela específica é ativada.

- Atribua um GUID à disponibilidade de um comando sem precisar carregar ou executar um VSPackage.

- Atribua um GUID para afetar a associação de chave ativa.

- Atribua um GUID para ativar a gravação de macro.

- Atribua um GUID para ativar o modo de depuração ou alternar entre o design e o modo de executar em um editor.

  componente Parte do software que pode fazer parte da funcionalidade de um aplicativo sem que esse aplicativo tenha informações pré-existentes sobre a implementação do software. A comunicação entre um componente e um aplicativo é exclusivamente por meio de interfaces de estilo OLE.

  gerenciador de componentes Um serviço, , que fornece serviços de coordenação de interface do usuário `SOleComponentManager` para componentes de nível superior. O `SOleComponentManager` serviço implementa a interface `IOleComponentManager` .

  gerenciador de interface do usuário do componente Um serviço, `SOleComponentUIManager` , que fornece serviços de coordenação de interface do usuário. O `SOleComponentUIManager` serviço implementa as `IOleComponentUIManager` `IOleInPlaceComponentUIManager` interfaces e .

  context bag Um `IVsUserContext` objeto (objeto COM) anexado a um componente de ambiente. Esse objeto contém palavras-chave de pesquisa, **palavras-chave F1** e atributos relacionados ao componente. Além disso, os pacotes de contexto apontam para quaisquer pacotes de subcontexto que estão vinculados a eles.

  provedor de contexto Um componente no IDE que tem um pacote de contexto associado a ele. Esses componentes incluem uma janela de ferramentas, editor ou hierarquia de projeto.

  designer Uma interface de programação que permite aos usuários manipular elementos da interface do usuário (formulários, botões e outros controles).

  DocData Um objeto COM encapsulando os dados subjacentes de um documento em um mundo em que há separação de documento/exibição (por exemplo, no caso do editor de texto, esse seria o buffer de texto subjacente a todas as exibições do editor de texto). Se o EditorFactory não fornecer esse objeto, o IDE fabrica um em seu nome. A responsabilidade desse objeto é gerenciar a persistência de dados e a semântica de compartilhamento para várias exibições sobre esse mesmo `DocData` . Se o `DocData` objeto for `IOleCommandTarget` compatível com a interface , ele será incluído no roteamento de comandos do UIShell.

  Tecnologia DocObject usada para hospedar a interface do usuário em um quadro fornecido pelo host. Mais especificamente, esse termo refere-se a qualquer incorporação que dá suporte às `IOleDocument` interfaces relacionadas e . Essa tecnologia tem muitos aplicativos potenciais, como um detalhe de implementação de documentos COM, janelas de ferramentas no Visual Basic 5.0, designers ActiveX no Visual Basic 6.0 e assim por diante.

  document Usado para se referir genericamente ao documento como um todo – tanto o `DocData` quanto o `DocView` . Por exemplo, um DocumentFrame contém um , mas também mantém uma referência ao para `DocView` `DocData` manipular a persistência.

  DocView O DocObject/Embedding/WindowPane com o qual o usuário interage para exibir e manipular o `DocData` subjacente. Os usuários não aproveitam a separação de Documento/Exibição que faz parte do `DocObject` design da interface. Os usuários usam um DocObject inteiro para atuar como uma exibição em vez de usar uma noção mais abstrata (e menos formalizada) de dados subjacentes conhecidos como `DocData` . `DocView` Os objetos são sempre inseridos com objetos de quadro do documento (janelas filho MDI) do IDE.

  DTE O objeto (Extensibilidade das Ferramentas de Desenvolvimento) é o ponto de acesso mais alto no modelo de automação Visual Studio, que permite automatizar e estender programaticamente o `DTE` IDE.

  Janela Ferramenta de Janela de Ajuda Dinâmica implementada pelo IDE e exibe uma lista de tópicos da palavra-chave de pesquisa ou da Ajuda **F1.**

  editor Código (classe, CLSID) que implementa o `DocView` . Ele também implementa se há suporte `DocData` para a exibição e a separação de dados.

  extensão Um recurso que modifica, personaliza ou adiciona a um IDE. Você cria extensões usando o modelo de automação ou VSPackages.

  editor externo Um editor que não é específico para o IDE, como o Microsoft Word. Ele foi registrado por meio de seus próprios mecanismos e pode ser usado fora do IDE. Se esse editor puder ser inserido, ele aparecerá dentro de uma janela no IDE. Se ele não puder ser inserido, uma janela de nível superior separada será criada.

  árvore de hierarquia de nós, cada nó associado a um conjunto de propriedades.

  componente de nível superior independente Um componente que usa uma janela de nível superior sem modo e pode operar efetivamente como uma janela de aplicativo autônoma, mas é implementado como um objeto em processo. Portanto, um componente independente de nível superior deve coordenar serviços de modalidade e loop de mensagens com o IDE. Objetos em processo não têm seu próprio loop de mensagem.

  provedor de informações O provedor de informações é um módulo que pode procurar palavras-chave e retornar uma lista de tópicos, na forma de `IVsUserContextItem` objetos . Para fornecer **itens de palavra-chave F1** e pesquisa para o provedor de informações, registre o arquivo de Ajuda compilado (*. HxS*) com o sistema. Os tópicos da Ajuda nesses arquivos fornecem a lista de tópicos exibidos na janela Ajuda Dinâmica e mostram se um usuário pressiona **F1**.

  componente in-loco Um objeto VSPackage que implementa a interface para gerenciar uma janela que está contida visualmente em uma janela de documento pertencente `IOleInPlaceComponent` ao IDE. Os componentes in-locar não participam da mesclaização de menu OLE padrão; em vez disso, eles integram seus elementos de interface do usuário ao IDE.

  Há dois tipos de componentes in-in-place: componentes in-in-place e controles de componentes.

  Componentes embutidos no local têm menus, barras de ferramentas e comandos que são totalmente integrados à interface do usuário do IDE, aparecendo como se fossem internos diretamente no IDE.

  Os controles de componente não têm nenhum de seus próprios elementos de interface do usuário integrados ao IDE; em vez disso, eles usam menus, comandos e barras de ferramentas do IDE. Por exemplo, o comando Negrito pode ser usado para em negrito uma palavra selecionada dentro de um controle de rich text inserido em um formulário. No entanto, os controles de componente podem solicitar que elementos de interface do usuário específicos do componente instalados dinamicamente sejam exibidos.

  serviço de linguagem Um conjunto de objetos que permite aos desenvolvedores do VSPackage implementar recursos de editores de código de linguagem de computador, como marcação de texto e colorização.

  Projeto de arquivos diversos usado para a casa de arquivos abertos que não estão em nenhum projeto. A lista de itens neste projeto não é persistida.

  Projetos de projeto são composto por objetos de hierarquia ou objetos COM que implementam a `IVsHierarchy` interface .

  designer ou editor específico do projeto Um designer que não pode ser usado independentemente do tipo de projeto. Todos os designers específicos do projeto devem inserir suas informações de Fábrica do Editor no Registro. Em seguida, o IDE pode insinuar o designer sempre que um determinado tipo de arquivo é aberto em um projeto específico.

  janela de tipo de projeto Uma janela que acompanha constantemente a hierarquia e o item do projeto ativo no momento do contexto de seleção global. As janelas de tipo de projeto usam o serviço para alertar o IDE das alterações e `SVsTrackSelectionEx` exibir comentários para o usuário. Gerenciador de Soluções é um exemplo de uma janela de tipo de projeto.

  janela Propriedades anteriormente navegador de propriedades.

  projetos baseados em referência Projeto que não exige que os arquivos para o projeto sejam no mesmo diretório. Em vez disso, as referências a arquivos de outros diretórios não relacionados são armazenadas e mantidas pelo próprio projeto.

  executando a tabela de documentos Estrutura interna pela qual o IDE mantém a lista de todos os documentos abertos no momento. A lista inclui todos os documentos abertos na memória, independentemente de os documentos estarem sendo editados no momento. Um documento é qualquer item salvo, incluindo procedimentos armazenados abertos em um editor, arquivos em um projeto ou no arquivo de projeto principal (por exemplo, arquivo *.vcproj).

  contexto de seleção Dados que fazem parte dos detalhes de cada janela no IDE e são usados para acompanhar seleções ativas. O contexto de seleção consiste em:

- Ponteiro para a `IVsHierarchy` interface da hierarquia do projeto

- Identificador de item do item de projeto.

- Ponteiro para a `ISelectionContainer` interface que fornece acesso às propriedades para os objetos ativos.

- Matriz de valores de elemento.

  service Um contrato para um conjunto de interfaces COM que reside em um único objeto COM. Ao criar um serviço, que é identificado por um GUID, você define o conjunto de interfaces COM que executa o serviço. Objetos COM usam serviços para se comunicar entre si.

  solução Grupo de projetos relacionados com os quais um usuário funciona.

  designer padrão Um designer que pode ser usado independentemente do tipo de projeto. Todos os designers padrão devem inserir suas informações de Fábrica do Editor no Registro. Em seguida, o IDE pode insinuar o designer sempre que um arquivo com uma extensão específica é aberto. Os dados devem persistir em um arquivo.

  Editor padrão que pode ser usado independentemente de qualquer tipo de projeto específico. Esses editores têm EditorFactories registrados no Registro. Isso permite que o IDE localize e invoque o editor.

  editor de sistema operacional padrão Uma incorporação que não é Visual Studio específica. Ele é registrado usando as chaves Win32 conhecidas (por exemplo, o Win32 Explorer sabe como invocar). Se tal editor puder ser inserido, o editor ainda aparecerá em seu lugar no IDE. Caso contrário, uma janela de nível superior separada será criada para tais editores.

  subcontexto recipiente de um `IVsUserContext` objeto vinculado a um recipiente de contexto. O objeto mantém palavras-chave de pesquisa, palavras-chave **F1** e atributos para uma seleção dentro de um componente IDE. Exemplos de subcontexto incluem um comando em uma janela de ferramentas ou uma palavra-chave em um editor.

  Janela de ferramentas da lista de tarefas implementada pelo IDE e exibe uma lista de tarefas ativas.

  nome comum do buffer de texto para o objeto `VSTextBuffer` .

  Nome comum da exibição de texto do objeto `VSTextView` .

  componente de nível superior de ferramenta um componente que opera como uma janela pop-up sem janelas restritas, coordenando rigidamente com a interface do usuário do IDE. Assim como os componentes de nível superior independentes, os componentes de nível superior da ferramenta também devem coordenar os serviços de modalidade e de loop de mensagem com o IDE.

  componente de nível superior um objeto VSPackage que gerencia uma janela de nível superior não restrita de modelos em vez da área do cliente de uma janela do IDE. Os componentes de nível superior implementam a `IOleComponent` interface para aproveitar os serviços de loop de mensagens, como o acesso ao tempo ocioso.

  Interface do usuário ativa um objeto VSPackage que está visível e atualmente tem foco.

  Hierarquia de interface do usuário um objeto COM que implementa a `IVsUIHierarchy` interface para permitir a exibição de uma hierarquia. A janela hierarquia da interface do usuário implementa a `ISelectionContainer` interface para atualizar a janela Propriedades; outras janelas do tipo projeto podem usar essa implementação, se desejado.

  Tabela de comandos do VSCT Visual Studio. O arquivo. vsct contém informações sobre o posicionamento e os comportamentos de menus, barras de ferramentas e comandos no formato XML.

  VSPackage uma parte de software instalável que estende o IDE do Visual Studio, contribuindo com um ou mais dos seguintes itens: interface do usuário, serviços, tipos de projeto ou Editor/Designer. Um VSPackage consiste em um objeto COM que implementa a `IVsPackage` interface e um ou mais objetos com que implementam outras interfaces para dar suporte à seleção e a outros recursos. Além disso, um VSPackage tem requisitos de registro específicos.
