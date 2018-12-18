---
title: 'Passo a passo: Criando uma Web Part para o SharePoint usando um Designer | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], designer
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 1b5cfd9afaf0c37dcf267c63641b7917efe4c249
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49831803"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint-by-using-a-designer"></a>Passo a passo: Criar uma web part para SharePoint usando um designer

Se você criar web parts para um site do SharePoint, os usuários podem modificar diretamente o conteúdo, aparência e comportamento de páginas do site usando um navegador. Este passo a passo mostra como criar uma web part visualmente usando o SharePoint **Web Part Visual** modelo de projeto no Visual Studio.

A web part que você criará exibe uma exibição de calendário mensal e uma caixa de seleção para cada lista de calendários no site. Os usuários podem especificar quais listas de calendário para incluir na exibição de calendário mensal marcando as caixas de seleção.

Esta explicação passo a passo ilustra as seguintes tarefas:

- Criando uma web part usando o **Web Part Visual** modelo de projeto.
- Criando a web part usando o designer do Visual Web Developer no Visual Studio.
- Adicionar código para manipular os eventos de controles na web part.
- Testando a web part no SharePoint.

    > [!NOTE]
    > Seu computador pode mostrar diferentes nomes ou localizações para alguns elementos da interface do usuário para o Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos

Você precisa dos seguintes componentes para concluir esta instrução passo a passo:

- Edições com suporte do Windows e do SharePoint.

## <a name="create-a-web-part-project"></a>Criar um projeto de web part

Primeiro, crie um projeto de web part usando o **Web Part Visual** modelo de projeto.

1. Inicie [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] usando o **executar como administrador** opção.

2. Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.

     A caixa de diálogo **Novo Projeto** é exibida.

3. No **novo projeto** caixa de diálogo, em qualquer um **Visual c#** ou **Visual Basic**, expanda **Office/SharePoint**e, em seguida, escolha o  **Soluções do SharePoint** categoria.

4. Na lista de modelos, escolha o **SharePoint 2013 - Web Part Visual** modelo e, em seguida, escolha o **Okey** botão.

     O **Assistente para personalização do SharePoint** é exibida. Usando esse assistente, você pode especificar o site que você usará para depurar o projeto e o nível de confiança da solução.

5. No **qual é o nível de confiança para essa solução do SharePoint?** , escolha o **implantar como uma solução de farm** botão de opção.

6. Escolha o **concluir** botão para aceitar o site do SharePoint local padrão.

## <a name="designing-the-web-part"></a>Criando a web part

Crie a web part adicionando controles a partir de **caixa de ferramentas** para a superfície do designer Visual Web Developer.

1. No designer Visual Web Developer, escolha o **Design** tab para alternar para modo de exibição de Design.

2. Na barra de menus, escolha **modo de exibição** > **caixa de ferramentas**.

3. No **Standard** nó do **caixa de ferramentas**, escolha o **CheckBoxList** controlar e, em seguida, execute uma das seguintes etapas:

    - Abra o menu de atalho para o **CheckBoxList** de controle, escolha **cópia**, abra o menu de atalho para a primeira linha no designer e, em seguida, escolha **colar**.

    - Arraste o **CheckBoxList** controlar da **caixa de ferramentas**e conecte-se o controle para a primeira linha no designer.

4. Repita a etapa anterior, mas mover um botão para a próxima linha do designer.

5. No designer, escolha o **Button1** botão.

6. Na barra de menus, escolha **modo de exibição** > **janela propriedades**.

     O **propriedades** janela é aberta.

7. No **texto** propriedade do botão, digite **atualização**.

## <a name="handling-the-events-of-controls-on-the-web-part"></a>Manipulando os eventos de controles na web part

Adicione o código que permite que o usuário adicione calendários ao modo de exibição de calendário mestre.

1. Realize um dos seguintes conjuntos de etapas:

   - No designer, clique duas vezes o **atualização** botão.

   - No **propriedades** janela para o **atualização** botão, escolher o **eventos** botão. No **clique em** propriedade, digite **Button1_Click**e, em seguida, escolha a tecla Enter.

     O arquivo de código de controle de usuário é aberto no Editor de código e o `Button1_Click` manipulador de eventos é exibida. Posteriormente, você adicionará código para este manipulador de eventos.

