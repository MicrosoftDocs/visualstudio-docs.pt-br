---
title: Interfaces do Windows Script | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4c750627-6797-4857-9f5e-e5f54371f83c
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f98e60a82735ae561edf404763e0700f71b3a3d4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49905357"
---
# <a name="windows-script-interfaces"></a>Interfaces do Windows Script

Interfaces do Microsoft Windows Script fornecem uma maneira para um aplicativo adicionar scripts e automação OLE. Hosts de script que dependem do Windows Script podem usar mecanismos de script de várias fontes e fornecedores para o script entre componentes. A tarefa de implementar o script em si – idioma, sintaxe, formato persistente, o modelo de execução e assim por diante – é deixada para o respectivo fornecedor.

A documentação do Windows Script é dividida nas seguintes seções:

[Hosts de script do Windows](../winscript/windows-script-hosts.md)

[Mecanismos de script do Windows](../winscript/windows-script-engines.md)

[Visão geral de depuração de script ativo](../winscript/active-script-debugging-overview.md)

[Visão geral da criação de perfil de script ativo](../winscript/active-script-profiling-overview.md)

[Referência de interfaces de script do Windows](../winscript/reference/windows-script-interfaces-reference.md)

## <a name="windows-script-background"></a>Contexto do Windows Script

Interfaces do Windows Script se enquadram em duas categorias: hosts do Windows Script e mecanismos do Windows Script. Um host cria um mecanismo de script e chama o mecanismo para executar os scripts. Exemplos de hosts do Windows Script incluem:

- Microsoft Internet Explorer

- Ferramentas de criação da Internet

- Shell

Mecanismos do Windows Script podem ser desenvolvidos para qualquer linguagem ou o ambiente de tempo de execução, incluindo:

- Microsoft VBScript (Visual Basic Scripting Edition)

- Perl

- Lisp

Para tornar a implementação do host o mais flexível possível, um wrapper de automação OLE para Windows Script é fornecido. No entanto, um host que usa esse objeto wrapper para criar uma instância do mecanismo de script não tem o grau de controle sobre o namespace de tempo de execução, o modelo de persistência e assim por diante e o teria se usasse o Windows Script diretamente.

O design do Windows Script isola os elementos da interface necessários somente em um ambiente de criação para que hosts de não criação (como navegadores e visualizadores) e mecanismos de script (por exemplo, VBScript) possam ser mantidos leves.

## <a name="windows-script-basic-architecture"></a>Arquitetura básica do Windows Script

A ilustração a seguir mostra a interação entre um host do Windows Script e um mecanismo do Windows Script.

As etapas envolvidas na interação entre o host e o mecanismo são fornecidas na lista a seguir.

1.  Criar um projeto. O host carrega um projeto ou documento. (Essa etapa não é específica para o Windows Script, mas é incluída aqui para integridade.)

2.  Crie o mecanismo do Windows Script. O host chama `CoCreateInstance` para criar um novo mecanismo do Windows Script, especificando o CLSID (identificador de classe) do mecanismo de script específico a ser usado. Por exemplo, o navegador HTML do Internet Explorer recebe o identificador de classe do mecanismo de script por meio do atributo CLSID= da marca HTML \<OBJECT>.

3.  Carregue o script. Se o conteúdo do script é mantido, o host chama o método `IPersist*::Load` do mecanismo de script para alimentar o recipiente de propriedades, fluxo ou armazenamento de script. Caso contrário, o host usa o método `IPersist*::InitNew` ou [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) para criar um script nulo. Um host que mantém um script como texto pode usar [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) para alimentar o texto do script ao mecanismo de script, depois de chamar `IActiveScriptParse::InitNew`.

4.  Adicione itens nomeados. Para cada item de nível superior nomeado (como páginas e formulários) importado para o namespace do mecanismo de script, o host chama o método [IActiveScript::AddNamedItem](../winscript/reference/iactivescript-addnameditem.md) para criar uma entrada no namespace do mecanismo. Essa etapa não é necessária se os itens nomeados de nível superior já fazem parte do estado persistente do script carregado na etapa 3. Um host não usa `IActiveScript::AddNamedItem` para adicionar itens nomeados como subníveis (como controles em uma página HTML); em vez disso, o mecanismo indiretamente obtém itens de subnível de itens de nível superior usando as interfaces `ITypeInfo` e `IDispatch` do host.

5.  Execute o script. O host faz com que o mecanismo inicie a execução do script, definindo o sinalizador SCRIPTSTATE_CONNECTED no método [IActiveScript::SetScriptState](../winscript/reference/iactivescript-setscriptstate.md). Essa chamada provavelmente executaria qualquer trabalho de construção de mecanismo de script, incluindo associação estática, conexão a eventos (veja abaixo) e execução de código, de forma semelhante a uma função `main()` em script.

6.  Obtenha informações sobre o item. Cada vez que o mecanismo de script deve associar um símbolo com um item de nível superior, ele chama o método [IActiveScriptSite::GetItemInfo](../winscript/reference/iactivescriptsite-getiteminfo.md), que retorna informações sobre o item fornecido.

7.  Conectar eventos. Antes de iniciar o script real, o mecanismo de script se conecta aos eventos de todos os objetos relevantes por meio da interface `IConnectionPoint`.

8.  Invoque propriedades e métodos. Conforme o script é executado, o mecanismo de script percebe referências a propriedades e métodos em objetos nomeados por meio de `IDispatch::Invoke` ou outros mecanismos de associação OLE padrão.

## <a name="windows-script-terms"></a>Termos do Windows Script

Essa lista contém as definições dos termos relacionados a scripts usados neste documento.

|Termo|Definição|
|----------|----------------|
|Objeto de código|Uma instância criada pelo mecanismo de script que está associado a um item nomeado, tal como o módulo por trás de um formulário no Visual Basic ou uma classe C++ associada a um item nomeado. De preferência, este é um objeto OLE COM (Component Object Model) que dá suporte à automação OLE para que o host ou outra entidade que não seja de script possa manipular o objeto de código.|
|Item nomeado|Um objeto OLE COM (preferencialmente um que dá suporte à automação OLE) que o host considera interessante para o script. Exemplos incluem a página HTML e o navegador em um navegador da Web e o documento e as caixas de diálogo no Microsoft Word.|
|script|Os dados que compõem o programa executado pelo mecanismo de script. Um script pode ser quaisquer dados executáveis contíguos, incluindo partes de texto, blocos de `pcode` ou até mesmo códigos de byte executáveis específicos de computador. Um host carrega um script no mecanismo de script por meio de uma das interfaces `IPersist*` ou por meio da interface [IActiveScriptParse](../winscript/reference/iactivescriptparse.md).|
|Mecanismo de script|O objeto OLE que processa scripts. Um mecanismo de script implementa as interfaces [IActiveScript](../winscript/reference/iactivescript.md) e, opcionalmente, [IActiveScriptParse](../winscript/reference/iactivescriptparse.md).|
|Host de script|O aplicativo ou programa proprietário do mecanismo do Windows Script. O host implementa as interfaces [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) e, opcionalmente, [IActiveScriptSiteWindow](../winscript/reference/iactivescriptsitewindow.md).|
|Miniscript|Uma parte de um script que é anexado a um objeto por meio da interface [IActiveScriptParse](../winscript/reference/iactivescriptparse.md). A coleção agregada de miniscripts é o script.|
|Linguagem de script|A linguagem na qual um script é escrito (VBScript, por exemplo) e a semântica dessa linguagem.|