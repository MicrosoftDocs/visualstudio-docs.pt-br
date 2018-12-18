---
title: Escrever código em soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VST.Project.RefactoringCancelled
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], writing code
- managed code [Office development in Visual Studio]
- Office development in Visual Studio, programming languages supported
- Office applications [Office development in Visual Studio], automating
- Office applications [Office development in Visual Studio], writing code
- writing code for Office solutions
- programming [Office development in Visual Studio], model
- Automation [Office development in Visual Studio], managed code
- application development [Office development in Visual Studio], programming model
- Office solutions [Office development in Visual Studio], writing code
- automating Office applications
- application development [Office development in Visual Studio], writing code
- application development [Office development in Visual Studio], automating
- Office projects [Office development in Visual Studio], changing namespaces
- solutions [Office development in Visual Studio], programming model
- programming [Office development in Visual Studio]
- namespaces [Office developmentin Visual Studio], changing in Office solutions
- projects [Office development in Visual Studio], writing code
- Office applications [Office development in Visual Studio], programming model
- managed code extensions [Office development in Visual Studio], writing code
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: e9773c06293f189e572ef84e9b10f45a1ca5d5d8
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670982"
---
# <a name="write-code-in-office-solutions"></a>Escrever código em soluções do Office
  Há alguns aspectos de escrever código em projetos do Office que são diferentes dos outros tipos de projetos no Visual Studio. Muitas dessas diferenças estão relacionadas à forma como os modelos de objeto do Office são expostos ao código gerenciado. Outras diferenças relacionadas ao design de projetos do Office.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="managed-code-and-office-programming"></a>O código gerenciado e programação do Office  
 A tecnologia-chave que torna possível a criação de uma solução integrada do Microsoft Office é a automação, que é parte da tecnologia de modelo de objeto de componente (COM). A automação permite que você use o código para criar e controlar os objetos de software expostos por qualquer aplicativo, DLL, ou de controles ActiveX que oferece suporte a interfaces programáticas apropriadas.  
  
### <a name="understand-primary-interop-assemblies"></a>Entender os assemblies de interoperabilidade primários  
 Aplicativos do Microsoft Office expõem grande parte das suas funcionalidades para automação. No entanto, você não pode usar código gerenciado (como Visual Basic ou c#) diretamente para automatizar aplicativos do Office. Para automatizar aplicativos do Office usando código gerenciado, você deve usar a assemblies de interoperabilidade primários (PIAs) do Office. Assemblies de interoperabilidade primários habilitar código gerenciado interaja com o modelo de objeto COM base em aplicativos do Office.  
  
 Cada aplicativo do Microsoft Office tem um PIA. Quando você cria um projeto do Office no Visual Studio, uma referência para o PIA apropriado é automaticamente adicionada ao projeto. Para automatizar os recursos de outros aplicativos do Office do projeto, você deve adicionar manualmente uma referência para o PIA apropriado. Para obter mais informações, consulte [como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md).  
  
### <a name="use-primary-interop-assemblies-at-design-time-and-runtime"></a>Usar assemblies de interoperabilidade primários no tempo de execução e tempo de design  
 Você deve ter os PIAs do Office instalado e registrado no cache de assembly global no seu computador de desenvolvimento para executar a maioria das tarefas de desenvolvimento. Para obter mais informações, consulte [configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md).  
  
 Os PIAs do Office não são necessários em computadores de usuários finais para executar soluções do Office que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. Para obter mais informações, consulte [Design e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md).  
  
### <a name="use-types-in-primary-interop-assemblies"></a>Usar tipos em assemblies de interoperabilidade primários  
 Os PIAs do Office contém uma combinação de tipos que expõem o modelo de objeto dos aplicativos do Office e infraestrutura adicional que não se destina a ser usado diretamente em seu código. Para obter uma visão geral dos tipos nos PIAs do Office, consulte [visão geral de classes e interfaces em assemblies de interoperabilidade primários do Office](/previous-versions/office/office-12/ms247299\(v\=office.12\)).  
  
 Como os tipos dos PIAs do Office correspondem aos tipos de modelos de objeto COM base em com, a maneira de usar esses tipos geralmente é diferente de outros tipos gerenciados. Por exemplo, a maneira de você chama métodos com parâmetros opcionais em um assembly de interoperabilidade primário do Office depende a linguagem de programação que você está usando em seu projeto. Para mais informações, consulte os seguintes tópicos:  
  
-   [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md).  
  
-   [Associação tardia em soluções do Office](../vsto/late-binding-in-office-solutions.md).  
  
## <a name="program-model-of-office-projects"></a>Modelo do programa de projetos do Office  
 Todos os projetos do Office incluem um ou mais classes geradas que fornecem o ponto de entrada para seu código. Essas classes também fornecem acesso ao modelo de objeto do aplicativo host e o acesso aos recursos, como painéis de ações e painéis de tarefas personalizados.  
  
### <a name="understand-the-generated-classes"></a>Entender as classes geradas  
 Em projetos de nível de documento para Excel e Word, a classe gerada é semelhante a um objeto de nível superior no modelo de objeto do aplicativo. Por exemplo, o gerado `ThisDocument` classe em um projeto de documento do Word fornece os mesmos membros que o <xref:Microsoft.Office.Interop.Word.Document> classe no modelo de objeto do Word. Para obter mais informações sobre as classes geradas em projetos de nível de documento, consulte [personalizações no nível de documento do programa](../vsto/programming-document-level-customizations.md).  
  
 Projetos de suplemento do VSTO fornecem uma classe gerada chamada `ThisAddIn`. Essa classe não se assemelha a uma classe no modelo de objeto do aplicativo host. Em vez disso, essa classe representa o suplemento VSTO em si, e fornece membros que você pode usar para acessar o modelo de objeto do aplicativo host e acessar outros recursos disponíveis para suplementos do VSTO. Para obter mais informações, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
 Incluem todas as classes geradas em projetos do Office `Startup` e `Shutdown` manipuladores de eventos. Para começar a escrever código, você geralmente adiciona código para esses manipuladores de eventos. Para inicializar o suplemento do VSTO, você pode adicionar código para o `Startup` manipulador de eventos. Para limpar os recursos usados pelo seu suplemento do VSTO, você pode adicionar código para o `Shutdown` manipulador de eventos. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).  
  
