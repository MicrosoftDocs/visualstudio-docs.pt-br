---
title: Adicionar referências no Gerenciador de Referências
ms.date: 08/02/2019
ms.topic: how-to
f1_keywords:
- VS.ReferenceManager
helpviewer_keywords:
- C# projects, references
- references [Visual Studio], adding
- assemblies [Visual Studio], references
- Visual Basic projects, references
- project references, adding
- referencing components, adding references
- project references, removing
- referencing assemblies
- referencing components, removing references
- references [Visual Studio], removing
- referencing components, assemblies not listed
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5f67c41f860417a27a6003a19672d4cd617d37a6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284720"
---
# <a name="how-to-add-or-remove-references-by-using-the-reference-manager"></a>Como adicionar ou remover referências usando o Gerenciador de Referências

É possível usar a caixa de diálogo Gerenciador de Referências para adicionar e gerenciar referências aos componentes que você, a Microsoft ou outra empresa desenvolveram. Se você estiver desenvolvendo um aplicativo Universal do Windows, o projeto referenciará automaticamente todas as DLLs corretas do SDK do Windows. Se você estiver desenvolvendo um aplicativo .NET, seu projeto fará referência automaticamente *mscorlib.dll*. Algumas APIs do .NET são expostas em componentes que precisam ser adicionados manualmente. As referências a componentes COM ou a componentes personalizados devem ser adicionadas manualmente.

## <a name="reference-manager-dialog-box"></a>Caixa de diálogo Gerenciador de Referências

A caixa de diálogo Gerenciador de Referências mostra diferentes categorias à esquerda, dependendo do tipo de projeto:

- **Assemblies**, com os subgrupos **Estrutura** e **Extensões**

- **COM** lista todos os componentes COM disponíveis para referência

- **Projeto**

- **Projetos compartilhados**

- **Windows**, com os subgrupos **Core** e **Extensões**. É possível explorar as referências no SDK do Windows ou nos SDKs de extensão usando o **Pesquisador de Objetos**.

- **Procurar**, com o subgrupo **Recente**

## <a name="add-a-reference"></a>Adicionar uma referência

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó **Referências** ou **Dependências** e escolha **Adicionar Referência**. Você também pode clicar com o botão direito do mouse no nó do projeto e selecionar **Adicionar**  >  **referência**.

   O **Gerenciador de Referências** é aberto e lista as referências disponíveis por grupo.

2. Especifique as referências a serem adicionadas e selecione **OK**.

## <a name="assemblies-tab"></a>Guia Assemblies

A guia **Assemblies** lista todos os assemblies .NET que estão disponíveis para referência. A guia **Assemblies** não lista os assemblies do GAC (cache de assembly global), pois os assemblies no GAC fazem parte do ambiente de tempo de execução. Se você implantar ou copiar um aplicativo que contém uma referência a um assembly registrado no GAC, o assembly não será implantado nem copiado com o aplicativo, independentemente da configuração **local de cópia** . Para obter mais informações, consulte [Gerenciar referências em um projeto](../ide/managing-references-in-a-project.md).

Ao adicionar uma referência manualmente a qualquer namespace EnvDTE (<xref:EnvDTE>, <xref:EnvDTE80>, <xref:EnvDTE90>, <xref:EnvDTE90a> ou <xref:EnvDTE100>), defina a propriedade **Inserir Tipos de Interoperabilidade** da referência como **Falso** na janela **Propriedades**. Definir essa propriedade como **true** pode causar problemas de compilação devido a determinadas propriedades EnvDTE que não podem ser inseridas.

Todos os projetos de área de trabalho contêm uma referência implícita ao **mscorlib**. Os projetos do Visual Basic contêm uma referência implícita a <xref:Microsoft.VisualBasic>. Todos os projetos contêm uma referência implícita a **System.Core**, mesmo se ela for removida da lista de referências.

Se um tipo de projeto não der suporte a assemblies, a guia não será exibida na caixa de diálogo Gerenciador de Referências.

A guia **assemblies** consiste em duas subguias:

