---
title: Visão geral de modelos de projeto do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- templates [Office development in Visual Studio], about project templates
- Excel Workbook project template
- Word Template project template
- Excel [Office development in Visual Studio], project templates
- Project [Office development in Visual Studio], project templates
- project templates [Office development in Visual Studio]
- project templates, Word
- InfoPath [Office development in Visual Studio], project templates
- Excel Template project template
- project templates, 2007 Microsoft Office system
- project templates, Excel
- PowerPoint [Office development in Visual Studio], project templates
- Word [Office development in Visual Studio], Word project templates
- Office projects [Office development in Visual Studio], templates
- Excel projects in Visual Studio
- Word Document project template
- Visio [Office development in Visual Studio], project templates
- Word projects in Visual Studio
- Outlook [Office development in Visual Studio], project templates
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d1ad35b9aecc9e7559902104f447cbbec3415b49
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49934321"
---
# <a name="office-project-templates-overview"></a>Visão geral de modelos de projeto do Office
  As ferramentas de desenvolvedor do Microsoft Office no Visual Studio incluem modelos de projeto para criar os seguintes tipos de soluções do Office:  
  
- [Personalizações no nível do documento](#DocLevel)  
  
- [Suplementos do VSTO](#AppLevel)  
  
  Para obter uma comparação detalhada desses tipos de soluções do Office, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md).  
  
  Os modelos de projeto do Office estão disponíveis na **novo projeto** caixa de diálogo de **Office** nó do **Visual c#** e **Visual Basic**nós de linguagem. Cada modelo gera um projeto com configuração adequada para o aplicativo de destino, incluindo referências de assembly e configurações de depuração.  
  
  Cada projeto fornece arquivos e código para que você comece em um tipo de solução específico. O código gerado para cada projeto inclui manipuladores de eventos de inicialização e desligamento. Você pode adicionar código a esses manipuladores de eventos para inicializar sua solução quando ela for carregada e limpá-la quando ela for descarregada. Para obter mais informações, consulte [projetos do Office no ambiente do Visual Studio](../vsto/office-projects-in-the-visual-studio-environment.md) e [eventos em projetos do Office](../vsto/events-in-office-projects.md).  
  
> [!NOTE]  
>  As ferramentas de desenvolvimento do Office estão incluídas em determinadas edições do Visual Studio. Para obter mais informações, consulte [configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md).  
  
##  <a name="DocLevel"></a> Personalizações no nível do documento  
 O **Office** nó na **novo projeto** caixa de diálogo fornece os seguintes modelos de projeto para ajudá-lo a iniciar a criação de personalizações no nível de documento para Word e Excel:  
  
- **Word 2013 e o documento do VSTO 2016**  
  
- **Word 2013 e o modelo do VSTO 2016**  
  
- **Excel 2013 e pasta de trabalho do VSTO 2016**  
  
- **Excel 2013 e modelo do VSTO 2016**  
  
- **Documento do VSTO do Word 2010**  
  
- **Modelo do VSTO do Word 2010**  
  
- **Pasta de trabalho do VSTO do Excel 2010**  
  
- **Modelo do VSTO do Excel 2010**  
  
  Os modelos de projeto da Pasta de Trabalho do Excel e do Documento do Word fornecem código para que você comece a criar uma solução que se baseie em uma pasta de trabalho ou em um documento específico. Nesses tipos de solução, seu código é executado apenas quando o documento associado é aberto no Word ou Excel.  
  
  Os modelos de projeto do Modelo do Excel e Modelo do Word se comportam de forma idêntica aos modelos de projeto da Pasta de Trabalho do Excel e do Documento do Word. No entanto, os modelos de projeto do Modelo do Word e Modelo do Excel tornam mais fácil para os usuários criar novas cópias locais de documento ou pasta de trabalho do modelo personalizado em sua solução. Os recursos em sua solução estão disponíveis no novo documento que o usuário cria do modelo.  
  
> [!NOTE]  
>  Modelos do Word que fazem referência a extensões de código gerenciado não podem ser usados como global VSTO Add-ins. O assembly não será chamado se o modelo for carregado do diretório Inicialização do Word. Para obter mais informações, consulte [limitações de modelos globais e Excel Add-ins (arquivos. xla)](#Limitations)  
  
 Para obter informações sobre como começar esses tipos de projeto, consulte os seguintes tópicos:  
  
-   [Personalizações em nível de documento do programa](../vsto/programming-document-level-customizations.md)  
  
-   [Soluções do Word](../vsto/word-solutions.md)  
  
-   [Soluções do Excel](../vsto/excel-solutions.md)  
  
-   [Passo a passo: Criar a primeira personalização no nível de documento para Word](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)  
  
-   [Passo a passo: Criar a primeira personalização no nível de documento para Excel](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)  
  
##  <a name="AppLevel"></a> Suplementos do VSTO  
 O **Office/SharePoint** nó na **novo projeto** caixa de diálogo fornece os seguintes modelos de projeto para ajudá-lo a iniciar a criação de suplementos do VSTO.  
  
- **Suplemento do VSTO do Excel 2013 e 2016**  
  
- **Suplemento do InfoPath 2013 VSTO**  
  
- **Suplemento do VSTO do Outlook 2013 e 2016**  
  
- **Suplemento do PowerPoint 2013 e 2016**  
  
- **Project 2013 e 2016 em**  
  
- **Suplemento do Visio 2013 e 2016**  
  
- **Suplemento do Word 2013 e 2016**  
  
- **Suplemento do Excel 2010**  
  
- **Suplemento do InfoPath 2010**  
  
- **Suplemento do Outlook 2010**  
  
- **Suplemento do PowerPoint 2010**  
  
- **Suplemento do Project 2010**  
  
- **Suplemento do Visio 2010**  
  
- **Suplemento do Word 2010**  
  
  Quando você cria um projeto que se baseia em um desses modelos de projeto, o código na sua solução é executado quando o aplicativo associado é aberto. Diferentemente dos projetos no nível de documento, seu código não é associado a um único documento.  
  
  Para obter mais informações sobre como começar esses tipos de projeto, consulte os seguintes tópicos:  
  
- [Introdução à programação VSTO Add-ins](../vsto/getting-started-programming-vsto-add-ins.md)  
  
- [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)  
  
- [Passo a passo: Criar seu primeiro suplemento VSTO para Excel](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)  
  
- [Passo a passo: Criar seu primeiro suplemento VSTO para Outlook](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)  
  
- [Passo a passo: Criar seu primeiro suplemento VSTO para PowerPoint](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)  
  
- [Passo a passo: Criar seu primeiro suplemento VSTO para o projeto](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)  
  
- [Passo a passo: Criar seu primeiro suplemento VSTO para Word](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)  
  
## <a name="document-vs-template-solutions"></a>Vs. soluções de modelo de documento  
 Quando você cria uma solução em torno de uma pasta de trabalho do Excel e de um documento do Word, é preciso decidir a melhor maneira de disponibilizar esse documento a seus usuários.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Em algumas situações, talvez seja conveniente fornecer uma cópia de um documento para cada usuário. Nesse caso, crie sua solução usando um projeto de documento do Excel ou Word.  
  
 Em outras situações, talvez seja conveniente tornar um modelo disponível em um servidor, de modo que cada usuário possa abrir o modelo e salvar uma cópia local como um documento. Nesse caso, crie sua solução usando um projeto de modelo do Excel ou Word.  
  
## <a name="comparison"></a>Comparação  
 A tabela a seguir descreve as diferenças entre documentos e modelos.  
  
|Documentos|Modelos|  
|---------------|---------------|  
|Os usuários podem abrir e modificar um documento, a menos que ele seja definido para ser somente leitura. Todas as alterações salvas são mantidas no original.|Os usuários podem abrir um modelo para criar uma cópia local como um novo documento. Eles não podem modificar o original, a menos que recebam permissões especiais.|  
|Quando aberto, o documento gera o evento <xref:Microsoft.Office.Tools.Word.Document.Open>.|Quando aberto, o modelo gera o evento <xref:Microsoft.Office.Tools.Word.Document.New>.|  
  
##  <a name="Limitations"></a> Limitações de modelos globais e Excel Add-ins (arquivos. xla)  
 Documentos, pastas de trabalho e modelos podem não funcionar corretamente como modelos globais ou Add-ins do VSTO do Excel (arquivos. xla).  
  
## <a name="word-templates"></a>Modelos do Word  
 Se um modelo do Microsoft Office Word tiver extensões de código gerenciado, o assembly do projeto não será chamado se o modelo for anexado como um modelo global ou carregado do diretório de inicialização do Word. Além disso, o documento não reconhece o formato de um modelo que faz parte de uma solução do Office.  
  
## <a name="excel-add-ins-xla-files"></a>Excel Add-ins (arquivos. xla)  
 Não há nenhum projeto do Office para a criação de um suplemento do VSTO do Excel (*. xla* arquivo). É possível salvar uma pasta de trabalho como um arquivo .xla, mas não é uma operação com suporte e não é recomendada. Se você salvar uma pasta de trabalho que gerencia extensões de código como um **Microsoft Office Excel Add-In (\*. xla)** arquivo, você pode selecioná-lo no **Add-Ins** caixa de diálogo para aplicar a outra pasta de trabalho. Em alguns casos, seu código será executado na pasta de trabalho de destino depois que o suplemento do VSTO é aplicado, mas não há suporte para tal uso da solução do Office.  
  
## <a name="see-also"></a>Consulte também  
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Começar a programar personalizações no nível de documento para Excel](../vsto/getting-started-programming-document-level-customizations-for-excel.md)   
 [Começar a programar personalizações no nível de documento para Word](../vsto/getting-started-programming-document-level-customizations-for-word.md)   
 [Introdução à programação VSTO Add-ins](../vsto/getting-started-programming-vsto-add-ins.md)  
  
  