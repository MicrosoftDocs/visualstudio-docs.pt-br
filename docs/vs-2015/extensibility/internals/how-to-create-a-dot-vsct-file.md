---
title: 'Como: criar um. Arquivo VSCT | Microsoft Docs'
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
- VSCT files, creating
ms.assetid: b955f51c-f9f9-49c3-a8e4-63b6eb0e0341
caps.latest.revision: 20
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: bbfdcf605a1c4346874ec222937a458225788151
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51802623"
---
# <a name="how-to-create-a-vsct-file"></a>Como: criar um. Arquivo VSCT
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Há várias maneiras de criar um arquivo de configuração (. VSCT) de tabela de comando com base em XML Visual Studio.  
  
- Você pode criar um novo VSPackage no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] modelo de pacote.  
  
- Você pode usar o compilador de configuração de tabela do comando baseado em XML, Vsct.exe, para gerar um arquivo de um arquivo. ctc existente.  
  
- Você pode usar Vsct.exe para gerar um arquivo. VSCT de um arquivo CTO já existente.  
  
- Você pode criar manualmente um novo arquivo. VSCT.  
  
  Este tópico explica como criar manualmente um novo arquivo. VSCT.  
  
### <a name="to-manually-create-a-new-vsct-file"></a>Para criar manualmente um novo arquivo. VSCT  
  
1.  Inicie o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
2.  Sobre o **arquivo** , aponte para **New**e, em seguida, clique em **arquivo**.  
  
3.  No **modelos** painel, clique em **arquivo XML** e, em seguida, clique em **abrir**.  
  
4.  Sobre o **modo de exibição** menu, clique em **janela propriedades** para exibir as propriedades do arquivo XML.  
  
5.  No **propriedades** janela, clique no botão Procurar (...) na propriedade de esquemas.  
  
6.  Na lista de esquemas XSD, selecione o esquema de vsct.xsd. Se não estiver na lista, clique em **adicionar** e, em seguida, localize o arquivo em uma unidade local. Clique em **Okey** quando tiver terminado.  
  
7.  No arquivo XML, digite `<CommandTable` e, em seguida, pressione TAB. A marca de fechamento, digitando `>`.  
  
     Isso cria um arquivo. VSCT básica.  
  
8.  Preencha os elementos do arquivo XML que você deseja adicionar, de acordo com o [VSCT esquema](../../extensibility/vsct-xml-schema-reference.md). Para obter mais informações, consulte [criação. Arquivos do VSCT](../../extensibility/internals/authoring-dot-vsct-files.md)  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Simplesmente adicionando um arquivo. VSCT para um projeto não causa compilá-lo. Você deve incorporá-la no processo de compilação.  
  
### <a name="to-add-a-vsct-file-to-project-compilation"></a>Para adicionar um arquivo. VSCT para compilação de projeto  
  
1.  Abra seu arquivo de projeto no editor. Se o projeto é carregado, você deve descarregá-lo pela primeira vez.  
  
2.  Adicionar um [elemento ItemGroup](../../msbuild/itemgroup-element-msbuild.md) que contém um elemento VSCTCompile, conforme mostrado no exemplo a seguir.  
  
    ```xml  
    <ItemGroup>  
      <VSCTCompile Include="TopLevelMenu.vsct">  
        <ResourceName>Menus.ctmenu</ResourceName>  
      </VSCTCompile>  
    </ItemGroup>  
  
    ```  
  
     O elemento ResourceName deve sempre ser definido como `Menus.ctmenu`.  
  
3.  Se seu projeto contém um arquivo. resx, adicione um elemento de EmbeddedResource que contém um elemento MergeWithCTO, conforme mostrado no exemplo a seguir.  
  
    ```xml  
    <EmbeddedResource Include="VSPackage.resx">  
      <MergeWithCTO>true</MergeWithCTO>  
      <ManifestResourceName>VSPackage</ManifestResourceName>  
    </EmbeddedResource>  
  
    ```  
  
     Essa marcação deve ficar dentro do elemento ItemGroup que contém recursos inseridos.  
  
4.  Abra o arquivo de pacote, geralmente chamado *NomeDoProjeto*Package.cs ou *ProjectName*Package.vb no editor.  
  
5.  Adicione um atributo ProvideMenuResource à classe de pacote, conforme mostrado no exemplo a seguir.  
  
    ```csharp  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    ```  
  
     O primeiro valor do parâmetro deve corresponder ao valor do atributo ResourceName definido no arquivo de projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Criação de páginas. Arquivos do VSCT](../../extensibility/internals/authoring-dot-vsct-files.md)   
 [Tabela de comando do Visual Studio (. Arquivos de VSCT)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [Como: criar um. Arquivo VSCT de um existente. Arquivos CTC](../../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-ctc-file.md)   
 [Como: criar um. Arquivo VSCT de um existente. Arquivo CTO](../../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file.md)   
 [Referência do esquema XML do VSCT](../../extensibility/vsct-xml-schema-reference.md)

