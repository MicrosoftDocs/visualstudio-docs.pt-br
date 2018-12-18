---
title: Como criar modelos de item | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- project item templates, XML reference
- project item templates, custom template locations
- project item templates, creating
- project item templates, metadata files
ms.assetid: 77bc53d4-d607-4820-a032-7e3b365891b5
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 8559fb8b32b83d352bd9ec82cf426903aff13a19
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49863616"
---
# <a name="how-to-create-item-templates"></a>Como criar modelos de item
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As etapas no [primeiro procedimento](../ide/how-to-create-item-templates.md#export_template) deste tópico mostram como criar um modelo de item usando o assistente **Exportar Modelo**. Se seu modelo for consistir em vários arquivos, consulte [Como criar modelos de item de vários arquivos](../ide/how-to-create-multi-file-item-templates.md).  
  
 O assistente faz grande parte do trabalho para você para criar o modelo básico, mas, em muitos casos, será necessário modificar manualmente o arquivo .vstemplate depois de exportar o modelo. Por exemplo, se você desejar que o item apareça na caixa de diálogo **Adicionar Novo Item** para um projeto do aplicativo [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)], precisará executar algumas etapas adicionais. O [segundo procedimento](../ide/how-to-create-item-templates.md#modify_template) neste tópico o ajudará a realizar essa tarefa.  
 
 Em alguns casos, você pode desejar ou precisar criar um modelo de item manualmente desde o princípio. O [terceiro procedimento](../ide/how-to-create-item-templates.md#create_template) mostra como fazer isso.  
  
 Consulte [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md) para obter informações sobre os elementos que podem ser usados no arquivo .vstemplate.  
  
### <a name="to-add-a-custom-project-item-template-to-the-add-new-item-dialog-box"></a>Para adicionar um modelo de item de projeto personalizado à caixa de diálogo Adicionar Novo Item  
  
1.  Criar ou abrir um projeto no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
2.  Adicionar um item ao projeto e modifique-o, se desejar.  
  
3.  Modifique o arquivo de código para indicar em que ponto a substituição de parâmetro deve ocorrer. Para obter mais informações, consulte [Como substituir parâmetros em um modelo](../ide/how-to-substitute-parameters-in-a-template.md).  
  
4.  No menu **Arquivo**, clique em **Exportar Modelo**.  
  
5.  Clique em **Modelo de Item**, selecione o projeto que contém o item e clique em **Próximo**.  
  
6.  Selecione o item para o qual você deseja criar um modelo e clique em **Próximo**.  
  
7.  Selecione as referências de assembly a incluir no modelo e clique em **Próximo**.  
  
8.  Digite o nome do arquivo de ícone, imagem de visualização, nome do modelo e descrição do modelo, então clique em **Concluir**.  
  
     Os arquivos para o modelo são adicionados a um arquivo .zip e copiados de qualquer diretório que você especificar na caixa de diálogo. O local padrão é a pasta **..\Users\\<nome de usuário\>\Documents\Visual Studio \<Versão>\My Exported Templates\\**.  
  
    > [!WARNING]
    >  Em versões anteriores do Visual Studio, o local padrão é **..\Users\\<nome de usuário\>\Documents\Visual Studio \<Version>\Templates\ItemTemplates**.  
  
### <a name="to-enable-the-item-template-to-be-used-in-a-store-project"></a>Para habilitar o modelo de item a ser usado em um projeto de repositório  
  
1. Siga as etapas no procedimento acima para exportar um modelo de item.  
  
2. Extraia o arquivo .vstemplate do arquivo .zip copiado para a pasta ..\Users\\*username*\Documents\Visual Studio *Version*\Templates\ItemTemplates\ (ou **My Exported Templates**).  
  
3. Abra o arquivo .vstemplate no Visual Studio.  
  
4. Para um projeto C# do repositório do Windows 8.1, no arquivo .vstemplate, adicione o seguinte XML dentro da marcação de abertura e fechamento `<TemplateData>`: `<TemplateGroupID>WinRT-Managed</TemplateGroupID>`.  
  
    Um projeto de repositório C++ Windows 8.1 usa um valor de `WinRT-Native-6.3`. Para Windows 10 e outros tipos de projeto, consulte [Elemento TemplateGroupID (modelos do Visual Studio)](../extensibility/templategroupid-element-visual-studio-templates.md).  
  
    O exemplo a seguir mostra todo o conteúdo de um arquivo .vstemplate após a linha de XML `<TemplateGroupID>WinRT-Managed</TemplateGroupID>` ter sido adicionada a ele. Este exemplo é específico para projetos C#. Você pode modificar os elementos <ProjectTpe> e \< [TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md)> elementos para especificar outros tipos de projeto e linguagem.  
  
   ```xml  
   <VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">  
     <TemplateData>  
       <DefaultName>MyItemStoreTemplate.xaml</DefaultName>  
       <Name>MyItemStoreTemplate</Name>  
       <Description>This is an example itemtemplate</Description>  
       <ProjectType>CSharp</ProjectType>  
       <SortOrder>10</SortOrder>  
       <Icon>__TemplateIcon.ico</Icon>  
       <TemplateGroupID>WinRT-Managed</TemplateGroupID>  
     </TemplateData>  
     <TemplateContent>  
       <References />  
       <ProjectItem SubType="Designer" TargetFileName="$fileinputname$.xaml" ReplaceParameters="true">MyItemTemplate.xaml</ProjectItem>  
       <ProjectItem SubType="Code" TargetFileName="$fileinputname$.xaml.cs" ReplaceParameters="true">MyItemTemplate.xaml.cs</ProjectItem>  
     </TemplateContent>  
   </VSTemplate>  
   ```  
  
    Para outros valores TemplateGroupID possíveis, consulte [Elemento TemplateGroupID (modelos do Visual Studio)](../extensibility/templategroupid-element-visual-studio-templates.md). Para referência completa a .vstemplate, consulte [Referência do esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)  
  
5. No Visual Studio, salve o arquivo .vstemplate e feche-o.  
  
6. Copie e cole o arquivo .vstemplate de volta no arquivo .zip localizado na pasta ..\Users\\*nome de usuário*\Documents\Visual Studio *Versão*\Templates\ItemTemplates\.  
  
    Se a caixa de diálogo **Copiar Arquivo** for exibida, escolha a opção **Copiar e Substituir**.  
  
   Agora você pode adicionar um item com base nesse modelo para um projeto [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] usando a caixa de diálogo **Adicionar Novo Item**.  
  
   Para obter mais informações sobre nomes de parâmetro, consulte [Parâmetros de Modelo](../ide/template-parameters.md).  
  
### <a name="to-enable-templates-for-specific-project-sub-types"></a>Para habilitar modelos para subtipos de projeto específicos  
  
1. O ambiente de desenvolvimento permite que você disponibilize itens de projeto na caixa de diálogo Adicionar Item para determinados projetos. Use esse procedimento para disponibilizar itens personalizados para Windows, Web, Office ou projetos de banco de dados.  
  
    Localize o elemento ProjectType no arquivo .vstemplate para o modelo de item.  
  
    Adicione um elemento [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) imediatamente após o elemento ProjectType.  
  
2. Defina o valor de texto do elemento para um dos seguintes valores:  
  
   1. Windows  
  
   2. Office  
  
   3. Banco de Dados  
  
   4. Web  
  
      Por exemplo: `<ProjectSubType>Database</ProjectSubType>`.  
  
      O exemplo a seguir mostra um modelo de item disponível para projetos do Office.  
  
   ```  
   <VSTemplate Version="2.0.0" Type="Item" Version="2.0.0">  
       <TemplateData>  
           <Name>Class</Name>  
           <Description>An empty class file</Description>  
           <Icon>Class.ico</Icon>  
           <ProjectType>CSharp</ProjectType>  
           <ProjectSubType>Office</ProjectSubType>  
           <DefaultName>Class.cs</DefaultName>  
       </TemplateData>  
       <TemplateContent>  
           <ProjectItem>Class1.cs</ProjectItem>  
       </TemplateContent>  
   </VSTemplate>  
  
   ```  
  
### <a name="to-manually-create-an-item-template-without-using-the-export-template-wizard"></a>Para criar manualmente um modelo de item sem usar o assistente Exportar Modelo  
  
1.  Crie um projeto e um item de projeto.  
  
2.  Modifique o item de projeto até que ele esteja pronto para ser salvo como um modelo.  
  
3.  Conforme apropriado, modifique o arquivo de código para indicar o ponto em que a substituição de parâmetro deve ocorrer. Para obter mais informações sobre substituição de parâmetro, consulte Como substituir parâmetros em um modelo.  
  
4.  Crie um arquivo XML e salve-o usando uma extensão de nome de arquivo .vstemplate no mesmo diretório que o novo modelo de item.  
  
5.  Crie o arquivo XML .vstemplate para fornecer metadados de modelo de item. Para obter mais informações, consulte [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md) e o exemplo na seção anterior.  
  
6.  Salve o arquivo .vstemplate e feche-o.  
  
7.  No Windows Explorer, selecione os arquivos que você deseja incluir em seu modelo, clique com o botão direito do mouse na seleção, clique em Enviar para e, em seguida, clique em Pasta Compactada (zipada). Os arquivos selecionados são compactados em um arquivo .zip.  
  
8.  Copie o arquivo .zip e cole-o no local do modelo de item do usuário. No Visual Studio 2015, o diretório padrão é... \Users\\< nome de usuário\>\Documents\Visual Studio 2015\Templates\ItemTemplates\\. Para obter mais informações, consulte Como localizar e organizar modelos de projeto e item.  
  
## <a name="see-also"></a>Consulte também  
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)   
 [Como criar modelos de item de vários arquivos](../ide/how-to-create-multi-file-item-templates.md)   
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)