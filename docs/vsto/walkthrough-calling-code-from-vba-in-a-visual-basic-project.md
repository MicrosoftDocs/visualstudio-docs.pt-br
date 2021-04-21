---
title: 'Walkthrough: chamar o código do VBA em um projeto Visual Basic'
description: Saiba como chamar um método em uma personalização em nível de documento para o Microsoft Word do código Visual Basic for Applications (VBA) no documento.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], Visual Basic for Applications and
- ThisDocument class
- Word [Office development in Visual Studio], calling code from VBA
- Visual Basic [Office development in Visual Studio], calling code from VBA
- VBA [Office development in Visual Studio], calling code in document-level customizations
- Office documents [Office development in Visual Studio, Visual Basic for Applications and
- calling code from VBA
- document-level customizations [Office development in Visual Studio], calling code
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f4fe056f70e0af03809b43d60968bd8a1a50bf08
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824478"
---
# <a name="walkthrough-call-code-from-vba-in-a-visual-basic-project"></a>Walkthrough: chamar o código do VBA em um projeto Visual Basic
  Este tutorial demonstra como chamar um método em uma personalização em nível de documento para Microsoft Office o Word do código Visual Basic for Applications (VBA) no documento. O procedimento envolve três etapas básicas: adicionar um método à `ThisDocument` classe de item de host, expor o método ao código VBA e, em seguida, chamar o método do código VBA no documento.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Embora este passo a passos use o Word especificamente, os conceitos demonstrados pelo passo a passos também se aplicam a projetos de nível de documento para o Excel.

 Este passo a passo ilustra as seguintes tarefas:

- Criando um documento que contém código VBA.

- Confiar no local do documento usando a central de confiabilidade no Word.

- Adicionando um método à `ThisDocument` classe de item de host.

- Expondo o método ao código VBA.

- Chamar o método do código VBA.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-a-document-that-contains-vba-code"></a>Criar um documento que contém código VBA
 A primeira etapa é criar um documento habilitado para macro que contenha uma macro simples do VBA. O documento deve conter um projeto do VBA antes de você criar um projeto do Visual Studio baseado nesse documento. Caso contrário, o Visual Studio não pode modificar o projeto do VBA para habilitar o código VBA para chamar o assembly de personalização.

 Se você já tiver um documento que contém código VBA que deseja usar, poderá ignorar esta etapa.

### <a name="to-create-a-document-that-contains-vba-code"></a>Para criar um documento que contém código VBA

1. Inicie o Word.

2. Salve o documento ativo como um **documento habilitado para macro do Word \* (. docm)** com o nome **DocumentWithVBA**. Salve-o em um local conveniente, como o desktop.

3. Na faixa de faixas, clique na guia **desenvolvedor** .

    > [!NOTE]
    > Se a guia **desenvolvedor** não estiver visível, você deverá primeiro mostrá-la. Para obter mais informações, consulte [como: mostrar a guia Desenvolvedor na faixa de faixas](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).

4. No grupo de **códigos** , clique em **Visual Basic**.

     O Editor do Visual Basic é aberto.

5. Na janela do **projeto** , clique duas vezes em **ThisDocument**.

     O arquivo de código para o `ThisDocument` objeto é aberto.

6. Adicione o código VBA a seguir ao arquivo de código. Esse código define uma função simples que não faz nada. A única finalidade dessa função é garantir que exista um projeto do VBA no documento. Isso é necessário para etapas posteriores neste passo a passos.

    ```vb
    Sub EmptySub()
    End Sub
    ```

7. Salve o documento e saia do Word.

## <a name="create-the-project"></a>Criar o projeto
 Agora você pode criar um projeto de nível de documento para o Word que usa o documento habilitado para macro criado anteriormente.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. No menu **Arquivo** , aponte para **Novo** e clique em **Projeto**. Se o IDE estiver definido para usar Visual Basic configurações de desenvolvimento, no menu **arquivo** , clique em **novo projeto**.

3. No painel modelos, expanda **Visual Basic** e, em seguida, expanda **Office/SharePoint**.

4. Selecione o nó **suplementos do Office** .

5. Na lista de modelos de projeto, selecione o **documento word 2010** ou o projeto de **documento do Word 2013** .

6. Na caixa **nome** , digite **CallingCodeFromVBA**.

7. Clique em **OK**.

     O **Assistente de ferramentas do Visual Studio para o Office Project** é aberto.

8. Selecione **copiar um documento existente** e, na caixa **caminho completo do documento existente** , especifique o local do documento **DocumentWithVBA** que você criou anteriormente. Se você estiver usando seu próprio documento habilitado para macro, especifique o local deste documento.

9. Clique em **Concluir**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o documento **DocumentWithVBA** no designer e adiciona o projeto **CallingCodeFromVBA** ao **Gerenciador de soluções**.

## <a name="trust-the-location-of-the-document"></a>Confiar no local do documento
 Antes de expor o código em sua solução para o código VBA no documento, você deve confiar no VBA no documento a ser executado. Há várias maneiras de fazer isso. Para esta explicação, confie no local do documento na central de **confiabilidade** do Word.

### <a name="to-trust-the-location-of-the-document"></a>Para confiar no local do documento

1. Inicie o Word.

2. Clique na guia **arquivo** .

3. Clique no botão **Opções do Word** .

4. No painel categorias, clique em **central de confiabilidade**.

5. No painel de detalhes, clique em **configurações da central de confiabilidade**.

6. No painel categorias, clique em **locais confiáveis**.

7. No painel de detalhes, clique em **Adicionar novo local**.

8. Na caixa de diálogo **Microsoft Office local confiável** , navegue até a pasta que contém o projeto **CallingCodeFromVBA** .

9. Selecione as **subpastas deste local também são confiáveis**.

10. Na caixa de diálogo **Microsoft Office local confiável** , clique em **OK**.

11. Na caixa de diálogo **central de confiabilidade** , clique em **OK**.

12. Na caixa de diálogo **Opções do Word** , clique em **OK**.

13. Saia do Word.

## <a name="add-a-method-to-the-thisdocument-class"></a>Adicionar um método à classe ThisDocument
 Agora que o projeto do VBA está configurado, adicione um método à `ThisDocument` classe de item de host que você pode chamar a partir do código VBA.

### <a name="to-add-a-method-to-the-thisdocument-class"></a>Para adicionar um método à classe ThisDocument

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **ThisDocument. vb** e clique em **Exibir código**.

     O arquivo **ThisDocument. vb** é aberto no editor de código.

2. Adicione o método a seguir à classe `ThisDocument`. Esse método cria uma tabela com duas linhas e duas colunas no início do documento. Os parâmetros especificam o texto que é exibido na primeira linha. Mais adiante neste tutorial, você chamará esse método do código VBA no documento.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/CallingCodeFromVBA/ThisDocument.vb" id="Snippet1":::

3. Compile o projeto.

## <a name="expose-the-method-to-vba-code"></a>Expor o método ao código VBA
 Para expor o `CreateTable` método ao código VBA no documento, defina a propriedade **EnableVbaCallers** para o `ThisDocument` item de host como **true**.

### <a name="to-expose-the-method-to-vba-code"></a>Para expor o método ao código VBA

1. Em **Gerenciador de soluções**, clique duas vezes em **ThisDocument. vb**.

     O arquivo **DocumentWithVBA** é aberto no designer.

2. Na janela **Propriedades** , selecione a propriedade **EnableVbaCallers** e altere o valor para **true**.

3. Clique em **OK** na mensagem que é exibida.

4. Compile o projeto.

## <a name="call-the-method-from-vba-code"></a>Chamar o método do código VBA
 Agora você pode chamar o `CreateTable` método do código VBA no documento.

> [!NOTE]
> Neste tutorial, você adicionará código VBA ao documento durante a depuração do projeto. O código VBA que você adicionar a este documento será substituído na próxima vez que você compilar o projeto, pois o Visual Studio substitui o documento na pasta de saída da compilação por uma cópia do documento da pasta principal do projeto. Se você quiser salvar o código VBA, poderá copiá-lo para o documento na pasta do projeto. Para obter mais informações, consulte [combinar VBA e personalizações em nível de documento](../vsto/combining-vba-and-document-level-customizations.md).

### <a name="to-call-the-method-from-vba-code"></a>Para chamar o método do código VBA

1. Pressione **F5** para executar o projeto.

2. Na guia **desenvolvedor** , no grupo **código** , clique em **Visual Basic**.

     O Editor do Visual Basic é aberto.

3. No menu **Inserir** , clique em **módulo**.

4. Adicione o código a seguir ao novo módulo.

     Esse código chama o `CreateTable` método no assembly de personalização. A macro acessa esse método usando a `CallVSTOAssembly` Propriedade do `ThisDocument` objeto. Essa propriedade foi gerada automaticamente quando você define a propriedade **EnableVbaCallers** anteriormente neste passo a passos.

    ```vb
    Sub CreateTable()
        Call ThisDocument.CallVSTOAssembly.CreateTable("Employee Name", "Start Date")
    End Sub
    ```

5. Pressione **F5**.

6. Verifique se uma nova tabela foi adicionada ao documento.

7. Saia do Word sem salvar as alterações.

## <a name="next-steps"></a>Próximas etapas
 Você pode saber mais sobre como chamar código em soluções do Office do VBA nestes tópicos:

- Chame o código em uma personalização do Visual C# a partir do VBA. Esse processo é diferente do processo de Visual Basic. Para obter mais informações, consulte [Walkthrough: chamar código do VBA em um projeto do Visual C&#35;](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md).

- Chame o código em um suplemento do VSTO do VBA. Para obter mais informações, consulte [Walkthrough: chamar código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md).

## <a name="see-also"></a>Consulte também
- [Combine personalizações do VBA e no nível do documento](../vsto/combining-vba-and-document-level-customizations.md)
- [Programar personalizações em nível de documento](../vsto/programming-document-level-customizations.md)
- [Como: expor código ao VBA em um projeto Visual Basic](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
- [Como: expor código ao VBA em um projeto do Visual C&#35;](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
- [Walkthrough: chamar o código do VBA em um projeto do Visual C&#35;](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)
