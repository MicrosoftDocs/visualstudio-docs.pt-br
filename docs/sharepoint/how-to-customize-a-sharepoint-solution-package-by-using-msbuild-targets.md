---
title: Personalizar o pacote de solução do SharePoint usando destinos do MSBuild
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: e6570b1e3c16f1935813682e2c29051c4ac7d64a
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016877"
---
# <a name="how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets"></a>Como: personalizar um pacote de solução do SharePoint usando destinos do MSBuild
  Usando destinos do MSBuild em um prompt de comando, você pode personalizar como o Visual Studio cria arquivos de pacote do SharePoint (*. wsp*). Por exemplo, você pode personalizar as propriedades do MSBuild para alterar o diretório intermediário de empacotamento e os grupos de itens do MSBuild que especificam os arquivos enumerados.

## <a name="customize-and-run-msbuild-targets"></a>Personalizar e executar destinos do MSBuild
 Se você personalizar os destinos BeforeLayout e AfterLayout, poderá executar tarefas antes do layout do pacote, como adicionar, remover ou modificar arquivos que serão empacotados.

#### <a name="to-customize-the-beforelayout-target"></a>Para personalizar o destino BeforeLayout

1. Abra um editor, como o bloco de notas e, em seguida, adicione o código a seguir.

   ```xml
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <Target Name="BeforeLayout">
       <Message Importance="high" Text="In the BeforeLayout Target"></Message>
     </Target>
   </Project>
   ```

    Este exemplo exibe uma mensagem antes do empacotamento desse destino.

2. Nomeie o arquivo **customLayout. SharePoint. targets**e, em seguida, salve-o na pasta do projeto do SharePoint.

3. Abra o projeto, abra o menu de atalho e escolha **descarregar projeto**.

4. No **Gerenciador de soluções**, abra o menu de atalho para o projeto e escolha **Editar** * \<ProjectName> . vbproj* ou **Edit** * \<ProjectName> . csproj*.

5. Após a `Import` linha próxima ao final do arquivo de projeto, adicione a linha a seguir.

   ```xml
   <Import Project="CustomLayout.SharePoint.targets" />
   ```

6. Salve e feche o arquivo de projeto.

7. No **Gerenciador de soluções**, abra o menu de atalho do projeto e, em seguida, escolha **recarregar projeto**.

   Quando você publicar o projeto, a mensagem será exibida na saída antes do início do empacotamento.

#### <a name="to-customize-the-afterlayout-target"></a>Para personalizar o destino AfterLayout

1. Na barra de menus, escolha **arquivo**  >  **abrir**  >  **arquivo**.

2. Na caixa de diálogo **Abrir arquivo** , navegue até a pasta do projeto, escolha o arquivo customLayout. Target e, em seguida, escolha o botão **abrir** .

3. Logo antes da `</Project>` marca, adicione o seguinte código:

   ```xml
   <Target Name="AfterLayout">
     <Message Importance="high" Text="In the AfterLayout Target"></Message>
   </Target>
   ```

    Este exemplo exibe uma mensagem após esse destino ser empacotado.

4. Salve e feche o arquivo de destinos.

5. Reinicie o Visual Studio e, em seguida, abra o projeto.

   Quando você publica o projeto, a mensagem BeforeLayout é exibida antes de o empacotamento ser iniciado e a mensagem AfterLayout é exibida após a conclusão do empacotamento.

## <a name="see-also"></a>Consulte também
- [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
