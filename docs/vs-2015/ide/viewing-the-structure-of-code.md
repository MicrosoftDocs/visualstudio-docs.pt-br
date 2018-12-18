---
title: Exibindo a estrutura do código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.documentoutline.window
- vs.objectbrowser
- vs.classview
- VS.CodeDefinitionView
- VS.CodeDefinitionWindow
- vs.componentpicker
- vs.callbrowser
helpviewer_keywords:
- document outline window.
- Visual Studio, object browser
- Visual Studio, code definition window
- call hierarchy
- Visual Studio, document outline window
- code definition window
- Visual Studio, class view
- Visual Studio, call hierarchy window
- class view
- object browser
ms.assetid: e6064f58-5ad9-4f05-8c3f-12e994b6583f
caps.latest.revision: 32
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: d110056488b7555bc7bbccc5cbad3205d9de7405
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49901639"
---
# <a name="viewing-the-structure-of-code"></a>Exibindo a estrutura do código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível examinar objetos e membros em projetos do Visual Studio e objetos e membros em componentes do .NET Framework, componentes COM, DLLs (bibliotecas de vínculo dinâmico) e TLBs (bibliotecas de tipos).  
  
 As seguintes seções deste documento descrevem as diferentes janelas de estrutura de código.  
  
 [Modo de Exibição de Classe (Visual Basic, C#, C++)](#BKMK_ClassView)  
  
 [Hierarquia de Chamada (Visual Basic, C#, C++)](#BKMK_CallHierarchy)  
  
 [Pesquisador de Objetos](#BKMK_ObjectBrowser)  
  
 [Janela de Definição de Código (C#, C++)](#BKMK_CodeDefinition)  
  
 Também é possível usar o **Gerenciador de Soluções** para procurar os tipos e membros em seus projetos, pesquisar símbolos, exibir a Hierarquia de Chamada de um método, localizar referências de símbolos e muito mais sem precisar mudar entre as várias janelas de ferramentas listadas anteriormente.  
  
 Se tiver o Visual Studio Enterprise, você pode usar mapas de código para visualizar a estrutura do código e suas dependências em toda a solução, bem como detalhar as partes do código que lhe interessarem. Para obter mais informações, consulte [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md).  
  
> [!NOTE]
>  A edição do Visual Studio e as configurações que você está usando podem afetar os recursos no IDE. Eles podem ser diferentes dos descritos neste tópico.  
  
##  <a name="BKMK_ClassView"></a> Modo de Exibição de Classe (Visual Basic, C#, C++)  
 O **Modo de Exibição de Classe** é mostrado como parte do **Gerenciador de Soluções**, bem como em uma janela separada. A janela **Modo de Exibição de Classe** exibe os elementos de um aplicativo. O painel superior exibe namespaces, tipos, interfaces, enumerações e classes, e o painel inferior exibe os membros que pertencem ao tipo selecionado no painel superior. Usando essa janela, você pode passar para definições de membro no código-fonte (ou no **Pesquisador de Objetos** se o elemento for definido fora de sua solução).  
  
 Não é necessário compilar um projeto para exibir seus elementos no **Modo de Exibição de Classe**. A janela é atualizada conforme você modifica o código em seu projeto.  
  
 É possível adicionar código ao seu projeto selecionando o nó do projeto e escolhendo o botão **Adicionar** para abrir a caixa de diálogo **Adicionar Novo Item**. O código é adicionado em um arquivo separado.  
  
 Caso tenha sido realizado o check-in do seu projeto para controle do código-fonte, cada elemento do **Modo de Exibição de Classe** exibirá um ícone que indica o status do código-fonte do arquivo. Comandos de controle do código-fonte comuns, como **Fazer Check-Out**, **Fazer Check-In** e **Obter Versão Mais Recente**, também estão disponíveis no menu de atalho do elemento.  
  
### <a name="class-view-toolbar"></a>Barra de Ferramentas Modo de Exibição de Classe  
 A barra de ferramentas Modo de Exibição de Classe contém os comandos a seguir.  
  
|||  
|-|-|  
|**Nova Pasta**|Cria uma pasta ou subpasta virtual na qual você pode organizar os elementos usados com frequência. Eles são salvos no arquivo de solução ativo (.suo). Após você renomear ou excluir um elemento em seu código, ele pode aparecer em uma pasta virtual como um nó de erro. Para corrigir esse problema, exclua o nó de erro. Se tiver renomeado um elemento, você pode movê-lo da hierarquia do projeto para a pasta novamente.|  
|**Voltar**|Navega para o item selecionado anteriormente.|  
|**Avançar**|Navega para o item selecionado seguinte.|  
|**Exibir em Diagrama de Classe** (somente em projetos de código gerenciado)|É disponibilizado quando você seleciona um namespace ou tipo no **Modo de Exibição de Classe**. Quando um namespace é selecionado, o diagrama de classe mostra todos os tipos contidos nele. Quando um tipo é selecionado, o diagrama de classe mostra apenas esse tipo.|  
  
### <a name="class-view-settings"></a>Configurações do Modo de Exibição de Classe  
 O botão **Configurações do Modo de Exibição de Classe** na barra de ferramentas tem as seguintes configurações.  
  
|||  
|-|-|  
|**Mostrar Tipos Base**|Tipos base são exibidos.|  
|**Mostrar Tipos Derivados**|Tipos derivados são exibidos.|  
|**Mostrar Tipos e Membros Ocultos**|Tipos e membros ocultos (que não devem ser usados por clientes) são exibidos em texto cinza claro.|  
|**Mostrar Membros Públicos**|Membros públicos são exibidos.|  
|**Mostrar Membros Protegidos**|Membros protegidos são exibidos.|  
|**Mostrar Membros Particulares**|Membros particulares são exibidos.|  
|**Mostrar Outros Membros**|Outros tipos de membros são exibidos, incluindo membros internos (ou Amigos no Visual Basic).|  
|**Mostrar Membros Herdados**|Membros herdados são exibidos.|  
|**Mostrar Métodos de Extensão**|Métodos de extensão são exibidos.|  
  
### <a name="class-view-shortcut-menu"></a>Menu de atalho do Modo de Exibição de Classe  
 O menu de atalho no **Modo de Exibição de Classe** pode conter os seguintes comandos, dependendo do tipo de projeto selecionado.  
  
|||  
|-|-|  
|**Ir para Definição**|Localiza a definição do elemento no código-fonte ou no **Pesquisador de Objetos** se o elemento não estiver definido no projeto aberto.|  
|**Procurar definição**|Exibe o item selecionado no **Pesquisador de Objetos**.|  
|**Localizar Todas as Referências**|Localiza o item do objeto selecionado e exibe os resultados em uma janela **Localizar Resultados**.|  
|**Filtrar por Tipo** (somente código gerenciado)|Exibe apenas o namespace ou o tipo selecionado. É possível remover o filtro escolhendo o botão **Limpar Localizar** (X) ao lado da caixa **Localizar**.|  
|**Copiar**|Copia o nome totalmente qualificado do item.|  
|**Classificar em Ordem Alfabética**|Lista tipos e membros em ordem alfabética por nome.|  
|**Classificar por Tipo de Membro**|Lista tipos e membros ordenados segundo o tipo (de forma que classes precedam interfaces, interfaces precedam representantes e métodos precedam propriedades).|  
|**Classificar por Acesso a Membro**|Lista tipos e membros ordenados segundo o tipo de acesso, como público ou privado.|  
|**Agrupar por Tipo de Membro**|Classifica tipos e membros em grupos por tipo de objeto.|  
|**Ir para Declaração** (somente para código C++)|Exibe a declaração do tipo ou membro no código-fonte, se disponível.|  
|**Ir para Definição**|Exibe a definição do tipo ou membro no código-fonte, se disponível.|  
|**Ir para Referência**|Exibe uma referência ao tipo ou membro no código-fonte, se disponível.|  
|**Exibir Hierarquia de Chamada**|Exibe o método selecionado na janela **Hierarquia de Chamada**.|  
  
##  <a name="BKMK_CallHierarchy"></a> Hierarquia de Chamada (Visual Basic, C#, C++)  
 A janela **Hierarquia de Chamada** mostra onde um determinado método (ou propriedade ou construtor) é chamado e lista os métodos que são chamados desse método. É possível exibir vários níveis de grafo de chamadas, que mostra as relações de chamador/computador chamado entre os métodos em um escopo especificado.  
  
 Você pode exibir a janela **Hierarquia de Chamada** selecionando um método (ou propriedade ou construtor) e, em seguida, escolhendo **Exibir Hierarquia de Classe** no menu de atalho. A exibição deve se parecer com a imagem a seguir.  
  
 ![Hierarquia de chamada com vários nós abertos](../ide/media/multiplenodes.png "MultipleNodes")  
Janela de Hierarquia de Chamada  
  
 Usando a lista suspensa na barra de ferramentas, é possível especificar o escopo da hierarquia: a solução, o projeto atual ou o documento atual.  
  
 O painel principal exibe as chamadas do método e para ele, e o painel **Chamar Sites** exibe o local da chamada selecionada. Para membros virtuais ou abstratos, um nó **Substitui o nome do método** é exibido. Para membros de interface, um nó **Implementa o nome do método** é exibido.  
  
 A janela **Hierarquia de Chamada** não encontra referências do grupo do método, que incluem os locais nos quais um método é adicionado como um manipulador de eventos ou é atribuído a um delegado. Para localizar essas referências, use o comando **Localizar todas as referências**.  
  
 O menu de atalho na janela **Hierarquia de Chamada** contém os comandos a seguir.  
  
|||  
|-|-|  
|**Adicionar como Nova Raiz**|Adiciona o nó selecionado como um novo nó raiz.|  
|**Remover Raiz**|Remove o nó raiz selecionado do painel do modo de exibição de árvore.|  
|**Ir para Definição**|Navega para a definição original de um método.|  
|**Localizar Todas as Referências**|Localiza no projeto todas as referências ao método selecionado.|  
|**Copiar**|Copia o nó selecionado (mas não seus subnós).|  
|**Atualizar**|Atualiza as informações.|  
  
##  <a name="BKMK_ObjectBrowser"></a> Pesquisador de Objetos  
 O **Pesquisador de Objetos** exibe descrições do código em seus projetos.  
  
 Você pode filtrar o que deseja exibir no **Pesquisador de Objetos**. Usando a lista suspensa na parte superior da janela, você pode escolher entre as seguintes opções:  
  
- Qualquer .NET Framework  
  
- Silverlight  
  
- A solução ativa  
  
- Um conjunto personalizado de componentes  
  
  Componentes personalizados podem incluir executáveis de código gerenciado, assemblies de biblioteca, bibliotecas de tipos e arquivos .ocx. Não é possível adicionar componentes personalizados C++. Configurações personalizadas são salvas no diretório de aplicativo do usuário do Visual Studio, %APPDATA%\Roaming\Microsoft\VisualStudio\11.0\ObjBrowEX.dat.  
  
  O painel esquerdo do **Pesquisador de Objetos** mostra contêineres físicos, como componentes COM e do .NET Framework. É possível expandir os nós do contêiner para exibir os namespaces que eles contêm e, em seguida, expandir os namespaces para exibir os tipos que eles contêm. Quando você seleciona um tipo, seus membros (como propriedades e métodos) são listados no painel direito. O painel inferior direito exibe informações detalhadas sobre o item selecionado.  
  
  Você pode pesquisar um item específico usando a caixa **Pesquisar** na parte superior da janela. As pesquisas não diferenciam maiúsculas de minúsculas. Os resultados da pesquisa são exibidos no painel esquerdo. Para limpar uma pesquisa, escolha o botão **Limpar Pesquisa** (X) ao lado da caixa **Pesquisar**.  
  
  O **Pesquisador de Objetos** mantém controle das seleções feitas, e você pode navegar entre suas seleções usando os botões **Avançar** e **Voltar** na barra de ferramentas.  
  
  É possível usar o **Pesquisador de Objetos** para adicionar uma referência de assembly a uma solução aberta selecionando um item (assembly, namespace, tipo ou membro) e escolhendo o botão **Adicionar Referência** na barra de ferramentas.  
  
### <a name="object-browser-settings"></a>Configurações do Pesquisador de Objetos  
 Usando o botão **Configurações do Pesquisador de Objetos** na barra de ferramentas, você pode especificar um dos seguintes modos de exibição.  
  
|||  
|-|-|  
|**Exibir Namespaces**|Exibe namespaces em vez de contêineres físicos, no painel esquerdo. Namespaces armazenados em vários contêineres físicos são mesclados.|  
|**Exibir Contêineres**|Exibe contêineres físicos em vez de namespaces, no painel esquerdo. As configurações **Exibir Namespaces** e **Exibir Contêineres** são mutuamente exclusivas.|  
|**Mostrar Tipos Base**|Exibe tipos de base.|  
|**Mostrar Tipos Derivados**|Exibe tipos derivados.|  
|**Mostrar Tipos e Membros Ocultos**|Exibe tipos e membros ocultos (que não devem ser usados por clientes) em texto cinza claro.|  
|**Mostrar Membros Públicos**|Exibe membros públicos.|  
|**Mostrar Membros Protegidos**|Exibe membros protegidos.|  
|**Mostrar Membros Particulares**|Exibe membros particulares.|  
|**Mostrar Outros Membros**|Exibe outros tipos de membros, incluindo membros internos (ou Amigos no Visual Basic).|  
|**Mostrar Membros Herdados**|Exibe membros herdados.|  
|**Mostrar Métodos de Extensão**|Exibe métodos de extensão.|  
  
### <a name="object-browser-shortcut-menu-commands"></a>Comandos do menu de atalho do Pesquisador de Objetos  
 O menu de atalho no **Pesquisador de Objetos** pode conter os seguintes comandos, dependendo do tipo de item selecionado.  
  
|||  
|-|-|  
|**Procurar definição**|Mostra o nó principal do item selecionado.|  
|**Localizar Todas as Referências**|Localiza o item do objeto selecionado e exibe os resultados em uma janela **Localizar Resultados**.|  
|**Filtrar Por Tipo**|Exibe apenas o namespace ou o tipo selecionado. É possível remover o filtro escolhendo o botão **Limpar Pesquisa**.|  
|**Copiar**|Copia o nome totalmente qualificado do item.|  
|**Removerr**|Se o escopo for um conjunto de componentes personalizado, remove o componente selecionado do escopo.|  
|**Classificar em Ordem Alfabética**|Lista tipos e membros em ordem alfabética por nome.|  
|**Classificar por Tipo de Objeto**|Lista tipos e membros ordenados segundo o tipo (de forma que classes precedam interfaces, interfaces precedam representantes e métodos precedam propriedades).|  
|**Classificar por Acesso a Objeto**|Lista tipos e membros ordenados segundo o tipo de acesso, como público ou privado.|  
|**Agrupar por Tipo de Objeto**|Classifica tipos e membros em grupos por tipo de objeto.|  
|**Ir para Declaração** (somente projetos em C++)|Exibe a declaração do tipo ou membro no código-fonte, se disponível.|  
|**Ir para Definição**|Exibe a definição do tipo ou membro no código-fonte, se disponível.|  
|**Ir para Referência**|Exibe uma referência ao tipo ou membro no código-fonte, se disponível.|  
|**Exibir Hierarquia de Chamada**|Exibe o método selecionado na janela **Hierarquia de Chamada**.|  
  
##  <a name="BKMK_CodeDefinition"></a> Janela de Definição de Código (C#, C++)  
 A Janela de **Definição de Código** exibe a definição de um membro ou tipo selecionado no projeto ativo. O tipo ou membro pode ser selecionado no editor de código ou em uma janela de exibição de código.  
  
 Embora essa janela seja somente leitura, você pode definir pontos de interrupção ou indicadores nela. Para modificar a definição exibida, escolha **Editar Definição** no menu de atalho. Isso abre o arquivo de origem no editor de códigos e move o ponto de inserção para a linha em que a definição começa.  
  
### <a name="code-definition-shortcut-menu"></a>Menu de atalho de Definição de Código  
 O menu de atalho na Janela de **Definição de Código** pode conter os seguintes comandos, dependendo da linguagem de programação.  
  
|||  
|-|-|  
|**Criar Testes de Unidade**|Cria testes de unidade para o elemento selecionado.|  
|**Gerar Diagrama de Sequência**|Quando um método é selecionado, gera um diagrama de sequência.|  
|**Criar Acessador Particular**|Se um teste de unidade estiver presente na solução, gera um método que o teste usa para acessar o código.|  
|**Ir para Definição**|Localiza a definição (ou definições, para classes parciais) e as exibe em uma janela **Localizar Resultados**.|  
|**Localizar Todas as Referências**|Localiza as referências ao tipo ou membro na solução.|  
|**Exibir Hierarquia de Chamada**|Exibe o método na janela **Hierarquia de Chamada**.|  
|**Mostrar Testes de Chamada**|Se houver testes de unidade no projeto, mostrará os testes que chamam o código selecionado.|  
|**Executar Testes de Chamada**|Se houver testes de unidade no projeto, execute os testes para o código selecionado.|  
|**Ponto de Interrupção**|Insere um ponto de interrupção (ou um tracepoint).|  
|**Executar até o cursor**|Executa o programa em modo de depuração até o local do cursor.|  
|**Copiar**|Copia a linha selecionada.|  
|**Estrutura de tópicos**|Comandos de estrutura de tópicos padrão.|  
|**Editar Definição**|Move o ponto de inserção para a definição na janela de código.|  
|**Escolher Codificação**|Abre a janela **Codificação** para que você possa definir uma codificação para o arquivo.|  
  
### <a name="document-outline-window"></a>Janela de Estrutura de Tópicos do Documento  
 É possível usar a janela **Estrutura de Tópicos do Documento** em conjunto com exibições de designer, como o designer de uma página XAML ou um designer do Windows Forms, ou com páginas HTML. Esta janela exibe os elementos em um modo de exibição de árvore para que você pode exibir a estrutura lógica do formulário ou página e localizar controles que estão incorporados profundamente ou ocultos.  
  
## <a name="see-also"></a>Consulte também  
 [Ícones do Pesquisador de Objetos e do Modo de Exibição de Classe](../ide/class-view-and-object-browser-icons.md)



