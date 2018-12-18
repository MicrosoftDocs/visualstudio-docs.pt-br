---
title: Vincular um caso de uso a documentos e diagramas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.usecasediagram.artifact.properties.artifactlink
- vs.teamarch.usecasediagram.artifact
helpviewer_keywords:
- use case diagrams
ms.assetid: 4c9ed205-9197-4ed5-b39d-ddfa24a0a421
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: a5b4ef580825115a1d44c3abb39404332a4277ea
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787907"
---
# <a name="link-a-use-case-to-documents-and-diagrams"></a>Vincular um caso de uso a documentos e diagramas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode vincular um caso de uso em um diagrama de caso de uso para outro diagrama ou documento. Por exemplo, você pode vincular o caso de uso para os documentos e diagramas a seguir:  
  
- Um diagrama de sequência que mostra como os objetivos do caso de uso são obtidos com as interações entre usuários e o sistema ou seus componentes principais.  
  
- Um diagrama de atividade que mostra as ações detalhadas do sistema e os usuários ou de seus componentes principais, conforme realizam o caso de uso.  
  
- Uma página do OneNote ou um parágrafo que descreve o caso de uso em detalhes.  
  
- Um documento do Word ou apresentação do PowerPoint que descreve o caso de uso em detalhes. Você pode manter tais documentos na solução ou em um local acessível para sua equipe, como um site do SharePoint.  
  
  Para vincular um caso de uso a um documento, você cria um artefato no diagrama de caso e conecte-se o caso de uso para o artefato. Nas propriedades do artefato, você deve definir o caminho do arquivo de outro diagrama ou documento. Quando você clica duas vezes o artefato, o outro diagrama ou o documento é aberto.  
  
  Você pode se conectar como muitos artefatos para cada caso de uso conforme desejado. Você também pode vincular os artefatos para outros tipos de elemento em um diagrama de caso de uso.  
  
### <a name="to-open-a-document-associated-with-an-artifact"></a>Para abrir um documento associado a um artefato  
  
-   No diagrama de caso de uso, clique duas vezes na forma de artefato.  
  
     O documento associado é aberto.  
  
### <a name="to-link-a-use-case-to-a-diagram-or-file-in-the-same-solution"></a>Para vincular um caso de uso em um diagrama ou um arquivo na mesma solução  
  
1.  Desenhe um diagrama como um diagrama de sequência ou um diagrama de atividade para ilustrar um cenário de caso de uso.  
  
2.  Volte para o diagrama de caso de uso.  
  
3.  Arraste o arquivo ou o diagrama no Gerenciador de soluções em uma parte em branco do diagrama de caso.  
  
4.  Conectar-se de que o artefato para o caso de uso usando um **dependência**.  
  
### <a name="to-link-to-a-solution-file-such-as-a-word-document-or-powerpoint-presentation"></a>Para vincular a um arquivo de solução como um documento do Word ou apresentação do PowerPoint  
  
1.  Adicione o documento à solução.  
  
    1.  Mova o documento do Word na mesma pasta do Windows como a solução.  
  
    2.  No Gerenciador de soluções, clique com botão direito a solução, aponte para **Add**e, em seguida, clique em **Item existente**.  
  
    3.  Navegue até o documento do Word e clique em **adicionar**.  
  
         O documento do Word é exibido em uma pasta de solução no Gerenciador de soluções.  
  
2.  Arraste o documento do Word no Gerenciador de soluções em uma parte em branco do diagrama de caso.  
  
     Um novo artefato é exibida.  
  
3.  Conectar-se de que o artefato para o caso de uso usando um **dependência**.  
  
### <a name="to-link-to-a-shared-document-onenote-element-or-web-page"></a>Para vincular a um documento compartilhado, o OneNote elemento ou página da web  
  
1.  Obter a URL do elemento de dados compartilhado. Isso pode ser, por exemplo, um início de caminho do arquivo de rede '\\\\', ou uma página da web ou URL do Sharepoint início 'http://' ou um link para uma seção do OneNote, página ou início de parágrafo ' onenote:'.  
  
2.  Na caixa de ferramentas, clique em **artefato** e, em seguida, clique no diagrama de caso.  
  
3.  Com o novo artefato selecionado, digite ou cole a URL para o **hiperlink** propriedade.  
  
    > [!NOTE]
    >  Se você quiser fornecer um caminho de arquivo, é melhor escolher um arquivo em um espaço de trabalho comuns (começando com '\\\\'), ou um arquivo em sua solução do Visual Studio. Isso garante que o caminho do arquivo permanecerá válido no computador de outro membro da equipe, ou se a solução é movida. Para adicionar um documento como um documento do Word à sua solução, clique com botão direito na solução no Gerenciador de soluções, aponte para **Add** e, em seguida, clique em **Item existente**.  
  
## <a name="see-also"></a>Consulte também  
 [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)   
 [Diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)   
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)



