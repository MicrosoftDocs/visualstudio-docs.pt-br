---
title: 'Como: marcar controles como controles seguros | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, safe controls
- SharePoint development in Visual Studio, advanced packaging tools
- safe controls [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: cd7ed13504d3d91f4239a8ea070454e1c31b1114
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016254"
---
# <a name="how-to-mark-controls-as-safe-controls"></a>Como: marcar controles como controles seguros
  Por segurança, o SharePoint diferencia os controles da Web que são protegidos contra injeção de script e controles da Web que não são. Controles protegidos, ou *controles seguros*, podem ser acessados por usuários não confiáveis. Você pode marcar controles como seguros na propriedade entradas de controle seguro de um item de projeto do SharePoint ou no **Designer de pacotes** ao adicionar um assembly ao pacote. Para obter mais informações, consulte

- [web.config configurações de arquivo alteram](/previous-versions/office/developer/sharepoint-2007/bb802890(v=office.12)) e [registram um assembly de Web Part como um controle seguro](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11)).

> [!IMPORTANT]
> Esses procedimentos são para fins ilustrativos. Marque controles seguros somente se você tiver certeza de que eles são seguros.

## <a name="marking-safe-controls-in-the-safe-control-entries-property"></a>Marcando controles seguros na propriedade entradas de controle seguro

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-safe-control-entries-property"></a>Para marcar os controles como seguros ou não seguros na propriedade entradas de controle seguro

1. Crie uma solução do SharePoint com um projeto de Web Part Visual.

2. Adicione dois controles à Web Part: uma caixa de texto e um botão. Deixe os nomes com seus valores padrão, TextBox1 e Button1, respectivamente.

3. Adicione duas entradas à propriedade de entradas de **controle seguro** da Web Part. Para fazer isso, escolha o botão de reticências (![elipse do designer móvel ASP.net](../sharepoint/media/mwellipsis.gif "Elipse do designer móvel ASP.NET")) ao lado da propriedade **entradas de controle seguro** na janela **Propriedades** .

     A caixa de diálogo **entradas de controle seguro** é exibida.

4. Na caixa de diálogo **entradas de controle seguro** , escolha o botão **Adicionar** duas vezes para adicionar duas entradas de controle seguro ao painel **Membros** : uma para o botão e uma para a caixa de texto.

5. Escolha a primeira entrada de controle seguro e, em seguida, altere o valor de sua propriedade **Safe** para **false**, sua propriedade de **nome de tipo** para **Button1**e sua propriedade **Safe from script** como **false**.

     Esta etapa identifica o controle de botão como um controle não seguro.

6. Escolha a segunda entrada de controle seguro na lista. Deixe o valor de sua propriedade **segura** como **true** e defina sua propriedade **Name de tipo** como **TextBox1** e sua propriedade **Safe from script** como **true**.

     O controle de caixa de texto agora está marcado como um controle que é seguro contra injeção de script.

7. Escolha o botão **OK** para fechar a caixa de diálogo.

## <a name="marking-safe-controls-in-the-package-designer"></a>Marcando controles seguros no designer de pacotes

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-package-designer"></a>Para marcar os controles como seguros ou não seguros no designer de pacotes

1. Crie uma solução do SharePoint com um projeto de Web Part Visual.

2. Adicione dois controles à Web Part: uma caixa de texto e um botão. Deixe os nomes com seus valores padrão, TextBox1 e Button1, respectivamente.

     Anote o namespace do controle porque ele é usado posteriormente.

3. Na barra de menus, escolha **Compilar**compilar  >  **solução** para compilar o projeto.

4. Crie outra solução do SharePoint.

5. No **Gerenciador de soluções**, abra o menu de atalho do arquivo *Package. Package* e, em seguida, escolha **abrir** para abrir o **Designer de pacotes**.

6. No **Designer de pacotes**, escolha a guia **avançado** .

7. Em **assemblies adicionais**, escolha o botão **Adicionar** e, em seguida, escolha **Adicionar assembly existente** na lista.

8. Na caixa de diálogo **Adicionar assembly existente** , escolha o botão de reticências (![ASP.NET Mobile Designer Ellipse](../sharepoint/media/mwellipsis.gif "Elipse do designer móvel ASP.NET")) ao lado de **caminho de origem**.

9. Escolha o assembly da solução do SharePoint que você criou na etapa 1 e, em seguida, escolha o botão **abrir** .

10. Para este exemplo, deixe a opção de **destino de implantação** como GlobalAssemblyCache.

     Esta etapa faz com que o assembly seja implantado no cache de assembly global (GAC) do sistema. Se você quiser que o assembly implante na pasta do aplicativo Web (bin), selecione essa opção em vez disso. Para obter mais informações, consulte [Implantando Web Parts no SharePoint Foundation](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14)).

11. Na caixa **controles seguros** , escolha o botão **clique aqui para adicionar um novo item** .

12. Insira os valores para as propriedades da tabela a seguir.

    |Nome da propriedade|Valor|
    |-------------------|-----------|
    |Namespace|O namespace totalmente qualificado para o controle, como **BdcModelProject1. VisualWebPart1**.|
    |Nome do Tipo|Button1|
    |Nome do Assembly|Um nome de assembly forte, como: Microsoft. Office. SharePoint. ClientExtensions, Version = 14.0.0.0, Culture = neutral, PublicKeyToken = 71e9bce111e9429c.|
    |Safe|Desmarque a caixa de seleção **seguro** .|
    |Seguro contra script|Deixe a caixa de seleção **seguro contra o script** desmarcada.|

    > [!NOTE]
    > O valor do **nome do assembly** para assemblies adicionados por meio da guia **avançado** do **Designer de pacotes** não pode ser um token, ele deve ser um assembly de nome forte. Para obter mais informações, consulte [Criando e usando assemblies de nomes fortes](/previous-versions/dotnet/netframework-4.0/xwb8f617(v=vs.100)).

13. Escolha a tecla **Tab** para criar outra entrada de controle seguro.

14. Escolha o botão **clique aqui para adicionar um novo item** novamente.

15. Insira os valores para as propriedades da tabela a seguir.

    |Nome da propriedade|Valor|
    |-------------------|-----------|
    |Namespace|O namespace totalmente qualificado para o controle, como **BdcModelProject1. VisualWebPart1**.|
    |Nome do Tipo|TextBox1|
    |Nome do Assembly|Um nome de assembly forte, como: Microsoft. Office. SharePoint. ClientExtensions, Version = 14.0.0.0, Culture = neutral, PublicKeyToken = 71e9bce111e9429c.|
    |Safe|Marque a caixa de seleção **seguro** .|
    |Seguro contra script|Marque a caixa de seleção **seguro contra script** .|

16. Escolha a tecla **Tab** e, em seguida, escolha o botão **OK** para fechar a caixa de diálogo.

## <a name="see-also"></a>Consulte também
- [Fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
