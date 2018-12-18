---
title: 'Como: criar um. Arquivo VSCT | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, creating
ms.assetid: b955f51c-f9f9-49c3-a8e4-63b6eb0e0341
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 612ad5668ebb1033ef07dcad1fc07030d78e1643
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49921204"
---
# <a name="how-to-create-a-vsct-file"></a>Como: criar um arquivo. VSCT  
  
Há várias maneiras para criar uma configuração de tabela do comando baseado em XML Visual Studio (*VSCT*) arquivos.  
  
- Você pode criar um novo VSPackage no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] modelo de pacote.  
  
- Você pode usar o compilador de configuração da tabela de comando baseado em XML, *Vsct.exe*para gerar um arquivo de uma já existente *. ctc* arquivo.  
  
- Você pode usar *Vsct.exe* para gerar um *VSCT* arquivo de uma já existente *CTO já* arquivo.  
  
- Você pode criar manualmente um novo *VSCT* arquivo.  
  
  Este artigo explica como criar manualmente um novo *VSCT* arquivo.  
  
### <a name="to-manually-create-a-new-vsct-file"></a>Para criar manualmente um novo arquivo. VSCT  
  
1. Inicie o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
2. Sobre o **arquivo** , aponte para **New**e, em seguida, clique em **arquivo**.  
  
3. No **modelos** painel, clique em **arquivo XML** e, em seguida, clique em **abrir**.  
  
4. Sobre o **modo de exibição** menu, clique em **propriedades** para exibir as propriedades do arquivo XML.  
  
5. No **propriedades** janela, clique no **procurar** botão o **esquemas** propriedade.  
  
6. Na lista de esquemas XSD, selecione a *vsct.xsd* esquema. Se não estiver na lista, clique em **adicionar** e, em seguida, localize o arquivo em uma unidade local. Clique em **Okey** quando tiver terminado.  
  
7. No arquivo XML, digite *< CommandTable* e, em seguida, pressione **guia**. A marca de fechamento ao digitar *>*.  
  
    Essa ação cria um basic *VSCT* arquivo.  
  
8. Preencha os elementos do arquivo XML que você deseja adicionar, de acordo com o [referência de esquema XML do VSCT](../../extensibility/vsct-xml-schema-reference.md). Para obter mais informações, consulte [criar arquivos. VSCT](../../extensibility/internals/authoring-dot-vsct-files.md)  
  
<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-ctc-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-ctc-file"></a>Como: criar um arquivo. VSCT de um arquivo. ctc existente  
  
Você pode criar um XML com base em *VSCT* arquivo de uma tabela existente do comando *. ctc* arquivo de origem. Ao fazer isso, você pode tirar proveito do novo com base em XML [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] formato de compilador de tabela (VSCT) do comando.  
  
### <a name="to-create-a-vsct-file-from-a-ctc-file"></a>Para criar um arquivo. VSCT de um arquivo. ctc  
  
1. Obtenha uma cópia da linguagem Perl.  
  
2. Obter uma cópia do script Perl *ConvertCTCToVSCT.pl*, normalmente localizado na  *\<caminho de instalação do SDK do Visual Studio > \VisualStudioIntegration\Tools\bin* pasta.  
  
3. Obtenha uma cópia do *. ctc* arquivo de origem que você deseja converter.  
  
4. Coloque os arquivos no mesmo diretório.  
  
5. No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] janela de prompt de comando, navegue até o diretório.  
  
6. Tipo  
  
   ```  
   perl.exe ConvertCTCtoVSCT.pl PkgCmd.ctc PkgCmd.vsct  
   ```  
  
    em que *PkgCmd.ctc* é o nome da *. ctc* arquivo e *PkgCmd.vsct* é o nome da *VSCT* arquivo que você deseja criar.  
  
    Essa ação cria um novo *VSCT* arquivo XML de origem de tabela de comando. Você pode compilar o arquivo usando *Vsct.exe*, o compilador VSCT, como você faria com qualquer outro *VSCT* arquivo.  
  
   > [!NOTE]
   >  Você pode melhorar a legibilidade do *VSCT* reformatar os comentários XML o arquivo.  
  
