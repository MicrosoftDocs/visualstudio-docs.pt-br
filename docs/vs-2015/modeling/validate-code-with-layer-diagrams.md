---
title: Validar o código com diagramas de camada | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- layer diagrams, validating
- validation, layer diagrams
- validation, code
- code exploration, validating
- architecture, validating
- Visual Studio Ultimate, validating code
- validation, architecture
- validation, dependencies
- MSBuild, tasks
- MSBuild, layer diagrams
- MSBuild, validating code
ms.assetid: 70cbe55d-4b33-4355-b0a7-88c770a6f75c
caps.latest.revision: 84
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 4d010345c551572bb6458110d2de9ca33fc73155
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792158"
---
# <a name="validate-code-with-layer-diagrams"></a>Validar o código com diagramas de camada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para certificar-se de que o código não causa conflito com seu design, valide o código com diagramas de camada no Visual Studio. Isso pode ajudar a:  
  
- Encontrar conflitos entre dependências no código e nas dependências do diagrama de camada.  
  
- Encontre dependências que talvez sejam afetadas por alterações propostas.  
  
   Por exemplo, é possível editar o diagrama de camada para mostrar alterações na arquitetura em potencial e, em seguida, validar o código para ver as dependências afetadas.  
  
- Refatore ou migre o código para um design diferente.  
  
   Encontre o código ou as dependências que exijam trabalho quando você move o código para uma arquitetura diferente.  
  
  **Requisitos**  
  
- Visual Studio  
  
- Visual Studio em seu servidor do Team Foundation Build para validar o código automaticamente com o Team Foundation Build  
  
