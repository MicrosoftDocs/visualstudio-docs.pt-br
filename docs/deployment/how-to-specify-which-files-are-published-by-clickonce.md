---
title: Como especificar quais arquivos são publicados pelo ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- Microsoft.VisualStudio.Publish.BaseProvider.Dialog.File
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, file exclusion
- files, publishing via ClickOnce
ms.assetid: 579c134a-d50f-4e0c-8e05-2a4ff654896a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c7ab6d724b40168f84227edb6ccfafc6245c30e0
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381776"
---
# <a name="how-to-specify-which-files-are-published-by-clickonce"></a>Como especificar os arquivos a serem publicados pelo ClickOnce
Ao publicar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo, todos os arquivos que não são de código no projeto são implantados junto com o aplicativo. Em alguns casos, talvez você não queira ou precise publicar determinados arquivos, ou talvez queira instalar determinados arquivos com base em condições. O Visual Studio fornece os recursos para excluir arquivos, marcar arquivos como arquivos de dados ou pré-requisitos e criar grupos de arquivos para instalação condicional.

 Os arquivos de um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo são gerenciados na caixa de diálogo **arquivos de aplicativo** , acessíveis na página **publicar** do **Designer de projeto**.

 Inicialmente, há um único grupo de arquivos chamado **(obrigatório)**. Você pode criar grupos de arquivos adicionais e atribuir arquivos a eles. Você não pode alterar o **grupo de download** para arquivos que são necessários para a execução do aplicativo. Por exemplo, o. exe do aplicativo ou os arquivos marcados como arquivos de dados devem pertencer ao grupo **(obrigatório)** .

 O valor de status de publicação padrão de um arquivo é marcado com **(automático)**. Por exemplo, o. exe do aplicativo tem um status de publicação de **include (auto)** por padrão.

 Os arquivos com a propriedade de **ação de compilação** definida como **conteúdo** são designados como arquivos de aplicativo e serão marcados como incluídos por padrão. Eles podem ser incluídos, excluídos ou marcados como arquivos de dados. As exceções são as seguintes:

- Os arquivos de dados, como os arquivos do SQL Database (*. MDF* e *. mdb*) e os arquivos XML serão marcados como arquivos de dados por padrão.

- Referências a assemblies (arquivos *. dll* ) são designadas da seguinte maneira quando você adiciona a referência: se **Copy local** for **false**, ele será marcado por padrão como um assembly de pré-requisito (**pré-requisito (auto)**) que deve estar presente no GAC antes que o aplicativo seja instalado. Se **Copy local** for **true**, o assembly será marcado por padrão como um assembly de aplicativo (**include (auto)**) e será copiado para a pasta do aplicativo na instalação. Uma referência COM será exibida na caixa de diálogo **arquivos de aplicativo** (como um arquivo *. ocx* ) somente se sua propriedade **isolada** estiver definida como **true**. Por padrão, ele será incluído.

### <a name="to-add-files-to-the-application-files-dialog-box"></a>Para adicionar arquivos à caixa de diálogo arquivos de aplicativo

1. Selecione um arquivo de dados em **Gerenciador de soluções**.

2. No janela Propriedades, altere a propriedade de **ação de compilação** para o valor de **conteúdo** .

### <a name="to-exclude-files-from-clickonce-publishing"></a>Para excluir arquivos da publicação do ClickOnce

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Clique no botão **arquivos de aplicativo** para abrir a caixa de diálogo arquivos de **aplicativo** .

4. Na caixa de diálogo **arquivos de aplicativo** , selecione o arquivo que você deseja excluir.

5. No campo **status da publicação** , selecione **excluir** na lista suspensa.

### <a name="to-mark-files-as-data-files"></a>Para marcar arquivos como arquivos de dados

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Clique no botão **arquivos de aplicativo** para abrir a caixa de diálogo arquivos de **aplicativo** .

4. Na caixa de diálogo **arquivos de aplicativo** , selecione o arquivo que você deseja marcar como dados.

5. No campo **status da publicação** , selecione **arquivo de dados** na lista suspensa.

### <a name="to-mark-files-as-prerequisites"></a>Para marcar arquivos como pré-requisitos

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Clique no botão **arquivos de aplicativo** para abrir a caixa de diálogo arquivos de **aplicativo** .

4. Na caixa de diálogo **arquivos de aplicativo** , selecione o assembly de aplicativo (arquivo *. dll* ) que você deseja marcar como um pré-requisito. Observe que seu aplicativo deve ter uma referência ao assembly de aplicativo para que ele apareça na lista.

5. No campo **status da publicação** , selecione **pré-requisito** na lista suspensa.

### <a name="to-add-a-new-file-group"></a>Para adicionar um novo grupo de arquivos

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Clique no botão **arquivos de aplicativo** para abrir a caixa de diálogo arquivos de **aplicativo** .

4. Na caixa de diálogo **arquivos de aplicativo** , selecione o campo de **grupo** para um arquivo que você deseja incluir no novo grupo.

    > [!NOTE]
    > Os arquivos devem ter a propriedade de **ação de compilação** definida como **conteúdo** antes que os nomes de arquivo apareçam na caixa de diálogo **arquivos de aplicativo** .

5. No campo **baixar grupo** , selecione **\<New...>** na lista suspensa.

6. Na caixa de diálogo **novo grupo** , insira um nome para o grupo e clique em **OK**.

### <a name="to-add-a-file-to-a-group"></a>Para adicionar um arquivo a um grupo

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. Clique no botão **arquivos de aplicativo** para abrir a caixa de diálogo arquivos de **aplicativo** .

4. Na caixa de diálogo **arquivos de aplicativo** , selecione o campo de **grupo** para um arquivo que você deseja incluir no novo grupo.

5. No campo **baixar grupo** , selecione um grupo na lista suspensa.

    > [!NOTE]
    > Você não pode alterar o **grupo de download** para arquivos que são necessários para a execução do aplicativo.

## <a name="see-also"></a>Veja também
- [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [Como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)