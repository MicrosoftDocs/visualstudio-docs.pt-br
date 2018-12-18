---
title: 'Passo a passo: Criando uma Web Part para SharePoint | Microsoft Docs'
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
- Web Parts [SharePoint development in Visual Studio], developing
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 09b9299c6428ef63ccf71220fc3cb599e9e3b5a9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49872402"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint"></a>Passo a passo: Criar uma web part do SharePoint

Web Parts permitem aos usuários modificar diretamente o conteúdo, aparência e comportamento das páginas do site do SharePoint usando um navegador. Este passo a passo mostra como criar uma Web Part usando o **Web Part** modelo de item no Visual Studio 2010.

A Web Part exibe os funcionários em uma grade de dados. O usuário Especifica o local do arquivo que contém os dados de funcionários. O usuário também pode filtrar a grade de dados para que os funcionários que são gerentes aparecem na lista somente.

Esta explicação passo a passo ilustra as seguintes tarefas:

- Criando uma Web Part usando o Visual Studio **Web Part** modelo de item.

- Criação de uma propriedade que pode ser definido pelo usuário da Web Part. Essa propriedade especifica o local do arquivo de dados de funcionário.

- Renderizar o conteúdo em uma Web Part adicionando controles para a Web Part controla a coleção.

- Criando um novo item de menu, conhecido como um *verbo,* que aparece no menu de verbos de Web part de renderizado. Verbos permitem ao usuário modificar os dados que aparece na Web Part.

- Testando a Web Part no SharePoint.

    > [!NOTE]
    > Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos

- Edições com suporte do Microsoft Windows e do SharePoint.

- Visual Studio 2017 ou serviços de DevOps do Azure.

## <a name="create-an-empty-sharepoint-project"></a>Criar um projeto vazio do SharePoint

Primeiro, crie um projeto do SharePoint vazio. Posteriormente, você irá adicionar uma Web Part ao projeto usando o **Web Part** modelo de item.

1. Inicie [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] usando o **executar como administrador** opção.

2. Na barra de homens, escolha **arquivo** > **New** > **projeto**.

3. No **novo projeto** diálogo caixa, expanda o **SharePoint** nó sob o idioma que você deseja usar e, em seguida, escolha o **2010** nó.

4. No **modelos** painel, escolha **o projeto do SharePoint 2010**e, em seguida, escolha o **Okey** botão.

     O **Assistente para personalização do SharePoint** é exibida. Este assistente permite que você selecione o site que você usará para depurar o projeto e o nível de confiança da solução.

5. Escolha o **implantar como uma solução de farm** botão de opção e, em seguida, escolha o **concluir** botão para aceitar o site do SharePoint local padrão.

## <a name="add-a-web-part-to-the-project"></a>Adicionar uma web part ao projeto

Adicionar um **Web Part** item ao projeto. O **Web Part** item adiciona o arquivo de código de Web Part. Posteriormente, você adicionará código ao arquivo de código de Web Part para renderizar o conteúdo da Web Part.

1. Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.

2. No **Adicionar Novo Item** na caixa de **modelos instalados** painel, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.

3. Na lista de modelos do SharePoint, escolha o **Web Part** modelo e, em seguida, escolha o **Add** botão.

     O **Web Part** item aparece na **Gerenciador de soluções**.

## <a name="rendering-content-in-the-web-part"></a>Renderizar o conteúdo na web part

Você pode especificar quais controles você deseja que apareça na Web Part adicionando-os à coleção controls da classe Web Part.