### <a name="access-the-generated-classes-at-runtime"></a>Acessar as classes geradas em tempo de execução  
 Quando uma solução do Office é carregada, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] cria uma instância de cada uma das classes geradas em seu projeto. Você pode acessar esses objetos de qualquer código em seu projeto usando o `Globals` classe. Por exemplo, você pode usar o `Globals` classe para chamar o código no `ThisAddIn` classe a partir de um manipulador de eventos de um botão da faixa de opções em um suplemento do VSTO.  
  
 Para obter mais informações, consulte [Global de acesso a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).  
  
### <a name="namespace-considerations-in-office-solutions"></a>Considerações de Namespace em soluções do Office  
 Não é possível alterar o *namespace padrão* (ou *namespace raiz* no Visual Basic) de um projeto do Office depois de criar o projeto. O namespace padrão sempre corresponderá o nome do projeto que você especificou quando criou o projeto. Se você renomear seu projeto, o namespace padrão não é alterado. Para obter mais informações sobre o namespace padrão em projetos, consulte [página de aplicativo, Designer de projeto &#40;C&#35; &#41; ](/visualstudio/ide/reference/application-page-project-designer-csharp) e [página de aplicativo, Designer de projeto &#40;Visual Basic&#41; ](/visualstudio/ide/reference/application-page-project-designer-visual-basic).  
  
### <a name="change-the-namespace-of-host-item-classes-in-c-projects"></a>Alterar o namespace das classes de item de host em projetos c#  
 Classes de item de host (por exemplo, o `ThisAddIn`, `ThisWorkbook`, ou `ThisDocument` classes) têm seus próprios namespaces em projetos do Office do Visual c#. Por padrão, o namespace para itens de host em seu projeto coincide com o nome do projeto que você especificou quando criou o projeto.  
  
 Para alterar o namespace dos itens de host em um projeto do Office do Visual c#, use o **Namespace para Item de Host** propriedade. Para obter mais informações, consulte [propriedades em projetos do Office](../vsto/properties-in-office-projects.md).  
  
## <a name="supported-programming-languages-in-office-projects"></a>Suporte para linguagens de programação em projetos do Office  
 Os modelos de projeto do Office no Visual Studio dão suporte a apenas os Visual Basic e Visual c# linguagens de programação. Portanto, esses modelos de projeto estão disponíveis apenas sob o **Visual Basic** e **Visual c#** nós do **novo projeto** da caixa de diálogo [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
## <a name="language-choice-and-office-programming"></a>Escolha da linguagem e programação do Office  
 Microsoft Office e o Visual Basic for Applications (VBA) foram desenvolvidos para trabalhar juntos para otimizar o fluxo de trabalho de personalização do aplicativo. Visual Basic herdou alguns desses desenvolvimentos. Por exemplo, Visual Basic dá suporte a parâmetros opcionais, que significa que você pode escrever menos código ao chamar alguns métodos em assemblies de interoperabilidade primários do Microsoft Office que quando você usa o Visual c#.  
  
## <a name="program-with-visual-basic-vs-visual-c-in-office-solutions"></a>Programa com o Visual Basic vs. Visual c# em soluções do Office  
 Você pode criar soluções do Office usando Visual Basic ou Visual c#. Como os modelos de objeto do Microsoft Office foram projetados para ser usado com o Microsoft Visual Basic for Applications (VBA), os desenvolvedores de Visual Basic podem trabalhar confortavelmente com os objetos expostos pelos aplicativos do Microsoft Office. Desenvolvedores do Visual c# podem usar a maioria dos mesmos recursos como os desenvolvedores de Visual Basic, mas há alguns casos em que eles devem escrever código adicional para usar os modelos de objeto do Office. Também há algumas diferenças entre os recursos básicos de programação no desenvolvimento do Office e o código gerenciado escrito em Visual Basic e c#.  
  
## <a name="key-differences-between-visual-basic-and-visual-c"></a>Principais diferenças entre o Visual Basic e Visual c#  
 A tabela a seguir mostra as principais diferenças entre o Visual Basic e Visual c# no desenvolvimento do Office.  
  
|Recurso|Descrição|Suporte ao Visual Basic|Suporte do Visual c#|  
|-------------|-----------------|--------------------------|------------------------|  
|Parâmetros opcionais|Muitos métodos do Microsoft Office têm parâmetros que não são necessários quando você chama o método. Se nenhum valor for passado para o parâmetro, um valor padrão é usado.|Visual Basic oferece suporte a parâmetros opcionais.|Visual c# dá suporte a parâmetros opcionais na maioria dos casos. Para obter mais informações, consulte [parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md).|  
|Passando parâmetros por referência|Parâmetros opcionais na maioria dos assemblies de interoperabilidade primários do Microsoft Office podem ser passados por valor. No entanto, em alguns assemblies de interoperabilidade primários, os parâmetros opcionais que aceitam tipos de referência devem ser passados por referência.<br /><br /> Para obter mais informações sobre parâmetros de tipo de valor e referência, consulte [passar argumentos por valor e por referência &#40;Visual Basic&#41; ](/dotnet/visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference) (para Visual Basic) e [passar parâmetros &#40;C&#35; Guia de programação do&#41;](/dotnet/csharp/programming-guide/classes-and-structs/passing-parameters).|Nenhum trabalho adicional é necessário para passar parâmetros por referência. O compilador do Visual Basic passa automaticamente os parâmetros por referência quando necessário.|Na maioria dos casos, o compilador do Visual c# passa automaticamente os parâmetros por referência quando necessário. Para obter mais informações, consulte [parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md).|  
|Propriedades parametrizadas|Algumas propriedades aceitam parâmetros e atuam como funções de somente leitura.|Visual Basic oferece suporte às propriedades que aceitam parâmetros.|Visual c# oferece suporte às propriedades que aceitam parâmetros.|  
|Associação tardia|Associação tardia envolve a determinar as propriedades de objetos em tempo de execução, em vez de variáveis de conversão para o tipo de objeto em tempo de design.|Visual Basic que executa a associação tardia quando **Option Strict** está desativado. Quando **Option Strict** estiver ativado, você deverá converter explicitamente objetos e tipos de uso no <xref:System.Reflection> namespace para acessar membros de associação tardia. Para obter mais informações, consulte [associação tardia em soluções do Office](../vsto/late-binding-in-office-solutions.md).|Visual c# executa a associação tardia em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]. Para obter mais informações, consulte [associação tardia em soluções do Office](../vsto/late-binding-in-office-solutions.md).|  
  
## <a name="key-differences-between-office-development-and-managed-code"></a>Principais diferenças entre o desenvolvimento do Office e o código gerenciado  
 A tabela a seguir mostra as principais diferenças entre o desenvolvimento do Office e o código gerenciado escrito em Visual Basic ou Visual c#.  
  
|Recurso|Descrição|Suporte do Visual Basic e Visual c#|  
|-------------|-----------------|-----------------------------------------|  
|Índices de matriz|O limite inferior de matriz de coleções em aplicativos do Microsoft Office começa com 1. Visual Basic e Visual c# usam matrizes com base em 0. Para obter mais informações, consulte [matrizes &#40;C&#35; guia de programação do&#41; ](/dotnet/csharp/programming-guide/arrays/index) e [matrizes no Visual Basic](/dotnet/visual-basic/programming-guide/language-features/arrays/index).|Para acessar o primeiro item de uma coleção no modelo de objeto de um aplicativo do Microsoft Office, use o índice 1 em vez de 0.|  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)   
 [Eventos em projetos do Office](../vsto/events-in-office-projects.md)   
 [Como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)   
 [Como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md)   
 [Associação tardia em soluções do Office](../vsto/late-binding-in-office-solutions.md)   
 [Desenvolvimento colaborativo de soluções do Office](../vsto/collaborative-development-of-office-solutions.md)  
  
  