<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-cto-file"></a>Como: criar um arquivo. VSCT de um arquivo CTO já existente  
  
Você pode criar um XML com base em *VSCT* arquivo de um binário existente *CTO já* arquivo. Isso permite aproveitar o novo formato de compilador de tabela do comando. Esse processo funciona mesmo se o *CTO já* arquivo foi compilado a partir de um *. ctc* arquivo. Você pode editar e compilar o *VSCT* arquivo em outro arquivo CTO já.  
  
### <a name="to-create-a-vsct-file-from-a-cto-file"></a>Para criar um arquivo. VSCT de um arquivo CTO já  
  
1.  Obter cópias do *CTO já* arquivo e correspondente *.ctsym* arquivo.  
  
2.  Coloque os arquivos no mesmo diretório que o *vsct.exe* compilador.  
  
3.  No prompt de comando do Visual Studio, vá para o diretório que contém o *CTO já* e *.ctsym* arquivos.  
  
4.  Tipo  

    ```
    vsct.exe <ctofilename>.cto <vsctfilename>.vsct -S<symfilename>.ctsym
    ```

     em que \<ctofilename\> é o nome da *CTO já* arquivo, \<vsctfilename\> é o nome da *VSCT* arquivo você deseja criar e \<symfilename\> é o nome da *.ctsym* arquivo.  
  
     Esse processo cria uma nova *VSCT* arquivo de compilador de tabela de comandos XML. Você pode editar e compilar o arquivo com *vsct.exe*, o compilador vsct, como você faria com qualquer outro *VSCT* arquivo.  
  
## <a name="compile-the-code"></a>Compilar o código  
 Simplesmente adicionando um *VSCT* arquivo a um projeto não causa compilá-lo. Você deve incorporá-la no processo de compilação.  
  
### <a name="to-add-a-vsct-file-to-project-compilation"></a>Para adicionar um arquivo. VSCT para compilação de projeto  
  
1.  Abra seu arquivo de projeto no editor. Se o projeto é carregado, você deve descarregá-lo pela primeira vez.  
  
2.  Adicionar um [elemento ItemGroup](../../msbuild/itemgroup-element-msbuild.md) que contém um `VSCTCompile` elemento, conforme mostrado no exemplo a seguir.  
  
    ```xml  
    <ItemGroup>  
      <VSCTCompile Include="TopLevelMenu.vsct">  
        <ResourceName>Menus.ctmenu</ResourceName>  
      </VSCTCompile>  
    </ItemGroup>  
  
    ```  
  
     O `ResourceName` elemento deve sempre ser definido como `Menus.ctmenu`.  
  
3.  Se o projeto contiver uma *. resx* do arquivo, adicione uma `EmbeddedResource` elemento que contém um `MergeWithCTO` elemento, conforme mostrado no exemplo a seguir:  
  
    ```xml  
    <EmbeddedResource Include="VSPackage.resx">  
      <MergeWithCTO>true</MergeWithCTO>  
      <ManifestResourceName>VSPackage</ManifestResourceName>  
    </EmbeddedResource>  
  
    ```  
  
     Essa marcação deve ficar dentro de `ItemGroup` elemento que contém recursos inseridos.  
  
4.  Abra o arquivo de pacote, geralmente chamado  *\<ProjectName\>Package.cs* ou  *\<ProjectName\>Package.vb*, no editor.  
  
5.  Adicionar um `ProvideMenuResource` atributo à classe de pacote, conforme mostrado no exemplo a seguir.  
  
    ```csharp  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    ```  
  
     O primeiro valor do parâmetro deve corresponder ao valor da `ResourceName` atributo definido no arquivo de projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos. VSCT de autor](../../extensibility/internals/authoring-dot-vsct-files.md)   
 [Arquivos de tabela (. VSCT) de comando do Visual Studio](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [Referência de esquema XML do VSCT](../../extensibility/vsct-xml-schema-reference.md)