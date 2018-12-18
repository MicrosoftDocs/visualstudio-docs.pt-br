---
title: 'Passo a passo: Criar uma região de formulário do Outlook'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], creating
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 693261bb6894681b613ad0db2f0b3c116109a782
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49813681"
---
# <a name="walkthrough-design-an-outlook-form-region"></a>Passo a passo: Criar uma região de formulário do Outlook
  Regiões de formulário personalizadas estendem formulários do Microsoft Office Outlook padrão ou personalizados. Neste passo a passo, você criará uma região de formulário personalizada é exibida como uma nova página na janela Inspetor de um item de contato. Esta região do formulário exibe um mapa de cada endereço listado para o contato, enviando as informações de endereço para o Windows Live Search site Local. Para obter informações sobre regiões de formulário, consulte [regiões de formulário do Outlook criar](../vsto/creating-outlook-form-regions.md).  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Criar um novo projeto de suplemento do VSTO do Outlook.  
  
-   Adicionando uma região de formulário ao projeto de suplemento do VSTO.  
  
-   Projetar o layout da região do formulário.  
  
-   Personalizando o comportamento da região do formulário.  
  
-   Testando a região de formulário do Outlook.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
- [!INCLUDE[Outlook_15_short](../vsto/includes/outlook-15-short-md.md)] ou [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)].  
  
  ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma versão em vídeo deste tópico, consulte [vídeo como: criar uma região de formulário do Outlook](http://go.microsoft.com/fwlink/?LinkID=140824).  
  
## <a name="create-a-new-outlook-vsto-add-in-project"></a>Criar um novo projeto de suplemento do VSTO do Outlook  
 Primeiro, crie um projeto de suplemento do VSTO básico.  
  
### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>Para criar um novo projeto de suplemento do VSTO do Outlook  
  
1.  Na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], crie um projeto de suplemento do VSTO do Outlook com o nome **MapItAddIn**.  
  
2.  No **novo projeto** caixa de diálogo, selecione **criar diretório para solução**.  
  
3.  Salve o projeto para qualquer diretório.  
  
     Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
## <a name="add-a-form-region-to-the-outlook-vsto-add-in-project"></a>Adicionar uma região de formulário ao projeto de suplemento do VSTO do Outlook  
 Uma solução de suplemento do VSTO do Outlook pode conter um ou mais itens de região de formulário do Outlook. Adicionar um item de região de formulário ao seu projeto usando o **nova região de formulário do Outlook** assistente.  
  
### <a name="to-add-a-form-region-to-the-outlook-vsto-add-in-project"></a>Para adicionar uma região de formulário ao projeto de suplemento do VSTO do Outlook  
  
1.  Na **Gerenciador de soluções**, selecione o **MapItAddIn** projeto.  
  
2.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
3.  No **Adicionar Novo Item** caixa de diálogo, selecione **região de formulário do Outlook**, nomeie o arquivo **MapIt**e, em seguida, clique em **adicionar**.  
  
     O **região do formulário NewOutlook** assistente é iniciado.  
  
4.  Sobre o **selecione como você deseja criar a região do formulário** , clique em **projetar uma nova região de formulário**e, em seguida, clique em **próxima**.  
  
5.  No **selecione o tipo da região de formulário que você deseja criar** , clique em **separado**e, em seguida, clique em **próxima**.  
  
     Um *separado* região do formulário adiciona uma nova página a um formulário do Outlook. Para obter mais informações sobre os tipos de região de formulário, consulte [regiões de formulário do Outlook criar](../vsto/creating-outlook-form-regions.md).  
  
6.  No **fornecer um texto descritivo e selecionar suas preferências de exibição** página, digite **mapa ele** no **nome** caixa.  
  
     Esse nome aparece na faixa de opções da janela do Inspetor quando o item de contato é aberto.  
  
7.  Selecione **inspetores que estão no modo de redação** e **inspetores que estão no modo de leitura**e, em seguida, clique em **próxima**.  
  
8.  Sobre o **identificar as classes de mensagem que exibirão esta região do formulário** página, desmarque **mensagem de email**, selecione **entre em contato com**e, em seguida, clique em **concluir**.  
  
     Um *MapIt.cs* ou *MapIt.vb* arquivo é adicionado ao seu projeto.  
  
## <a name="design-the-layout-of-the-form-region"></a>Criar o layout da região do formulário  
 Desenvolver as regiões do formulário visualmente, usando o *designer de região de formulário*. Você pode arrastar controles gerenciados para a superfície de designer de região de formulário. Use o designer e o **propriedades** janela para ajustar a aparência e layout do controle.  
  
### <a name="to-design-the-layout-of-the-form-region"></a>Para criar o layout da região do formulário  
  
1.  Na **Gerenciador de soluções**, expanda o **MapItAddIn** do projeto e, em seguida, clique duas vezes em *MapIt.cs* ou *MapIt.vb* para abrir a região do formulário Designer.  
  
2.  O designer com o botão direito e, em seguida, clique em **propriedades**.  
  
3.  No **propriedades** janela, defina **tamanho** para **664, 469**.  
  
     Isso garante que a região do formulário será grande o suficiente para exibir um mapa.  
  
