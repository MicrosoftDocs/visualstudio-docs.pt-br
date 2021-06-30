---
title: Atualizar uma extensão do Visual Studio
description: Saiba como atualizar sua extensão do Visual Studio para trabalhar com o Visual Studio 2022.
ms.date: 06/08/2021
ms.topic: conceptual
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: 512e9a71cde5ca29c737c1623aa0c8f9c37dd60d
ms.sourcegitcommit: 0499d813d5c24052c970ca15373d556a69507250
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2021
ms.locfileid: "113046125"
---
# <a name="update-a-visual-studio-extension-for-visual-studio-2022"></a>Atualizar uma extensão do Visual Studio para o Visual Studio 2022

> [!IMPORTANT]
> O Conselho deste guia destina-se a orientar os desenvolvedores na migração de extensões que exigem grandes alterações para funcionar no Visual Studio 2019 e 2022. Nesses casos, é recomendável ter dois projetos VSIX e a compilação condicional.
> Muitas extensões poderão funcionar tanto no Visual Studio 2019 quanto na 2022 com pequenas alterações que não exigirão seguir o aviso sobre a modernização de sua extensão neste guia.
> Experimente sua extensão no Visual Studio 2022 e avalie qual é a melhor opção para sua extensão.

Você pode atualizar sua extensão para trabalhar com o Visual Studio 2022 Preview seguindo este guia. O Visual Studio 2022 Preview é um aplicativo de 64 bits e apresenta algumas alterações significativas no SDK do VS. Este guia orienta você pelas etapas necessárias para que sua extensão funcione com a visualização atual do Visual Studio 2022, de modo que sua extensão pode estar pronta para os usuários instalarem antes do Visual Studio 2022 alcançar GA.

## <a name="installing"></a>Instalando

