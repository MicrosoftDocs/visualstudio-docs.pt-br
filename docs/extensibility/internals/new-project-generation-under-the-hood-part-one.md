---
title: 'Nova geração de projeto: nos bastidores, parte um | Microsoft Docs'
description: Veja detalhadamente o que acontece no IDE (ambiente de desenvolvimento integrado) do Visual Studio enquanto você cria seu próprio tipo de projeto (parte 1 de 2).
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 66778698-0258-467d-8b8b-c351744510eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 27a7e0f3175388b963e85950ea903843caff3baa
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063143"
---
# <a name="new-project-generation-under-the-hood-part-one"></a>Geração de novo projeto: Bastidores, parte um
Já pensou em como criar seu próprio tipo de projeto? Imaginando o que realmente acontece quando você cria um novo projeto? Vamos examinar os bastidores e ver o que realmente está acontecendo.

 Há várias tarefas que o Visual Studio coordena para você:

- Ele exibe uma árvore de todos os tipos de projeto disponíveis.

- Ele exibe uma lista de modelos de aplicativo para cada tipo de projeto e permite que você escolha um.

- Ele coleta informações do projeto para o aplicativo, como nome do projeto e caminho.

- Ele passa essas informações para a fábrica de projetos.

- Ele gera itens de projeto e pastas na solução atual.

## <a name="the-new-project-dialog-box"></a>A caixa de diálogo novo projeto
 Tudo começa quando você seleciona um tipo de projeto para um novo projeto. Vamos começar clicando em **novo projeto** no menu **arquivo** . A caixa de diálogo **novo projeto** é exibida, semelhante a:

 ![Captura de tela da caixa de diálogo Novo Projeto.](../../extensibility/internals/media/newproject.gif)

 Vamos analisar com mais detalhes. A árvore de **tipos de projeto** lista os vários tipos de projeto que você pode criar. Ao selecionar um tipo de projeto como o **Visual C# Windows**, você verá uma lista de modelos de aplicativo para começar. Os **modelos instalados do Visual Studio** são instalados pelo Visual Studio e estão disponíveis para qualquer usuário do seu computador. Novos modelos que você cria ou coleta podem ser adicionados aos **meus modelos** e estão disponíveis apenas para você.

 Quando você seleciona um modelo como **aplicativo do Windows**, uma descrição do tipo de aplicativo é exibida na caixa de diálogo; Nesse caso, **um projeto para criar um aplicativo com uma interface de usuário do Windows**.

 Na parte inferior da caixa de diálogo **novo projeto** , você verá vários controles que coletam mais informações. Os controles que você vê dependem do tipo de projeto, mas geralmente incluem uma caixa de texto **nome** do projeto, uma caixa de texto de **local** e um botão **procurar** relacionado e uma caixa de texto **nome da solução** e caixa **de seleção criar diretório relacionado para solução** .

## <a name="populating-the-new-project-dialog-box"></a>Populando a caixa de diálogo novo projeto
 De onde a caixa de diálogo **novo projeto** obtém suas informações? Há dois mecanismos em funcionamento aqui, um deles preteridos. A caixa de diálogo **novo projeto** combina e exibe as informações obtidas de ambos os mecanismos.

 O método mais antigo (preterido) usa entradas de registro do sistema e arquivos. VSDir. Esse mecanismo é executado quando o Visual Studio é aberto. O método mais recente usa arquivos. vstemplate. Esse mecanismo é executado quando o Visual Studio é inicializado, por exemplo, executando

```
devenv /setup
```

 ou

```
devenv /installvstemplates
```

### <a name="project-types"></a>Tipos de projeto
 A posição e os nomes dos nós raiz de **tipos de projeto** , como o **Visual C#** e **outras linguagens**, são determinados pelas entradas do registro do sistema. A organização dos nós filho, como banco de **dados** e **dispositivo inteligente**, espelha a hierarquia das pastas que contêm os arquivos. vstemplate correspondentes. Primeiro, vamos examinar os nós raiz.

#### <a name="project-type-root-nodes"></a>Nós raiz do tipo de projeto
 Quando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] é inicializado, ele atravessa as subchaves da chave do registro do sistema HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\NewProjectTemplates\TemplateDirs para criar e nomear os nós raiz da árvore de **tipos de projeto** . Essas informações são armazenadas em cache para uso posterior. Examine a chave TemplateDirs \\ {FAE04EC1-301F-11D3-BF4B-00C04F79EFBC} \\ /1. Cada entrada é um GUID VSPackage. O nome da subchave (/1) é ignorado, mas sua presença indica que se trata de um nó raiz de **tipos de projeto** . Um nó raiz pode, por sua vez, ter várias subchaves que controlam sua aparência na árvore de **tipos de projeto** . Vamos dar uma olhada em alguns deles.

