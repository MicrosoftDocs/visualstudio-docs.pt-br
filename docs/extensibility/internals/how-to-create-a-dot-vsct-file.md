---
title: 'Como: criar um. Arquivo vsct | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, creating
ms.assetid: b955f51c-f9f9-49c3-a8e4-63b6eb0e0341
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c3155ff69db461e652b11ff6e8ec6d405000244f
ms.sourcegitcommit: 3154387056160bf4c36ac8717a7fdc0cd9faf3f9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78409087"
---
# <a name="how-to-create-a-vsct-file"></a>Como criar um arquivo. vsct

Há várias maneiras de criar um arquivo de configuração de tabela de comando ( *. vsct*) do Visual Studio baseado em XML.

- Você pode criar um novo VSPackage no modelo de pacote [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].

- Você pode usar o compilador de configuração de tabela de comando baseado em XML, *vsct. exe*, para gerar um arquivo de um arquivo *. CTC* existente.

- Você pode usar *vsct. exe* para gerar um arquivo *. vsct* a partir de um arquivo *. CTO* existente.

- Você pode criar manualmente um novo arquivo *. vsct* .

  Este artigo explica como criar um novo arquivo *. vsct* manualmente.

### <a name="to-manually-create-a-new-vsct-file"></a>Para criar manualmente um novo arquivo. vsct

1. Inicie o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].

2. No menu **Arquivo** , aponte para **Novo**e clique em **Arquivo**.

3. No painel **modelos** , clique em **arquivo XML** e, em seguida, clique em **abrir**.

4. No menu **Exibir** , clique em **Propriedades** para exibir as propriedades do arquivo XML.

5. Na janela **Propriedades** , clique no botão **procurar** na propriedade **esquemas** .

6. Na lista de esquemas XSD, selecione o esquema *vsct. xsd* . Se não estiver na lista, clique em **Adicionar** e localize o arquivo em uma unidade local. Clique em **OK** quando terminar.

7. No arquivo XML, digite *< comandotable* e pressione **Tab**. Feche a marca digitando *>* .

    Essa ação cria um arquivo *. vsct* básico.

8. Preencha os elementos do arquivo XML que você deseja adicionar, de acordo com a referência de [esquema XML vsct](../../extensibility/vsct-xml-schema-reference.md). Para obter mais informações, consulte [Author. vsct files](../../extensibility/internals/authoring-dot-vsct-files.md).

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-ctc-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-ctc-file"></a>Como: criar um arquivo. vsct de um arquivo. CTC existente

Você pode criar um arquivo *. vsct* baseado em XML de um arquivo de origem *. CTC* de tabela de comandos existente. Ao fazer isso, você pode aproveitar o novo formato de compilador VSCT (tabela de comandos de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]) baseado em XML.

### <a name="to-create-a-vsct-file-from-a-ctc-file"></a>Para criar um arquivo. vsct de um arquivo. CTC

1. Obtenha uma cópia da linguagem Perl.

2. Obtenha uma cópia do script Perl *ConvertCTCToVSCT.pl*, normalmente localizada no caminho de *instalação do SDK do\<Visual Studio > pasta \VisualStudioIntegration\Tools\bin* .

3. Obtenha uma cópia do arquivo de origem *. CTC* que você deseja converter.

4. Coloque os arquivos no mesmo diretório.

5. Na janela do prompt de comando do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], navegue até o diretório.

6. Type

   ```
   perl.exe ConvertCTCtoVSCT.pl PkgCmd.ctc PkgCmd.vsct
   ```

    em que *PkgCmd. CTC* é o nome do arquivo *. CTC* e *PkgCmd. vsct* é o nome do arquivo *. vsct* que você deseja criar.

    Essa ação cria um novo arquivo de origem de tabela de comandos XML *. vsct* . Você pode compilar o arquivo usando *vsct. exe*, o compilador vsct, como faria com qualquer outro arquivo *. vsct* .

   > [!NOTE]
   > Você pode melhorar a legibilidade do arquivo *. vsct* Reformatando os comentários XML.

