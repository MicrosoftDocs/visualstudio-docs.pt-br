---
title: 'Como: personalizar um pacote de solução do SharePoint usando destinos do MSBuild | Microsoft Docs'
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
- SharePoint development in Visual Studio, packages
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 434d673c62d0b26efa1559db7d7d98747146fd2d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49889665"
---
# <a name="how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets"></a>Como: personalizar um pacote de solução do SharePoint usando destinos do MSBuild
  Usando destinos do MSBuild no prompt de comando, você pode personalizar como o Visual Studio cria arquivos de pacote do SharePoint (*. wsp*). Por exemplo, você pode personalizar as propriedades do MSBuild para alterar o diretório intermediário de empacotamento e os grupos de itens do MSBuild que especificam os arquivos enumerados.  
  
## <a name="customize-and-run-msbuild-targets"></a>Personalizar e executar os destinos do MSBuild  
 Se você personalizar as metas de BeforeLayout e AfterLayout, você pode executar tarefas antes do layout do pacote, como adicionando, removendo ou modificando os arquivos que serão empacotados.  
  
#### <a name="to-customize-the-beforelayout-target"></a>Para personalizar o destino BeforeLayout  
  
1. Abra um editor, como o bloco de notas e, em seguida, adicione o seguinte código.  
  
   ```xml  
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
     <Target Name="BeforeLayout">  
       <Message Importance="high" Text="In the BeforeLayout Target"></Message>  
     </Target>  
   </Project>  
   ```  
  
    Este exemplo exibe uma mensagem antes do empacotamento desse destino.  
  
2. Nomeie o arquivo **CustomLayout.SharePoint.targets**e, em seguida, salve-o na pasta para o projeto do SharePoint.  
  
3. Abra o projeto, abra o menu de atalho e, em seguida, escolha **descarregar projeto**.  
  
4. Na **Gerenciador de soluções**, abra o menu de atalho para o projeto e, em seguida, escolha **editar**  *\<ProjectName >. vbproj* ou **editar**  *\<ProjectName >. csproj*.  
  
5. Após o `Import` linha perto do fim do arquivo de projeto, adicione a seguinte linha.  
  
   ```xml  
   <Import Project="CustomLayout.SharePoint.targets" />  
   ```  
  
6. Salve e feche o arquivo de projeto.  
  
7. Na **Gerenciador de soluções**, abra o menu de atalho para o projeto e, em seguida, escolha **recarregar projeto**.  
  
   Quando você publica o projeto, a mensagem será exibida na saída antes do início de empacotamento.  
  
#### <a name="to-customize-the-afterlayout-target"></a>Para personalizar o destino AfterLayout  
  
1. Na barra de menus, escolha **arquivo** > **abra** > **arquivo**.  
  
2. No **abrir arquivo** caixa de diálogo, navegue até a pasta do projeto, escolha o arquivo CustomLayout.target e, em seguida, escolha o **abrir** botão.  
  
3. Antes de `</Project>` marca, adicione o seguinte código:  
  
   ```xml  
   <Target Name="AfterLayout">  
     <Message Importance="high" Text="In the AfterLayout Target"></Message>  
   </Target>  
   ```  
  
    Este exemplo exibe uma mensagem depois que esse destino é empacotado.  
  
4. Salve e feche o arquivo de destino.  
  
5. Reinicie o Visual Studio e, em seguida, abra o projeto.  
  
   Quando você publica o projeto, a mensagem BeforeLayout aparece antes do início de empacotamento e a mensagem AfterLayout aparece após a conclusão de empacotamento.  
  
## <a name="see-also"></a>Consulte também
 [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)  
  
