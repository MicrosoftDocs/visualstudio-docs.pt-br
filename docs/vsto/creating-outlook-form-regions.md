---
title: Criar regiões de formulário do Outlook
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- MICROSOFT.OFFICE.TOOLS.OUTLOOK.FORMREGION
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio]
- form regions [Office development in Visual Studio], creating
- Outlook [Office development in Visual Studio], form regions
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d5d4aed381841d5f88209aefdcff641a2a821f01
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50673075"
---
# <a name="create-outlook-form-regions"></a>Criar regiões de formulário do Outlook
  Você pode usar regiões de formulário para personalizar formulários do Microsoft Office Outlook. Visual Studio fornece ferramentas avançadas que tornam mais fácil para você criar, desenvolver e depurar as regiões do formulário.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
 Este tópico fornece as seguintes informações:  
  
-   [Vantagens de usar regiões de formulário](#Enhance)  
  
-   [Adicionar uma região de formulário do Outlook ao seu projeto](#Adding)  
  
-   [Use o designer de região de formulário](#UsingFormRegionDesigner)  
  
-   [Use uma região de formulário projetada no Outlook](#UsingFormRegionDesignedOutlook)  
  
-   [Adicionar código personalizado a uma região de formulário](#AddingCustomCode)  
  
-   [Compile o projeto](#Building)  
  
-   [Depurar uma região de formulário](#Debugging)  
  
-   [Implantar uma região de formulário](#Deploying)  
  
##  <a name="Enhance"></a> Vantagens de usar regiões de formulário  
 Regiões de formulário oferecem muitos aprimoramentos sobre o desenvolvimento de formulários do Outlook tradicional:  
  
- Personalize a página padrão de qualquer forma padrão.  
  
- Adicione até 12 páginas extras para qualquer forma padrão.  
  
- Substituir ou aprimorar qualquer formulário padrão.  
  
- Exibir interface do usuário personalizada no painel de leitura e em inspetores.  
  
  Para obter mais informações, consulte [personalizar páginas de formulário e regiões de formulário](/office/vba/outlook/Concepts/Forms/customizing-form-pages-and-form-regions).  
  
##  <a name="Adding"></a> Adicionar uma região de formulário do Outlook ao seu projeto  
 Você pode usar o **nova região de formulário do Outlook** Assistente para criar uma nova região de formulário ou importar uma região de formulário que foi projetada no Outlook. Além disso, se você tiver uma região de formulário que você usou em outro projeto de suplemento do VSTO do Outlook, você pode reutilizar sua região de formulário existente.  
  
###  <a name="CreatingFormRegion"></a> Criar uma nova região de formulário usando o Assistente  
 Para criar uma região de formulário, adicione uma **região de formulário do Outlook** item a um projeto de suplemento do VSTO do Outlook. Isso inicia o **nova região de formulário do Outlook** assistente.  
  
 Use o Assistente para indicar se deseja criar uma nova região de formulário ou importar uma região de formulário que foi projetada no Outlook. Para obter mais informações sobre como criar uma nova região de formulário, consulte [usar o designer de região de formulário](#UsingFormRegionDesigner). Para obter mais informações sobre como usar uma região de formulário projetada no Outlook, consulte [importar de uma região de formulário projetada no Outlook](#UsingFormRegionDesignedOutlook).  
  
 Use o Assistente para especificar o tipo da região de formulário que você deseja criar. A tabela a seguir descreve cada tipo de região de formulário.  
  
|Tipo de região|Descrição|  
|-----------------|-----------------|  
|Separado|Adiciona a região do formulário como uma nova página em um formulário do Outlook.|  
|Adjacente|Anexa a região do formulário à parte inferior da página padrão de um formulário do Outlook.|  
|Substituição|Adiciona a região do formulário como uma nova página que substitui a página padrão de um formulário do Outlook.|  
|Substituir tudo|Substitui todo o formulário do Outlook pela região do formulário.|  
  
 Você também pode usar o Assistente para especificar condições de exibição e selecionar o tipo de formulário para estender. Para obter mais informações, consulte [como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md).  
  
 As seleções feitas no assistente afetam as opções que estão disponíveis em outras páginas do assistente. Por exemplo, se você selecionar **Adjoining** ou **separado** no **criar uma nova região de formulário do Outlook** página, em seguida, a **título** e **Descrição** não estão disponíveis em campos de **fornecer um texto descritivo e selecionar suas preferências de exibição** página. Isso ocorre porque o Outlook não usa esses campos quando ela for exibida uma região do formulário adjacente ou separada.  
  
#### <a name="form-region-files"></a>Arquivos de região de formulário  
 Quando você concluir o **nova região de formulário do Outlook** assistente, o Visual Studio adiciona automaticamente os arquivos a seguir ao seu projeto:  
  
-   Um arquivo de código de região de formulário. Este arquivo tem o nome que você especificar para o **região de formulário do Outlook** item o **Adicionar Novo Item** caixa de diálogo. Adicione código para manipular eventos de região de formulário para esse arquivo.  
  
-   Um arquivo de código do designer de região de formulário. Esse arquivo contém o código gerado pelo designer de região de formulário e não deve ser editado diretamente.  
  
-   Um armazenamento de formulário do Outlook (*ofs*) arquivos.  
  
    > [!NOTE]  
    >  Esse arquivo somente é adicionado ao projeto, se você importar uma região de formulário que foi projetada no Outlook.  
  
#### <a name="form-region-factory-class"></a>Classe de fábrica de região de formulário  
 O arquivo de código de região de formulário contém uma classe parcial que implementa o <xref:Microsoft.Office.Tools.Outlook.IFormRegionFactory> interface. Isso é a classe de fábrica da região de formulário. A classe de fábrica da região de formulário é responsável por criar novas instâncias da região do formulário.  
  
 Você pode encontrar essa classe, expandindo a **fábrica de região de formulário** região.  
  
 O **nova região de formulário do Outlook** assistente adiciona os atributos para essa classe que especifique o nome interno da região do formulário e as classes de mensagem que exibem a região do formulário. Você pode modificar esses atributos manualmente depois que o arquivo foi adicionado ao projeto.  
  
 A maioria da classe de fábrica de região de formulário é implementada no arquivo de designer da região de formulário. No entanto, o `FormRegionInitializing` manipulador de eventos é exposto no arquivo de código de região de formulário. Você pode usar este manipulador de eventos para especificar se o Outlook deve exibir a região do formulário. Para obter mais informações, consulte [manipular eventos de região de formulário](#HandlingFormRegionEvents).  
  
###  <a name="AddingExistingFormRegion"></a> Adicionar uma região de formulário existente ao seu projeto  
 Se você tiver uma região de formulário do Outlook que você usou em outro projeto do Outlook, você pode reutilizá-lo em seu projeto de suplemento do VSTO do Outlook atual usando o **Add Existing Item** caixa de diálogo.  
  
 A região do formulário existente deve ter um arquivo de código (*. vb* ou *. CS*); não é possível adicionar o armazenamento de formulário do Outlook (*ofs*) arquivos usando o **Add Existing Item** caixa de diálogo. No entanto, você pode criar uma nova região de formulário importando um arquivo de armazenamento de formulário do Outlook. Para obter mais informações, consulte [como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md).  
  
##  <a name="UsingFormRegionDesigner"></a> Use o designer de região de formulário  
 O designer de região de formulário ajuda você a projetar o layout e aparência de uma região de formulário. Arraste os controles gerenciados para a superfície do designer, clique duas vezes em controles para abrir os manipuladores de eventos e definir propriedades na **propriedades** janela.  
  
> [!NOTE]  
>  Você pode encontrar as propriedades que afetam a maneira como a região do formulário é exibida no Outlook sob o **manifesto** nó na **propriedades** janela.  
  
 O designer de região de formulário está disponível somente se você selecionar **criar uma nova região de formulário** na **selecione como você deseja criar a região do formulário** página da **nova região de formulário do Outlook** Assistente.  
  
 Há três maneiras de abrir o designer de região de formulário:  
  
- Na **Gerenciador de soluções**, clique duas vezes no arquivo de código de região de formulário.  
  
- Na **Gerenciador de soluções**, o arquivo de código de região de formulário com o botão direito e, em seguida, clique em **View Designer**.  
  
- Na **Gerenciador de soluções**, selecione o arquivo de código de região de formulário e, em seguida, na **exibição** menu, clique em **Designer**.  
  
  O suporta de designer de região de formulário apenas controles gerenciados. Você não pode adicionar controles nativos do Outlook.  
  
##  <a name="UsingFormRegionDesignedOutlook"></a> Importar de uma região de formulário projetada no Outlook  
 Quando você cria no Outlook, você pode adicionar controles nativos do Outlook para a região do formulário. Controles nativos do Outlook permitem que você associar a dados do Outlook no tempo de design. No entanto, você não pode usar o designer de região de formulário para adicionar controles gerenciados ou alterar o design da região do formulário.  
  
 Você pode importar as regiões do formulário para um projeto de suplemento do VSTO do Outlook usando o **nova região de formulário do Outlook** assistente. Sobre o **selecione como você deseja criar a região do formulário** , selecione **importar um arquivo de armazenamento de formulário do Outlook (. ofs)**. Você pode, em seguida, navegue até o local de um arquivo de armazenamento de formulário do Outlook (*ofs*) arquivos. (Regiões de formulário como o outlook salva *ofs* arquivos.)  
  
 O **nova região de formulário do Outlook** assistente copia as *ofs* arquivo no diretório do projeto e adiciona as referências de controle para o arquivo de designer de região de formulário. Em seguida, você pode manipular eventos de controle no arquivo de código de região de formulário.  
  
 Para manipular eventos em um projeto do Visual Basic, selecione um evento da lista de nome de método na parte superior do Editor de códigos.  
  
 Para manipular eventos em um projeto c#, assinar eventos de controle no <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> método. Para obter mais informações, consulte [como: assinar e cancelar a assinatura de eventos &#40;C&#35; guia de programação do&#41;](/dotnet/csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events).  
  
 Você pode alterar as propriedades da região de formulário no `InitializeManifest` método da classe de fábrica de região de formulário.  
  
> [!NOTE]  
>  Para importar uma região de formulário, você deve estar trabalhando em um projeto que tem como alvo a mesma versão do Outlook que você instalou no computador de desenvolvimento. Por exemplo, se você tiver o Outlook 2010 instalado, a importação de um formulário região funcionará somente em um projeto foi criado usando o **suplemento do Outlook 2010** modelo de projeto.  
  
### <a name="update-an-imported-form-regions-design"></a>Atualizar o design de uma região formulário importado  
 Você pode adicionar, remover ou alterar os controles na região do formulário. Antes de fazer isso, fazer backup de qualquer código que você adicionou ao arquivo de código de região do formulário. Em seguida, abra o *ofs* no Outlook, modifique a região do formulário e, em seguida, salve as alterações. Use o **nova região de formulário do Outlook** Assistente para importar modificado *ofs* arquivo. Em seguida, você pode colar seu código para o novo arquivo de código de região do formulário.  
  
##  <a name="AddingCustomCode"></a> Adicionar código personalizado a uma região de formulário  
 O <xref:Microsoft.Office.Tools.Outlook> namespace fornece acesso a classes que representam a região do formulário, o item do Outlook que exibe a região do formulário e outros itens úteis. O **região de formulário do Outlook** item automaticamente adiciona uma referência a esse assembly no projeto e insere apropriado **usando** ou **importações** instrução na parte superior das arquivo de código de região de formulário.  
  
 Você pode usar as classes, métodos e propriedades no `Microsoft.Office.Interop.Outlook` namespace realizem a maioria das sua tarefas de programação do Outlook. Para obter mais informações sobre o modelo de objeto do Outlook, consulte [visão geral de modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md). Para obter exemplos de tarefas típicas que usar o modelo de objeto do Outlook, consulte [soluções do Outlook](../vsto/outlook-solutions.md).  
  
###  <a name="HandlingFormRegionEvents"></a> Manipular eventos de região de formulário  
 O **região de formulário do Outlook** item adiciona automaticamente os manipuladores de eventos de três a seguir ao arquivo de código de região do formulário.  
  
|evento|Descrição|  
|-----------|-----------------|  
|FormRegionInitializing|Ocorre antes que a região do formulário seja inicializada. Você pode verificar as condições em que esse manipulador de eventos para determinar se o Outlook deve exibir a região do formulário. Para obter mais informações, consulte [como: impedir que o Outlook exiba uma região de formulário](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md).|  
|FormRegionShowing|Ocorre após uma instância da região do formulário ser criada, mas antes da região do formulário ser exibida.|  
|FormRegionClosed|Ocorre antes da região do formulário ser fechada.|  
  
##  <a name="Building"></a> Compile o projeto  
 Quando você compila um projeto de suplemento do VSTO do Outlook que contém uma região de formulário, o Visual Studio adiciona as informações a seguir no registro:  
  
- Uma chave para cada classe de mensagem que está associado uma ou mais regiões de formulário.  
  
- Uma entrada para cada região do formulário e um valor associado que representa o nome do suplemento do VSTO do Outlook.  
  
  O Outlook usa essas informações para carregar as regiões do formulário.  
  
##  <a name="Debugging"></a> Depurar uma região de formulário  
 Você pode depurar um Add-in do VSTO do Outlook que contém uma região de formulário, assim como você faria para depurar outros [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projetos. Quando você inicia o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] depurador, o Visual Studio inicia automaticamente o Outlook.  
  
 Para exibir a região do formulário, você deve abrir o item do Outlook apropriado. Por exemplo, se uma região do formulário adjacente é acrescentada à parte inferior de um item de email, abra um item de email.  
  
##  <a name="Deploying"></a> Implantar uma região de formulário  
 Regiões de formulário são implantadas automaticamente com o Add-in associado do VSTO do Outlook. Portanto, não é preciso realizar quaisquer tarefas especiais para implantar uma região de formulário. Para obter mais informações sobre a implantação do VSTO Add-ins, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Diretrizes para criar regiões de formulário do Outlook](../vsto/guidelines-for-creating-outlook-form-regions.md)|Fornece informações que podem ajudá-lo a otimizar suas regiões de formulário e evitar possíveis problemas.|  
|[Como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)|Mostra como criar uma região de formulário para estender um formulário personalizado ou padrão do Microsoft Office Outlook usando o **nova região de formulário do Outlook** assistente.|  
|[Associar uma região de formulário uma classe de mensagem do Outlook](../vsto/associating-a-form-region-with-an-outlook-message-class.md)|Explica como especificar quais itens do Microsoft Office Outlook exibem uma região de formulário por meio da associação a região do formulário com a classe message de cada item.|  
|[Passo a passo: Criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)|Mostra como criar uma região de formulário personalizada é exibida como uma nova página na janela Inspetor de um item de contato.|  
|[Passo a passo: Importar de uma região de formulário projetada no Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)|Mostra como criar uma região de formulário no Microsoft Office Outlook e, em seguida, importe a região do formulário para um projeto de suplemento do VSTO do Outlook usando o **nova região de formulário do Outlook** assistente.|  
|[Acessar uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)|Descreve como escrever código para mostrar, ocultar ou modificar controles em uma região de formulário e permitir que os usuários executar o código de outras áreas no seu projeto usando o `Globals` classe.|  
|[Como: evitar que o Outlook exiba uma região de formulário](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)|Mostra como evitar que o Microsoft Office Outlook exiba uma região de formulário para um determinado item.|  
|Mostra como acessar o item do Outlook no qual uma região de formulário é exibida.|  
|[Personalizar ações em regiões de formulário do Outlook](../vsto/custom-actions-in-outlook-form-regions.md)|Descreve como habilitar usuários responder a um item do Outlook.|  
  