- Uma solução com um projeto de modelagem com um diagrama de camada. Esse diagrama de camada deve ser vinculado aos artefatos e projetos do Visual C# .NET ou do Visual Basic .NET que você deseja validar. Ver [criar diagramas de camada do seu código](../modeling/create-layer-diagrams-from-your-code.md).  
  
  Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
  É possível validar manualmente o código com base em um diagrama de camada aberto no Visual Studio ou em um prompt de comando. Também é possível validar o código automaticamente durante a execução de compilações locais ou do Team Foundation Build. Ver [vídeo do Channel 9: Design e validar sua arquitetura usando diagramas de camada](http://go.microsoft.com/fwlink/?LinkID=252073).  
  
> [!IMPORTANT]
>  Se você quiser executar a validação de camada com o Team Foundation Build, você deve instalar também a mesma versão do Visual Studio no seu servidor de compilação.  
  
-   [Se um item dá suporte a validação](#SupportsValidation)  
  
-   [Incluir outros assemblies .NET e projetos para validação](#IncludeReferences)  
  
-   [Validar código manualmente](#ValidateManually)  
  
-   [Validar código automaticamente](#ValidateAuto)  
  
-   [Solucionar problemas de validação de camada](#TroubleshootingValidation)  
  
-   [Entenda e resolva erros de validação de camada](#UnderstandingValidationErrors)  
  
##  <a name="SupportsValidation"></a> Se um item dá suporte a validação  
 É possível vincular camadas a sites, documentos do Office, arquivos de texto sem formatação e arquivos em projetos compartilhados entre vários aplicativos, mas o processo de validação não os incluirá. Os erros de validação não serão exibidos para referências a projetos ou assemblies vinculados a camadas separadas quando nenhuma dependência for exibida entre essas camadas. Essas referências não serão consideradas dependências, a menos que o código use essas referências.  
  
1.  No diagrama de camada, selecione uma ou mais camadas, clique com botão direito sua seleção e, em seguida, clique em **Exibir Links**.  
  
2.  Na **Gerenciador de camadas**, examine o **dá suporte à validação** coluna. Se o valor for falso, o item não dará suporte à validação.  
  
##  <a name="IncludeReferences"></a> Incluir outros assemblies .NET e projetos para validação  
 Quando você arrasta itens para o diagrama de camada, referências a projetos ou assemblies do .NET correspondentes são adicionadas automaticamente para o **referências de camada** pasta no projeto de modelagem. Essa pasta contém referências aos assemblies e aos projetos analisados durante a validação. É possível incluir outros assemblies e projetos do .NET para avaliação sem arrastá-los manualmente para o diagrama de camada.  
  
1.  Na **Gerenciador de soluções**, clique com botão direito no projeto de modelagem ou o **referências de camada** pasta e clique **Add Reference**.  
  
2.  No **adicionar referência** caixa de diálogo, selecione os assemblies ou projetos e, em seguida, clique em **Okey**.  
  
##  <a name="ValidateManually"></a> Validar código manualmente  
 Se você tiver um diagrama de camada aberto vinculado a itens de solução, você pode executar o **validar** comando de atalho do diagrama. Você também pode usar o prompt de comando para executar o **msbuild** com o **validatearchitecture** propriedade personalizada definida como **verdadeiro**. Por exemplo, à medida que fizer alterações no código, execute a validação da camada regularmente de forma que você possa capturar conflitos de dependência com antecedência.  
  
#### <a name="to-validate-code-from-an-open-layer-diagram"></a>Para validar o código com base em um diagrama de camada aberto  
  
1.  Clique com botão direito na superfície do diagrama e, em seguida, clique em **validar arquitetura**.  
  
    > [!NOTE]
    >  Por padrão, o **ação de compilação** propriedade no arquivo de diagrama (. layerdiagram) de camada é definida como **validar** para que o diagrama seja incluído no processo de validação.  
  
     O **Error List** janela relata os erros que ocorrem. Para obter mais informações sobre erros de validação, consulte [compreender e resolver erros de validação de camada](#UnderstandingValidationErrors).  
  
2.  Para exibir a origem de cada erro, clique duas vezes no erro na **Error List** janela.  
  
    > [!NOTE]
    >  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] pode mostrar um mapa de código em vez da origem do erro. Isso ocorre quando o código tem uma dependência em um assembly não especificado pelo diagrama de camada ou o código não tem uma dependência especificada pelo diagrama de camada. Examine o mapa de códigos ou o código para determinar se a dependência deve existir. Para obter mais informações sobre mapas de código, consulte [mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md).  
  
3.  Para gerenciar erros, consulte [gerenciar erros de validação](#ManageErrors).  
  
#### <a name="to-validate-code-at-the-command-prompt"></a>Para validar o código no prompt de comando  
  
1. Abra o prompt de comando do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
2. Escolha uma das seguintes opções:  
  
   - Para validar o código em um projeto de modelagem específico na solução, execute [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] com a propriedade personalizada a seguir.  
  
     ```  
     msbuild <FilePath+ModelProjectFileName>.modelproj /p:ValidateArchitecture=true  
     ```  
  
     - ou –  
  
       Navegue até a pasta que contém o arquivo de modelagem do projeto (.modelproj) e o diagrama de camada e, em seguida, execute [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] com a seguinte propriedade personalizada:  
  
     ```  
     msbuild /p:ValidateArchitecture=true   
     ```  
  
   - Para validar o código em todos os projeto de modelagem na solução, execute [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] com a propriedade personalizada a seguir:  
  
     ```  
     msbuild <FilePath+SolutionName>.sln /p:ValidateArchitecture=true   
     ```  
  
     - ou –  
  
       Navegue até a pasta da solução, que deve conter um projeto de modelagem com um diagrama de camada e, em seguida, execute [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] com a seguinte propriedade personalizada:  
  
     ```  
     msbuild /p:ValidateArchitecture=true  
     ```  
  
     Todos os erros ocorridos serão listados. Para obter mais informações sobre [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)], consulte [MSBuild](../msbuild/msbuild.md) e [tarefa MSBuild](../msbuild/msbuild-task.md).  
  
   Para obter mais informações sobre erros de validação, consulte [compreender e resolver erros de validação de camada](#UnderstandingValidationErrors).  
  
###  <a name="ManageErrors"></a> Gerenciar erros de validação  
 Durante o processo de desenvolvimento, você talvez queira suprimir alguns dos conflitos reportados durante a validação. Por exemplo, você talvez queira suprimir erros que já esteja resolvendo ou que não sejam relevantes para seu cenário específico. Quando você suprime um erro, é uma prática recomendada registrar em log um item de trabalho em [!INCLUDE[esprfound](../includes/esprfound-md.md)].  
  
> [!WARNING]
>  Você já deve estar conectado ao TFS fonte de código de controle (SCC) para criar ou vincular a um item de trabalho. Se você tentar abrir uma conexão em um SCC diferentes do TFS, o Visual Studio fecha automaticamente a solução atual. Certifique-se de que você já estiver conectado ao SCC apropriado antes de tentar criar ou vincular a um item de trabalho. Em versões posteriores do Visual Studio, os comandos de menu não estão disponíveis se você não estiver conectado a um SCC.  
  
##### <a name="to-create-a-work-item-for-a-validation-error"></a>Para criar um item de trabalho para um erro de validação  
  
- No **lista de erros** janela, o erro com o botão direito, aponte para **Criar Item de trabalho**e, em seguida, clique no tipo de item de trabalho que você deseja criar.  
  
  Use essas tarefas para gerenciar erros de validação na **Error List** janela:  
  
|**To**|**Siga estas etapas**|  
|------------|----------------------------|  
|Suprimir erros selecionados durante a validação|Clique em um ou vários erros selecionados, aponte para **gerenciar erros de validação**e, em seguida, clique em **suprimir erros**.<br /><br /> Os erros suprimidos são exibidos com formatação de tachado. Quando você executar a validação da próxima vez, esses erros não serão exibidos.<br /><br /> Os erros suprimidos são acompanhados em um arquivo .suppressions para o arquivo do diagrama de camada correspondente.|  
|Parar a supressão de erros selecionados|Clique com botão direito o erros ou erros suprimidos selecionados, aponte para **gerenciar erros de validação**e, em seguida, clique em **parar de suprimir erros**.<br /><br /> Os erros suprimidos selecionados serão exibidos quando você executar a validação na próxima vez.|  
|Restaurar todos os erros suprimidos na **Error List** janela|Clique com botão direito em qualquer lugar na **lista de erros** janela, aponte para **gerenciar erros de validação**e, em seguida, clique em **Mostrar todos os erros suprimidos**.|  
|Ocultar todos os erros suprimidos do **Error List** janela|Clique com botão direito em qualquer lugar na **lista de erros** janela, aponte para **gerenciar erros de validação**e, em seguida, clique em **ocultar todos os erros suprimidos**.|  
  
##  <a name="ValidateAuto"></a> Validar código automaticamente  
 É possível executar a validação da camada sempre que você executa uma compilação local. Se a equipe usar o Team Foundation Build, será possível executar a validação da camada com check-ins restritos, que você pode especificar criando uma tarefa MSBuild personalizada, e usar relatórios de compilação para coletar erros de validação. Para criar compilações de check-in, consulte [usar um processo de compilação de check-in para validar alterações](http://msdn.microsoft.com/library/9cfc8b9c-1023-40fd-8ab5-1b1bd9c172ec).  
  
#### <a name="to-validate-code-automatically-during-a-local-build"></a>Para validar automaticamente o código durante uma compilação local  
  
-   Use um editor de texto para abrir o arquivo do projeto de modelagem (.modelproj) e, em seguida, inclua a seguinte propriedade:  
  
```  
<ValidateArchitecture>true</ValidateArchitecture>  
```  
  
 \- ou -  
  
1. Na **Gerenciador de soluções**, o projeto de modelagem que contém o diagrama de camada ou diagramas com o botão direito e, em seguida, clique em **propriedades**.  
  
2. No **propriedades** janela, defina o projeto de modelagem **validar arquitetura** propriedade a ser **verdadeiro**.  
  
    Isso inclui o projeto de modelagem no processo de validação.  
  
3. Na **Gerenciador de soluções**, clique no arquivo de diagrama (. layerdiagram) de camada que você deseja usar para validação.  
  
4. No **propriedades** janela, certifique-se de que o diagrama **Build Action** estiver definida como **validar**.  
  
    Isso inclui o diagrama de camada no processo de validação.  
  
   Para gerenciar erros na janela lista de erros, consulte [gerenciar erros de validação](#ManageErrors).  
  
#### <a name="to-validate-code-automatically-during-a-team-foundation-build"></a>Para validar automaticamente o código durante um Team Foundation Build  
  
1. Na **Team Explorer**, clique duas vezes a definição de compilação e, em seguida, clique em **processo**.  
  
2. Sob **parâmetros do processo de compilação**, expanda **compilação**e digite o seguinte no **argumentos de MSBuild** parâmetro:  
  
    `/p:ValidateArchitecture=true`  
  
   Para obter mais informações sobre erros de validação, consulte [compreender e resolver erros de validação de camada](#UnderstandingValidationErrors). Para obter mais informações sobre [!INCLUDE[esprbuild](../includes/esprbuild-md.md)], consulte:  
  
-   [Compilar o aplicativo](http://msdn.microsoft.com/library/a971b0f9-7c28-479d-a37b-8fd7e27ef692)  
  
-   [Usar o modelo padrão para o processo de compilação](http://msdn.microsoft.com/library/43930b12-c21b-4599-a980-2995e3d16e31)  
  
-   [Modificar uma compilação herdada baseada em upgradetemplate. XAML](http://msdn.microsoft.com/library/ee1a8259-1dd1-4a10-9563-66c5446ef41c)  
  
-   [Personalizar o modelo de processo de compilação](http://msdn.microsoft.com/library/b94c58f2-ae6f-4245-bedb-82cd114f6039)  
  
-   [Monitore o andamento de uma compilação em execução](http://msdn.microsoft.com/library/e51e3bad-2d1d-4b7b-bfcc-c43439c6c8ef)  
  
##  <a name="TroubleshootingValidation"></a> Solucionar problemas de validação de camada  
 A tabela a seguir descreve problemas na validação da camada e sua resolução. Esses problemas são diferentes dos erros resultantes de conflitos entre o código e o design. Para obter mais informações sobre esses erros, consulte [compreender e resolver erros de validação de camada](#UnderstandingValidationErrors).  
  
|**Problema**|**Possível causa**|**Resolução**|  
|---------------|------------------------|--------------------|  
|Os erros de validação não ocorrem como esperado.|A validação não funciona em diagramas de camada copiados de outros diagramas de camada no Gerenciador de Soluções e que estejam no mesmo projeto de modelagem. Os diagramas de camada copiados dessa maneira contêm as mesmas referências do diagrama de camada original.|Adicione um novo diagrama de camada ao projeto de modelagem.<br /><br /> Copie os elementos do diagrama de camada de origem para o novo diagrama.|  
  
##  <a name="UnderstandingValidationErrors"></a> Entender e resolver erros de validação de camada  
 Quando você valida o código em um diagrama de camada, os erros de validação ocorrem quando o código entra em conflito com o design. Por exemplo, as seguintes condições podem fazer os erros de validação ocorrerem:  
  
- Um artefato é atribuído à camada errada. Nesse caso, mova o artefato.  
  
- Um artefato como, por exemplo, uma classe usa outra classe de maneira a entrar em conflito com a arquitetura. Nesse caso, refatore o código para remover a dependência.  
  
  Para resolver esses erros, atualize o código até que mais nenhum erro seja exibido durante a validação. É possível realizar essa tarefa de maneira iterativa.  
  
  A seção a seguir descreve a sintaxe usada nesses erros, explica o significado desses erros e sugere o que é possível fazer para o resolver ou gerenciá-los.  
  
|**Sintaxe**|**Descrição**|  
|----------------|---------------------|  
|*ArtifactN*(*ArtifactTypeN*)|*{1&gt;artefaton&lt;1* é um artefato associado uma camada no diagrama de camada.<br /><br /> *1&gt;tipoartefaton&lt;1* é o tipo de *2&gt;artefaton&lt;2*, como um **classe** ou **método**, por exemplo:<br /><br /> MySolution.MyProject.MyClass.MyMethod(Method)|  
|*NamespaceNameN*|O nome de um namespace.|  
|*LayerNameN*|O nome de uma camada no diagrama de camada.|  
|*Tipodependência*|O tipo de relação de dependência entre *artefato1* e *artefato2*. Por exemplo, *artefato1* tem um **chamadas** relação com *artefato2*.|  
  
|**Erro de sintaxe**|**Descrição do erro**|  
|----------------------|---------------------------|  
|AV0001: Dependência inválida: *artefato1*(*Tipoartefato1*)--> *artefato2*(*Tipoartefato2*)<br /><br /> Camadas: *LayerName1*, *LayerName2* &#124; dependências: *Tipodependência*|*Artefato1* na *LayerName1* não deve ter uma dependência na *artefato2* na *LayerName2* porque *LayerName1* não tem uma dependência direta no *LayerName2*.|  
|AV1001: Namespace de inválido: *artefato*<br /><br /> Camada: *Nomecamada* &#124; necessário Namespace: *Nomenamespace1* &#124; Namespace atual: *Nomenamespace2*|*{1&gt;nomecamada&lt;1* exige que seus artefatos associados devam pertencer ao *Nomenamespace1*. *Artefato* está no *Nomenamespace2*, e não *Nomenamespace1*.|  
|AV1002: Depende do Namespace proibido: *artefato1*(*Tipoartefato1*) &#124; *artefato2*(*Tipoartefato2*)<br /><br /> Camada: *Nomecamada* &#124; proibido Namespace: *NamespaceName* &#124; dependências: *Tipodependência*|*{1&gt;nomecamada&lt;1* exige que seus artefatos associados não devam depender *NamespaceName*. *Artefato1* não pode depender *artefato2* porque *artefato2* está em *NamespaceName*.|  
|AV1003: No Namespace proibido: *artefato*(*Tipoartefato*)<br /><br /> Camada: *Nomecamada* &#124; proibido Namespace: *NamespaceName*|*{1&gt;nomecamada&lt;1* exige que seus artefatos associados não possam pertencer ao *NamespaceName*. *Artefato* pertence *NamespaceName*.|  
|AV3001: Link ausente: camada '*Nomecamada*'contém links para'*artefato*' que não foi encontrado. Você não tem uma referência de assembly?|*{1&gt;nomecamada&lt;1* links para um artefato que não pode ser encontrado. Por exemplo, um link para uma classe talvez não seja encontrado porque o projeto de modelagem não tem uma referência para o assembly que contém a classe.|  
|AV9001: A análise arquitetônica encontrou erros internos. Os resultados talvez não estejam completos. Para obter mais informações, consulte o log de eventos da compilação detalhado ou a janela de saída.|Consulte o log de eventos da compilação ou a janela de saída para obter mais detalhes.|  
  
## <a name="security"></a>Segurança  
  
## <a name="see-also"></a>Consulte também  
 [Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)