4.  Sobre o **modo de exibição** menu, clique em **caixa de ferramentas**.  
  
5.  Do **controles comuns** guia da **caixa de ferramentas**, adicione um **WebBrowser** à região do formulário.  
  
     O **WebBrowser** exibirá um mapa de cada endereço listado para o contato.  
  
## <a name="customize-the-behavior-of-the-form-region"></a>Personalizar o comportamento da região do formulário  
 Adicione código para manipuladores de eventos de região de formulário para personalizar a forma de uma região de formulário se comporta no tempo de execução. Para esta região do formulário, o código examina as propriedades de um item do Outlook e determina se é exibir a região de formulário do mapa-lo. Se ele exibe a região do formulário, o código navega para o Windows Live Search Local e carrega um mapa de cada endereço listado no item de contato do Outlook.  
  
### <a name="to-customize-the-behavior-of-the-form-region"></a>Para personalizar o comportamento da região do formulário  
  
1. Na **Gerenciador de soluções**, clique com botão direito *MapIt.cs* ou *MapIt.vb*e, em seguida, clique em **Exibir código**.  
  
    *MapIt.cs* ou *MapIt.vb* é aberto no Editor de códigos.  
  
2. Expanda o **fábrica de região de formulário** região de código.  
  
    A classe de fábrica da região de formulário chamado `MapItFactory` é exposto.  
  
3. Adicione o seguinte código ao manipulador de eventos do `MapItFactory_FormRegionInitializing`. Esse manipulador de eventos é chamado quando o usuário abre um item de contato. O código a seguir determina se o item de contato contém um endereço. Se o item de contato não contiver um endereço, esse código define a <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> propriedade do <xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs> classe para **verdadeiro** e a região do formulário não será exibida. Caso contrário, o suplemento do VSTO gerará o <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> eventos e exibe a região do formulário.  
  
    [!code-csharp[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#1)]
    [!code-vb[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#1)]  
  
4. Adicione o seguinte código ao manipulador de eventos do <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing>. Esse código executa as seguintes tarefas:  
  
   - Concatena cada endereço no item de contato e cria uma cadeia de caracteres de URL.  
  
   - Chamadas a <xref:System.Windows.Forms.WebBrowser.Navigate%2A> método da <xref:System.Windows.Forms.WebBrowser> do objeto e passa a cadeia de caracteres de URL como um parâmetro.  
  
     O site da Web Local de pesquisa é exibida na região de formulário de mapa-lo e apresenta cada endereço do bloco de rascunho.  
  
     [!code-csharp[Trin_Outlook_FR_Separate#2](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#2)]
     [!code-vb[Trin_Outlook_FR_Separate#2](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#2)]  
  
## <a name="test-the-outlook-form-region"></a>Testar a região de formulário do Outlook  
 Quando você executa o projeto, o Visual Studio abre o Outlook. Abra um item de contato para exibir a região de formulário do mapa-lo. A região de formulário do mapa ele aparece como uma página na forma de qualquer item de contato que contém um endereço.  
  
### <a name="to-test-the-map-it-form-region"></a>Para testar a região de formulário do mapa-lo  
  
1.  Pressione **F5** para executar o projeto.  
  
     O Outlook abrirá.  
  
2.  No Outlook, sobre o **página inicial** , clique em **novos itens**e, em seguida, clique em **entre em contato com**.  
  
3.  No formulário de contato, digite **Ann Beebe** como contato nomear e, em seguida, especifique os seguintes endereços de três.  
  
    |Tipo de endereço|Endereço|  
    |------------------|-------------|  
    |**Negócios**|**4567 de Main St. Buffalo, NY**|  
    |**Início**|**1234 do Norte St. Buffalo, NY**|  
    |**Outros**|**3456 Main St. Seattle, WA**|  
  
4.  Salve e feche o item de contato.  
  
5.  Reabra o **Ann Beebe** item de contato.  
  
6.  No **mostram** grupo da faixa de opções do item, clique em **mapa ele** para abrir a região de formulário do mapa-lo.  
  
     A região de formulário do mapa ela aparece e exibe o site de pesquisa Local. O **comerciais**, **Home**, e **outros** endereços aparecem no bloco de rascunho. No bloco de rascunho, selecione um endereço que você deseja mapear.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre como personalizar a interface do usuário de um aplicativo do Outlook com estes tópicos:  
  
-   Para saber mais sobre como personalizar a faixa de opções de um item do Outlook, consulte [personalizar uma faixa de opções para Outlook](../vsto/customizing-a-ribbon-for-outlook.md).  
  
## <a name="see-also"></a>Consulte também  
 [Acessar uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)   
 [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)   
 [Diretrizes para criar regiões de formulário do Outlook](../vsto/guidelines-for-creating-outlook-form-regions.md)   
 [Passo a passo: Importar de uma região de formulário projetada no Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)   
 [Como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)   
 [Associar uma região de formulário uma classe de mensagem do Outlook](../vsto/associating-a-form-region-with-an-outlook-message-class.md)   
 [Personalizar ações em regiões de formulário do Outlook](../vsto/custom-actions-in-outlook-form-regions.md)   
 [Como: evitar que o Outlook exiba uma região de formulário](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)  
  
  