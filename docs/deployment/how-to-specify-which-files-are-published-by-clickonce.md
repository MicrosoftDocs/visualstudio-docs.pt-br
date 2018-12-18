---
title: 'Como: especificar quais arquivos são publicados pelo ClickOnce | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: efe2e5ab9f2074c1706f14ac52f655921af4b9a2
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39080458"
---
# <a name="how-to-specify-which-files-are-published-by-clickonce"></a>Como: especificar quais arquivos são publicados pelo ClickOnce
Ao publicar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquivos de aplicativo, tudo sem código no projeto são implantados juntamente com o aplicativo. Em alguns casos, você talvez não queira ou precise publicar certos arquivos, ou você talvez queira instalar determinados arquivos com base em condições. Visual Studio fornece os recursos para excluir arquivos, marcar arquivos como arquivos de dados ou pré-requisitos e criar grupos de arquivos para instalação condicional.  
  
 Arquivos para um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo são gerenciadas na **arquivos de aplicativo** caixa de diálogo, acessível a partir o **publicar** página do **Designer de projeto**.  
  
 Inicialmente, há um grupo de arquivo único chamado **(obrigatório)**. Você pode criar grupos de arquivos adicionais e atribuir arquivos neles. Não é possível alterar o **grupo de Download** para arquivos que são necessários para a execução do aplicativo. Por exemplo, o aplicativo .exe ou arquivos marcado como arquivos de dados devem pertencer à **(obrigatório)** grupo.  
  
 Status de publicação padrão valor de um arquivo é marcada com **(automática)**. Por exemplo, .exe do aplicativo tem um status de publicação dos **incluir (Auto)** por padrão.  
  
 Arquivos com o **ação de compilação** propriedade definida como **conteúdo** são designados como arquivos de aplicativo e será marcado como incluído por padrão. Eles podem ser incluídos, excluídos ou marcados como arquivos de dados. As exceções são da seguinte maneira:  
  
-   Arquivos de dados como banco de dados SQL (*mdf* e *. mdb*) arquivos e arquivos XML serão marcados como arquivos de dados por padrão.  
  
-   Referências aos assemblies (*. dll* arquivos) são designados como a seguir quando você adiciona a referência: se **Copy Local** está **False**, ela é marcada por padrão como um pré-requisito assembly (**pré-requisito (Auto)**) que devem estar presentes no GAC, antes do aplicativo está instalado. Se **Copy Local** é **verdadeiro**, o assembly é marcado por padrão como um assembly de aplicativo (**incluir (Auto)**) e será copiada para a pasta do aplicativo durante a instalação. Uma referência COM aparecerá na **arquivos de aplicativo** caixa de diálogo (como um *. ocx* arquivo) somente se seu **isolado** propriedade é definida como **True**. Por padrão, ele será incluído.  
  
### <a name="to-add-files-to-the-application-files-dialog-box"></a>Para adicionar arquivos à caixa de diálogo arquivos do aplicativo  
  
1.  Selecione um arquivo de dados no **Gerenciador de soluções**.  
  
2.  Na janela Propriedades, altere o **ação de compilação** propriedade para o **conteúdo** valor.  
  
### <a name="to-exclude-files-from-clickonce-publishing"></a>Para excluir arquivos de publicação do ClickOnce  
  
1.  Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2.  Clique o **publicar** guia.  
  
3.  Clique o **arquivos de aplicativo** para abrir o **arquivos de aplicativo** caixa de diálogo.  
  
4.  No **arquivos de aplicativo** caixa de diálogo, selecione o arquivo que você deseja excluir.  
  
5.  No **Status da publicação** campo, selecione **excluir** na lista suspensa.  
  
### <a name="to-mark-files-as-data-files"></a>Para marcar os arquivos como arquivos de dados  
  
1.  Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2.  Clique o **publicar** guia.  
  
3.  Clique o **arquivos de aplicativo** para abrir o **arquivos de aplicativo** caixa de diálogo.  
  
4.  No **arquivos de aplicativo** caixa de diálogo, selecione o arquivo que você deseja marcar como dados.  
  
5.  No **Status da publicação** campo, selecione **arquivo de dados** na lista suspensa.  
  
### <a name="to-mark-files-as-prerequisites"></a>Para marcar os arquivos como pré-requisitos  
  
1.  Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2.  Clique o **publicar** guia.  
  
3.  Clique o **arquivos de aplicativo** para abrir o **arquivos de aplicativo** caixa de diálogo.  
  
4.  No **arquivos de aplicativo** caixa de diálogo, selecione o assembly do aplicativo (*. dll* arquivo) que você deseja marcar como um pré-requisito. Observe que o seu aplicativo deve ter uma referência ao assembly do aplicativo para que ele apareça na lista.  
  
5.  No **Status da publicação** campo, selecione **pré-requisito** na lista suspensa.  
  
### <a name="to-add-a-new-file-group"></a>Para adicionar um novo grupo de arquivos  
  
1.  Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2.  Clique o **publicar** guia.  
  
3.  Clique o **arquivos de aplicativo** para abrir o **arquivos de aplicativo** caixa de diálogo.  
  
4.  No **arquivos de aplicativo** caixa de diálogo, selecione o **grupo** field para um arquivo que você deseja incluir no novo grupo.  
  
    > [!NOTE]
    >  Os arquivos devem ter o **ação de compilação** propriedade definida como **conteúdo** antes que os nomes de arquivo são exibidos no **arquivos de aplicativo** caixa de diálogo.  
  
5.  No **grupo de Download** campo, selecione  **\<novo... >** na lista suspensa.  
  
6.  No **novo grupo** caixa de diálogo, insira um nome para o grupo e, em seguida, clique em **Okey**.  
  
### <a name="to-add-a-file-to-a-group"></a>Para adicionar um arquivo a um grupo  
  
1.  Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2.  Clique o **publicar** guia.  
  
3.  Clique o **arquivos de aplicativo** para abrir o **arquivos de aplicativo** caixa de diálogo.  
  
4.  No **arquivos de aplicativo** caixa de diálogo, selecione o **grupo** field para um arquivo que você deseja incluir no novo grupo.  
  
5.  No **grupo de Download** , selecione um grupo na lista suspensa.  
  
    > [!NOTE]
    >  Não é possível alterar o **grupo de Download** para arquivos que são necessários para a execução do aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)   
 [Como: publicar um aplicativo ClickOnce usando o Assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)