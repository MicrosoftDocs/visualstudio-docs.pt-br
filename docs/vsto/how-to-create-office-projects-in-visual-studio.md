---
title: 'Como: criar projetos do Office no Visual Studio'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VST.SelectDocWizard.Page1
- VST.SelectDocWizard.Http
- VST.SelectDocWizard.Extension
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], creating projects
- Office applications [Office development in Visual Studio], creating
- Office projects [Office development in Visual Studio]
- projects [Office development in Visual Studio], creating
- document-level customizations [Office development in Visual Studio], creating
- application-level add-ins [Office development in Visual Studio], creating projects
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c70668f2d4cb9597e00a7e3848b78b9f2ed49db7
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547557"
---
# <a name="how-to-create-office-projects-in-visual-studio"></a>Como: criar projetos do Office no Visual Studio
  Você pode usar o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] para criar o suplemento do VSTO e personalizações em nível de documento para aplicativos Microsoft Office. Para obter mais informações sobre esses tipos de projetos, consulte [visão geral do desenvolvimento de soluções do Office &#40;&#41;do VSTO ](../vsto/office-solutions-development-overview-vsto.md).

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-create-a-vsto-add-in-project"></a>Para criar um projeto de suplemento do VSTO

1. No menu **Arquivo**, escolha **Novo** > **Projeto**. Se o ambiente de desenvolvimento integrado (IDE) estiver definido para usar [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] as configurações de desenvolvimento, no menu **arquivo** , escolha **novo**  >  **projeto**.

    A caixa de diálogo **Novo Projeto** aparecerá.

   > [!NOTE]
   > Os projetos do Office visam o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] por padrão. Para obter mais informações, consulte [.NET Framework perfil do cliente](/dotnet/framework/deployment/client-profile).

2. No painel modelos, no nó do idioma que você deseja usar, expanda **Office/SharePoint**.

3. Escolha o nó **suplementos do Office** .

4. Na lista de modelos de projeto, selecione um modelo de projeto de suplemento do VSTO. Para obter uma lista de modelos de projeto de suplemento do VSTO disponíveis, consulte [visão geral dos modelos do Office Project](../vsto/office-project-templates-overview.md).

   > [!NOTE]
   > Se os modelos de projeto não estiverem visíveis quando você selecionar o nó **suplementos do Office** , certifique-se de que **.NET Framework 4** ou posterior esteja selecionado na caixa de combinação na parte superior da caixa de diálogo. Os modelos de projeto do Office são visíveis para as duas versões do .NET Framework.

5. Na caixa **nome** , digite um nome para o projeto. Por padrão, o nome do projeto também é usado como o nome da solução.

