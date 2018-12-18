---
title: Localizando os comandos de Menu | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- localize
- localization
- vsct
- menu commands
- localize visual studio
- localize vsct
ms.assetid: b04ee0f6-82ea-47e6-853a-72382267d6da
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6b16771e4d47416f09774ce2f4765de9d6023e94
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51753891"
---
# <a name="localizing-menu-commands"></a>Localizando comandos de menu
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode fornecer o texto localizado para o menu e barra de ferramentas de comandos com a criação de arquivos. VSCT localizada e localizados os arquivos. resx para o VSPackage e, em seguida, atualizar os arquivos de projeto incorporar as alterações.  
  
 Para obter informações sobre como localizar a experiência de instalação, consulte [Localizando os pacotes VSIX](../extensibility/localizing-vsix-packages.md).  
  
## <a name="localizing-command-names"></a>Localizando os nomes de comando  
 Os VSPackages, comandos de menu e botões da barra de ferramentas são definidos no arquivo. VSCT.  
  
1. Na **Gerenciador de soluções**, altere o nome do arquivo. VSCT do *filename*VSCT para *filename*.en US.vsct.  
  
2. Faça uma cópia do *filename*.en-US.vsct para cada idioma de localizado.  
  
    Nome de cada cópia *filename*. *Localidade*VSCT, onde *localidade* é um nome de cultura específica. Para obter uma lista de valores de nome de cultura, consulte [IDs de localidade atribuídas pela Microsoft](https://msdn.microsoft.com/library/windows/apps/jj657969.aspx).  
  
    Eles *filename*. *Localidade*arquivos. VSCT conterá o texto de menu traduzido para o seu pacote.  
  
3. Abra cada *filename*. *Localidade*arquivo. VSCT para localizar o texto.  
  
   1. Modificar a [ButtonText](../extensibility/buttontext-element.md) elemento valores conforme apropriado para o idioma específico.  
  
   2. Se você for fornecer ícones localizadas, modifique a [Bitmap](../extensibility/bitmap-element.md) valores para apontar para os arquivos de destino.  
  
      O exemplo a seguir mostra o texto do botão em inglês e espanhol para abrir uma janela de ferramentas do Gerenciador de árvore da família.  
  
      [FamilyTree.en US.vsct]  
  
   ```xml  
   <Button guid="guidLocalizedPackageCmdSet" id="cmdidFamilyTree" priority="0x0100" type="Button">  
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>  
     <Icon guid="guidImages" id="bmpPic2" />  
     <Strings>  
       <CommandName>cmdidFamilyTree</CommandName>  
       <ButtonText>Family Tree Explorer</ButtonText>  
     </Strings>  
   </Button>  
   ```  
  
    [FamilyTree.es ES.vsct]  
  
   ```xml  
   <Button guid="guidLocalizedPackageCmdSet" id="cmdidFamilyTree" priority="0x0100" type="Button">  
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>  
     <Icon guid="guidImages" id="bmpPic2" />  
     <Strings>  
       <CommandName>cmdidFamilyTree</CommandName>  
       <ButtonText>Explorar el arbol genealogico</ButtonText>  
     </Strings>  
   </Button>  
  
   ```  
  
## <a name="localizing-other-text-resources"></a>Localização de outros recursos de texto  
 Recursos de texto diferentes nomes de comando são definidos em arquivos de recurso (. resx).  
  
1.  Renomeie VSPackage.resx para VSPackage.en resx.  
  
2.  Faça uma cópia do arquivo resx VSPackage.en para cada idioma localizado.  
  
     Nome de cada cópia VSPackage. *Localidade*. resx, onde *localidade* é um nome de cultura específica.  
  
3.  Renomear Resources para resx Resources.  
  
4.  Faça uma cópia do arquivo resx Resources para cada idioma localizado.  
  
     Nome de cada cópia de recursos. *Localidade*. resx, onde *localidade* é um nome de cultura específica.  
  
5.  Abra cada arquivo. resx para modificar os valores de cadeia de caracteres conforme apropriado para o determinado idioma e cultura. O exemplo a seguir mostra a definição de recurso localizado para a barra de título de uma janela de ferramentas.  
  
     [Resources resx]  
  
    ```xml  
    <data name="ToolWindowTitle" xml:space="preserve">  
      <value>Family Tree Explorer</value>  
    </data>  
    ```  
  
     [Es Resources.es]  
  
    ```xml  
    <data name="ToolWindowTitle" xml:space="preserve">  
      <value>Explorador del arbol genealogico</value>  
    </data>  
  
    ```  
  
## <a name="incorporating-localized-resources-into-the-project"></a>Incorporação de recursos localizados no projeto  
 Você deve modificar o arquivo assemblyinfo.cs e o arquivo de projeto para incorporar os recursos localizados.  
  
1.  Do **propriedades** nó no **Gerenciador de soluções**, abra o arquivo assemblyinfo.cs ou AssemblyInfo no editor.  
  
2.  Adicione a seguinte entrada.  
  
    ```csharp  
    [assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]  
    ```  
  
     Isso define o inglês dos EUA como o idioma padrão.  
  
3.  Descarregue o projeto.  
  
4.  Abra o arquivo de projeto no editor.  
  
5.  Localize o `ItemGroup` elemento que contém `EmbeddedResource` elementos.  
  
6.  No `EmbeddedResource` elemento que chama VSPackage.en-resx, substitua o `ManifestResourceName` elemento com um `LogicalName` elemento, definido como `VSPackage.en-US.Resources`, da seguinte maneira.  
  
    ```xml  
    <EmbeddedResource Include="VSPackage.en-US.resx">  
      <MergeWithCTO>true</MergeWithCTO>  
      <LogicalName>VSPackage.en-US.Resources</LogicalName>  
    </EmbeddedResource>  
    ```  
  
7.  Para cada idioma localizado, copie o `EmbeddedResource` elemento para VsPackage.en-US e defina o **Include** atributo e **LogicalName** elemento da cópia para a localidade de destino, conforme mostrado no exemplo a seguir exemplo.  
  
8.  Para cada um localizado `VSCTCompile` elemento, adicione uma `ResourceName` elemento que aponta para `Menus.ctmenu`, conforme mostrado no exemplo a seguir.  
  
    ```xml  
    <ItemGroup>  
      <VSCTCompile Include="LocalizedPackage.es-ES.vsct">  
        <ResourceName>Menus.ctmenu</ResourceName>  
      </VSCTCompile>  
    </ItemGroup>  
    ```  
  
9. Salve o arquivo de projeto e recarregar o projeto.  
  
10. Compile o projeto.  
  
     Isso cria um assembly principal e assemblies de recursos para cada idioma. Para obter informações sobre como localizar o processo de implantação, consulte [Localizando os pacotes VSIX](../extensibility/localizing-vsix-packages.md)  
  
## <a name="see-also"></a>Consulte também  
 [Ampliar Menus e comandos](../extensibility/extending-menus-and-commands.md)   
 [MenuCommands Vs. OleMenuCommands](../misc/menucommands-vs-olemenucommands.md)   
 [Globalização e localização](http://msdn.microsoft.com/library/9a59696b-d89b-45bd-946d-c75da4732d02)

