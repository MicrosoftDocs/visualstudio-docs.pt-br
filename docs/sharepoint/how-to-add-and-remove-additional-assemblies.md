---
title: 'Como: Adicionar e remover assemblies adicionais | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.CustomAssembly
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 07b9016a4e246d3ed5a2697d924f556517a8226f
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014827"
---
# <a name="how-to-add-and-remove-additional-assemblies"></a>Como: Adicionar e remover assemblies adicionais
  Se um pacote do SharePoint depender de outros assemblies para funcionalidade ou dados, você poderá adicionar os assemblies ao seu pacote de solução (. wsp). Dessa forma, o servidor do SharePoint garante que os assemblies personalizados sejam instalados com um pacote.

 Você também pode adicionar e alterar os controles seguros e os arquivos de recurso de classe associados aos assemblies.

## <a name="add-additional-assemblies-safe-controls-and-class-resources"></a>Adicionar assemblies, controles seguros e recursos de classe adicionais
 Você pode adicionar assemblies adicionais ao pacote de solução do SharePoint. Assemblies adicionais em uma solução em área restrita são implantados no cache de assembly global, mas itens de projeto do SharePoint em uma solução de área restrita são adicionados ao banco de dados de conteúdo. Você também pode adicionar controles seguros e recursos de classe a esses assemblies adicionais. Para obter mais informações sobre controles seguros, consulte [fornecendo informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md) ou "criando uma entrada SafeControl" em [implantando o Web Parts no SharePoint Foundation](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14)).

#### <a name="to-add-an-existing-assembly"></a>Para adicionar um assembly existente

1. Abra o **Designer de pacotes**. Para obter mais informações, consulte [como: personalizar um pacote de solução do SharePoint](../sharepoint/how-to-customize-a-sharepoint-solution-package.md).

2. Escolha a guia **avançado** .

3. Escolha o botão **Adicionar** e, em seguida, escolha **Adicionar assembly existente** na lista.

     A caixa de diálogo **Adicionar assembly existente** é exibida.

4. Escolha as reticências (![elipse do designer móvel ASP.net](../sharepoint/media/mwellipsis.gif "Elipse do designer móvel ASP.NET")) e escolha o assembly que você deseja adicionar. É recomendável usar um caminho relativo para o assembly selecionado para fins de portabilidade.

5. Para o **destino de implantação**, escolha o botão de opção **GlobalAssemblyCache** para implantar o assembly no cache de assembly global ou escolha o botão de opção **WebApplication** para implantar o assembly na pasta do WebApplication no servidor que está executando o SharePoint.

#### <a name="to-add-an-assembly-from-project-output"></a>Para adicionar um assembly da saída do projeto

1. Abra o **Designer de pacotes**.

     Para obter mais informações, consulte [como: personalizar um pacote de solução do SharePoint](../sharepoint/how-to-customize-a-sharepoint-solution-package.md).

2. Escolha a guia **avançado** .

3. Escolha o botão **Adicionar** e, em seguida, escolha **Adicionar assembly da saída do projeto** na lista.

     A caixa de diálogo **Adicionar assembly do projeto de saída** é exibida.

4. Na lista **projeto de origem** e escolha o projeto de origem que você deseja adicionar.

5. Para o **destino de implantação**, escolha o botão de opção **GlobalAssemblyCache** para implantar o assembly no cache de assembly global ou escolha o botão de opção **WebApplication** para implantar o assembly na pasta do WebApplication no servidor que está executando o SharePoint.

#### <a name="to-add-a-safe-control"></a>Para adicionar um controle seguro

1. Abra a caixa de diálogo **Editar assembly existente** . Para fazer isso, abra o designer de pacotes, escolha a guia **avançado** , escolha um assembly e, em seguida, escolha o botão **Editar** .

2. No painel **controles seguros** , escolha o botão **clique aqui para adicionar um novo item** .

3. Na coluna **nome do assembly** , insira o nome do assembly.

4. Na coluna **namespace** , digite o nome do namespace para o controle seguro.

5. Na coluna **nome do tipo** , digite o nome do tipo.

#### <a name="to-add-a-class-resource"></a>Para adicionar um recurso de classe

1. Abra a caixa de diálogo **Editar assembly existente** . Para fazer isso, abra o designer de pacotes, escolha a guia **avançado** , escolha um assembly e, em seguida, escolha o botão **Editar** .

2. No painel **recursos de classe** , escolha o botão **clique aqui para adicionar um novo item** .

3. Na coluna **nome do arquivo** , escolha as reticências (![elipse do designer móvel ASP.net](../sharepoint/media/mwellipsis.gif "Elipse do designer móvel ASP.NET")) e escolha o recurso de classe que você deseja adicionar.

## <a name="delete-custom-assemblies"></a>Excluir assemblies personalizados
 Você pode excluir assemblies de um pacote do SharePoint ou excluir controles seguros e recursos de classe de assemblies existentes.

#### <a name="to-delete-an-existing-assembly"></a>Para excluir um assembly existente

1. Abra o **Designer de pacotes**. Para obter mais informações, consulte [como: personalizar um pacote de solução do SharePoint](../sharepoint/how-to-customize-a-sharepoint-solution-package.md).

2. Escolha a guia **avançado** .

3. No painel **assemblies adicionais** , escolha o assembly personalizado que você deseja excluir.

4. Escolha o botão **excluir** .

#### <a name="to-delete-a-safe-control-for-an-assembly"></a>Para excluir um controle seguro de um assembly

1. Abra a caixa de diálogo **Editar assembly existente** . Para fazer isso, abra o designer de pacotes, escolha a guia **avançado** , escolha um assembly e, em seguida, escolha o botão **Editar** .

2. Escolha o controle seguro que você deseja excluir.

3. Escolha a chave excluir.

#### <a name="to-delete-a-class-resource-for-an-assembly"></a>Para excluir um recurso de classe para um assembly

1. Abra a caixa de diálogo **Editar assembly existente** . Para fazer isso, abra o designer de pacotes, escolha a guia **avançado** , escolha um assembly e, em seguida, escolha o botão **Editar** .

2. Escolha o recurso de classe que você deseja excluir.

3. Escolha a chave excluir.

## <a name="see-also"></a>Consulte também
- [Criar recursos do SharePoint](../sharepoint/creating-sharepoint-features.md)
- [Como personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [Como: Adicionar e remover itens para recursos do SharePoint](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