Instale o Visual Studio 2022 Preview a partir de [downloads do visual studio 2022 Preview](https://visualstudio.microsoft.com/vs/preview/vs2022).

### <a name="extensions-written-in-a-net-language"></a>Extensões gravadas em uma linguagem .NET

O SDK do VS direcionado para o Visual Studio 2022 para extensões gerenciadas é *exclusivamente* no NuGet:

- O meta-Package [Microsoft. VisualStudio. SDK](https://www.nuget.org/packages/Microsoft.VisualStudio.Sdk/) (versões 17. x) traz a maioria ou todos os assemblies de referência necessários.
- O pacote [Microsoft. VSSDK. BuildTools](https://www.nuget.org/packages/Microsoft.VSSDK.BuildTools/) (versões 17. x) deve ser referenciado de seu projeto VSIX para que ele possa criar um VSIX em conformidade com o Visual Studio 2022.

As extensões *devem* ser compiladas com a plataforma "qualquer CPU" ou "x64". A plataforma "x86" é incompatível com o processo de 64 bits do Visual Studio 2022.

### <a name="extensions-written-in-c"></a>Extensões gravadas em C++

O SDK do VS para extensões compiladas com C++ está disponível com o SDK do Visual Studio instalado, como de costume.

As extensões *devem* ser compiladas especificamente no SDK do Visual Studio 2022 e para AMD64.

### <a name="update-your-extension-to-visual-studio-2022"></a>Atualize sua extensão para o Visual Studio 2022

#### <a name="extensions-with-running-code"></a>Extensões com código em execução

Extensões com código em execução *devem* ser compiladas especificamente para o Visual Studio 2022. O Visual Studio 2022 não carregará nenhuma extensão que não direcione o Visual Studio 2022 especificamente.

Saiba como migrar suas extensões anteriores do Visual Studio 2022 para o Visual Studio 2022:

1. [Modernizar seus projetos](#modernize-your-vsix-project).
1. [Refatore seu código-fonte em um projeto compartilhado](#use-shared-projects-for-multi-targeting) para permitir o direcionamento do Visual Studio 2022 e versões mais antigas.
1. [Adicione um projeto VSIX direcionado ao Visual Studio 2022](#add-a-visual-studio-2022-target)e nossa [tabela de remapeamento de pacote/assembly](migrated-assemblies.md).
1. [Fazendo os ajustes de código necessários](#handle-breaking-api-changes).
1. [Testando sua extensão do Visual Studio 2022](#test-your-extension).
1. [Publicando sua extensão do Visual Studio 2022](#publish-your-extension).

#### <a name="extensions-without-running-code"></a>Extensões sem código de execução

As extensões que não contêm nenhum código em execução (por exemplo, modelos de projeto/item) *não* são necessárias para seguir as etapas acima, incluindo a produção de dois VSIX distintos.

Em vez disso, o único VSIX deve ser modificado para que seu `source.extension.vsixmanifest` arquivo declare dois destinos de instalação, desta forma:

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

Você pode ignorar as etapas neste artigo sobre como usar projetos compartilhados e vários VSIX. Você pode prosseguir com os [testes](#test-your-extension)!

> [!NOTE]
> Se você estiver criando uma *nova* extensão do Visual Studio, usando o visual Studio 2022 Preview e quiser (também) direcionar o visual Studio 2019 ou uma versão anterior, confira [este guia](target-previous-versions.md).

### <a name="msbuild-tasks"></a>tarefas MSBuild

Se você criar tarefas do MSBuild, lembre-se de que, no Visual Studio 2022, é muito mais provável que elas sejam carregadas em um processo de MSBuild.exe de 64 bits. Se sua tarefa exigir um processo de 32 bits para ser executado, consulte [esta documentação do MSBuild](../../msbuild/how-to-configure-targets-and-tasks.md#usingtask-attributes-and-task-parameters) para garantir que o MSBuild saiba carregar sua tarefa em um processo de 32 bits.

## <a name="modernize-your-vsix-project"></a>Modernizar seu projeto VSIX

Antes de adicionar o suporte do Visual Studio 2022 à sua extensão, é altamente recomendável deixar esse tempo para limpar e modernizar seu projeto existente antes de continuar, incluindo:

1. [Migre do packages.config para `PackageReference` ](/nuget/consume-packages/migrate-packages-config-to-package-reference)o.

1. Substitua todas as referências de assembly do SDK do VS com itens PackageReference.

   ```diff
   -<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   +<PackageReference Include="Microsoft.VisualStudio.OLE.Interop" Version="..." />
   ```

   > [!TIP]
   > Você pode substituir *muitas* referências de assembly por apenas *um* PackageReference ao nosso metapacote:
   >
   >```diff
   >-<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop.8.0" />
   >+<PackageReference Include="Microsoft.VisualStudio.Sdk" Version="..." />
   >```

   Certifique-se de escolher as versões de pacote que correspondem à versão mínima do Visual Studio que você está direcionando.

   Alguns assemblies que não são exclusivos do SDK do VS (por exemplo, Newtonsoft.Json.dll) podem ter sido detectáveis por meio de uma `<Reference Include="Newtonsoft.Json" />` referência simples antes do visual studio 2022 mas, no visual studio 2022, requer uma referência de pacote porque, no visual studio 2022, removemos alguns diretórios de tempo de execução e SDK do Visual Studio do caminho de pesquisa de assembly padrão do MSBuild.

   Ao alternar de referências diretas de assembly para referências de pacote NuGet, você pode pegar referências de assembly adicionais e pacotes do analisador devido ao NuGet instalar automaticamente o fechamento transitivo de dependências. Isso geralmente é OK, mas pode resultar em avisos adicionais sendo sinalizados durante o Build. Trabalhe com esses avisos e resolva o máximo possível e considere suprimir esses avisos que você não pode resolver usando regiões em código `#pragma warning disable <id>` .

## <a name="use-shared-projects-for-multi-targeting"></a>Usar projetos compartilhados para vários destinos

[Projetos compartilhados](/xamarin/cross-platform/app-fundamentals/shared-projects?tabs=windows) são um tipo de projeto que foram introduzidos no Visual Studio 2015. Projetos compartilhados no Visual Studio permitem que os arquivos de código-fonte sejam compartilhados entre vários projetos e compilados de maneira diferente usando símbolos de compilação condicional e conjuntos de referências exclusivos.

Como o Visual Studio 2022 requer um conjunto distinto de assemblies de referência de todas as versões anteriores do VS, nossas diretrizes são usar projetos compartilhados para multidirecionar de forma conveniente a extensão para o Visual Studio 2022 e o Visual Studio 2022 (e versões posteriores), fornecendo o compartilhamento de código, mas referências distintas.

No contexto das extensões do Visual Studio, você poderia ter um projeto VSIX para o Visual Studio 2022 e posterior e um projeto VSIX para o Visual Studio 2019 e anterior. Cada um desses projetos conteria apenas uma `source.extension.vsixmanifest` e as referências de pacote para o SDK 16. x ou para o SDK 17. x. Esses projetos VSIX também teriam uma referência de projeto compartilhada para um novo projeto compartilhado que hospedará todo o código-fonte que pode ser compartilhado entre as duas versões do VS.

Como ponto de partida, para este documento, vamos pressupor que você já tem um projeto VSIX destinado ao Visual Studio 2019 e que deseja que sua extensão funcione no Visual Studio 2022.

Todas essas etapas podem ser concluídas com o Visual Studio 2019.

1. Se você ainda não tiver feito isso, [modernizar seus projetos](#modernize-your-vsix-project) para facilitar as etapas mais adiante neste processo de atualização.

1. Adicione um novo projeto compartilhado à sua solução para cada projeto existente que referencia o SDK do VS.
   ![Adicionar novo comando de projeto ](media/update-visual-studio-extension/add-new-project.png)
    ![ novo modelo de projeto](media/update-visual-studio-extension/new-shared-project-template.png)

1. Adicione uma referência de cada projeto que referencia o SDK do VS ao correspondente do projeto compartilhado.
   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="Adicionar referência de projeto compartilhado" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. Mova todo o código-fonte (incluindo. cs,. resx) de cada projeto referenciado pelo SDK do VS para o correspondente do projeto compartilhado.
Deixe o `source.extension.vsixmanifest` arquivo no projeto VSIX.
   ![O projeto compartilhado contém todos os arquivos de origem](media/update-visual-studio-extension/source-files-in-shared-project.png)

1. Os arquivos de metadados (notas de versão, licença, ícones e assim por diante) e VSCT devem ser movidos para um diretório compartilhado e adicionados como arquivos vinculados ao projeto VSIX.
   ![Adicionar metadados e arquivos VSCT como arquivos vinculados](media/update-visual-studio-extension/add-linked-items-to-vsix.png)
    - Para arquivos de metadados, defina BuildAction como `Content` e defina include no VSIX como `true` .

      ![Incluir arquivos de metadados no VSIX](./media/update-visual-studio-extension/include-metadata-files-in-vsix.png)
    - Para arquivos VSCT, defina BuildAction como `VSCTCompile` e não inclua no VSIX.
      O Visual Studio pode reclamar que essa configuração não tem suporte, mas você pode alterar manualmente a ação de compilação descarregando o projeto e alterando `Content` para `VSCTCompile`

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

1. Crie seus projetos para confirmar que você não introduziu nenhum novo erro.

Seu projeto agora está pronto para adicionar suporte ao Visual Studio 2022.

## <a name="add-a-visual-studio-2022-target"></a>Adicionar um destino do Visual Studio 2022

Este documento pressupõe que você concluiu as etapas para [fatorar sua extensão do Visual Studio com projetos compartilhados](#use-shared-projects-for-multi-targeting).

Vá para adicionar suporte do Visual Studio 2022 à sua extensão com estas etapas, que podem ser concluídas usando o Visual Studio 2019:

1. Adicione um novo projeto VSIX à sua solução. Esse será o projeto destinado ao Visual Studio 2022. Remova qualquer código-fonte que veio com o modelo, mas *Mantenha o `source.extension.vsixmanifest` arquivo*.

1. Em seu novo projeto VSIX, adicione uma referência de projeto compartilhado ao mesmo projeto compartilhado ao qual o VSIX de direcionamento do Visual Studio 2019 faz referência.

   ![Uma solução com um projeto compartilhado e dois projetos VSIX](media/update-visual-studio-extension/shared-project-with-two-heads.png)

1. Verifique se o novo projeto VSIX foi criado corretamente. Talvez seja necessário adicionar referências para corresponder ao projeto do VSIX original para resolver quaisquer erros do compilador.

1. Para extensões gerenciadas VS, atualize suas referências de pacote de 16. x (ou anterior) para as versões de pacote 17. x em seu arquivo de projeto direcionado ao Visual Studio 2022 usando o Gerenciador de pacotes NuGet ou editando diretamente o arquivo de projeto:

    ```diff
    -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
    +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview.1" />
    -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
    +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-preview.1" />
    ```

   Você usará as versões que estão realmente disponíveis no nuget.org. Aqueles usados anteriormente são apenas para fins de demonstração.

   Em muitos casos, as IDs de pacote foram alteradas. Consulte a [tabela de mapeamento de pacote/assembly](migrated-assemblies.md) para obter uma lista de alterações no Visual Studio 2022.

   As extensões escritas em C++ ainda não têm um SDK disponível para compilar com o.

1. Para projetos C++, eles devem ser compilados para AMD64. Para extensões gerenciadas, considere alterar seu projeto de compilação para qualquer CPU para direcionamento `x64` , para refletir isso no Visual Studio 2022 sua extensão sempre é carregada em um processo de 64 bits. `Any CPU` também está bem, mas pode produzir avisos se você fizer referência a qualquer binário nativo somente x64.

   Qualquer dependência que sua extensão possa ter em um módulo nativo precisará ser atualizada de uma imagem x86 para uma imagem AMD64.

1. Edite seu `source.extension.vsixmanifest` arquivo para refletir direcionando o Visual Studio 2022. Defina a `<InstallationTarget>` marca para refletir o Visual Studio 2022 e indicar uma carga AMD64:

   ```xml
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
      <ProductArchitecture>amd64</ProductArchitecture>
   </InstallationTarget>
   ```

   No Visual Studio 2019, o designer desse arquivo não expõe o novo `ProductArchitecture` elemento, portanto, essa alteração precisará ser feita com um editor de XML, que pode ser acessado por meio do comando **abrir com** no **Gerenciador de soluções**.

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
