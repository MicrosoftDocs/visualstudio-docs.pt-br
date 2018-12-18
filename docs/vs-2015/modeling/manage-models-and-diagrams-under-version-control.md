---
title: Gerenciar modelos e diagramas com controle de versão | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- models, version control
ms.assetid: ca6443e3-6d11-4da8-aae7-ca7dcc410076
caps.latest.revision: 32
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 20cb2e89a85f00782a172245dcdd8f47025ddd12
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51738040"
---
# <a name="manage-models-and-diagrams-under-version-control"></a>Gerenciar modelos e diagramas com controle de versão
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Gerenciar diferentes versões de seus projetos de modelagem e diagramas, incluindo mapas de código (arquivos. dgml), usando [usar o controle de versão do Team Foundation ou Git](http://msdn.microsoft.com/library/33267cee-fe5f-4aa3-b2cd-6d22ceace314); ambos com local Team Foundation Server ou na nuvem com o Visual Studio Team Services.  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
> [!IMPORTANT]
>  Tome cuidado quando vários usuários trabalham no mesmo projeto de modelagem. Descubra como você pode [organizar modelos em projetos de médio ou grandes](../modeling/structure-your-modeling-solution.md).  
  
##  <a name="ModelingProjects"></a> Arquivos em um projeto de modelagem  
 Mais de um usuário pode trabalhar em um projeto de modelagem ao mesmo tempo, desde que trabalhem em arquivos diferentes.  
  
 Para evitar ou resolver conflitos entre as alterações feitas por usuários diferentes, é importante entender como o modelo é armazenado em arquivos.  
  
-   Cada pacote é armazenado em um separado **. UML** arquivo, que é mantido na **ModelDefinition** pasta do projeto. O modelo também tem um **. UML** arquivo. Se um desses arquivos for excluído ou corrompido, o pacote ou modelo correspondente será perdido.  
  
-   Cada diagrama é armazenado em dois arquivos. Por exemplo, um diagrama de classe tem:  
  
    -   **DiagramName.classdiagram** -se esse arquivo é excluído ou corrompido, o diagrama será perdido, mas as classes e as associações que ele mostrava ainda estarão no modelo e podem ser vistas no Gerenciador de modelos UML.  
  
    -   **DiagramName.classdiagram.layout** -se esse arquivo é excluído, as formas ainda aparecerão o diagrama, mas eles perderão seus tamanhos e posições. Cada arquivo de layout é subsidiário a um arquivo de diagrama. Para vê-lo, clique em [+] ao lado do arquivo de diagrama no Gerenciador de soluções.  
  
> [!NOTE]
>  É importante manter a consistência entre os arquivos. Por exemplo, se você usar o controle de origem para reverter as alterações em um arquivo. UML, você deve reverter as alterações correspondentes na. * diagram e. layout arquivos ao mesmo tempo. Elementos representados em um. \*arquivo de diagrama será perdido se eles não forem também representados em um arquivo. UML.  
  
##  <a name="Shared"></a> Trabalhando em projetos compartilhados de modelagem  
 Para minimizar conflitos entre o trabalho simultâneo em diferentes partes de um projeto:  
  
-   Divida seu projeto de modelagem em pacotes que representem diferentes áreas de trabalho. Mova todo o modelo para os pacotes, em vez de deixá-lo no modelo de raiz. Para obter mais informações, consulte [definir pacotes e namespaces](../modeling/define-packages-and-namespaces.md).  
  
-   Diferentes usuários não devem trabalhar no mesmo pacote ou diagrama ao mesmo tempo.  
  
-   Se você estiver usando perfis, verifique se que todos instalaram os mesmos perfis. Ver [personalizar o modelo com perfis e estereótipos](../modeling/customize-your-model-with-profiles-and-stereotypes.md).  
  
-   Para ajudar a garantir que você altere somente o pacote que você está trabalhando:  
  
    -   Defina as **LinkedPackage** propriedade de uma classe, componente ou diagrama de caso de uso UML.  
  
    -   No Gerenciador de modelos UML, arraste uma atividade ou interação para seu pacote assim que você criou. Esse elemento será exibido no Gerenciador de modelos UML quando você cria o primeiro nó no diagrama de sequência ou atividade.  
  
-   Para ajudar a manter o controle de pacotes, renomeie os arquivos de pacote para refletir os nomes de pacote real.  
  
-   Na [!INCLUDE[esprscc](../includes/esprscc-md.md)], sempre executam **Fazer Check-In** e **obter última versão** operações no projeto de modelagem completo, nunca em arquivos individuais.  
  
-   Sempre executar uma **obter** operação imediatamente antes de fazer check-in no projeto de modelagem.  
  
-   Sempre feche todos os diagramas antes de executar uma **obter** operação.  
  
    > [!NOTE]
    >  Se um arquivo estiver aberto quando você executa um **obter**, e a operação resulta em alterações locais, em seguida, você será solicitado a recarregar o arquivo. Nesse caso, clique em **não**e, em seguida, recarregue o projeto completo. Na **Gerenciador de soluções**, a modelagem com o botão direito nó do projeto, clique em **descarregar projeto**e, em seguida, clique em **recarregar projeto**.  
  
###  <a name="Exclusive"></a> Alterações que exigem acesso exclusivo para o modelo  
 Antes de fazer os seguintes tipos de alterações, certifique-se de que você tenha um bloqueio de Check-Out em todo o projeto.  
  
-   Renomear ou excluir elementos que são referenciados de outros pacotes.  
  
-   Alterando as propriedades de relacionamentos que cruzem os limites dos pacotes.  
  
-   Para saber mais sobre os bloqueios de Check-Out, consulte [Check out e editar arquivos](http://msdn.microsoft.com/library/eb404d63-c448-4994-9416-3e6d50ec554a).  
  
##### <a name="to-move-a-diagram-file-in-or-out-of-a-project-folder"></a>Para mover um arquivo de diagrama para dentro ou fora de uma pasta de projeto  
  
1.  Inicie **prompt de comando do desenvolvedor do Visual Studio**.  
  
2.  Use **renomear tf** para mover o arquivo de diagrama e seu **. layout** arquivo:  
  
     `tf rename sourcePath targetPath`  
  
3.  No Gerenciador de soluções, clique no arquivo e, em seguida, clique em **excluir do projeto**.  
  
4.  Adicione o arquivo à pasta de destino.  
  
     No Gerenciador de soluções, clique com botão direito na pasta de destino ou o projeto, aponte para **Add**e, em seguida, clique em **Item existente**. Na caixa de diálogo, selecione o arquivo de diagrama e, em seguida, clique em **adicionar**. O arquivo de layout será adicionado automaticamente.  
  
    > [!NOTE]
    >  É possível mover o arquivo para um projeto diferente.  
  
##  <a name="Merging"></a> Mesclando alterações em arquivos de modelo e diagramas  
 Depois de mais de um usuário tem trabalhado em um modelo simultaneamente, [!INCLUDE[esprscc](../includes/esprscc-md.md)] perguntará se você deseja mesclar as alterações nos arquivos de modelo. Trabalhar em projetos separados como descrito nas seções anteriores evitará a maioria das mesclagens. Normalmente, os conflitos restantes podem ser mesclados automaticamente com segurança. Os seguintes tipos de alterações não devem causar dificuldade:  
  
-   Tipos de linhas da vida. Quando você adiciona uma linha da vida a uma interação (diagrama de sequência), seu tipo é armazenado no modelo de raiz, a menos que você criou na linha de vida de um tipo existente.  
  
-   Novas atividades e interações são inicialmente armazenadas no modelo de raiz.  
  
-   Adicionando elementos e relações.  
  
-   Renomear ou excluir elementos que são referenciados somente dentro de seu próprio pacote.  
  
## <a name="see-also"></a>Consulte também  
 [Análise e modelagem de arquitetura](../modeling/analyze-and-model-your-architecture.md)   
 [Modelos de compartilhamento e diagramas de exportação](../modeling/share-models-and-exporting-diagrams.md)



