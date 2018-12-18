---
title: Estender modelos e diagramas UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-techdebt
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML - extending
- UML model, extending
ms.assetid: b5bfa61e-ea59-4c3b-b5af-53475d7d13cd
caps.latest.revision: 39
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 74f3c518682997dca57a630c6f084437f7175d80
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51794758"
---
# <a name="extend-uml-models-and-diagrams"></a>Estender modelos e diagramas UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico resume as diferentes maneiras em que você pode estender a ferramentas incluídas com o Visual Studio de modelagem UML. Para ver quais versões do Visual Studio dão suporte a cada tipo de modelo e a ferramenta, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 No cenário de exemplo a seguir, Fabrikam projeta e instala o tratamento de sistemas de bagagem de aeroporto. Do projeto em um aeroporto para o próximo, existem muitas semelhanças no equipamento básico e o software que controla a ele. No entanto, também há vários fatores que podem variar amplamente, como a configuração de belts transportadora, mesas de check-in, os compartimentos de armazenamento e outro equipamentos de tratamento de recipiente.  
  
 Ao iniciar um novo projeto, a equipe da Fabrikam cria um modelo UML para ajudá-los a discutir esses requisitos entre si e com seus clientes. Eles usam diagramas de atividade para representar o fluxo de recipientes, conosco de objeto que representa cada peça do equipamento. O modelo UML não representa diretamente o código do sistema.  
  
 Equipe de ferramentas da Fabrikam faz uma série de aprimoramentos para ajudar as equipes de desenvolvimento. As seções a seguir descrevem os diferentes tipos de extensões que você pode definir. Você pode combinar várias dessas técnicas em uma extensão do Visual Studio.  
  
 Para obter mais informações, consulte este vídeo: ![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo")[série MSDN How Do I: ferramentas UML e extensibilidade](http://go.microsoft.com/fwlink/?LinkId=214467).  
  
##  <a name="Requirements"></a> Requisitos  
  
-   [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
-   [SDK de modelagem para Visual Studio 2015](http://www.microsoft.com/download/details.aspx?id=48148).  
  
## <a name="profiles"></a>Perfis  
 Perfis permitem que você definir estereótipos e propriedades adicionais nos elementos UML.  
  
 Os desenvolvedores de ferramentas da Fabrikam definem estereótipos em nós de objeto de diagramas de atividade, como «Esteira» e «check-in desk». Quando um membro da equipe cria uma esquema usando um diagrama de atividade de tratamento de bagagem, eles agora podem definir estereótipos para indicar o tipo de equipamento de cada nó representa. Os desenvolvedores de ferramenta definem propriedades adicionais sobre alguns dos estereótipos, para que os usuários podem registrar valores, como a capacidade de uma esteira e a direção de uma mesa de check-in.  
  
 Para obter mais informações, consulte [definir um perfil para estender UML](../modeling/define-a-profile-to-extend-uml.md).  
  
## <a name="custom-toolbox-items"></a>Itens de caixa de ferramentas personalizado  
 Um item de caixa de ferramentas personalizado cria um elemento ou um grupo de elementos de um protótipo que você define em um diagrama. Por exemplo, você poderia criar uma ferramenta que cria casos de uso em uma cor específica ou estereótipo ou um grupo de classes e as associações que representa um padrão de design. Você pode adicionar esses itens de caixa de ferramentas para extensões do Visual Studio e distribuí-los a outros usuários.  
  
 Para obter mais informações, consulte [definir um personalizado item de caixa de ferramentas de modelagem](../modeling/define-a-custom-modeling-toolbox-item.md).  
  
## <a name="validation"></a>Validação  
 Você pode definir regras para garantir que um modelo UML está em conformidade com as restrições especificadas.  
  
 Os desenvolvedores de ferramentas da Fabrikam definem regras para ajudar a evitar erros simples nos modelos de tratamento de bagagem de membros da equipe. Por exemplo, uma mesa de check-in não pode ser conectada diretamente a um compartimento de armazenamento. Deve haver pelo menos uma esteira entre eles.  
  
 Para obter mais informações, consulte [definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md).  
  
## <a name="menu-commands"></a>Comandos de menu  
 Você pode definir comandos que os usuários podem chamar clicando com o elementos em um diagrama UML. Os comandos podem atualizar o modelo e os diagramas ou executar outras operações no [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)].  
  
 A Fabrikam define os comandos de menu para automatizar as operações executadas com frequência, como criar uma mesa de check-in e conectá-lo a uma esteira selecionado ou reorganizar um diagrama de acordo com as regras de layout da empresa.  
  
 Ver [definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md).  
  
## <a name="gestures"></a>Gestos  
 Você pode definir comandos que os usuários iniciam clicando duas vezes em um elemento de diagrama ou arrastando-se para um diagrama ou um elemento no diagrama. Você pode definir comandos que podem lidar com itens arrastados de outros diagramas UML, de outras partes do Visual Studio ou de outros aplicativos ou Windows Explorer (ou Explorador de arquivos.  
  
 Os membros da equipe Fabrikam podem associar um arquivo como uma especificação de qualquer elemento de modelo arrastando-o na área de trabalho do Windows. Os desenvolvedores de ferramenta definido um estereótipo que fornece a qualquer elemento com uma propriedade de caminho de arquivo e um gesto que define o estereótipo e o caminho do arquivo quando um arquivo é solto em um elemento.  
  
 Para obter mais informações, consulte [definir um manipulador de gesto em um diagrama de modelagem](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md).  
  
## <a name="responding-to-changes"></a>Respondendo a alterações  
 Você pode escrever código que responde às alterações no modelo, seja ele causado por ações do usuário ou por outro código de programa.  
  
 Os desenvolvedores da Fabrikam criar código que define a cor de um elemento depende do seu estereótipo automaticamente. Isso torna fácil para os usuários distinguir as diferentes funções desempenhadas pelos elementos nos modelos.  
  
 Para obter mais informações, consulte [como: responder a alterações em um modelo UML](../misc/how-to-respond-to-changes-in-a-uml-model.md).  
  
## <a name="model-bus"></a>Model Bus  
 Model Bus permite que você acesse um diagrama ou um modelo de outro diagrama ou de outro [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] extensão. Entre outras coisas, isso permite que você distribua informações por mais de um modelo, para que várias pessoas podem trabalhar no modelo combinado ao mesmo tempo.  
  
 A Fabrikam usa elementos em diagramas de atividade para representar o equipamento de tratamento de bagagem. Cada item dos equipamentos pode ter uma especificação mais detalhada em outro diagrama, que pode ser em outro modelo. As restrições de validação no diagrama de fluxo de bagagem podem recuperar as propriedades relevantes do equipamento de outros diagramas. As referências a outros diagramas são armazenadas em propriedades adicionais definidas em estereótipos.  
  
 Para obter mais informações, consulte [modelos de UML integrar com outros modelos e ferramentas](../modeling/integrate-uml-models-with-other-models-and-tools.md).  
  
## <a name="generation"></a>geração  
 De um modelo, você pode gerar o código do programa, scripts, configurações, documentos, novos modelos ou outros artefatos.  
  
 Nos sistemas de coleta de bagagem Fabrikam projeta, grande parte do código do programa é o mesmo de um projeto para a próxima. O principal aspecto de variável é o plano do fluxo de bagagem em torno do aeroporto. Depois que a equipe de design tiver a experiência dos seus primeiros projetos alguns, os desenvolvedores de ferramentas criar um modelo que gera, do modelo de fluxo de bagagem, grande parte do código de variável de programa e outros arquivos, como documentos do usuário. Isso reduz consideravelmente a taxa de erro e o tempo de desenvolvimento para cada novo projeto.  
  
 Para obter mais informações, consulte [gerar arquivos de um modelo UML](../modeling/generate-files-from-a-uml-model.md).  
  
## <a name="team-foundation-server-integration"></a>Integração do Team Foundation Server  
 Você pode vincular itens de trabalho a elementos de modelo e acessar os itens vinculados de forma programática.  
  
 Os desenvolvedores de ferramentas da Fabrikam escrevem uma ferramenta que gera uma agenda de trabalho para cada projeto de aeroporto. Os itens de trabalho na agenda são vinculados aos elementos de modelo.  
  
 Para obter mais informações, consulte [definir um manipulador de link de item de trabalho](../modeling/define-a-work-item-link-handler.md).  
  
## <a name="tools-that-update-models"></a>Ferramentas que atualizar modelos  
 Você pode criar aplicativos autônomos e extensões do Visual Studio que podem carregar modelos de UML.  
  
 Os desenvolvedores da Fabrikam criar uma ferramenta que lê um modelo e gera relatórios sobre o andamento do trabalho em cada elemento do modelo.  
  
 Para obter mais informações, consulte [ler um modelo UML no código do programa](../modeling/read-a-uml-model-in-program-code.md).  
  
## <a name="domain-specific-languages"></a>Linguagens específicas de domínio  
 Quando você usa com frequência um tipo específico de modelo, ele pode ser útil criar uma linguagem específica de domínio. Isso pode ser feito para atender às suas necessidades de negócios mais perto do que um modelo UML, mas requer mais esforço para compilá-lo e mantê-lo. Para obter mais informações, consulte [SDK de modelagem para Visual Studio - linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md).  
  
## <a name="external-resources"></a>Recursos externos  
  
|**Categoria**|**Links**|  
|------------------|---------------|  
|**Vídeos**|![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo") [série MSDN How Do I: ferramentas UML e extensibilidade](http://go.microsoft.com/fwlink/?LinkId=214467)<br /><br /> ![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo") [Channel 9: UML com o Visual Studio](http://go.microsoft.com/fwlink/?LinkId=199957)|  
|**Fóruns**|-   [Visualização do Visual Studio e ferramentas de modelagem](http://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visualização do Visual Studio e modelagem (ferramentas DSL) do SDK](http://go.microsoft.com/fwlink/?LinkId=184721)|  
|**Blogs**|[Visual Studio ALM + Team Foundation Server Blog](http://go.microsoft.com/fwlink/?LinkID=201340)|  
|**Artigos técnicos e diários**|[MSDN Architecture Center](http://go.microsoft.com/fwlink/?LinkId=201343)|  
  
## <a name="see-also"></a>Consulte também  
 [Criar modelos para seu aplicativo](../modeling/create-models-for-your-app.md)   
 [Referência de API para extensibilidade de modelagem UML](../modeling/api-reference-for-uml-modeling-extensibility.md)



