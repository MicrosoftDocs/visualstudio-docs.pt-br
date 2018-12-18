---
title: Criar diagramas de camada do seu código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- architecture, layer diagrams
- layer diagrams
- diagrams - modeling, layer
- constraints, architectural
ms.assetid: 58c3ea71-2dbc-4963-bf82-40f1924cf973
caps.latest.revision: 64
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 0a1c5af9394f36f7f89a20b711657a3ca76e8d1f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727294"
---
# <a name="create-layer-diagrams-from-your-code"></a>Criar diagramas de camada por meio de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para visualizar a arquitetura de alto nível, a lógica do seu sistema de software, crie uma *diagrama de camada* no Visual Studio. Para certificar-se de que o código permaneça consistente com esse design, valide o código com um diagrama de camada. É possível criar diagramas de camada para projetos do Visual C# .NET e do Visual Basic .NET. Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)  
  
 ![Criar um diagrama de camada](../modeling/media/layerdiagramvisualizecode.png "LayerDiagramVisualizeCode")  
  
 Um diagrama de camada permite organizar itens de solução do Visual Studio em grupos abstratos, lógicos, chamados *camadas*. É possível usar camadas para descrever as tarefas principais realizadas por esses artefatos ou os componentes principais do sistema. Cada camada pode conter outras camadas que descrevem tarefas mais detalhadas. Você também pode especificar desejadas ou existentes *dependências* entre camadas. Essas dependências, representadas como setas, mostram quais camadas podem usar ou atualmente usam a funcionalidade representada por outras camadas. Para manter controle arquitetônico do código, mostre as dependências desejadas no diagrama e, em seguida, valide o código no diagrama.  
  
##  <a name="CreateDiagram"></a> Criar um diagrama de camada  
 Antes de criar um diagrama de camada, verifique se a solução tem um projeto de modelagem. Ver [diagramas e projetos de modelagem UML criar](../modeling/create-uml-modeling-projects-and-diagrams.md).  
  
> [!IMPORTANT]
>  Não adicione, arraste ou copie um diagrama de camada existente de um projeto de modelagem a outro projeto de modelagem ou a outro local na solução. Isso preserva as referências do diagrama original, mesmo que você altere o diagrama. Isso também impede que a validação da camada funcione corretamente e talvez cause outros problemas como, por exemplo, elementos não encontrados ou outros erros quando você tenta abrir o diagrama.  
>   
>  Em vez disso, adicione um novo diagrama de camada ao projeto de modelagem. Copie os elementos do diagrama de origem para o novo diagrama. Salve o projeto de modelagem e o novo diagrama de camada.  
  
#### <a name="to-add-a-new-layer-diagram-to-a-modeling-project"></a>Para adicionar um novo diagrama de camada a um projeto de modelagem  
  
1.  Sobre o **arquitetura** menu, escolha **UML novo ou diagrama de camada**.  
  
2.  Sob **modelos**, escolha **diagrama de camada**.  
  
3.  Nomeie o diagrama.  
  
4.  Na **adicionar ao projeto de modelagem**, navegue até e selecione um projeto de modelagem existente na solução.  
  
     -ou-  
  
     Escolher **criar um novo projeto de modelagem** para adicionar um novo projeto de modelagem à solução.  
  
    > [!NOTE]
    >  O diagrama de camada deve estar dentro de um projeto de modelagem. Porém, é possível vinculá-lo a itens em qualquer lugar na solução.  
  
5.  Não se esqueça de salvar o projeto de modelagem e o diagrama de camada.  
  