1. Na **Gerenciador de soluções**, abra *WebPart1.vb* (no Visual Basic) ou *WebPart1.cs* (em c#).

     O arquivo de código de Web Part é aberto no Editor de código.

2. Adicione as seguintes instruções à parte superior do arquivo de código de Web Part.

     [!code-csharp[SP_WebPart#1](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#1)]
     [!code-vb[SP_WebPart#1](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#1)]

3. Adicione o seguinte código para o `WebPart1` classe. Esse código declara os seguintes campos:

   - Uma grade de dados para exibir os funcionários na Web Part.

   - Texto que aparece no controle que é usado para filtrar a grade de dados.

   - Um rótulo que exibe um erro se a grade de dados é não é possível exibir dados.

   - Uma cadeia de caracteres que contém o caminho do arquivo de dados de funcionário.

     [!code-csharp[SP_WebPart#2](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#2)]
     [!code-vb[SP_WebPart#2](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#2)]

4. Adicione o seguinte código para o `WebPart1` classe. Esse código adiciona uma propriedade personalizada chamada `DataFilePath` para a Web Part. Uma propriedade personalizada é uma propriedade que pode ser definida pelo usuário no SharePoint. Essa propriedade obtém e define o local de um arquivo de dados XML que é usado para preencher a grade de dados.

     [!code-csharp[SP_WebPart#3](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#3)]
     [!code-vb[SP_WebPart#3](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#3)]

5. Substitua o `CreateChildControls` método com o código a seguir. Esse código executa as seguintes tarefas:

   - Adiciona a grade de dados e o rótulo que é declarado na etapa anterior.

   - Associa a grade de dados para um arquivo XML que contém dados de funcionários.

     [!code-csharp[SP_WebPart#4](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#4)]
     [!code-vb[SP_WebPart#4](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#4)]

6. Adicione o seguinte método à classe `WebPart1`. Esse código executa as seguintes tarefas:

   - Cria um verbo que aparece no menu de verbos de Web Part da Web part renderizado.

   - Manipula o evento que é gerado quando o usuário escolhe o verbo no menu de verbos. Esse código filtra a lista de funcionários que aparece na grade de dados.

     [!code-csharp[SP_WebPart#5](../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs#5)]
     [!code-vb[SP_WebPart#5](../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb#5)]

## <a name="test-the-web-part"></a>Testar a web part

Quando você executa o projeto, abre o site do SharePoint. A Web Part é automaticamente adicionada à Galeria de Web Parts no SharePoint. Você pode adicionar a Web Part a qualquer página de Web Part.

1. Cole o seguinte XML em um arquivo do bloco de notas. Esse arquivo XML contém os dados de exemplo que serão exibido na Web Part.

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

2. No bloco de notas, na barra de menus, escolha **arquivo** > **Salvar como**.

3. No **Salvar como** na caixa de **Salvar como tipo** , escolha **todos os arquivos**.

4. No **nome do arquivo** , digite **Data. XML**.

5. Escolha qualquer pasta usando o **procurar nas pastas** botão e, em seguida, escolha o **salvar** botão.

6. No Visual Studio, escolha o **F5** chave.

     Abre o site do SharePoint.

7. Sobre o **ações do Site** menu, escolha **mais opções**.

8. No **Create** , escolha o **página de Web Parts** digite e, em seguida, escolha o **criar** botão.

9. No **nova página de Web Parts** página, nomeie a página **Samplewebpartpage**e, em seguida, escolha o **criar** botão.

     A página de Web Part aparece.

10. Selecione qualquer zona na página de Web Parts.

11. Na parte superior da página, escolha o **inserir** guia e, em seguida, escolha o **Web Part** botão.

12. No **categorias** painel, escolha o **personalizado** pasta, escolha o **WebPart1** Web Part e, em seguida, escolha o **adicionar** botão.

     A Web Part aparece na página.

## <a name="test-the-custom-property"></a>Testar a propriedade personalizada

Para preencher a grade de dados que aparece na Web Part, especifique o caminho do arquivo XML que contém dados sobre cada funcionário.

1. Escolha a seta que aparece no lado direito da Web Part e, em seguida, escolha **Editar Web Part** no menu que aparece.

     Um painel que contém as propriedades para a Web Part aparece no lado direito da página.

2. No painel, expanda o **Miscelânea** nó, digite o caminho do arquivo XML que você criou anteriormente, escolha o **Apply** botão e, em seguida, escolha o **Okey** botão.

     Verifique se é exibida uma lista de funcionários na Web Part.

## <a name="test-the-web-part-verb"></a>Testar o verbo de web part

Mostrar e ocultar os funcionários que não são gerentes, clicando em um item que aparece no menu de verbos de Web Part.

1. Escolha a seta que aparece no lado direito da Web Part e, em seguida, escolha **Mostrar apenas os gerentes** no menu que aparece.

     Somente os funcionários que são gerentes aparecem na Web Part.

2. Escolha a seta novamente e, em seguida, escolha **Mostrar todos os funcionários** no menu que aparece.

     Todos os funcionários são exibidos na Web Part.

## <a name="see-also"></a>Consulte também

[Criar web parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)  
[Como: criar uma web part do SharePoint](../sharepoint/how-to-create-a-sharepoint-web-part.md)  
[Como: criar uma web part do SharePoint usando um Designer](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)  
[Passo a passo: Criar uma web part para SharePoint usando um designer](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
