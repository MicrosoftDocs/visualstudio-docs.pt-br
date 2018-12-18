---
title: Localizando os comandos de Menu | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- localize
- localization
- vsct
- menu commands
- localize visual studio
- localize vsct
ms.assetid: b04ee0f6-82ea-47e6-853a-72382267d6da
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c8eb9e566f4f5916961a95a1c61f8fdcbb689f1e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49876211"
---
# <a name="localize-menu-commands"></a>Localizar os comandos de menu
Você pode fornecer o texto localizado para comandos de menu e barra de ferramentas criando localizada *VSCT* localizadas e arquivos *. resx* arquivos para o VSPackage e, em seguida, atualizar os arquivos de projeto incorporar o alterações.  
  
 Para obter informações sobre como localizar a experiência de instalação, consulte [pacotes VSIX localizar](../extensibility/localizing-vsix-packages.md).  
  
## <a name="localize-command-names"></a>Localizar nomes de comando  
 Em VSPackages, comandos de menu e botões da barra de ferramentas são definidos na *VSCT* arquivo.  
  
1. Na **Gerenciador de soluções**, altere o nome da *. VSCT* arquivo da *filename.vsct* para *filename.en US.vsct*.  
  
2. Faça uma cópia do *filename.en US.vsct* para cada idioma localizado.  
  
    Nome de cada cópia *filename. { Localidade} VSCT*, onde *{localidade}* é um nome de cultura específica. Para obter uma lista de valores de nome de cultura, consulte [IDs de localidade atribuídas pela Microsoft](/windows/uwp/publish/supported-languages).  
  
    Eles *filename. Locale.VSCT* arquivos conterá o texto de menu traduzido para o seu pacote.  
  
3. Abra cada *filename. Locale.VSCT* arquivo para localizar o texto.  
  
   1. Modificar a [ButtonText](../extensibility/buttontext-element.md) elemento valores conforme apropriado para o idioma específico.  
  
   2. Se você for fornecer ícones localizadas, modifique a [Bitmap](../extensibility/bitmap-element.md) valores para apontar para os arquivos de destino.  
  
      O exemplo a seguir mostra o texto do botão em inglês e espanhol para abrir uma janela de ferramentas do Gerenciador de árvore da família.  
  
      [*FamilyTree.en US.vsct*]  
  
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
  
    [*FamilyTree.es ES.vsct*]  
  
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
  
## <a name="localize-other-text-resources"></a>Localizar outros recursos de texto  
 Recursos de texto diferentes nomes de comando são definidos no recurso (*. resx*) arquivos.  
  
1.  Renomeie *VSPackage.resx* à *VSPackage.en resx*.  
  
2.  Faça uma cópia do *VSPackage.en resx* idioma localizado do arquivo para cada um.  
  
     Nome de cada cópia *VSPackage. { Localidade} resx*, onde *{localidade}* é um nome de cultura específica.  
  
3.  Renomeie *Resources* à *Resources resx*.  
  
4.  Faça uma cópia do *Resources resx* idioma localizado do arquivo para cada um.  
  
     Nome de cada cópia *recursos. { Localidade} resx*, onde *{localidade}* é um nome de cultura específica.  
  
5.  Abra cada *. resx* arquivo para modificar a cadeia de caracteres de valores conforme apropriado para o determinado idioma e cultura. O exemplo a seguir mostra a definição de recurso localizado para a barra de título de uma janela de ferramentas.  
  
     [*Resources resx*]  
  
    ```xml  
    <data name="ToolWindowTitle" xml:space="preserve">  
      <value>Family Tree Explorer</value>  
    </data>  
    ```  
  
     [*Resources.es ES*]  
  
    ```xml  
    <data name="ToolWindowTitle" xml:space="preserve">  
      <value>Explorador del arbol genealogico</value>  
    </data>  
  
    ```  
  
## <a name="incorporate-localized-resources-into-the-project"></a>Incorporar recursos localizados do projeto  
 Você deve modificar o *assemblyinfo.cs* arquivo e o arquivo de projeto para incorporar os recursos localizados.  
  
1.  Dos **propriedades** nó no **Gerenciador de soluções**, abra *assemblyinfo.cs* ou *AssemblyInfo* no editor.  
  
2.  Adicione a seguinte entrada.  
  
    ```csharp  
    [assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]  
    ```  
  
     Isso define o inglês dos EUA como o idioma padrão.  
  
3.  Descarregue o projeto.  
  
4.  Abra o arquivo de projeto no editor.  
  
5.  Localize o `ItemGroup` elemento que contém `EmbeddedResource` elementos.  
  
6.  No `EmbeddedResource` elemento que chama *VSPackage.en resx*, substitua o `ManifestResourceName` elemento com um `LogicalName` elemento, definido como `VSPackage.en-US.Resources`, da seguinte maneira.  
  
    ```xml  
    <EmbeddedResource Include="VSPackage.en-US.resx">  
      <MergeWithCTO>true</MergeWithCTO>  
      <LogicalName>VSPackage.en-US.Resources</LogicalName>  
    </EmbeddedResource>  
    ```  
  
7.  Para cada idioma localizado, copie o `EmbeddedResource` elemento para `VsPackage.en-US`e defina as **Include** atributo e **LogicalName** elemento da cópia para a localidade de destino, conforme mostrado no exemplo a seguir exemplo.  
  
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
  
     Isso cria um assembly principal e assemblies de recursos para cada idioma. Para obter informações sobre como localizar o processo de implantação, consulte [pacotes VSIX localizar](../extensibility/localizing-vsix-packages.md)  
  
## <a name="see-also"></a>Consulte também  
 [Ampliar menus e comandos](../extensibility/extending-menus-and-commands.md)   
 [MenuCommands vs. OleMenuCommands](../extensibility/menucommands-vs-olemenucommands.md)   
 [Globalizar e localizar aplicativos](../ide/globalizing-and-localizing-applications.md)