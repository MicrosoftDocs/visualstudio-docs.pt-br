---
title: 'Walkthrough: criar uma região de formulário do Outlook'
description: Saiba como você pode criar uma região de formulário personalizada do Microsoft Outlook que aparece como uma nova página na janela Inspetor de um item de contato.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 80c574799029f3fe8c4769d852886a625ffd93aa
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824270"
---
# <a name="walkthrough-design-an-outlook-form-region"></a>Walkthrough: criar uma região de formulário do Outlook
  As regiões de formulário personalizadas estendem formulários do Outlook Microsoft Office padrão ou personalizados. Neste tutorial, você criará uma região de formulário personalizada que aparece como uma nova página na janela Inspetor de um item de contato. Essa região de formulário exibe um mapa de cada endereço listado para o contato, enviando as informações de endereço para o site de pesquisa local do Windows Live. Para obter informações sobre regiões de formulário, consulte [criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md).

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Criando um novo projeto de suplemento do VSTO do Outlook.

- Adicionar uma região de formulário ao projeto de suplemento do VSTO.

- Criando o layout da região do formulário.

- Personalização do comportamento da região do formulário.

- Testando a região de formulário do Outlook.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)] ou mais recente.

  ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") Para obter uma versão de vídeo deste tópico, consulte [vídeo como criar uma região de formulário do Outlook](/previous-versions/visualstudio/visual-studio-2008/cc837160(v=vs.90)).

## <a name="create-a-new-outlook-vsto-add-in-project"></a>Criar um novo projeto de suplemento do VSTO do Outlook
 Primeiro, crie um projeto de suplemento do VSTO básico.

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>Para criar um novo projeto de suplemento do VSTO do Outlook

1. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , crie um projeto de suplemento do VSTO do Outlook com o nome **MapItAddIn**.

2. Na caixa de diálogo **novo projeto** , selecione **criar diretório para solução**.

3. Salve o projeto em qualquer diretório.

     Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

## <a name="add-a-form-region-to-the-outlook-vsto-add-in-project"></a>Adicionar uma região de formulário ao projeto de suplemento do VSTO do Outlook
 Uma solução de suplemento do VSTO do Outlook pode conter um ou mais itens da região do formulário do Outlook. Adicione um item de região de formulário ao seu projeto usando o assistente de **nova região de formulário do Outlook** .

### <a name="to-add-a-form-region-to-the-outlook-vsto-add-in-project"></a>Para adicionar uma região de formulário ao projeto de suplemento do VSTO do Outlook

1. Em **Gerenciador de soluções**, selecione o projeto **MapItAddIn** .

2. No menu **Projeto** , clique em **Adicionar Novo Item**.

3. Na caixa de diálogo **Adicionar novo item** , selecione **região de formulário do Outlook**, nomeie o arquivo como **MapIt** e clique em **Adicionar**.

     O assistente de **região de formulário NewOutlook** é iniciado.

4. Na página **Selecione como você deseja criar a região de formulário** , clique em **criar uma nova região de formulário** e em **Avançar**.

5. Na página **Selecione o tipo de região de formulário que você deseja criar** , clique em **separado** e, em seguida, clique em **Avançar**.

     Uma região de formulário *separada* adiciona uma nova página a um formulário do Outlook. Para obter mais informações sobre tipos de região de formulário, consulte [criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md).

6. No **texto descritivo do fornecimento e selecione a página preferências de exibição** , digite **mapeá-lo** na caixa **nome** .

     Esse nome aparece na faixa de da janela do Inspetor quando o item de contato está aberto.

7. Selecione os **inspetores que estão no modo de redação** e **nos inspetores que estão no modo de leitura** e clique em **Avançar**.

8. Na página **identificar as classes de mensagem que exibirão esta região de formulário** , desmarque a **mensagem de email**, selecione **contato** e clique em **concluir**.

     Um arquivo *MapIt. cs* ou *MapIt. vb* é adicionado ao seu projeto.

## <a name="design-the-layout-of-the-form-region"></a>Criar o layout da região do formulário
 Desenvolva regiões de formulário visualmente usando o *Designer de região de formulário*. Você pode arrastar controles gerenciados para a superfície do designer de região de formulário. Use o designer e a janela **Propriedades** para ajustar o layout e a aparência do controle.

### <a name="to-design-the-layout-of-the-form-region"></a>Para criar o layout da região do formulário

1. Em **Gerenciador de soluções**, expanda o projeto **MapItAddIn** e clique duas vezes em *MapIt. cs* ou *MapIt. vb* para abrir o designer de região do formulário.

2. Clique com o botão direito do mouse no designer e clique em **Propriedades**.

3. Na janela **Propriedades** , defina **tamanho** como **664, 469**.

     Isso garante que a região do formulário será grande o suficiente para exibir um mapa.

