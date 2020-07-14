---
title: 'Walkthrough: criando uma Web Part para SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], developing
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7d8b5e05fb234e9997bce615f7b2de1d790c1ae0
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014581"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint"></a>Walkthrough: criar uma Web Part para o SharePoint

Web Parts permitir que os usuários modifiquem diretamente o conteúdo, a aparência e o comportamento das páginas do site do SharePoint usando um navegador. Este tutorial mostra como criar uma Web Part usando o modelo de item de **Web Part** no Visual Studio 2010.

A Web Part exibe os funcionários em uma grade de dados. O usuário especifica o local do arquivo que contém os dados do funcionário. O usuário também pode filtrar a grade de dados para que os funcionários que são gerentes apareçam somente na lista.

Este passo a passo ilustra as seguintes tarefas:

- Criar uma Web Part usando o modelo de item de **Web Part** do Visual Studio.

- Criar uma propriedade que pode ser definida pelo usuário da Web Part. Esta propriedade especifica o local do arquivo de dados do funcionário.

- Renderização de conteúdo em uma Web Part adicionando controles à coleção de controles de Web Part.

- Criar um novo item de menu, conhecido como um *verbo,* que aparece no menu de verbos da Web Part renderizada. Os verbos permitem que o usuário modifique os dados que aparecem na Web Part.

- Testando a Web Part no SharePoint.

    > [!NOTE]
    > Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos

- Edições com suporte do Microsoft Windows e do SharePoint.

- Visual Studio 2017 ou Azure DevOps Services.

## <a name="create-an-empty-sharepoint-project"></a>Criar um projeto do SharePoint vazio

Primeiro, crie um projeto do SharePoint vazio. Posteriormente, você adicionará uma Web Part ao projeto usando o modelo de item de **Web Part** .

1. Comece [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] usando a opção **Executar como administrador** .

2. Na barra de homens, escolha **arquivo**  >  **novo**  >  **projeto**.

3. Na caixa de diálogo **novo projeto** , expanda o nó do **SharePoint** sob o idioma que você deseja usar e escolha o nó **2010** .

4. No painel **modelos** , escolha **projeto do SharePoint 2010**e, em seguida, escolha o botão **OK** .

     O **Assistente para personalização do SharePoint** é exibido. Este assistente permite que você selecione o site que será usado para depurar o projeto e o nível de confiança da solução.

5. Escolha o botão de opção **implantar como uma solução de farm** e, em seguida, escolha o botão **concluir** para aceitar o site do SharePoint local padrão.

## <a name="add-a-web-part-to-the-project"></a>Adicionar uma Web Part ao projeto

Adicione um item de **Web Part** ao projeto. O item de **Web Part** adiciona o arquivo de código de Web Part. Posteriormente, você adicionará código ao arquivo de código da Web Part para renderizar o conteúdo da Web Part.

1. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

2. Na caixa de diálogo **Adicionar novo item** , no painel **modelos instalados** , expanda o nó **SharePoint** e escolha o nó **2010** .

3. Na lista de modelos do SharePoint, escolha o modelo de **Web Part** e, em seguida, escolha o botão **Adicionar** .

     O item de **Web Part** aparece em **Gerenciador de soluções**.

## <a name="rendering-content-in-the-web-part"></a>Renderizando conteúdo na Web Part

Você pode especificar quais controles você deseja que apareçam na Web Part adicionando-os à coleção Controls da classe Web Part.