##### <a name="default"></a>(Padrão)
 Essa é a ID de recurso da cadeia de caracteres localizada que nomeia o nó raiz. O recurso de cadeia de caracteres está localizado na DLL satélite selecionada pelo GUID VSPackage.

 No exemplo, o GUID VSPackage é

 {FAE04EC1-301F-11D3-BF4B-00C04F79EFBC}

 e a ID do recurso (valor padrão) do nó raiz (/1) é #2345

 Se você pesquisar o GUID na chave pacotes próximos e examinar a subchave SatelliteDll, poderá encontrar o caminho do assembly que contém o recurso de cadeia de caracteres:

 \<Visual Studio installation path>\VC # \VCSPackages\1033\csprojui.dll

 Para verificar isso, abra o explorador de arquivos e arraste csprojui.dll para o diretório do Visual Studio. A tabela de cadeia de caracteres mostra que #2345 de recursos tem a legenda **Visual C#**.

##### <a name="sortpriority"></a>SortPriority
 Isso determina a posição do nó raiz na árvore de **tipos de projeto** .

 SortPriority REG_DWORD 0x00000014 (20)

 Quanto menor o número da prioridade, maior a posição na árvore.

##### <a name="developeractivity"></a>DeveloperActivity
 Se essa subchave estiver presente, a posição do nó raiz será controlada pela caixa de diálogo Configurações do desenvolvedor. Por exemplo,

 VC de REG_SZ DeveloperActivity #

 indica que o Visual C# será um nó raiz se o Visual Studio estiver definido para [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] desenvolvimento. Caso contrário, será um nó filho de **outras linguagens**.

##### <a name="folder"></a>Pasta
 Se essa subchave estiver presente, o nó raiz se tornará um nó filho da pasta especificada. Uma lista de pastas possíveis aparece sob a chave

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\11.0\NewProjectTemplates\PseudoFolders

 Por exemplo, a entrada projetos de banco de dados tem uma chave de pasta que corresponde à entrada de outros tipos de projeto em PseudoFolders. Portanto, na árvore de **tipos de projeto** , os projetos de banco de **dados** serão um nó filho de **outros tipos de projeto**.

