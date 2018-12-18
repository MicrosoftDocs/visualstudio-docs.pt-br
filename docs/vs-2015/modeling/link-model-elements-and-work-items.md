---
title: Vincular elementos de modelo e itens de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.common.removeworkitemsdialog
- vs.teamarch.common.linkworkitemsdialog
helpviewer_keywords:
- UML - extending, linking to TFS work items
- UML - extending, linking work items
- work items, creating from UML models
- UML model, creating work items
- work items, linking to UML models
- UML model, linking work items
ms.assetid: e687a490-0f93-412c-a1ff-eea83cf7ba07
caps.latest.revision: 49
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 55dfd83f3c9324b08bbb88c8404350c2aebf129f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51752077"
---
# <a name="link-model-elements-and-work-items"></a>Vincular elementos de modelo e itens de trabalho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Acompanhe tarefas, casos de teste, bugs, requisitos, problemas e outros trabalhos relacionados ao seu modelo vinculando os elementos de modelo no Visual Studio e itens de trabalho no Team Foundation Server ou o Visual Studio Team Services. Anexe documentos a itens de trabalho vinculados para associá-los a elementos de modelo.  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
> [!NOTE]
>  Você deve usar o Team Explorer para criar e abrir links. Verifique se o projeto e os diagramas de modelagem têm controle de versão de forma que outras pessoas possam abrir diagramas vinculados.  
  
 Por exemplo, é possível vincular:  
  
- Um item de trabalho de histórico do usuário e um diagrama de atividade para mostrar como realizar o histórico como uma sequência de operações  
  
- Um caso de uso em um diagrama de caso de uso e em itens de trabalho de caso de teste para verificar se o caso uso está implementado corretamente  
  
- Um atributo em uma classe em um diagrama de classes UML e em um item de trabalho de bug para mostrar um erro na implementação do atributo  
  
- Um componente em um diagrama de componente e em um item de trabalho de tarefa para acompanhar o desenvolvimento do componente. Essa tarefa costuma ser dividida em tarefas menores  
  
  É possível vincular itens de trabalho a qualquer elemento selecionado em diagramas de modelagem ou no Gerenciador de Modelos UML, como estes itens:  
  
- Todos os elementos em modelo UML como, por exemplo, classes UML, linhas da vida, casos de uso, subsistemas, atividades, nós de objeto, componentes, interfaces  
  
- Todas as relações em modelos UML como, por exemplo, associações, generalizações, dependências, fluxos, mensagens  
  
- Partes de elementos como, por exemplo, os atributos e as operações de classes, as ocorrências de execução das linhas de vida, os PINs de entrada e saída das atividades, além das partes e das portas de componentes  
  
- Camadas e dependências de camada  
  
- Comentários e links de comentário  
  
- Diagramas. Para selecionar um diagrama, escolha uma parte em branco do diagrama.  
  
> [!WARNING]
>  Você já deve estar conectado ao TFS fonte de código de controle (SCC) para criar ou vincular a um item de trabalho. Se você tentar abrir uma conexão em um SCC diferentes do TFS, o Visual Studio fecha automaticamente a solução atual. Certifique-se de que você já estiver conectado ao SCC apropriado antes de tentar criar ou vincular a um item de trabalho. Em versões posteriores do Visual Studio, os comandos de menu não estão disponíveis se você não estiver conectado a um SCC.  
  