4. No menu **Exibir** , clique em **Caixa de Ferramentas**.

5. Na guia **controles comuns** da caixa de **ferramentas**, adicione um **WebBrowser** à região do formulário.

     O **WebBrowser** exibirá um mapa de cada endereço listado para o contato.

## <a name="customize-the-behavior-of-the-form-region"></a>Personalizar o comportamento da região de formulário
 Adicione código aos manipuladores de eventos da região de formulário para personalizar a forma com que uma região de formulário se comporta em tempo de execução. Para essa região de formulário, o código examina as propriedades de um item do Outlook e determina se a região do formulário de mapa de ti deve ser exibida. Se ele exibir a região do formulário, o código navegará para a pesquisa local do Windows Live e carregará um mapa de cada endereço listado no item de contato do Outlook.

### <a name="to-customize-the-behavior-of-the-form-region"></a>Para personalizar o comportamento da região do formulário

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em *MapIt. cs* ou *MapIt. vb* e clique em **Exibir código**.

    *MapIt. cs* ou *MapIt. vb* é aberto no editor de código.

2. Expanda o formulário região de código de **fábrica** .

    A classe de fábrica de região de formulário chamada `MapItFactory` é exposta.

3. Adicione o seguinte código ao manipulador de eventos do `MapItFactory_FormRegionInitializing`. Esse manipulador de eventos é chamado quando o usuário abre um item de contato. O código a seguir determina se o item de contato contém um endereço. Se o item de contato não contiver um endereço, esse código definirá a <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> propriedade da <xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs> classe como **true** e a região do formulário não será exibida. Caso contrário, o suplemento do VSTO gerará o <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> evento e exibirá a região do formulário.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb" id="Snippet1":::

4. Adicione o seguinte código ao manipulador de eventos do <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing>. Esse código executa as seguintes tarefas:

   - Concatena cada endereço no item de contato e cria uma cadeia de caracteres de URL.

   - Chama o <xref:System.Windows.Forms.WebBrowser.Navigate%2A> método do <xref:System.Windows.Forms.WebBrowser> objeto e passa a cadeia de caracteres da URL como um parâmetro.

     O site de pesquisa local aparece na região do formulário de mapa e apresenta cada endereço no bloco de rascunho.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb" id="Snippet2":::

## <a name="test-the-outlook-form-region"></a>Testar a região de formulário do Outlook
 Quando você executa o projeto, o Visual Studio abre o Outlook. Abra um item de contato para exibir a região do formulário de mapa. A região do formulário de mapa é exibida como uma página na forma de qualquer item de contato que contenha um endereço.

### <a name="to-test-the-map-it-form-region"></a>Para testar a região do formulário de mapa de ti

1. Pressione **F5** para executar o projeto.

     O Outlook é aberto.

2. No Outlook, na guia **início** , clique em **novos itens** e, em seguida, em **contato**.

3. No formulário de contato, digite **Ana Beebe** como o nome do contato e, em seguida, especifique os três endereços a seguir.

    |Tipo de endereço|Endereço|
    |------------------|-------------|
    |**Negócios**|**4567 principal St. Buffalo, NY**|
    |**Início**|**1234 norte St. Buffalo, NY**|
    |**Outras**|**3456 principal St. Seattle, WA**|

4. Salve e feche o item de contato.

5. Reabra o item de contato **Ana Beebe** .

    No Outlook, isso pode ser feito no grupo **Localizar** abrindo o catálogo de endereços para contatos ou digitando Ana Beebe em **Pesquisar pessoas**.

6. No grupo **Mostrar** da faixa de mapa do item, clique em **mapeá-lo** para abrir a região de formulário mapear ti.

     A região do formulário de mapa é exibida e exibe o site de pesquisa local. Os endereços **comercial**, **residencial** e **outros** são exibidos no bloco de rascunho. No bloco de rascunho, selecione um endereço que você deseja mapear.

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como personalizar a interface do usuário de um aplicativo do Outlook a partir destes tópicos:

- Para saber mais sobre como personalizar a faixa de visualização de um item do Outlook, confira [personalizar uma faixa de visualização para o Outlook](../vsto/customizing-a-ribbon-for-outlook.md).

## <a name="see-also"></a>Consulte também
- [Acessar uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)
- [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)
- [Diretrizes para criar regiões de formulário do Outlook](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [Walkthrough: importar uma região de formulário projetada no Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
- [Como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [Associar uma região de formulário a uma classe de mensagem do Outlook](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
- [Ações personalizadas nas regiões de formulário do Outlook](../vsto/custom-actions-in-outlook-form-regions.md)
- [Como: impedir que o Outlook exiba uma região de formulário](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)