2. Adicione as seguintes instruções na parte superior do arquivo de código de controle de usuário.

     [!code-vb[SP_VisualWebPart#1](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#1)]
     [!code-csharp[SP_VisualWebPart#1](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#1)]

3. Adicione a seguinte linha de código para o `VisualWebPart1` classe. Esse código declara um controle de exibição de calendário mensal.

     [!code-vb[SP_VisualWebPart#2](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#2)]
     [!code-csharp[SP_VisualWebPart#2](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#2)]

4. Substitua os `Page_Load` método da `VisualWebPart1` classe pelo código a seguir. Esse código executa as seguintes tarefas:

   - Adiciona um modo de exibição de calendário mensal ao controle de usuário.

   - Adiciona uma caixa de seleção para cada lista de calendários no site.

   - Especifica um modelo para cada tipo de item que aparece na exibição de calendário.

     [!code-vb[SP_VisualWebPart#3](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#3)]
     [!code-csharp[SP_VisualWebPart#3](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#3)]

5. Substitua os `Button1_Click` método da `VisualWebPart1` classe pelo código a seguir. Esse código adiciona itens de cada calendário selecionado para o modo de exibição de calendário mestre.

     [!code-vb[SP_VisualWebPart#4](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#4)]
     [!code-csharp[SP_VisualWebPart#4](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#4)]

## <a name="test-the-web-part"></a>Testar a web part

Quando você executa o projeto, abre o site do SharePoint. A web part é automaticamente adicionada à Galeria de Web Parts no SharePoint. Para testar este projeto, você executará as seguintes tarefas:

- Adicione um evento a cada uma das duas listas de calendário separado.
- Adicione a web part a uma página de web Parts.
- Especifique as listas a serem incluídas na exibição de calendário mensal.

### <a name="to-add-events-to-calendar-lists-on-the-site"></a>Para adicionar eventos a listas de calendário no site

1. No Visual Studio, escolha o **F5** chave.

     Abre o site do SharePoint e o [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] barra de início rápido é exibido na página.

2. Na barra de início rápido, sob **listas**, escolha o **calendário** link.

     O **calendário** página será exibida.

     Se você nenhum link calendário seja exibido na barra de início rápido, escolha o **conteúdo do Site** link. Se a página de conteúdo do Site não mostra um **calendário** item, crie um.

3. Na página do calendário, escolha um dia e, em seguida, escolha o **adicionar** link no dia selecionado para adicionar um evento.

4. No **Title** , digite **evento no calendário padrão**e, em seguida, escolha o **salvar** botão.

5. Escolha o **conteúdo do Site** vincular e, em seguida, escolha o **adicionar um aplicativo** lado a lado.

6. No **Create** , escolha o **calendário** digite, nomeie o calendário e, em seguida, escolha o **criar** botão.

7. Adicionar um evento para o novo calendário, nomeie o evento **evento no calendário personalizado**e, em seguida, escolha o **salvar** botão.

### <a name="to-add-the-web-part-to-a-web-part-page"></a>Para adicionar a web part a uma página de web part

1. Sobre o **conteúdo do Site** página, abra o **páginas do Site** pasta.

2. Na faixa de opções, escolha o **arquivos** guia, abra o **novo documento** menu e, em seguida, escolha o **página de Web Parts** comando.

3. Sobre o **nova página de Web Parts** página, nomeie a página **Samplewebpartpage**e, em seguida, escolha o **criar** botão.

     Página de web Parts é exibida.

4. Na zona superior da página de web parts, escolha o **inserir** guia e, em seguida, escolha o **Web Part** botão.

5. Escolha o **personalizado** pasta, escolha o **VisualWebPart1** da web part e, em seguida, escolha o **Add** botão.

     A web part aparece na página. Os seguintes controles aparecem na parte da web:

    - Um modo de exibição de calendário mensal.

    - Uma **atualização** botão.

    - Um **calendário** caixa de seleção.

    - Um **calendário personalizado** caixa de seleção.

### <a name="to-specify-lists-to-include-in-the-monthly-calendar-view"></a>Para especificar as listas para incluir na exibição de calendário mensal

Na web part, especifique os calendários que você deseja incluir na exibição mensal de calendário e, em seguida, escolha o **atualização** botão.

Os eventos de todos os calendários que você especificou aparecem na exibição de calendário mensal.

## <a name="see-also"></a>Consulte também

[Criar web parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)  
[Como: criar uma web part do SharePoint](../sharepoint/how-to-create-a-sharepoint-web-part.md)  
[Passo a passo: Criar uma web part do SharePoint](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
