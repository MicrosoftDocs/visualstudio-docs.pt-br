---
title: 'Diagramas de camada: Diretrizes | Microsoft Docs'
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
ms.assetid: 2903bec7-a93b-46a6-aac6-994ac4f3f1a7
caps.latest.revision: 57
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: fa7483a000b5abd59b846edceead3af93f41dbc4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51734441"
---
# <a name="layer-diagrams-guidelines"></a>Diagramas de camada: diretrizes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Descrever a arquitetura do aplicativo em um alto nível, criando *diagramas de camada* no Visual Studio. Certifique-se de que o código permaneça consistente com esse design, validando seu código com um diagrama de camada. Você também pode incluir validação de camada no processo de compilação. Ver [vídeo do Channel 9: Design e validar sua arquitetura usando diagramas de camada](http://go.microsoft.com/fwlink/?LinkID=252073).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="what-is-a-layer-diagram"></a>O que é um diagrama de camada?  
 Como um diagrama de arquitetura tradicional, um diagrama de camada identifica os principais componentes ou unidades funcionais de design e suas interdependências. Cada nó no diagrama, chamado um *camada*, representa um grupo lógico de namespaces, projetos ou outros artefatos. Você pode desenhar as dependências que devem existir no seu design. Ao contrário de um diagrama de arquitetura tradicional, você pode verificar que as dependências reais no código-fonte está em conformidade com as dependências pretendidas que você especificou. Fazendo parte de validação de um build normal no [!INCLUDE[esprtfs](../includes/esprtfs-md.md)], você pode garantir que o código do programa continua a aderir a arquitetura do sistema por meio de alterações futuras. Ver [diagramas de camada: referência](../modeling/layer-diagrams-reference.md).  
  
##  <a name="Update"></a> Como criar ou atualizar seu aplicativo com diagramas de camada  
 As etapas a seguir fornecem uma visão geral de como usar diagramas de camada no processo de desenvolvimento. As seções posteriores neste tópico descrevem mais detalhes sobre cada etapa. Se você estiver desenvolvendo um novo design, omita as etapas que se referem ao código existente.  
  
> [!NOTE]
>  Essas etapas aparecem na ordem aproximada. Você provavelmente deseja sobrepor as tarefas, reordená-los de acordo com sua própria situação e revisá-las no início de cada iteração em seu projeto.  
  