#### <a name="project-type-child-nodes-and-vstdir-files"></a>Nós filho do tipo de projeto e arquivos. vstdir
 A posição dos nós filho na árvore de **tipos de projeto** segue a hierarquia das pastas nas pastas ProjectTemplates. Para modelos de máquina (**modelos instalados do Visual Studio**), o local típico é \Program Files\Microsoft Visual Studio 14.0 \ Common7\IDE\ProjectTemplates\ e para modelos de usuário (**meus modelos**), o local típico é \Meus Documentos\visual Studio 14.0 \ Templates\ProjectTemplates \\ . As hierarquias de pastas desses dois locais são mescladas para criar a árvore de **tipos de projeto** .

 Para o Visual Studio com configurações de desenvolvedor de C#, a árvore de **tipos de projeto** é semelhante a esta:

 ![Captura de tela da árvore de pastas de tipos de projeto no Visual Studio com configurações de desenvolvedor de C#.](../../extensibility/internals/media/projecttypes.png)

 A pasta ProjectTemplates correspondente é parecida com esta:

 ![Captura de tela da árvore de pastas de modelos de projeto no Visual Studio com configurações de desenvolvedor de C#.](../../extensibility/internals/media/projecttemplates.png)

 Quando a caixa de diálogo **novo projeto** é aberta, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] percorre a pasta ProjectTemplates e recria sua estrutura na árvore de **tipos de projeto** com algumas alterações:

- O nó raiz na árvore de **tipos de projeto** é determinado pelo modelo de aplicativo.

- O nome do nó pode ser localizado e pode conter caracteres especiais.

- A ordem de classificação pode ser alterada.

##### <a name="finding-the-root-node-for-a-project-type"></a>Localizando o nó raiz para um tipo de projeto
 Quando o Visual Studio percorre as pastas ProjectTemplates, ele abre todos os arquivos. zip e extrai todos os arquivos. vstemplate. Um arquivo. vstemplate usa XML para descrever um modelo de aplicativo. Para obter mais informações, consulte [nova geração de projeto: nos bastidores, parte dois](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md).

 A \<ProjectType> marca determina o tipo de projeto para o aplicativo. Por exemplo, o arquivo de \CSharp\SmartDevice\WindowsCE\1033\WindowsCE-EmptyProject.zip contém um arquivo EmptyProject. vstemplate que tem esta marca:

```
<ProjectType>CSharp</ProjectType>
```

 A \<ProjectType> marca, e não a subpasta na pasta ProjectTemplates, determina o nó raiz de um aplicativo na árvore de **tipos de projeto** . No exemplo, Windows CE aplicativos apareceriam sob o nó raiz do **Visual C#** e, mesmo que você fosse mover a pasta WindowsCE para a pasta VisualBasic, Windows CE aplicativos ainda apareceriam sob o nó raiz do **Visual C#** .

##### <a name="localizing-the-node-name"></a>Localizando o nome do nó
 Quando o Visual Studio percorre as pastas ProjectTemplates, ele examina todos os arquivos. vstdir encontrados. Um arquivo. vstdir é um arquivo XML que controla a aparência do tipo de projeto na caixa de diálogo **novo projeto** . No arquivo. vstdir, use a \<LocalizedName> marca para nomear o nó **tipos de projeto** .

 Por exemplo, o arquivo \CSharp\Database\TemplateIndex.vstdir contém esta marca:

```
<LocalizedName Package="{462b036f-7349-4835-9e21-bec60e989b9c}" ID="4598"/>
```

 Isso determina a DLL satélite e a ID de recurso da cadeia de caracteres localizada que nomeia o nó raiz, nesse caso, **banco de dados**. O nome localizado pode conter caracteres especiais que não estão disponíveis para nomes de pastas, como **.net**.

 Se nenhuma \<LocalizedName> marca estiver presente, o tipo de projeto será nomeado pela própria pasta, **SmartPhone2003**.

##### <a name="finding-the-sort-order-for-a-project-type"></a>Localizando a ordem de classificação para um tipo de projeto
 Para determinar a ordem de classificação do tipo de projeto, os arquivos. vstdir usam a \<SortOrder> marca.

 Por exemplo, o arquivo \CSharp\Windows\Windows.vstdir contém esta marca:

```
<SortOrder>5</SortOrder>
```

 O arquivo \CSharp\Database\TemplateIndex.vstdir tem uma marca com um valor maior:

```
<SortOrder>5000</SortOrder>
```

 Quanto menor o número na \<SortOrder> marca, maior a posição na árvore, de modo que o nó do **Windows** aparece mais alto do que o nó do **banco de dados** na árvore de **tipos de projeto** .

 Se nenhuma \<SortOrder> marca for especificada para um tipo de projeto, ela aparecerá em ordem alfabética após qualquer tipo de projeto que contenha \<SortOrder> especificações.

 Observe que não há arquivos. vstdir nas pastas meus documentos (**meus modelos**). Os nomes de tipo de projeto de aplicativo do usuário não são localizados e aparecem em ordem alfabética.

#### <a name="a-quick-review"></a>Uma revisão rápida
 Vamos modificar a caixa de diálogo **novo projeto** e criar um novo modelo de projeto de usuário.

1. Adicione uma subpasta MyProjectNode à pasta \Program Files\Microsoft Visual Studio 14.0 \ Common7\IDE\ProjectTemplates\CSharp.

2. Crie um arquivo myproject. vstdir na pasta MyProjectNode usando qualquer editor de texto.

3. Adicione essas linhas ao arquivo. vstdir:

   ```
   <TemplateDir Version="1.0.0">
       <SortOrder>6</SortOrder>
   </TemplateDir>
   ```

4. Salve e feche o arquivo. vstdir.

5. Crie um arquivo myproject. vstemplate na pasta MyProjectNode usando qualquer editor de texto.

6. Adicione essas linhas ao arquivo. vstemplate:

   ```
   <VSTemplate Version="2.0.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
       <TemplateData>
           <ProjectType>CSharp</ProjectType>
       </TemplateData>
   </VSTemplate>
   ```

7. Salve o arquivo. vstemplate e feche o editor.

8. Envie o arquivo. vstemplate para uma nova pasta MyProjectNode\MyProject.zip compactada.

9. Na janela de comando do Visual Studio, digite:

    ```
    devenv /installvstemplates
    ```

   Abra o Visual Studio.

10. Abra a caixa de diálogo **novo projeto** e expanda o nó do projeto do **Visual C#** .

    ![Captura de tela da árvore de pastas de tipos de projeto na caixa de diálogo novo projeto com MyProjectNode realçado no nó de projeto expandido do Visual C#.](../../extensibility/internals/media/myprojectnode.png)

    **MyProjectNode** aparece como um nó filho do Visual C# logo abaixo do nó Windows.

## <a name="see-also"></a>Confira também
- [Geração de novo projeto: Bastidores, parte dois](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)