6. Na caixa **local** , insira o caminho onde você deseja criar o projeto. Você pode usar caminhos absolutos e UNC (Convenção de nomenclatura universal). Não use HTTP, FTP ou outros caminhos de protocolo.

    Os locais têm os seguintes formatos:

   * [*unidade*\]\:

   * \\\\*Servidor do* \\ *Compartilhar*

     Não use estes caracteres no local:

   * Asterisco (*)

   * Barra vertical (|)

   * Dois pontos (:) (Exceto após a letra da unidade).

   * Aspas duplas (") (os caminhos que contêm espaços não precisam de aspas).

   * Menor que (\<)

   * Maior que (>)

   * Ponto de interrogação (?)

   * Sinal de porcentagem (%)

7. Clique no botão **OK**.

   ::: moniker range="vs-2017"

   > [!NOTE]
   > Os projetos de suplemento sempre são salvos quando são criados. Eles não podem ser criados como projetos temporários. Para obter mais informações sobre projetos temporários, consulte [projetos temporários](../ide/creating-solutions-and-projects.md#create-a-temporary-project).

   ::: moniker-end

### <a name="to-create-a-document-level-customization-project"></a>Para criar um projeto de personalização no nível do documento

1. No menu **Arquivo**, escolha **Novo** > **Projeto**. Se o IDE estiver definido para usar Visual Basic configurações de desenvolvimento, no menu **arquivo** , escolha **novo**  >  **projeto**.

    A caixa de diálogo **Novo Projeto** aparecerá.

2. No painel modelos, no nó do idioma que você deseja usar, expanda **Office/SharePoint**.

3. Selecione o nó **suplementos do Office** .

4. Na lista de modelos de projeto, selecione um modelo de projeto de nível de documento. Para obter uma lista de modelos de projeto de nível de documento disponíveis, consulte [visão geral dos modelos do Office Project](../vsto/office-project-templates-overview.md).

   > [!NOTE]
   > Se os modelos de projeto não estiverem visíveis quando você selecionar o nó **suplementos do Office** , certifique-se de que **.NET Framework 4** ou posterior esteja selecionado.

5. Na caixa **nome** , digite um nome para o projeto. Por padrão, esse nome também é usado para o documento. Se o IDE estiver definido para usar configurações de desenvolvimento do Visual C# ou configurações de desenvolvimento gerais, insira também um local e um nome de solução.

   > [!NOTE]
   > Você não pode usar caracteres substitutos no caminho do local do projeto ou no nome do projeto. Além disso, se você planeja implantar a solução para uso offline, os caracteres no nome do projeto devem se ajustar às especificações do protocolo HTTP.

6. Clique no botão **OK**.

    O **Assistente de ferramentas do Visual Studio para o Office Project** é aberto.

7. Selecione **criar um novo documento** se desejar criar um novo documento para a solução ou selecione **copiar um documento existente** se desejar personalizar um documento existente.

    Se você criar um novo documento, especifique o nome na caixa **nome** e selecione o formato do documento usando a caixa **Formatar** . Para obter mais informações sobre os formatos disponíveis, consulte [arquitetura de personalizações em nível de documento](../vsto/architecture-of-document-level-customizations.md).

    Se você usar um documento existente, especifique o local do documento no **caminho completo da caixa do documento existente** . Você pode usar caminhos absolutos e UNC. Não use HTTP, FTP ou outros caminhos de protocolo para o documento.

    Os locais têm os seguintes formatos:

   - [*unidade*\]\:

   - \\\\*Servidor do* \\ *Compartilhar*

     Não use estes caracteres no local:

   - Asterisco (*)

   - Barra vertical (|)

   - Dois pontos (:) (Exceto após a letra da unidade).

   - Aspas duplas (") (os caminhos que contêm espaços não precisam de aspas).

   - Menor que (\<)

   - Maior que (>)

   - Ponto de interrogação (?)

   - Sinal de porcentagem (%)

   > [!NOTE]
   > Se você usar um documento existente em um [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] projeto do, use apenas os documentos que foram criados no ou convertidos no [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] . Da mesma forma, se você usar um documento existente em um projeto do Word 2010, use apenas os documentos que foram criados ou convertidos para o Word 2010. Determinados recursos serão desabilitados no documento se você usar um documento que foi criado em uma versão anterior do Word. Se você tentar escrever código que usa esses recursos, você poderá encontrar erros em seu projeto. Para converter um documento, abra-o no [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou no Word 2010, na guia **arquivo** da faixa de palavras, escolha **informações**  >  **converter**.

8. Escolha **Concluir**.

9. Adicione a pasta do projeto e suas subpastas à lista de locais confiáveis na central de confiabilidade no Word nos seguintes casos:

   - Você está criando um documento do Word baseado em um arquivo *. docm* e o documento contém um projeto do VBA ou hospeda Windows Forms controles. Adicionar a pasta do projeto à lista de locais confiáveis ajudará a garantir que o documento funcione conforme o esperado no momento do design.

   - Você está criando um projeto de modelo do Word baseado em um arquivo *. dotx* . Você deve adicionar a pasta do projeto à lista de locais confiáveis para que você possa executar e depurar o projeto.

     Para obter mais informações sobre como adicionar um documento a locais confiáveis, consulte a Microsoft Office site online [criar, remover ou alterar um local confiável para seus arquivos](https://support.office.com/article/Create-remove-or-change-a-trusted-location-for-your-files-f5151879-25ea-4998-80a5-4208b3540a62).

## <a name="see-also"></a>Confira também
- [Visão geral dos modelos do Office Project](../vsto/office-project-templates-overview.md)
- [Desenvolvimento colaborativo de soluções do Office](../vsto/collaborative-development-of-office-solutions.md)
- [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)
- [Introdução à programação de suplementos do VSTO](../vsto/getting-started-programming-vsto-add-ins.md)