1.  [Criar um diagrama de camada](#Create) para o aplicativo inteiro ou para uma camada dentro dele.  
  
2.  [Definir camadas para representar as áreas funcionais principais ou componentes](#CreateLayers) do seu aplicativo. Nomeie dessas camadas de acordo com sua função, por exemplo, "Apresentação" ou "Serviços". Se você tiver um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução, você pode associar cada camada com uma coleção de *artefatos*, como namespaces, projetos, arquivos e assim por diante.  
  
3.  [Descubra as dependências existentes](#Generate) entre camadas.  
  
4.  [Editar as camadas e dependências](#EditArchitecture) para mostrar a atualização que você deseja que o código para refletir de design.  
  
5.  [Criar novas áreas do seu aplicativo](#NewAreas) criando camadas para representar os componentes ou blocos arquitetônicos principais e definir dependências para mostrar como cada camada usa os outros.  
  
6.  [Editar o layout e aparência do diagrama](#EditLayout) para ajudá-lo a discutir isso com seus colegas.  
  
7.  [Valide o código no diagrama de camada](#Validate) para realçar os conflitos entre o código e a arquitetura que você precisa.  
  
8.  [Atualize o código para estar de acordo com sua nova arquitetura](#UpdateCode). Desenvolver de forma iterativa e refatorar o código até que a validação não mostra nenhum conflito.  
  
9. [Incluir validação de camada no processo de build](#BuildValidation) para garantir que o código continue a aderir ao seu design.  
  
##  <a name="Create"></a> Criar um diagrama de camada  
 Um diagrama de camada deve ser criado dentro de um projeto de modelagem. Você pode adicionar um novo diagrama de camada a um projeto de modelagem existente, crie um novo projeto de modelagem para o diagrama de camada ou copie um diagrama de camada existente dentro do mesmo projeto de modelagem.  
  
> [!IMPORTANT]
>  Não adicione, arraste ou copie um diagrama de camada existente de um projeto de modelagem a outro projeto de modelagem ou em outro local na solução. Um diagrama de camada copiado dessa maneira terá as mesmas referências do diagrama original, mesmo se você modificar o diagrama. Isso impedirá a validação da camada funcione corretamente e pode causar outros problemas, como elementos ausentes ou outros erros ao tentar abrir o diagrama.  
  
 Ver [criar diagramas de camada do seu código](../modeling/create-layer-diagrams-from-your-code.md).  
  
##  <a name="CreateLayers"></a> Definir camadas para representar componentes ou áreas funcionais  
 Camadas representam grupos lógicos de *artefatos*, como projetos, arquivos de código, namespaces, classes e métodos. Você pode criar camadas de artefatos de projetos do Visual c# .NET e Visual Basic .NET, ou anexe especificações ou planos a uma camada vinculando documentos como arquivos Word ou apresentações do PowerPoint. Cada camada aparece como um retângulo no diagrama e mostra o número de artefatos que estão associados a ele. Uma camada pode conter camadas aninhadas que descrevem tarefas mais específicas.  
  
 Como diretriz geral, camadas de nome de acordo com a sua função, por exemplo, "Apresentação" ou "Serviços". Se os artefatos são estreitamente interdependentes, colocá-los na mesma camada. Se os artefatos podem ser atualizados separadamente ou usados em aplicativos separados, colocá-los em diferentes camadas. Para saber mais sobre padrões de disposição em camadas, visite o site Patterns & Practices [ http://go.microsoft.com/fwlink/?LinkId=145794 ](http://go.microsoft.com/fwlink/?LinkId=145794).  
  
> [!TIP]
>  Há determinados tipos de artefatos que você pode vincular a camadas, mas que não dão suporte a validação em relação ao diagrama de camada. Para ver se o artefato dá suporte à validação, abra **Gerenciador de camadas** para examinar as **dá suporte à validação** propriedade do link de artefato. Ver [descobrir dependências existentes entre camadas](#Generate).  
  
 Ao atualizar um aplicativo não familiar, você também pode criar mapas de código. Esses diagramas podem ajudar você a descobrir padrões e as dependências, enquanto você explora o código. Use o Gerenciador de soluções para explorar namespaces e classes, que normalmente correspondem bem a camadas existentes. Atribua esses artefatos de código em camadas, arrastando-os no Gerenciador de soluções para diagramas de camada. Em seguida, você pode usar diagramas de camada para ajudá-lo a atualizar o código e mantê-los consistentes com o seu design.  
  
 Consulte:  
  
-   [Criar diagramas de camada por meio de código](../modeling/create-layer-diagrams-from-your-code.md)  
  
-   [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)  
  
-   [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)  
  
##  <a name="Generate"></a> Descubra as dependências existentes entre camadas  
 Existirá uma dependência sempre que um artefato associado a uma camada tiver uma referência a um artefato associado a outra camada. Por exemplo, uma classe em uma camada declara uma variável que tem uma classe em outra camada. Você pode descobrir dependências existentes com a engenharia reversa-los.  
  
> [!NOTE]
>  As dependências não podem sofrer engenharia reversa para determinados tipos de artefatos. Por exemplo, nenhuma dependência sofrerá engenharia reversa de ou para uma camada vinculada a um arquivo de texto. Para ver quais artefatos têm dependências que você pode fazer engenharia reversa, uma ou várias camadas com o botão direito e, em seguida, clique em **Exibir Links**. Na **Gerenciador de camadas**, examine o **dá suporte à validação** coluna. As dependências não sofrerão engenharia reversa para artefatos para o qual essa coluna mostra **falsos**.  
  
#### <a name="to-reverse-engineer-existing-dependencies-between-layers"></a>Para fazer engenharia reversa de dependências existentes entre camadas  
  
- Selecione uma camada ou várias camadas, uma camada selecionada com o botão direito e, em seguida, clique em **gerar dependências**.  
  
  Normalmente, você verá algumas dependências que não devem existir. É possível editar essas dependências para alinhá-las com o design desejado.  
  
##  <a name="EditArchitecture"></a> Editar camadas e dependências para mostrar o design desejado  
 Para descrever as alterações que você planeja fazer em seu sistema ou a arquitetura pretendida, use as etapas a seguir para editar o diagrama de camada. Você também pode considerar fazer algumas alterações de refatoração para melhorar a estrutura do código antes de estendê-lo. Ver [melhorar a estrutura do código](#Improving).  
  
|**To**|**Execute estas etapas**|  
|------------|-----------------------------|  
|Excluir uma dependência que não deve existir|Clique a dependência e, em seguida, pressione **excluir**.|  
|Alterar ou restringir a direção de uma dependência|Defina suas **direção** propriedade.|  
|Criar novas dependências|Use o **dependência** e **dependência bidirecional** ferramentas.<br /><br /> Para desenhar várias dependências, clique duas vezes na ferramenta. Quando tiver terminado, clique no **ponteiro** ferramenta ou pressione a **ESC** chave.|  
|Especificar que os artefatos associados a uma camada não dependem dos namespaces especificados|Digite os namespaces da camada **dependências de Namespace proibido** propriedade. Use um ponto e vírgula (**;**) para separar os namespaces.|  
|Especificar que os artefatos associados a uma camada não devem pertencer aos namespaces especificados|Digite os namespaces da camada **Namespaces proibidos** propriedade. Use um ponto e vírgula (**;**) para separar os namespaces.|  
|Especificar que os artefatos associados a uma camada devem pertencer a um dos namespaces especificados|Digite o namespace da camada **Namespaces obrigatórios** propriedade. Use um ponto e vírgula (**;**) para separar os namespaces.|  
  
###  <a name="Improving"></a> Melhorar a estrutura do código  
 Alterações de refatoração foram os aprimoramentos que não afetam o comportamento do aplicativo, mas ajudam a tornar o código mais fácil de alterar e estender no futuro. Código bem estruturado tem um design que seja fácil de abstrair a um diagrama de camada.  
  
 Por exemplo, se você criar uma camada para cada namespace no código e, em seguida, fazer engenharia reversa de dependências, deve haver um conjunto mínimo de dependências unidirecionais entre as camadas. Se você criar um diagrama mais detalhado usando classes ou métodos como as camadas, o resultado também deve ter as mesmas características.  
  
 Se isso não for o caso, o código será mais difícil alterar ao longo do tempo e serão menos adequado para a validação usando diagramas de camada.  
  
##  <a name="NewAreas"></a> Novas áreas de design do seu aplicativo  
 Ao iniciar o desenvolvimento de um novo projeto ou uma nova área em um novo projeto, você pode desenhar camadas e dependências para ajudar a identificar os principais componentes antes de começar a desenvolver o código.  
  
-   **Mostrar os padrões de arquitetura identificáveis** em seus diagramas de camada, se possível. Por exemplo, um diagrama de camada que descreve um aplicativo da área de trabalho pode incluir camadas como apresentação, lógica de domínio e Data Store. Um diagrama de camada que aborda um recurso único dentro de um aplicativo pode ter camadas como modelo, exibição e controlador. Para obter mais informações sobre esses padrões, consulte [Patterns & Practices: arquitetura de aplicativo](http://go.microsoft.com/fwlink/?LinkId=145794).  
  
     Se você criar o padrões semelhantes com frequência, crie uma ferramenta personalizada. Ver [definir um personalizado item de caixa de ferramentas de modelagem](../modeling/define-a-custom-modeling-toolbox-item.md).  
  
-   **Criar um artefato de código para cada camada** como um namespace, classe ou componente. Isso torna mais fácil de seguir o código e vincular os artefatos de código a camadas. Assim que você cria cada artefato, você deve vinculá-lo a camada apropriada.  
  
-   **Não é preciso vincular a maioria das classes e outros artefatos a camadas** porque eles se encaixam dentro de artefatos maiores, como namespaces que você já tiver vinculado a camadas.  
  
-   **Criar um novo diagrama para um novo recurso**. Normalmente, haverá um ou mais diagramas de camada que descrevem o aplicativo inteiro. Se você estiver criando um novo recurso dentro do aplicativo, não adicionar ou alterar os diagramas existentes. Em vez disso, crie seu próprio diagrama que reflete as novas partes do código. As camadas no novo diagrama podem incluir a apresentação, lógica de domínio e as camadas de banco de dados para o novo recurso.  
  
     Quando você compila o aplicativo, seu código será validado tanto em relação ao diagrama como um todo e seu diagrama mais detalhado do recurso.  
  
##  <a name="EditLayout"></a> Editar o layout para apresentação e discussão  
 Para ajudar a identificar as camadas e dependências ou discuti-las com os membros da equipe, edite a aparência e o layout do diagrama das seguintes maneiras:  
  
-   Altere as posições de camadas, formas e tamanhos.  
  
-   Altere as cores de camadas e dependências.  
  
    -   Selecione um ou mais camadas ou dependências, clique com botão direito e depois clique em **propriedades**. No **propriedades** janela, edite o **cor** propriedade.  
  
##  <a name="Validate"></a> Valide o código no diagrama  
 Quando você tiver editado o diagrama, você pode validá-la com o código manualmente a qualquer momento ou automaticamente toda vez que você executar uma compilação local ou [!INCLUDE[esprbuild](../includes/esprbuild-md.md)].  
  
 Consulte:  
  
-   [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)  
  
-   [Incluir validação de camada no processo de compilação](#BuildValidation)  
  
##  <a name="UpdateCode"></a> Atualize o código para estar de acordo com a nova arquitetura  
 Normalmente, os erros serão exibidos na primeira vez que você valide o código em um diagrama de camada atualizada. Esses erros podem ter várias causas:  
  
- Um artefato é atribuído à camada errada. Nesse caso, mova o artefato.  
  
- Um artefato como, por exemplo, uma classe usa outra classe de maneira a entrar em conflito com a arquitetura. Nesse caso, refatore o código para remover a dependência.  
  
  Para resolver esses erros, atualize o código até que mais nenhum erro seja exibido durante a validação. Isso geralmente é um processo iterativo. Para obter mais informações sobre esses erros, consulte [validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md).  
  
> [!NOTE]
>  Conforme você desenvolve ou refatora o código, você pode ter os novos artefatos para vincular ao diagrama de camada. No entanto, isso pode não ser necessário, por exemplo, quando você tem camadas que representam a namespaces existentes, e o novo código apenas adiciona mais material a esses namespaces.  
  
 Durante o processo de desenvolvimento, você talvez queira suprimir alguns dos conflitos reportados durante a validação. Por exemplo, você talvez queira suprimir erros que já esteja resolvendo ou que não sejam relevantes para seu cenário específico. Quando você suprime um erro, é uma prática recomendada registrar em log um item de trabalho em [!INCLUDE[esprfound](../includes/esprfound-md.md)]. Para executar essa tarefa, consulte [validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md).  
  
##  <a name="BuildValidation"></a> Incluir validação de camada no processo de compilação  
 Para garantir que as alterações futuras no código em conformidade com os diagramas de camada, incluem a validação de camada ao processo de compilação padrão da sua solução. Sempre que outros membros da equipe Compile a solução, todas as diferenças entre as dependências no código e o diagrama de camada serão relatadas como erros de compilação. Para obter mais informações sobre como incluir validação de camada no processo de compilação, consulte [validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md).  
  
## <a name="see-also"></a>Consulte também  
 [Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)   
 [Criar diagramas de camada por meio de código](../modeling/create-layer-diagrams-from-your-code.md)



