---
title: Atualizar uma extensão Visual Studio dados
description: Saiba como atualizar sua extensão Visual Studio para trabalhar com o Visual Studio 2022.
ms.date: 06/08/2021
ms.topic: conceptual
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: 514c9654a741e4e1e565f0cb2becdbe3157fab0c
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308664"
---
# <a name="update-a-visual-studio-extension-for-visual-studio-2022"></a>Atualizar uma Visual Studio para o Visual Studio 2022

Você pode atualizar sua extensão para trabalhar com o Visual Studio 2022 Preview seguindo este guia. Visual Studio Versão Prévia 2022 é um aplicativo de 64 bits e apresenta algumas alterações significativas no SDK do VS. Este guia orienta você pelas etapas necessárias para que sua extensão esteja funcionando com a versão prévia atual do Visual Studio 2022, para que sua extensão possa estar pronta para que os usuários instalem antes que o Visual Studio 2022 atinja a GA.

## <a name="installing"></a>Instalando

Instale Visual Studio versão prévia 2022 [do Visual Studio 2022 Preview baixa](https://visualstudio.microsoft.com/vs/preview/vs2022).

### <a name="extensions-written-in-a-net-language"></a>Extensões escritas em uma linguagem .NET

O SDK do VS Visual Studio 2022 para extensões gerenciadas está em uso *exclusivamente* no NuGet:

- O meta-pacote [Microsoft.VisualStudio.Sdk](https://www.nuget.org/packages/Microsoft.VisualStudio.Sdk/) (versões 17.x) traz a maioria ou todos os assemblies de referência necessários.
- O [pacote Microsoft.VSSDK.BuildTools](https://www.nuget.org/packages/Microsoft.VSSDK.BuildTools/) (versões 17.x) deve ser referenciado do projeto VSIX para que ele possa criar um VSIX compatível com Visual Studio 2022.

As *extensões devem* ser compiladas com a plataforma "Qualquer CPU" ou "x64". A plataforma "x86" é incompatível Visual Studio processo de 64 bits do 2022.

### <a name="extensions-written-in-c"></a>Extensões escritas em C++

O SDK do VS para extensões compiladas com C++ está disponível com o SDK Visual Studio instalado, como de costume.

As *extensões devem* ser compiladas especificamente no SDK Visual Studio 2022 e para amd64.

### <a name="update-your-extension-to-visual-studio-2022"></a>Atualizar sua extensão para Visual Studio 2022

#### <a name="extensions-with-running-code"></a>Extensões com código em execução

As extensões com código *em execução devem* ser compiladas especificamente para Visual Studio 2022. Visual Studio 2022 não carregará nenhuma extensão que não se Visual Studio 2022 especificamente.

Saiba como migrar suas extensões pré-Visual Studio 2022 para o Visual Studio 2022:

1. [Modernize seus projetos.](#modernize-your-vsix-project)
1. [Recfactore seu código-fonte em um projeto](#use-shared-projects-for-multi-targeting) compartilhado para permitir o direcionamento Visual Studio 2022 e versões mais antigas.
1. [Adicione um Visual Studio vsix de 2022 direcionado a 2022](#add-a-visual-studio-2022-target)e nossa tabela de [remapeamento de pacote/assembly](migrated-assemblies.md).
1. [Fazendo ajustes de código necessários.](#handle-breaking-api-changes)
1. [Testando sua Visual Studio 2022.](#test-your-extension)
1. [Publicando sua extensão Visual Studio 2022.](#publish-your-extension)

#### <a name="extensions-without-running-code"></a>Extensões sem executar código

Extensões que não contêm nenhum código em execução (por  exemplo, modelos de projeto/item) não são necessárias para seguir as etapas acima, incluindo a produção de dois VSIXs distintos.

Em vez disso, um VSIX deve ser modificado para que seu `source.extension.vsixmanifest` arquivo declare dois destinos de instalação, desta forma:

```xml
<Installation>
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0,17.0)">
      <ProductArchitecture>x86</ProductArchitecture>
   </InstallationTarget>
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
      <ProductArchitecture>amd64</ProductArchitecture>
   </InstallationTarget>
</Installation>
```

Você pode ignorar as etapas neste artigo sobre como usar projetos compartilhados e vários VSIXs. Você pode prosseguir com o [teste](#test-your-extension)!

> [!NOTE]
> Se você estiver visando uma nova extensão *Visual Studio,* usando o Visual Studio 2022 Preview e quiser (também) direcionar o Visual Studio 2019 ou uma versão anterior, confira este [guia.](target-previous-versions.md)

### <a name="msbuild-tasks"></a>tarefas MSBuild

Se você for autor de tarefas do MSBuild, esteja ciente de que, no Visual Studio 2022, é muito mais provável que elas sejam carregadas em um processo de MSBuild.exe de 64 bits. Se sua tarefa exigir que um processo de 32 bits seja executado, consulte esta documentação do [MSBuild](../../msbuild/how-to-configure-targets-and-tasks.md#usingtask-attributes-and-task-parameters) para garantir que o MSBuild saiba como carregar sua tarefa em um processo de 32 bits.

## <a name="modernize-your-vsix-project"></a>Modernizar seu projeto VSIX

Antes de adicionar Visual Studio 2022 à sua extensão, é recomendável aproveitar esse tempo para limpar e modernizar seu projeto existente antes de ir além, incluindo:

1. [Migre de packages.config para `PackageReference` ](/nuget/consume-packages/migrate-packages-config-to-package-reference).

1. Substitua quaisquer referências de assembly do VS SDK do assembly direto por itens PackageReference.

   ```diff
   -<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   +<PackageReference Include="Microsoft.VisualStudio.OLE.Interop" Version="..." />
   ```

   > [!TIP]
   > Você pode substituir *muitas referências* de assembly por apenas *um* PackageReference para nosso metapacote:
   >
   >```diff
   >-<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop.8.0" />
   >+<PackageReference Include="Microsoft.VisualStudio.Sdk" >Version="..." />
   >```

   Escolha as versões de pacote que corresponderem à versão mínima Visual Studio que você está direcionando.

   Alguns assemblies que não são exclusivos do SDK do VS (por exemplo, Newtonsoft.Json.dll) podem ter sido descobertos por meio de uma referência simples antes do Visual Studio 2022, mas no Visual Studio 2022 exigem uma referência de pacote porque, no Visual Studio 2022, removemos alguns diretórios de runtime do Visual Studio e do SDK do caminho de pesquisa de assembly padrão do `<Reference Include="Newtonsoft.Json" />` MSBuild.

   Ao alternar de referências de assembly direto para referências de pacote NuGet, você pode escolher referências adicionais de assembly e pacotes de analisador devido ao NuGet instalar automaticamente o fechamento transitivo de dependências. Isso geralmente é OK, mas pode resultar em avisos adicionais sinalizados durante o build. Trabalhe com esses avisos e resolva o máximo possível e considere suprimir esses avisos que você não pode resolver usando regiões no `#pragma warning disable <id>` código.

## <a name="use-shared-projects-for-multi-targeting"></a>Usar projetos compartilhados para direcionamento múltiplo

[Projetos compartilhados](/xamarin/cross-platform/app-fundamentals/shared-projects?tabs=windows) são um tipo de projeto que foi introduzido no Visual Studio 2015. Projetos compartilhados no Visual Studio permitem que arquivos de código-fonte sejam compartilhados entre vários projetos e criem de forma diferente usando símbolos de compilação condicional e conjuntos exclusivos de referências.

Como o Visual Studio 2022 requer um conjunto distinto de assemblies de referência de todas as versões anteriores do VS, nossa orientação é usar projetos compartilhados para direcionar sua extensão para pré-Visual Studio 2022 e Visual Studio 2022 (e versões posteriores), dando a você compartilhamento de código, mas referências distintas.

No contexto de extensões Visual Studio, você pode ter um projeto VSIX para o Visual Studio 2022 e posterior e um projeto VSIX para Visual Studio 2019 e anterior. Cada um desses projetos conteria apenas um e o pacote faz referência ao `source.extension.vsixmanifest` SDK 16.x ou ao SDK 17.x. Esses projetos VSIX também teriam uma referência de projeto compartilhado para um novo projeto compartilhado que hospedará todo o código-fonte que pode ser compartilhado entre as duas versões do VS.

Como ponto de partida, para este documento, vamos supor que você já tenha um projeto VSIX destinado ao Visual Studio 2019 e que você deseja que sua extensão funcione no Visual Studio 2022.

Todas essas etapas podem ser concluídas com Visual Studio 2019.

1. Se você ainda não fez isso, [modernize](#modernize-your-vsix-project) seus projetos para facilitar as etapas posteriormente nesse processo de atualização.

1. Adicione um novo projeto compartilhado à sua solução para cada projeto existente que faz referência ao SDK do VS.
   ![Comando Adicionar Novo Projeto ](media/update-visual-studio-extension/add-new-project.png)
    ![ Novo modelo de projeto](media/update-visual-studio-extension/new-shared-project-template.png)

1. Adicione uma referência de cada projeto de referência do SDK do VS ao seu equivalente de projeto compartilhado.
   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="Adicionar referência de projeto compartilhado" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. Mova todo o código-fonte (incluindo .cs, .resx) de cada projeto de referência do SDK do VS para seu equivalente de projeto compartilhado.
Deixe o `source.extension.vsixmanifest` arquivo no projeto VSIX.
   ![O projeto compartilhado contém todos os arquivos de origem](media/update-visual-studio-extension/source-files-in-shared-project.png)

1. Arquivos de metadados (notas de versão, licença, ícones e assim por diante) e arquivos VSCT devem ser movidos para um diretório compartilhado e adicionados como arquivos vinculados ao projeto VSIX.
   ![Adicionar metadados e arquivos VSCT como arquivos vinculados](media/update-visual-studio-extension/add-linked-items-to-vsix.png)
    - Para arquivos de metadados, de definir BuildAction como `Content` e definir Incluir no VSIX como `true` .

      ![Incluir arquivos de metadados no VSIX](./media/update-visual-studio-extension/include-metadata-files-in-vsix.png)
    - Para arquivos VSCT, de definido BuildAction como `VSCTCompile` e não inclua no VSIX.
      Visual Studio pode se dizer que essa configuração não tem suporte, mas você pode alterar manualmente a ação de build descarregando o projeto e alterando `Content` para `VSCTCompile`

    ```diff
    -<Content Include="..\SharedFiles\VSIXProject1Package.vsct">
    -  <Link>VSIXProject1Package.vsct</Link>
    -</Content>
    +<VSCTCompile Include="..\SharedFiles\VSIXProject1Package.vsct">
    +  <Link>VSIXProject1Package.vsct</Link>
    +  <ResourceName>Menus.ctmenu</ResourceName>
    +</VSCTCompile>
    ```

      ![Definir arquivos VSCT como VSCTCompile](media/update-visual-studio-extension/build-linked-vsct-files.png)

1. Crie seus projetos para confirmar que você não introduziu novos erros.

Seu projeto agora está pronto para adicionar suporte Visual Studio 2022.

## <a name="add-a-visual-studio-2022-target"></a>Adicionar um Visual Studio 2022

Este documento pressu que você concluiu as etapas para fatorar sua [extensão Visual Studio com projetos compartilhados.](#use-shared-projects-for-multi-targeting)

Prossiga para adicionar Visual Studio 2022 à sua extensão com estas etapas, que podem ser concluídas usando Visual Studio 2019:

1. Adicione um novo projeto VSIX à sua solução. Esse será o projeto destinado ao Visual Studio 2022. Remova qualquer código-fonte que tenha vindo com o modelo, mas *mantenha o `source.extension.vsixmanifest` arquivo*.

1. Em seu novo projeto VSIX, adicione uma referência de projeto compartilhado ao mesmo projeto compartilhado que o Visual Studio vsIX de destino 2019.

   ![Uma solução com um projeto compartilhado e dois projetos VSIX](media/update-visual-studio-extension/shared-project-with-two-heads.png)

1. Verifique se o novo projeto VSIX é construído corretamente. Talvez seja necessário adicionar referências para corresponder ao projeto original do VSIX para resolver erros do compilador.

1. Para extensões gerenciadas do VS, atualize suas referências de pacote de 16.x (ou anterior) para as versões do pacote 17.x no arquivo de projeto direcionado ao Visual Studio 2022 usando o nuGet Gerenciador de Pacotes ou editando diretamente o arquivo de projeto:

    ```diff
    -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
    +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview.1" />
    -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
    +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-preview.1" />
    ```

   Você usará versões que estão realmente disponíveis no nuget.org. Os usados anteriormente são apenas para fins de demonstração.

   Em muitos casos, as IDs do pacote foram alteradas. Consulte a tabela [de mapeamento de pacote/assembly](migrated-assemblies.md) para ver uma lista de alterações no Visual Studio 2022.

   As extensões escritas em C++ ainda não têm um SDK disponível para compilação.

1. Para projetos C++, eles devem ser compilados para amd64. Para extensões gerenciadas, considere alterar seu projeto de criar para Qualquer CPU para direcionamento para , para refletir isso no Visual Studio 2022 sua extensão sempre carrega em um processo de `x64` 64 bits. `Any CPU` também é bom, mas pode produzir avisos se você referenciar binários nativos somente x64.

   Qualquer dependência que sua extensão possa ter em um módulo nativo terá que ser atualizada de uma imagem x86 para uma imagem amd64.

1. Edite `source.extension.vsixmanifest` o arquivo para refletir o direcionamento Visual Studio 2022. De definir `<InstallationTarget>` a marca para refletir Visual Studio 2022 e indicar um payload amd64:

   ```xml
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
      <ProductArchitecture>amd64</ProductArchitecture>
   </InstallationTarget>
   ```

   No Visual Studio 2019, o designer desse arquivo não expõe o novo elemento, portanto, essa alteração precisará ser feita com um editor xml, que você pode acessar por meio do comando Abrir com `ProductArchitecture` **no Gerenciador de Soluções**. 

   Esse `ProductArchitecture` elemento é crítico. Visual Studio 2022 não *instalará* sua extensão sem ela.

   | Elemento | Valor | Descrição |
   | - | - | - |
   | ProductArchitecture | X86, AMD64 | As plataformas com suporte neste VSIX. Não é sensível a minúsculas. Uma plataforma por elemento e um elemento por InstallTarget. Para versões de produto menores que 17.0, o valor padrão é x86 e pode ser omitido.  Para as versões do produto 17.0 e superiores, esse elemento é necessário e não há nenhum valor padrão. Por Visual Studio 2022, o único conteúdo válido para esse elemento é "amd64". |

1. Faça quaisquer outros ajustes necessários em seu source.extension.vsixmanifest para corresponder ao que é Visual Studio 2019 (se for o caso). É essencial que a ID do VSIX, no elemento do `Identity` manifesto, seja idêntica para ambas as extensões.

Neste ponto, você tem uma Visual Studio VSIX de 2022. Você deve criar seu Visual Studio vsix de 2022 direcionado a 2022 e trabalhar por meio de [quaisquer quebras de build que apareçam](#handle-breaking-api-changes). Se você não tiver quebras de build em seu projeto vsIX Visual Studio 2022, parabéns: você está pronto para teste!

## <a name="handle-breaking-api-changes"></a>Lidar com alterações da API da quebra

Há alterações [da API da](breaking-api-list.md) Visual Studio 2022 que podem exigir alterações no código de quando ele foi em versões anteriores. Revise esse documento para ver dicas sobre como atualizar seu código para cada uma delas.

Ao adaptar seu código, recomendamos que você [use](#use-conditional-compilation-symbols) a compilação condicional para que seu código possa continuar a dar suporte ao pré-Visual Studio 2022 ao adicionar suporte para o Visual Studio 2022.

Quando você obter sua Visual Studio de extensão direcionada para 2022, prossiga para [testar](#test-your-extension).

## <a name="use-conditional-compilation-symbols"></a>Usar símbolos de compilação condicional

Se você quiser usar o mesmo código-fonte, até mesmo o mesmo arquivo, para o Visual Studio 2022 e versões anteriores, talvez seja necessário usar a compilação condicional para que você possa bifurcar seu código para se adaptar às alterações significativas. A compilação condicional é um recurso das linguagens C#, Visual Basic e C++ que podem ser usadas para compartilhar a maioria dos códigos ao acomodar APIs divergentes em locais específicos.

Mais informações sobre o uso de diretivas de pré-processador e símbolos de compilação condicional podem ser encontradas na diretiva microsoft docs [#if pré-processador](/dotnet/csharp/language-reference/preprocessor-directives#conditional-compilation).

Seus projetos destinados a versões Visual Studio anteriores precisarão de um símbolo de compilação condicional que pode ser usado para bifurcar o código para usar as diferentes APIs. Você pode definir o símbolo de compilação condicional na página de propriedades do projeto, conforme mostrado na imagem a seguir:

![Definindo símbolos de compilação condicional](media/update-visual-studio-extension/conditional-compilation-symbols.png)

Certifique-se de definir o símbolo de compilação para todas *as* configurações, pois, por padrão, o símbolo que você inserir só pode se aplicar a uma configuração.

### <a name="c-techniques"></a>Técnicas \# C

Em seguida, você pode usar esse símbolo como uma diretiva de pré-processador ( `#if` ), conforme mostrado no código a seguir. Em seguida, você pode bifurcar seu código para lidar com a alteração da quebra entre as diferentes Visual Studio versões.

```cs
    Guid myGuid = new Guid("{633FBA02-719B-40E7-96BF-0899767CD104}");
    uint myFlags = 0;
    IVsShell shell = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsShell, IVsShell>();
#if Visual Studio 2019
    shell.LoadUILibrary(myGuid, myFlags, out uint ptrLib);
#else
    shell.LoadUILibrary(myGuid, myFlags, out IntPtr ptrLib);
#endif
```

Em alguns casos, você pode simplesmente usar para evitar nomear o tipo, evitando assim `var` a necessidade de `#if` regiões. O snippet acima também pode ser escrito como:

```cs
    Guid myGuid = new Guid("{633FBA02-719B-40E7-96BF-0899767CD104}");
    uint myFlags = 0;
    IVsShell shell = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsShell, IVsShell>();
    shell.LoadUILibrary(myGuid, myFlags, out var ptrLib);
```

Ao usar a sintaxe , observe como você pode usar o menu suspenso de contexto do serviço de linguagem no documento mostrado abaixo para alterar o realce de sintaxe e a outra ajuda que o serviço de linguagem oferece para concentrar a atenção em uma versão de Visual Studio de destino para nossa extensão versus `#if` outra.

![Compilação condicional em um projeto compartilhado](media/update-visual-studio-extension/conditional-compilation-if-region.png)

### <a name="xaml-sharing-techniques"></a>Técnicas de compartilhamento XAML

O XAML não tem nenhum pré-processador para permitir a personalização de conteúdo com base em símbolos de pré-processador. Copiar e manter duas páginas XAML em que seu conteúdo deve ser diferente entre Visual Studio 2022 e versões anteriores pode ser necessário.

No entanto, em alguns casos, uma referência a um tipo que existe em assemblies distintos no Visual Studio 2022 e versões anteriores ainda pode ser representável em um arquivo XAML removendo o namespace que faz referência ao assembly:

```diff
-xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
-Value="{DynamicResource {x:Static vsui:TreeViewColors.SelectedItemActiveBrushKey}}"
+Value="{DynamicResource TreeViewColors.SelectedItemActiveBrushKey}"
```

## <a name="test-your-extension"></a>Testar sua extensão

Para testar uma extensão que se Visual Studio 2022, você precisará ter o Visual Studio versão prévia 2022 instalado.
Você não poderá executar extensões de 64 bits em versões do Visual Studio antes Visual Studio 2022 Preview.

Você pode usar Visual Studio Versão Prévia 2022 para criar e testar suas extensões, independentemente de Visual Studio 2022 ou uma versão anterior. Ao iniciar um projeto VSIX do Visual Studio 2022, uma instância experimental do Visual Studio será lançada.

É recomendável testar com cada versão do Visual Studio que você pretende dar suporte à extensão.

Agora você está pronto para publicar [sua extensão](#publish-your-extension).

## <a name="publish-your-extension"></a>Publicar sua extensão

Ótimo, então você adicionou um destino Visual Studio 2022 à sua extensão e testou-o. Agora você está pronto para publicar a extensão para o mundo a ser publicada.

### <a name="visual-studio-marketplace"></a>Visual Studio Marketplace

Publicar sua extensão no [Visual Studio Marketplace](https://marketplace.visualstudio.com/) é uma ótima maneira de fazer com que novos usuários encontrem e instalem sua extensão. Se sua extensão é Visual Studio 2022 exclusivamente ou se tem como destino versões mais antigas do VS também, o Marketplace está lá para dar suporte a você.

No futuro, o Marketplace permitirá que você carregue vários VSIXs em apenas uma listagem do Marketplace, permitindo que você carregue o VSIX direcionado ao Visual Studio 2022 e um VSIX pré-Visual Studio 2022. Os usuários obterão automaticamente o VSIX correto para a versão do VS que eles instalaram ao usar o gerenciador de extensões do VS.

Para as versões prévias do Visual Studio 2022, o Marketplace dará suporte apenas a um único arquivo VSIX por listagem do Marketplace. Embora Visual Studio 2022 está em versão prévia, incentivamos você a ter uma lista Visual Studio 2022 somente do Marketplace para sua extensão. Dessa forma, você pode iterar sua extensão Visual Studio 2022 conforme necessário sem afetar seus clientes em versões anteriores do Visual Studio. Você também pode marcar a extensão como "versão prévia" para definir a expectativa de que ela provavelmente será menos confiável, mesmo que a origem dessa não confiabilidade seja Visual Studio 2022, do que sua extensão base.

### <a name="custom-installer"></a>Instalador personalizado

Se você criar uma MSI/EXE para instalar sua extensão e gerar vsixinstaller.exe para instalar (parte de) sua extensão, saiba que o instalador do VSIX no Visual Studio 2022 foi atualizado. Os desenvolvedores precisarão usar a versão do instalador do VSIX que vem com o Visual Studio 2022 para instalar extensões no Visual Studio 2022. O instalador do VSIX no Visual Studio 2022 também instalará extensões aplicáveis voltadas para versões anteriores do Visual Studio instaladas lado a lado com o Visual Studio 2022 no mesmo computador.

### <a name="network-share"></a>Compartilhamento de rede

Você pode compartilhar sua extensão em uma LAN ou de qualquer outra maneira. Se você direcionar o Visual Studio 2022 e o pré-Visual Studio 2022, precisará compartilhar vários VSIXs individualmente e dar a eles nomes de arquivo (ou coloque-os em pastas exclusivas) que ajudam os usuários a saber qual VSIX instalar com base na versão do Visual Studio que eles instalaram.

### <a name="other-considerations"></a>Outras considerações

#### <a name="dependencies"></a>Dependências

Se o VSIX especificar outro VSIX como uma dependência por meio do elemento , cada VSIX referenciado precisará ser instalado nos mesmos destinos e arquiteturas de produto que o `<dependency>` VSIX. Se um VSIX dependente não dá suporte à instalação de Visual Studio, o VSIX falhará. Não há problema para o VSIX dependente dar suporte a mais destinos e arquiteturas do que o seu, mas não menos. Essa restrição significa que a abordagem de implantação e distribuição de um VSIX com dependências deve espelhar a de seus dependentes.

## <a name="q--a"></a>Perguntas e Respostas

**P:** Minha extensão não requer nenhuma alteração de interop, pois ela apenas fornece dados (por exemplo, modelos), posso criar uma única extensão que inclui Visual Studio 2022 também?

**R:** Sim!  Consulte [Extensões sem executar código para](#extensions-without-running-code) obter mais informações sobre isso.

**P:** uma dependência do NuGet está trazendo assemblies de interop antigos e causando conflitos de classes.

**R:** adicione a seguinte linha ao arquivo .csproj para evitar assemblies duplicados:

```xml
    <PackageReference Include="<Name of offending assembly>" ExcludeAssets="compile" PrivateAssets="all" />
```

Isso impedirá que referências de pacote importem a versão antiga do assembly de outras dependências.

**P:** Meus comandos e teclas de atalho não estão funcionando no Visual Studio depois de alternar meus arquivos de origem para um projeto compartilhado.

**R:** [a etapa 2.4](samples.md#step-2---refactor-source-code-into-a-shared-project) do exemplo do Otimizador de Imagem mostra como adicionar arquivos VSCT como itens vinculados para que eles sejam compilados em seu arquivo VSCT.

## <a name="next-steps"></a>Próximas etapas

Siga um exemplo passo a passo, [ImageOptimizer,](samples.md)com links para o projeto e alterações de código para cada etapa.