##  <a name="CreateLayers"></a> Criar camadas de artefatos  
 É possível criar camadas dos itens de solução do Visual Studio como, por exemplo, projetos, arquivos de código, namespaces, classes e métodos. Isso cria automaticamente links entre camadas e itens, incluindo-os no processo de validação da camada.  
  
 Também é possível vincular camadas a itens que não dão suporte à validação como, por exemplo, documentos do Word ou apresentações do Powerpoint, de forma que você pode associar uma camada a especificações ou planos. Também é possível vincular camadas a arquivos em projetos compartilhados entre vários aplicativos, mas o processo de validação não incluirá essas camadas, exibidas com nomes genéricos como, por exemplo, "Camada 1" e "Camada 2".  
  
 Para ver se um item vinculado dá suporte à validação, abra **Gerenciador de camadas** e examine o **dá suporte à validação** propriedade do item. Ver [Gerenciando links para artefatos](#Managing).  
  
|**To**|**Siga estas etapas**|  
|------------|----------------------------|  
|Criar uma camada para um único artefato|<ol><li>Arraste o item para o diagrama de camada destas origens:<br /><br /> <ul><li>**Gerenciador de Soluções**<br /><br />         Por exemplo, é possível arrastar arquivos ou projetos.</li><li>Mapas de código<br /><br />         Ver [mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md) e [mapas de código de uso para depurar seus aplicativos](../modeling/use-code-maps-to-debug-your-applications.md).</li><li>**Exibição de classe** ou **Pesquisador de objetos**</li></ul><br />     Uma camada é exibida no diagrama e está vinculada ao artefato.</li><li>Renomeie a camada para refletir as responsabilidades do código ou dos artefatos associados.</li></ol> **Importante:** arrastar arquivos binários para o diagrama de camada não adiciona automaticamente suas referências ao projeto de modelagem. Você deve adicionar manualmente os arquivos binários que você deseja validar ao projeto de modelagem. **Para adicionar arquivos binários ao projeto de modelagem** <ol><li>Na **Gerenciador de soluções**, abra o menu de atalho para o projeto de modelagem e, em seguida, escolha **Add Existing Item**.</li><li>No **Adicionar Item existente** caixa de diálogo, navegue até os arquivos binários, selecioná-los e, em seguida, escolha **Okey**.     Os arquivos binários são exibidos no projeto de modelagem.</li><li>Na **Gerenciador de soluções**, escolha um arquivo binário que você adicionou e, em seguida, pressione **F4** para abrir o **propriedades** janela.</li><li>Em cada arquivo binário, defina as **ação de compilação** propriedade **validar**.</li></ol>|  
|Criar uma única camada para todos os artefatos selecionados|Arraste todos os artefatos para o diagrama de camada ao mesmo tempo.<br /><br /> Uma camada é exibida no diagrama e está vinculada a todos os artefatos.|  
|Criar uma camada para cada artefato selecionado|Pressione e segure a **SHIFT** pressionada ao arrastar todos os artefatos para o diagrama de camada ao mesmo tempo. **Observação:** se você usar o **SHIFT** chave para selecionar um intervalo de itens, solte a tecla depois de selecionar os artefatos. Mantenha-o pressionado novamente ao arrastar os artefatos para o diagrama. <br /><br /> Uma camada para cada artefato é exibida no diagrama e está vinculada a cada artefato.|  
|Adicionar um artefato a uma camada|Arraste o artefato à camada.|  
|Criar uma nova camada desvinculada|No **caixa de ferramentas**, expanda o **diagrama de camada** seção e, em seguida, arraste uma **camada** ao diagrama de camada.<br /><br /> Para adicionar várias camadas, clique duas vezes na ferramenta. Quando tiver terminado, escolha o **ponteiro** ferramenta ou pressione a **ESC** chave.<br /><br /> - ou -<br /><br /> Abra o menu de atalho do diagrama de camada, escolha **Add**e, em seguida, escolha **camada**.|  
|Criar camadas aninhadas|Arraste uma camada existente para outra camada.<br /><br /> - ou -<br /><br /> Abra o menu de atalho para uma camada, escolha **Add**e, em seguida, escolha **camada**.|  
|Criar uma nova camada que contém duas ou mais camadas existentes|Selecione as camadas, abra o menu de atalho para a sua seleção e, em seguida, escolha **grupo**.|  
|Alterar a cor de uma camada|Defina suas **cor** propriedade para a cor que você deseja.|  
|Especificar que os artefatos associados a uma camada não devem pertencer aos namespaces especificados|Digite os namespaces da camada **Namespaces proibidos** propriedade. Use um ponto e vírgula (**;**) para separar os namespaces.|  
|Especificar que os artefatos associados a uma camada não dependem dos namespaces especificados|Digite os namespaces da camada **dependências de Namespace proibido** propriedade. Use um ponto e vírgula (**;**) para separar os namespaces.|  
|Especificar que os artefatos associados a uma camada devem pertencer a um dos namespaces especificados|Digite o namespace da camada **Namespaces obrigatórios** propriedade. Use um ponto e vírgula (**;**) para separar os namespaces.|  
  
 O número em uma camada indica o número de artefatos que estão associados à camada. No entanto, ao ler esse número, lembre-se do seguinte:  
  
-   Se uma camada estiver vinculada a um artefato que contenha outros artefatos, mas não estiver vinculada diretamente a outros artefatos, o número incluirá apenas o artefato vinculado. No entanto, os outros artefatos estão incluídos para análise durante a validação da camada.  
  
     Por exemplo, se uma camada estiver vinculada a um único namespace, o número de artefatos vinculados será 1, mesmo se o namespace contiver classes. Se a camada também tiver links para cada classe no namespace, o número incluirá as classes vinculadas.  
  
-   Se uma camada contiver outras camadas vinculadas a artefatos, a camada de contêiner também estará vinculada a esses artefatos, mesmo que o número na camada de contêiner não inclua esses artefatos.  
  
##  <a name="Managing"></a> Gerenciar links entre camadas e artefatos  
  
1.  No diagrama de camada, abra o menu de atalho para a camada e, em seguida, escolha **Exibir Links**.  
  
     **Gerenciador de camada** mostra os links de artefato para a camada selecionada.  
  
2.  Use as seguintes tarefas para gerenciar esses links:  
  
|**To**|**No Gerenciador de camadas**|  
|------------|---------------------------|  
|Excluir o links entre a camada e um artefato|Abra o menu de atalho para o link de artefato e, em seguida, escolha **excluir**.|  
|Mover o link de uma camada para outra|Arraste o link de artefato para uma camada existente no diagrama.<br /><br /> - ou -<br /><br /> 1.  Abra o menu de atalho para o link de artefato e, em seguida, escolha **Recortar**.<br />2.  No diagrama de camada, abra o menu de atalho para a camada e, em seguida, escolha **colar**.|  
|Copiar o link de uma camada para outra|1.  Abra o menu de atalho para o link de artefato e, em seguida, escolha **cópia**.<br />2.  No diagrama de camada, abra o menu de atalho para a camada e, em seguida, escolha **colar**.|  
|Criar uma nova camada com base em um link de artefato existente|Arraste o link de artefato para uma área em branco no diagrama.|  
|Verifique se um artefato vinculado dá suporte à validação no diagrama de camada.|Examine os **dá suporte à validação** coluna para o link de artefato.|  
  
##  <a name="Discovering"></a> Fazer engenharia reversa de dependências existentes  
 Existirá uma dependência sempre que um artefato associado a uma camada tiver uma referência a um artefato associado a outra camada. Por exemplo, uma classe em uma camada declara uma variável que tem uma classe em outra camada. É possível fazer engenharia reversa em dependências existentes para artefatos vinculados a camadas no diagrama.  
  
> [!NOTE]
>  As dependências não podem sofrer engenharia reversa para determinados tipos de artefatos. Por exemplo, nenhuma dependência sofrerá engenharia reversa de ou para uma camada vinculada a um arquivo de texto. Para ver quais artefatos têm dependências que você pode fazer engenharia reversa, abra o menu de atalho para uma ou várias camadas e, em seguida, escolha **Exibir Links**. Na **Gerenciador de camadas**, examine o **dá suporte à validação** coluna. As dependências não sofrerão engenharia reversa para artefatos para o qual essa coluna mostra **falsos**.  
  
- Selecione uma ou várias camadas, abra o menu de atalho para uma camada selecionada e, em seguida, escolha **gerar dependências**.  
  
  Normalmente, você verá algumas dependências que não devem existir. É possível editar essas dependências para alinhá-las com o design desejado.  
  
##  <a name="EditDependencies"></a> Editar camadas e dependências para mostrar o design desejado  
 Para descrever as alterações que você pretende fazer no sistema ou na arquitetura desejada, edite o diagrama de camada:  
  
|**To**|**Execute estas etapas**|  
|------------|-----------------------------|  
|Alterar ou restringir a direção de uma dependência|Defina suas **direção** propriedade.|  
|Criar novas dependências|Use o **dependência** e **dependência bidirecional** ferramentas.<br /><br /> Para desenhar várias dependências, clique duas vezes na ferramenta. Quando tiver terminado, escolha o **ponteiro** ferramenta ou pressione a **ESC** chave.|  
|Especificar que os artefatos associados a uma camada não dependem dos namespaces especificados|Digite os namespaces da camada **dependências de Namespace proibido** propriedade. Use um ponto e vírgula (**;**) para separar os namespaces.|  
|Especificar que os artefatos associados a uma camada não devem pertencer aos namespaces especificados|Digite os namespaces da camada **Namespaces proibidos** propriedade. Use um ponto e vírgula (**;**) para separar os namespaces.|  
|Especificar que os artefatos associados a uma camada devem pertencer a um dos namespaces especificados|Digite o namespace da camada **Namespaces obrigatórios** propriedade. Use um ponto e vírgula (**;**) para separar os namespaces.|  
  
##  <a name="EditLayout"></a> Alterar como os elementos aparecem no diagrama  
 É possível alterar o tamanho, a forma, a cor e a posição das camadas ou a cor das dependências editando-se suas propriedades.  
  
##  <a name="Codemaps"></a> Descubra padrões e as dependências em um mapa de código  
 Durante a criação de diagramas de camada, você também pode criar **mapas de código**. Esses diagramas podem ajudar você a descobrir padrões e as dependências, enquanto você explora o código. Use o Gerenciador de soluções, exibição de classe ou Pesquisador de objetos para explorar a assemblies, namespaces e classes – o que normalmente correspondem bem a camadas existentes. Para obter mais informações sobre mapas de código, consulte:  
  
-   [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)  
  
-   [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)  
  
-   [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)  
  
## <a name="see-also"></a>Consulte também  
 [Vídeo do Channel 9: Projetar e validar sua arquitetura usando diagramas de camada](http://go.microsoft.com/fwlink/?LinkID=252073)   
 [Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)   
 [Diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md)   
 [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)   
 [Visualizar código](../modeling/visualize-code.md)