1. A **estrutura** lista todos os assemblies que constituem a estrutura de destino.

   Para projetos não direcionados ao .NET Core ou à Plataforma Universal do Windows, a guia **Estrutura** enumera os assemblies da estrutura de destino. O usuário precisa adicionar todas as referências exigidas pelo aplicativo.

   Por padrão, os projetos Universais do Windows contêm referências a todos os assemblies da estrutura de destino. Em projetos gerenciados, um nó somente leitura na pasta **referências** em **Gerenciador de soluções** indica a referência a toda a estrutura. Da mesma forma, a guia **estrutura** não enumera nenhum dos assemblies da estrutura e, em vez disso, exibe a seguinte mensagem: "todos os assemblies de estrutura já estão referenciados. Use o Pesquisador de Objetos para explorar as referências no Framework".

2. **Extensões** lista todos os assemblies que os fornecedores externos de componentes e controles desenvolveram para estender a estrutura de destino. Dependendo da finalidade do aplicativo do usuário, esses assemblies podem ser necessários.

   **As extensões** são populadas enumerando os assemblies que são registrados nos seguintes locais:

   Computador de 32 bits:
   - `HKEY_CURRENT_USER\SOFTWARE\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`
   - `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`

   Computador de 64 bits:
   - `HKEY_CURRENT_USER\SOFTWARE\Wow6432Node\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`
   - `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\[Target Framework Identifier]\v[Target Framework Version]\AssemblyFoldersEx\[UserComponentName]\@default=[Disk location of assemblies]`

   E versões mais antigas do [Identificador de estrutura de destino]

   Por exemplo, se um projeto for direcionado ao .NET Framework 4 em um computador de 32 bits, as **Extensões** enumerarão os assemblies registrados em *\Microsoft\.NETFramework\v4.0\AssemblyFoldersEx*, *\Microsoft\.NETFramework\v3.5\AssemblyFoldersEx*, *\Microsoft\.NETFramework\v3.0\AssemblyFoldersEx* e *\Microsoft\.NETFramework\v2.0\AssemblyFoldersEx*.

Alguns componentes na lista podem não ser exibidos, dependendo da versão de estrutura do projeto. Isso pode ocorrer nas seguintes condições:

- Um componente que usa uma versão de estrutura recente é incompatível com um projeto direcionado a uma versão anterior.

   Para saber mais sobre como alterar a versão da estrutura de destino de um projeto, confira [Visão geral de destino da estrutura](visual-studio-multi-targeting-overview.md).

- Um componente que usa o .NET Framework 4 é incompatível com um projeto direcionado ao .NET Framework 4.5.

Você deve evitar adicionar referências de arquivo às saídas de outro projeto na mesma solução, porque essa ação poderá causar erros de compilação. Em vez disso, use a guia **Projetos** da caixa de diálogo **Adicionar Referência** para criar referências projeto a projeto. Essa ação facilita o desenvolvimento em equipe, permitindo um melhor gerenciamento das bibliotecas de classes criadas nos projetos. Para obter mais informações, consulte [Solução de problemas de referências desfeitas](../ide/troubleshooting-broken-references.md).

> [!NOTE]
> No Visual Studio 2015 ou posterior, uma referência de arquivo será criada, em vez de uma referência de projeto, se a versão da estrutura de destino de um projeto for .NET Framework 4.5 ou posterior e a versão de destino do outro projeto for .NET Framework 2, 3, 3.5 ou 4.0.

### <a name="to-display-an-assembly-in-the-add-reference-dialog-box"></a>Para exibir um assembly na caixa de diálogo Adicionar Referência

- Mova ou copie o assembly para um dos seguintes locais:

  - O diretório atual do projeto. (É possível encontrar esses assemblies usando a guia **Procurar**.)

  - Outros diretórios do projeto na mesma solução. (É possível encontrar esses assemblies usando a guia **Projetos**.)

  \- ou –

