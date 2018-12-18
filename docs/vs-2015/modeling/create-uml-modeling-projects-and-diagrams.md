---
title: Criar diagramas e projetos de modelagem UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.addnewdiagramdialog
- vs.teamarch.createnewmodelingprojectdialog
helpviewer_keywords:
- projects [Visual Studio ALM], modeling
- diagrams - modeling, modeling
- modeling diagrams
- projects, UML
- UML, deleting diagrams
- UML
- UML diagrams, adding
- UML, projects
- Visual Studio ALM, modeling projects
- modeling projects
- UML diagrams
- projects, modeling
ms.assetid: c178b04b-4fd2-4bed-97e3-d793dae8649c
caps.latest.revision: 50
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 5d841c9fde677eb4a8fb17e952a817364dab277e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51738391"
---
# <a name="create-uml-modeling-projects-and-diagrams"></a>Criar projetos e diagramas de modelagem UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os modelos de UML ajudam você a entende, discuta e criar sistemas de software. O Visual Studio fornece modelos para cinco dos mais usados com frequência diagramas UML: atividade, classe, componente, sequência e caso de uso. Além disso, você pode criar diagramas de camada, que ajudam você a definir a estrutura do seu sistema.  
  
 Diagramas de modelagem UML e diagramas de camada podem existir somente dentro de um projeto de modelagem. Cada projeto de modelagem contém um modelo UML compartilhado e vários diagramas UML. Cada diagrama é uma exibição parcial do modelo. O modelo UML contém todos os elementos em diagramas de UML e pode ser exibido usando o Gerenciador de modelos UML. Para obter informações sobre modelos e suas relações com diagramas, consulte [modelos e diagramas UML editar](../modeling/edit-uml-models-and-diagrams.md). Para obter informações sobre a modelagem de projetos sob controle de versão, consulte [gerenciar modelos e diagramas com controle de versão](../modeling/manage-models-and-diagrams-under-version-control.md) e [estruturar a solução de modelagem](../modeling/structure-your-modeling-solution.md)  
  