1. No **Gerenciador de soluções**, abra *WebPart1. vb* (em Visual Basic) ou *WebPart1.cs* (em C#).

     O arquivo de código da Web Part é aberto no editor de código.

2. Adicione as seguintes diretivas à parte superior do arquivo de código da Web Part.

     [!code-csharp[SP_WebPart#1](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#1)]
     [!code-vb[SP_WebPart#1](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#1)]

3. Adicione o código a seguir à classe `WebPart1` . Esse código declara os seguintes campos:

   - Uma grade de dados para exibir os funcionários na Web Part.

   - Texto que aparece no controle que é usado para filtrar a grade de dados.

   - Um rótulo que exibe um erro se a grade de dados não puder exibir dados.

   - Uma cadeia de caracteres que contém o caminho do arquivo de dados do funcionário.

     [!code-csharp[SP_WebPart#2](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#2)]
     [!code-vb[SP_WebPart#2](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#2)]

4. Adicione o código a seguir à classe `WebPart1` . Esse código adiciona uma propriedade personalizada chamada `DataFilePath` à Web Part. Uma propriedade personalizada é uma propriedade que pode ser definida no SharePoint pelo usuário. Essa propriedade obtém e define o local de um arquivo de dados XML que é usado para preencher a grade de dados.

     [!code-csharp[SP_WebPart#3](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#3)]
     [!code-vb[SP_WebPart#3](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#3)]

5. Substitua o método `CreateChildControls` pelo seguinte código. Esse código executa as seguintes tarefas:

   - Adiciona a grade de dados e o rótulo que você declarou na etapa anterior.

   - Associa a grade de dados a um arquivo XML que contém dados de funcionários.

     [!code-csharp[SP_WebPart#4](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#4)]
     [!code-vb[SP_WebPart#4](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#4)]

6. Adicione o método a seguir à classe `WebPart1`. Esse código executa as seguintes tarefas:

   - Cria um verbo que aparece no menu de verbos da Web Part da Web Part renderizada.

   - Manipula o evento que é gerado quando o usuário escolhe o verbo no menu de verbos. Esse código filtra a lista de funcionários que aparece na grade de dados.

     [!code-csharp[SP_WebPart#5](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#5)]
     [!code-vb[SP_WebPart#5](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#5)]

## <a name="test-the-web-part"></a>Testar a Web Part

Quando você executa o projeto, o site do SharePoint é aberto. A Web Part é adicionada automaticamente à galeria de Web Parts no SharePoint. Você pode adicionar a Web Part a qualquer página de Web Part.

1. Cole o XML a seguir em um arquivo do bloco de notas. Esse arquivo XML contém os dados de exemplo que aparecerão na Web Part.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
        <employees xmlns="http://schemas.microsoft.com/vsto/samples">
           <employee>
               <name>David Hamilton</name>
               <hireDate>2001-05-11</hireDate>
               <title>Sales Associate</title>
           </employee>
           <employee>
               <name>Karina Leal</name>
               <hireDate>1999-04-01</hireDate>
               <title>Manager</title>
           </employee>
           <employee>
               <name>Nancy Davolio</name>
               <hireDate>1992-05-01</hireDate>
               <title>Sales Associate</title>
           </employee>
           <employee>
               <name>Steven Buchanan</name>
               <hireDate>1955-03-04</hireDate>
               <title>Manager</title>
           </employee>
           <employee>
               <name>Suyama Michael</name>
               <hireDate>1963-07-02</hireDate>
               <title>Sales Associate</title>
           </employee>
        </employees>
    ```

2. No bloco de notas, na barra de menus, escolha **arquivo**  >  **salvar como**.

3. Na caixa de diálogo **salvar como** , na lista **salvar como tipo** , escolha **todos os arquivos**.

4. Na caixa **nome do arquivo** , digite **data.xml**.

5. Escolha qualquer pasta usando o botão **procurar pastas** e, em seguida, escolha o botão **salvar** .

6. No Visual Studio, escolha a tecla **F5** .

     O site do SharePoint é aberto.

7. No menu **ações do site** , escolha **mais opções**.

8. Na página **criar** , escolha o tipo de **página de Web Part** e, em seguida, escolha o botão **criar** .

9. Na página **nova página de Web Parts** , nomeie a página **SampleWebPartPage. aspx**e, em seguida, escolha o botão **criar** .

     A página Web Part é exibida.

10. Selecione qualquer zona na página de Web Parts.

11. Na parte superior da página, escolha a guia **Inserir** e, em seguida, escolha o botão **Web Part** .

12. No painel **categorias** , escolha a pasta **personalizada** , escolha a Web Part **WebPart1** e, em seguida, escolha o botão **Adicionar** .

     A Web Part aparece na página.

## <a name="test-the-custom-property"></a>Testar a propriedade personalizada

Para preencher a grade de dados que aparece na Web Part, especifique o caminho do arquivo XML que contém dados sobre cada funcionário.

1. Escolha a seta que aparece no lado direito da Web Part e escolha **Editar Web Part** no menu que aparece.

     Um painel que contém propriedades para a Web Part aparece no lado direito da página.

2. No painel, expanda o nó **diversos** , insira o caminho do arquivo XML que você criou anteriormente, escolha o botão **aplicar** e, em seguida, escolha o botão **OK** .

     Verifique se uma lista de funcionários aparece na Web Part.

## <a name="test-the-web-part-verb"></a>Testar o verbo da Web Part

Mostre e oculte os funcionários que não são gerentes clicando em um item que aparece no menu de verbos da Web Part.

1. Escolha a seta que aparece no lado direito da Web Part e, em seguida, escolha **Mostrar gerentes somente** no menu que aparece.

     Somente os funcionários que são gerentes aparecem na Web Part.

2. Escolha a seta novamente e, em seguida, escolha **Mostrar todos os funcionários** no menu exibido.

     Todos os funcionários aparecem na Web Part.

## <a name="see-also"></a>Consulte também

[Criar Web Parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md) 
 [Como: criar uma Web Part](../sharepoint/how-to-create-a-sharepoint-web-part.md) 
 do SharePoint [Como: criar uma Web Part do SharePoint usando um designer](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) 
 [Walkthrough: criar uma Web Part para o SharePoint usando um designer](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