- Defina uma chave do Registro que especifica o local dos assemblies a ser exibido:

  Para um sistema operacional de 32 bits, adicione uma das chaves do Registro a seguir.

  - `[HKEY_CURRENT_USER\SOFTWARE\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  - `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  Para um sistema operacional de 64 bits, adicione uma das chaves do Registro a seguir em um hive do Registro de 32 bits.

  - `[HKEY_CURRENT_USER\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  - `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\<VersionMinimum>\AssemblyFoldersEx\MyAssemblies]@="<AssemblyLocation>"`

  *\<VersionMinimum\>* é a versão mais baixa do Framework que se aplica. Se o *\<VersionMinimum\>* for v 3.0, as pastas especificadas em *AssemblyFoldersEx* se aplicarão a projetos direcionados .NET Framework 3,0 e posteriores.

  *\<AssemblyLocation\>* é o diretório dos assemblies que você deseja exibir na caixa de diálogo **Adicionar referência** , por exemplo, *C:\MyAssemblies*.

  A criação da chave do Registro sob o nó `HKEY_LOCAL_MACHINE` permite que todos os usuários vejam os assemblies no local especificado na caixa de diálogo **Adicionar Referência**. A criação da chave do Registro sob o nó `HKEY_CURRENT_USER` afeta somente a configuração do usuário atual.

  Abra a caixa de diálogo **Adicionar Referência** novamente. Os assemblies devem aparecer na guia **.net** . Se não tiverem, certifique-se de que os assemblies estejam localizados no diretório *AssemblyLocation* especificado, reinicie o Visual Studio e tente novamente.

## <a name="projects-tab"></a>Guia Projetos

A guia **Projetos** lista todos os projetos compatíveis dentro da solução atual, na subguia **Solução**.

Um projeto pode referenciar outro projeto direcionado a outra versão de estrutura. Por exemplo, você pode criar um projeto direcionado ao .NET Framework 4, mas que referencia um assembly que foi criado para o .NET Framework 2. Porém, o projeto .NET Framework 2 não pode referenciar um projeto .NET Framework 4. Para obter mais informações, confira [Visão geral do direcionamento de estrutura](../ide/visual-studio-multi-targeting-overview.md).

> [!NOTE]
> Um projeto direcionado ao .NET Framework 4 é incompatível com um projeto direcionado ao .NET Framework 4 Client Profile.

## <a name="shared-projects-tab"></a>Guia Projetos Compartilhados

Adicione uma referência a um projeto compartilhado na guia **Projetos Compartilhados** da caixa de diálogo Gerenciador de Referências. Os [Projetos Compartilhados](/xamarin/cross-platform/app-fundamentals/shared-projects?tabs=windows) permitem gravar códigos comuns que são referência de vários projetos de aplicativos diferentes.

## <a name="universal-windows-tab"></a>Guia Windows Universal

A guia **Windows Universal** lista todos os SDKs específicos às plataformas na qual sistemas operacionais Windows estão em execução.
Esta guia tem dois subgrupos: **núcleo** e **extensões**.

### <a name="core-subgroup"></a>Subgrupo Núcleo

Por padrão, os Projetos de Aplicativo Universal do Windows têm uma referência ao SDK do Windows Universal. Consequentemente, o subgrupo de **Núcleo** no **Gerenciador de Referências** não enumera nenhum dos assemblies do SDK do Windows Universal.

### <a name="extensions-subgroup"></a>Subgrupos Extensões

**Extensões** lista os SDKs de usuário que estendem a plataforma do Windows de destino.

O SDK é uma coleção de arquivos que o Visual Studio trata como um único componente. Na guia **extensões** , os SDKs que se aplicam ao projeto do qual a caixa de diálogo Gerenciador de referências foi chamada são listados como entradas únicas. Quando adicionado a um projeto, todo o conteúdo do SDK é consumido pelo Visual Studio de modo que o usuário não precisa realizar ações adicionais para aproveitar os conteúdos do SDK no IntelliSense, na caixa de ferramentas, no designer, no Pesquisador de Objetos, no build, na implantação, depuração nem nos pacotes.

Para obter informações sobre como exibir o SDK na guia **extensões** , consulte [criando um Software Development Kit](../extensibility/creating-a-software-development-kit.md).

> [!NOTE]
> Se um projeto referenciar um SDK que depende de outro SDK, o Visual Studio não consumirá o segundo SDK a menos que você adicione manualmente uma referência ao segundo SDK. Quando um usuário escolhe um SDK na guia **Extensões**, a caixa de diálogo Gerenciador de Referências ajuda a identificar dependências do SDK listando todas as dependências no painel de detalhes.

Se um tipo de projeto não der suporte para extensões, essa guia não será exibida na caixa de diálogo Gerenciador de Referências.

## <a name="com-tab"></a>Guia COM

A guia **com** lista todos os componentes com que estão disponíveis para referência. Se você deseja adicionar uma referência a uma DLL COM registrada que contém um manifesto interno, cancele o registro da DLL primeiro. Caso contrário, em vez de adicionar a referência do assembly como uma DLL nativa, o Visual Studio a adicionará como um Controle ActiveX.

Se um tipo de projeto não der suporte ao COM, a guia não será exibida na caixa de diálogo Gerenciador de Referências.

## <a name="browse"></a>Procurar

É possível usar o botão **Procurar** para procurar um componente no sistema de arquivos.

Um projeto pode referenciar um componente direcionado a outra versão de estrutura. Por exemplo, você pode criar um aplicativo direcionado ao .NET Framework 4.7, mas que referencia um componente direcionado ao .NET Framework 4. Para obter mais informações, confira [Visão geral do direcionamento de estrutura](../ide/visual-studio-multi-targeting-overview.md).

Evite adicionar referências de arquivo às saídas de outro projeto na mesma solução, porque essa tática pode causar erros de compilação. Em vez disso, use a guia **Solução** da caixa de diálogo Gerenciador de Referências para criar referências projeto a projeto. Essa ação facilita o desenvolvimento em equipe, permitindo um melhor gerenciamento das bibliotecas de classes criadas nos projetos. Para obter mais informações, consulte [Solução de problemas de referências desfeitas](../ide/troubleshooting-broken-references.md).

Não é possível navegar até o SDK e adicioná-lo ao projeto. Você só pode procurar um arquivo (por exemplo, um assembly ou *. winmd*) e adicioná-lo ao seu projeto.

Ao fazer uma referência de arquivo a um WinMD, o layout esperado é que os arquivos * \<FileName> . WinMD*, * \<FileName> . dll*e * \<FileName> . pri* são todos colocados juntos. Se você referenciar um WinMD nos seguintes cenários, um conjunto incompleto de arquivos será copiado no diretório de saída do projeto e, consequentemente, falhas de compilação e de runtime ocorrerão.

- **Componente nativo**: um projeto nativo criará um WinMD para cada conjunto não contínuo de namespaces e uma DLL que consiste na implementação. O WinMDs terá nomes distintos. Ao fazer referência a esse arquivo de componente nativo, o MSBuild não reconhecerá que os WinMDs nomeados de forma diferente formam um componente. Consequentemente, somente o nome idêntico * \<FileName> . dll* e * \<FileName> . winmd* serão copiados e ocorrerão erros de tempo de execução. Para resolver esse problema, crie uma SDK de extensão. Para obter mais informações, consulte [Criar um Software Development Kit](../extensibility/creating-a-software-development-kit.md).

- **Consumindo controles**: um controle XAML consiste em, no mínimo, um *\<FileName>.winmd*, *\<FileName>.dll*, *\<FileName>.pri*, *\<XamlName>.xaml* e um *\<ImageName>.jpg*. Quando o projeto é compilado, os arquivos de recursos associados à referência do arquivo não serão copiados no diretório de saída do projeto e somente * \<FileName> . winmd*, * \<FileName> . dll* e * \<FileName> . pri* serão copiados. Um erro de compilação é registrado para informar ao usuário que os recursos * \<XamlName> . XAML* e * \<ImageName> . jpg* estão ausentes. Para ter êxito, o usuário precisará copiar manualmente esses arquivos de recurso no diretório de saída do projeto para a compilação e a depuração/runtime. Para resolver esse problema, crie um SDK de Extensão seguindo as etapas em [Criar um Software Development Kit](../extensibility/creating-a-software-development-kit.md) ou edite o arquivo de projeto para adicionar a seguinte propriedade:

    ```xml
    <PropertyGroup>
       <GenerateLibraryOutput>True</GenerateLibraryOutput>
    </PropertyGroup>
    ```

    > [!NOTE]
    > Se você adicionar a propriedade, a compilação pode ficar mais lenta.

## <a name="recent"></a>Recente

Os **assemblies**, **com**, **Windows**e **Browse** oferecem suporte a uma guia **recente** , que enumera a lista de componentes que foram adicionados recentemente aos projetos.

## <a name="search"></a>Search

A barra de pesquisa na caixa de diálogo Gerenciador de Referências opera na guia que está no foco. Por exemplo, se um usuário digitar “Sistema” na barra de pesquisa enquanto a guia **Solução** estiver no foco, a pesquisa não retornará nenhum resultado a menos que a solução consista em um nome de projeto que contenha “Sistema”.

## <a name="see-also"></a>Veja também

- [Gerenciar referências em um projeto](../ide/managing-references-in-a-project.md)