> [!NOTE]
>  Há outro tipo de diagrama, o diagrama de classe do .NET, que é usado para visualizar o código do programa. Para obter mais informações, consulte [Projetando e exibindo Classes e tipos](http://go.microsoft.com/fwlink/?LinkId=142231).  
  
##  <a name="CreatingModelingDiagrams"></a> Criar um diagrama em um projeto de modelagem  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
#### <a name="to-create-a-diagram-and-add-it-to-a-project"></a>Criar um diagrama e adicioná-lo a um projeto  
  
1. Sobre o **arquitetura** menu, escolha **UML novo ou diagrama de camada**.  
  
2. No **adicionar novo diagrama** caixa de diálogo, clique no tipo de diagrama de modelagem que você deseja.  
  
    ![Adicionar caixa de diálogo Novo diagrama](../modeling/media/uml-adddiagram.png "UML_AddDiagram")  
  
3. Digite um nome para o novo diagrama.  
  
4. No **adicionar ao projeto de modelagem** caixa:  
  
   - Selecione um projeto de modelagem que já existe na solução e, em seguida, clique em **Okey**.  
  
     \- ou -  
  
   1.  Selecione **criar um novo projeto de modelagem**e, em seguida, clique em **Okey**.  
  
   2.  No **criar novo projeto de modelagem** caixa de diálogo, digite um nome e local para o novo projeto e, em seguida, clique em **Okey**.  
  
        ![Criar caixa de diálogo Novo projeto de modelagem](../modeling/media/uml-createmodel.png "UML_CreateModel")  
  
        Se sua solução estiver aberta, o novo projeto é adicionado à solução. Se você não tiver nenhuma solução aberta, você pode digitar um nome para uma nova solução.  
  
   Se você já tiver um projeto de modelagem, você também pode usar o procedimento a seguir.  
  
#### <a name="to-add-a-diagram-to-an-existing-modeling-project"></a>Para adicionar um diagrama em um projeto de modelagem existente  
  
1.  Na **Gerenciador de soluções**, clique na modelagem de nó do projeto.  
  
    > [!NOTE]
    >  O projeto de modelagem contém uma pasta de definição de modelo chamada **ModelDefinition**.  
  
2.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
3.  No **Adicionar Novo Item –**  *\<nome do projeto >* caixa de diálogo **modelos**, clique em de modelagem diagrama tipo, por exemplo, **UML Diagrama de componente**.  
  
4.  Digite um nome para o diagrama e, em seguida, clique em **adicionar**.  
  
     O diagrama de modelagem abre e aparece no projeto de modelagem.  
  
    > [!CAUTION]
    >  Não adicionar, copiar ou arrastar os arquivos existentes do diagrama para outros projetos de modelagem ou para outros locais na solução. Isso faz com que elementos desapareça da diagramas copiados ou erros ocorram quando você abre os diagramas. Você deve abrir o arquivo de diagrama do projeto de modelagem no qual ele foi criado. Isso ocorre porque um diagrama UML é um modo de exibição do modelo que pertence a seu projeto de modelagem. Para copiar um arquivo de diagrama, criar um novo diagrama e, em seguida, copiar os elementos do diagrama de origem para o novo diagrama. Para obter mais informações, consulte [diagramas e projetos de modelagem de solução de problemas](#TroubleshootingModelingProjects).  
  
#### <a name="to-create-a-blank-modeling-project"></a>Para criar um projeto de modelagem em branco  
  
1.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
2.  No **novo projeto** caixa de diálogo **modelos instalados**, clique em **projetos de modelagem**.  
  
3.  Na janela do meio, clique em **projeto de modelagem**.  
  
4.  Nomeie o projeto e especifique um local na **nome** e **local** caixas.  
  
5.  No **solução** caixa, selecione **adicionar à solução** para adicionar o novo projeto a uma solução já abertas; ou **criar nova solução** fechar qualquer solução aberta e adicionar o projeto para uma nova solução.  
  
##  <a name="RemovingModelingDiagrams"></a> Removendo diagramas de um projeto de modelagem  
 Você pode excluir permanentemente um diagrama, ou você pode excluir temporariamente um diagrama de um projeto e, em seguida, restaurá-lo.  
  
#### <a name="to-permanently-delete-a-diagram-from-a-project"></a>Para excluir permanentemente um diagrama de um projeto  
  
-   Na **Gerenciador de soluções**, clique no arquivo principal que representa o diagrama e, em seguida, clique em **excluir**.  
  
     O diagrama é removido do projeto e o sistema de arquivos. Os elementos mostrados no diagrama não são removidos do **Gerenciador de modelos UML**.  
  
    > [!NOTE]
    >  Cada diagrama tem dois arquivos, uma subsidiária para outro. Por exemplo, se você tiver um diagrama de componente com o nome `CD1`, você deve excluir o arquivo chamado `CD1.componentdiagram`. Seu arquivo subsidiário chamado `CD1.componentdiagram.layout` serão excluídos automaticamente.  
  
#### <a name="to-temporarily-exclude-a-diagram-from-a-project"></a>Para excluir temporariamente um diagrama de um projeto  
  
-   Na **Gerenciador de soluções**, clique no arquivo de diagrama e, em seguida, clique em **excluir do projeto**.  
  
     O diagrama é removido do projeto. Ele não é removido do sistema de arquivos.  
  
    > [!NOTE]
    >  Os elementos mostrados no diagrama não são removidos do **Gerenciador de modelos UML**.  
  
#### <a name="to-restore-a-temporarily-excluded-diagram-to-a-project"></a>Para restaurar um diagrama excluído temporariamente em um projeto  
  
1.  Na **Gerenciador de soluções**, clique na modelagem de nó do projeto.  
  
    > [!NOTE]
    >  O projeto de modelagem contém uma pasta de definição de modelo chamada **ModelDefinition**.  
  
2.  Sobre o **Project** menu, clique em **Add Existing Item**.  
  
3.  No **Adicionar Item existente** caixa de diálogo, localize o arquivo de diagrama, selecione o arquivo e, em seguida, clique em **Add**.  
  
     O diagrama de modelagem abre e aparece no projeto de modelagem.  
  
    > [!NOTE]
    >  Cada diagrama tem um par de arquivos no sistema de arquivos. Não selecione um arquivo que tem a extensão `.layout`. Além disso, o Visual Studio não suporta a adição de diagramas UML existentes para vários projetos de modelagem. Cada arquivo de diagrama deve ser aberto dentro do projeto de modelagem no qual ele foi criado. Isso ocorre porque um diagrama UML mostra uma exibição de um modelo que pertence a seu projeto de modelagem.  
  
##  <a name="NonModelDiagrams"></a> Diagramas que não necessitam de projetos de modelagem  
 Os seguintes tipos de diagramas não fazem parte de um projeto de modelagem:  
  
-   Diagramas de classe são criados como modos de exibição do código-fonte. Não estão relacionadas a diagramas de classe UML. Para obter mais informações, consulte [Projetando e exibindo Classes e tipos](../ide/designing-and-viewing-classes-and-types.md).  
  
-   Mapas de código. Ver [mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md).  
  
-   Diagramas que não são diagramas UML ou diagramas de camada, como linguagens específicas do domínio.  
  
##  <a name="TroubleshootingModelingProjects"></a> Solução de problemas de diagramas e projetos de modelagem  
 A tabela a seguir descreve problemas que podem ocorrer com como resolvê-los ou diagramas e projetos de modelagem:  
  
|**Problema**|**Faz com que**|**Resolução**|  
|---------------|----------------|--------------------|  
|O projeto de modelagem não pode ser aberto ou carregado na solução.<br /><br /> A seguinte mensagem é exibida:<br /><br /> "Um ou mais projetos na solução não foram carregados corretamente. Consulte a janela de saída para obter detalhes."<br /><br /> A janela Saída exibe a seguinte mensagem:<br /><br /> "*ModelingProjectFilenameAndPath*. modelproj: erro: formato de Guid não reconhecido."|Um projeto de modelagem tem referências a projetos que têm o mesmo nome e estão na mesma solução.<br /><br /> Por exemplo, uma camada está vinculada aos projetos que têm o mesmo nome e estão na mesma solução.|Use um editor de texto para abrir o projeto de modelagem de arquivo, remova as referências e, em seguida, tente abrir novamente o projeto de modelagem.<br /><br /> Para evitar esse problema, não adicione referências a projetos que têm o mesmo nome. Certifique-se de projetos têm nomes exclusivos.|  
|Elementos estão ausentes em diagramas que são adicionados, copiados ou arrastados para outros projetos de modelagem ou para outros locais na solução.<br /><br /> - ou -<br /><br /> As seguintes mensagens são exibidas quando você tenta abrir um diagrama:<br /><br /> -"Algumas formas ou conectores no diagrama estão ausentes porque suas definições não existe neste projeto. As definições foram excluídas do modelo enquanto o diagrama foi fechado ou o diagrama foi copiado para outro projeto que não contém essas definições."<br /><br /> - ou -<br /><br /> -"Deste documento está aberto por outro projeto."|O arquivo de diagrama foi adicionado, arrastado ou copiado de um projeto de modelagem a outro projeto de modelagem ou em outro local na solução.|Para copiar um arquivo de diagrama, criar um novo diagrama e, em seguida, copiar os elementos do diagrama de origem para o novo diagrama.|  
  
## <a name="see-also"></a>Consulte também  
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Estruturar a solução de modelagem](../modeling/structure-your-modeling-solution.md)