<a name="how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file"></a>

## <a name="how-to-create-a-vsct-file-from-an-existing-cto-file"></a>Como: criar um arquivo. vsct de um arquivo. CTO existente

Você pode criar um arquivo *. vsct* baseado em XML de um arquivo binário *. CTO* existente. Isso permite que você aproveite o novo formato de compilador de tabela de comando. Esse processo funciona mesmo que o arquivo *. CTO* tenha sido compilado a partir de um arquivo *. CTC* . Você pode editar e compilar o arquivo *. vsct* em outro arquivo. CTO.

### <a name="to-create-a-vsct-file-from-a-cto-file"></a>Para criar um arquivo. vsct de um arquivo. CTO

1. Obtenha cópias do arquivo *. CTO* e seu arquivo *. ctsym* correspondente.

2. Coloque os arquivos no mesmo diretório que o compilador *vsct. exe* .

3. No prompt de comando do Visual Studio, vá para o diretório que contém os arquivos *. CTO* e *. ctsym* .

4. Type

    ```
    vsct.exe <ctofilename>.cto <vsctfilename>.vsct -S<symfilename>.ctsym
    ```

     em que \<ctofilename\> é o nome do arquivo *. CTO* , \<vsctfilename\> é o nome do arquivo *. vsct* que você deseja criar e \<symfilename\> é o nome do arquivo *. ctsym* .

     Esse processo cria um novo arquivo de compilador de tabela de comandos XML *. vsct* . Você pode editar e compilar o arquivo com *vsct. exe*, o compilador vsct, como faria com qualquer outro arquivo *. vsct* .

## <a name="compile-the-code"></a>Compilar o código
 Simplesmente adicionar um arquivo *. vsct* a um projeto não faz com que ele seja compilado. Você deve incorporá-lo no processo de compilação.

### <a name="to-add-a-vsct-file-to-project-compilation"></a>Para adicionar um arquivo. vsct à compilação do projeto

1. Abra o arquivo de projeto no editor. Se o projeto for carregado, você deverá descarregá-lo primeiro.

2. Adicione um [elemento do grupo](../../msbuild/itemgroup-element-msbuild.md) de itens que contém um elemento `VSCTCompile`, conforme mostrado no exemplo a seguir.

    ```xml
    <ItemGroup>
      <VSCTCompile Include="TopLevelMenu.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>

    ```

     O elemento `ResourceName` sempre deve ser definido como `Menus.ctmenu`.

3. Se o seu projeto contiver um arquivo *. resx* , adicione um elemento `EmbeddedResource` que contém um elemento `MergeWithCTO`, conforme mostrado no exemplo a seguir:

    ```xml
    <EmbeddedResource Include="VSPackage.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <ManifestResourceName>VSPackage</ManifestResourceName>
    </EmbeddedResource>

    ```

     Essa marcação deve estar dentro do elemento `ItemGroup` que contém recursos incorporados.

4. Abra o arquivo de pacote, geralmente denominado *\<ProjectName\>Package.cs* ou *\<ProjectName\>Package. vb*, no editor.

5. Adicione um atributo `ProvideMenuResource` à classe de pacote, conforme mostrado no exemplo a seguir.

    ```csharp
    [ProvideMenuResource("Menus.ctmenu", 1)]
    ```

     O primeiro valor do parâmetro deve corresponder ao valor do atributo `ResourceName` que você definiu no arquivo de projeto.

## <a name="see-also"></a>Confira também
- [Arquivos Author. vsct](../../extensibility/internals/authoring-dot-vsct-files.md)
- [Arquivos de tabela de comando do Visual Studio (. vsct)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [Referência de esquema XML VSCT](../../extensibility/vsct-xml-schema-reference.md)