-   [Conectar a um projeto de equipe](#ConnectTFS)  
  
-   [Vincular um elemento de modelo para um novo item de trabalho](#LinkNew)  
  
-   [Vincular um elemento de modelo a um item de trabalho existente](#LinkExisting)  
  
-   [Exibir itens de trabalho vinculado a um elemento de modelo](#OpenWorkItem)  
  
-   [Exibir elementos de modelo vinculado a um item de trabalho](#ViewLinkedModels)  
  
-   [Excluir links entre elementos de modelo e itens de trabalho](#RemoveLinks)  
  
-   [Solução de problemas](#Troubleshooting)  
  
##  <a name="ConnectTFS"></a> Conectar a um projeto de equipe  
 Você deve primeiro se conectar ao seu projeto de equipe para criar, exibir ou remover links.  
  
1.  Sobre o **Team** menu, escolha **gerenciar conexões** para mostrar a janela do Team Explorer.  
  
2.  Se o projeto correto não for exibido, no Team Explorer, escolha **gerenciar conexões** e, em seguida, escolha **conectar-se ao projeto de equipe**. Em seguida, escolha os projetos corretos ou o servidor, se necessário.  
  
3.  Na **Team Explorer**, escolha o projeto no qual você deseja criar, vincular ou exibir itens de trabalho.  
  
##  <a name="LinkNew"></a> Vincular um elemento de modelo para um novo item de trabalho  
  
1.  Verifique se que você está conectado à instância do TFS que você deseja usar.  
  
2.  No diagrama de modelagem ou no **Gerenciador de modelos UML**, abra o menu de atalho para o elemento de modelo.  
  
3.  Escolher **Criar Item de trabalho** e o tipo de item de trabalho que você deseja criar.  
  
4.  No formulário do item de trabalho, preencha os campos. Escolher **Salvar Item de trabalho**.  
  
     O Visual Studio vincula o elemento de modelo ao novo item de trabalho. Um ícone é exibido em ou próximo ao elemento de modelo.  
  
> [!WARNING]
>  Você já deve estar conectado ao TFS fonte de código de controle (SCC) para criar ou vincular a um item de trabalho. Se você tentar abrir uma conexão em um SCC diferentes do TFS, o Visual Studio fecha automaticamente a solução atual. Certifique-se de que você já estiver conectado ao SCC apropriado antes de tentar criar ou vincular a um item de trabalho. Em versões posteriores do Visual Studio, os comandos de menu não estão disponíveis se você não estiver conectado a um SCC.  
  
##  <a name="LinkExisting"></a> Vincular um elemento de modelo a um item de trabalho existente  
 Ao vincular elementos de modelo a itens de trabalho, comece pelo elemento de modelo, e não pelo item de trabalho.  
  
1.  Verifique se que você está conectado à instância do TFS que você deseja usar.  
  
2.  No diagrama de modelagem ou no **Gerenciador de modelos UML**, abra o menu de atalho para o elemento de modelo. Escolher **Link para o Item de trabalho**. Em seguida, selecione seu projeto na **projeto** campo.  
  
3.  Escolha um ou mais itens de trabalho para vincular ao elemento de modelo seguindo uma destas etapas:  
  
    -   Escolha uma consulta no **consulta salva**.  
  
    -   Digite as IDs de um ou mais itens de trabalho, separados por espaços, no **IDs**.  
  
    -   Digite uma palavra ou frase em **título contém**.  
  
4.  Escolher **localizar**.  
  
5.  Na lista de itens de trabalho, selecione o item de trabalho ou os itens de trabalho que você deseja vincular.  
  
     Quando você terminar, o **itens de trabalho** propriedade do elemento de modelo mostra um número maior do que antes. Um ícone também é exibido em ou próximo ao elemento de modelo.  
  
> [!WARNING]
>  Você já deve estar conectado ao TFS fonte de código de controle (SCC) para criar ou vincular a um item de trabalho. Se você tentar abrir uma conexão em um SCC diferentes do TFS, o Visual Studio fecha automaticamente a solução atual. Certifique-se de que você já estiver conectado ao SCC apropriado antes de tentar criar ou vincular a um item de trabalho. Em versões posteriores do Visual Studio, os comandos de menu não estão disponíveis se você não estiver conectado a um SCC.  
  
##  <a name="OpenWorkItem"></a> Exibir itens de trabalho vinculado a um elemento de modelo  
  
1.  Na **Team Explorer**, verifique se você está conectado ao projeto de equipe onde os itens de trabalho estão vinculados ao elemento de modelo.  
  
2.  No diagrama de modelagem ou no **Gerenciador de modelos UML**, abra o menu de atalho para o elemento de modelo. Escolher **exibir itens de trabalho** para exibir a lista de itens de trabalho vinculados.  
  
    > [!NOTE]
    >  Somente os itens de trabalho do servidor conectado são exibidos. Se você não vir quaisquer itens de trabalho, verifique se você estiver conectado ao servidor correto em **Team Explorer**.  
  
##  <a name="ViewLinkedModels"></a> Exibir elementos de modelo vinculado a um item de trabalho  
 Você pode exibir diagramas de modelagem e os elementos que estão vinculados a um item de trabalho no Visual Studio Team Services e no Team Foundation Server 2012 ou posterior. Por exemplo, um item de trabalho talvez esteja vinculado a modelos de classe que mostram o design de novas classes que serão implementadas.  
  
1.  Na **Team Explorer**, verifique se você está conectado ao projeto de equipe onde os elementos de modelo estão vinculados ao item de trabalho.  
  
    > [!NOTE]
    >  Só é possível usar o Team Explorer, e não o Team Web Access, para exibir elementos de modelo vinculados. Verifique se o workspace está mapeado para o projeto de modelagem que contém os diagramas ou os elementos de modelagem. Se não tiver um workspace, você deverá criá-lo. Ver [solução de problemas](#Troubleshooting) e [criar e trabalhar com espaços de trabalho](http://msdn.microsoft.com/library/1d7f6ed8-ec7c-48f8-86da-9aea55a90d5a).  
  
2.  Abra o item de trabalho, escolha **Links**. Sob **Link de modelo**, abra o menu de atalho para o elemento de modelo vinculado. Escolher **Abrir Item vinculado**.  
  
     ![Elemento de modelo vinculado aberto de um item de trabalho](../modeling/media/workitem-openlinkedmodelelement.png "WorkItem_OpenLinkedModelElement")  
  
##  <a name="RemoveLinks"></a> Excluir links entre elementos de modelo e itens de trabalho  
 Remova um item de trabalho vinculado com base no elemento de modelo. Isso remove corretamente o link recíproco para esse elemento de modelo do item de trabalho. Do contrário, se você começar pelo item de trabalho, o link recíproco do elemento de modelo para o item de trabalho não será excluído.  
  
1.  No diagrama de modelagem ou no **Gerenciador de modelos UML**, abra o menu de atalho para o elemento de modelo.  
  
2.  Escolher **remover itens de trabalho**.  
  
     \- ou -  
  
    1.  Escolher **propriedades**, em seguida, **itens de trabalho** onde o número de itens de trabalho vinculados é exibido.  
  
    2.  No **itens de trabalho** propriedade, escolha o botão de reticências **[...]** .  
  
        > [!NOTE]
        >  Somente itens de trabalho no servidor atual são exibidos. Se a lista estiver vazia, mas o número de itens de trabalho não for zero, verifique se você está conectado ao servidor correto em **Team Explorer**.  
  
3.  Sob **remover Links para itens de trabalho**, desmarque os itens selecionados que você deseja desvincular. Escolha **OK**.  
  
##  <a name="Troubleshooting"></a> Solução de problemas  
  
|**Problema**|**Possível causa**|**Resolução**|  
|---------------|------------------------|--------------------|  
|Não é possível encontrar o elemento de modelo que você deseja vincular.|O elemento talvez esteja em um diagrama em um projeto de modelagem que esteja em [!INCLUDE[esprscc](../includes/esprscc-md.md)]. Você talvez não tenha um workspace que seja mapeado para o diagrama.|Mapeie o workspace para o projeto e o diagrama de modelagem. Se não tiver um workspace, você deverá criá-lo.<br /><br /> A mensagem de erro exibida para esse problema contém o caminho que é possível usar para mapear o workspace.<br /><br /> Ver [criar e trabalhar com espaços de trabalho](http://msdn.microsoft.com/library/1d7f6ed8-ec7c-48f8-86da-9aea55a90d5a).|  
|Não é possível encontrar o elemento de modelo vinculado.|O elemento vinculado talvez esteja em um diagrama que foi movido, renomeado ou excluído.|1.  No item de trabalho, exclua o link para o elemento de modelo.<br />2.  Crie um novo link com base no item de trabalho para o elemento de modelo.|  
|O item de trabalho não tem elementos de modelo vinculados esperados.|Um item de trabalho mostra apenas um elemento de camada vinculado caso o vínculo tenha sido criado com base no item de trabalho. A equipe não usa [!INCLUDE[esprscc](../includes/esprscc-md.md)], o caminho local dos diagramas será usado para criar os links. Se o projeto de modelagem e seus diagramas estiverem em [!INCLUDE[esprscc](../includes/esprscc-md.md)], todos os membros da equipe que podem acessar o projeto poderão exibir os elementos vinculados em itens de trabalho.|Tente atualizar o item de trabalho.|  
|A exclusão de um link para um elemento de modelo de um item de trabalho não exclui o link do elemento de modelo para o item de trabalho.||Exclua o link para o item de trabalho começando pelo elemento de modelo.|  
  
## <a name="see-also"></a>Consulte também  
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)



