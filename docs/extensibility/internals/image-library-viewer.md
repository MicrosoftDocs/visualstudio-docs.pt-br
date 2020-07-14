---
title: Visualizador de biblioteca de imagens | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 9d9c7fbb-ebae-4b20-9dd8-3c9070c0d0d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d9714879f93af052e244134ce225b07317455921
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536338"
---
# <a name="image-library-viewer"></a>Visualizador da biblioteca de imagens
A ferramenta Visualizador de biblioteca de imagens do Visual Studio pode carregar e Pesquisar manifestos de imagem, permitindo que o usuário manipule-os da mesma forma que o Visual Studio. O usuário pode alterar o plano de fundo, tamanhos, DPI, alto contraste e outras configurações. A ferramenta também exibe informações de carregamento para cada manifesto de imagem e exibe informações de origem para cada imagem no manifesto da imagem. Essa ferramenta é útil para:

1. Diagnóstico de erros

2. Garantindo que os atributos sejam definidos corretamente em manifestos de imagem personalizados

3. Procurando imagens no catálogo de imagens do Visual Studio para que uma extensão do Visual Studio possa usar imagens que se ajustam ao estilo do Visual Studio

   ![Herói do Visualizador de biblioteca de imagens](../../extensibility/internals/media/image-library-viewer-hero.png "Herói do Visualizador de biblioteca de imagens")

   **Moniker da imagem**

   Um moniker de imagem (ou moniker para curto) é um par GUID: ID que identifica exclusivamente um ativo de imagem ou de lista de imagens na biblioteca de imagens.

   **Arquivos de manifesto de imagem**

   Os arquivos de manifesto de imagem (. imagemanifest) são arquivos XML que definem um conjunto de ativos de imagem, os monikers que representam esses ativos e a imagem real ou imagens que representam cada ativo. Os manifestos de imagem podem definir imagens autônomas ou listas de imagens para suporte de interface do usuário herdado. Além disso, há atributos que podem ser definidos no ativo ou nas imagens individuais por trás de cada ativo para alterar quando e como esses ativos são exibidos.

   **Esquema de manifesto de imagem**

   Um manifesto de imagem completo tem esta aparência:

```xml
<ImageManifest>
      <!-- zero or one Symbols elements -->
      <Symbols>
        <!-- zero or more Guid, ID, or String elements -->
      </Symbols>
      <!-- zero or one Images elements -->
      <Images>
        <!-- zero or more Image elements -->
      </Images>
      <!-- zero or one ImageLists elements -->
      <ImageLists>
        <!-- zero or more ImageList elements -->
      </ImageLists>
</ImageManifest>
```

 **Símbolos**

 Como auxílio à legibilidade e à manutenção, o manifesto da imagem pode usar símbolos para valores de atributo. Os símbolos são definidos da seguinte maneira:

```xml
<Symbols>
      <Import Manifest="manifest" />
      <Guid Name="ShellCommandGuid" Value="8ee4f65d-bab4-4cde-b8e7-ac412abbda8a" />
      <ID Name="cmdidSaveAll" Value="1000" />
      <String Name="AssemblyName" Value="Microsoft.VisualStudio.Shell.UI.Internal" />
</Symbols>
```

|**Subelemento**|**Definição**|
|-|-|
|Importar|Importa os símbolos do arquivo de manifesto fornecido para uso no manifesto atual.|
|Guid|O símbolo representa um GUID e deve corresponder à formatação do GUID.|
|ID|O símbolo representa uma ID e deve ser um inteiro não negativo.|
|String|O símbolo representa um valor de cadeia de caracteres arbitrário.|

 Os símbolos diferenciam maiúsculas de minúsculas e são referenciados usando a sintaxe $ (Symbol-Name):

```xml
<Image Guid="$(ShellCommandGuid)" ID="$(cmdidSaveAll)" >
      <Source Uri="/$(AssemblyName);Component/Resources/image.xaml" />
</Image>
```

 Alguns símbolos são predefinidos para todos os manifestos. Eles podem ser usados no atributo URI do \<Source> \<Import> elemento ou para fazer referência a caminhos no computador local.

|**Símbolo**|**Descrição**|
|-|-|
|CommonProgramFiles|O valor da variável de ambiente% CommonProgramFiles%|
|LocalAppData|O valor da variável de ambiente% LocalAppData%|
|ManifestFolder|A pasta que contém o arquivo de manifesto|
|MyDocuments|O caminho completo da pasta meus documentos do usuário atual|
|ProgramFiles|O valor da variável de ambiente% ProgramFiles%|
|Sistema|A pasta Windows\System32|
|WinDir|O valor da variável de ambiente% WinDir%|

 **Imagem**

 O \<Image> elemento define uma imagem que pode ser referenciada por um moniker. O GUID e a ID agrupados formam o moniker da imagem. O moniker da imagem deve ser exclusivo em toda a biblioteca de imagens. Se mais de uma imagem tiver um determinado moniker, o primeiro encontrado durante a criação da biblioteca é aquele que é mantido.

 Ele deve conter pelo menos uma fonte. Embora as fontes de tamanho neutro forneçam os melhores resultados em uma ampla gama de tamanhos, elas não são necessárias. Se o serviço for solicitado a fornecer uma imagem de um tamanho não definido no \<Image> elemento e não houver fonte de tamanho neutro, o serviço escolherá a melhor fonte de tamanho específico e a dimensionará para o tamanho solicitado.

```xml
<Image Guid="guid" ID="int" AllowColorInversion="true/false">
      <Source ... />
      <!-- optional additional Source elements -->
</Image>
```

|**Atributo**|**Definição**|
|-|-|
|Guid|Necessária A parte GUID do moniker da imagem|
|ID|Necessária A parte de ID do moniker da imagem|
|AllowColorInversion|[Opcional, padrão verdadeiro] Indica se a imagem pode ter suas cores programaticamente invertidas quando usada em um plano de fundo escuro.|

 **Origem**

 O \<Source> elemento define um ativo de origem de imagem única (XAML e png).

```xml
<Source Uri="uri" Background="background">
      <!-- optional NativeResource element -->
 </Source>
```

|**Atributo**|**Definição**|
|-|-|
|Uri|Necessária Um URI que define de onde a imagem pode ser carregada. Pode ser um dos seguintes:<br /><br /> -Um [pacote URI](/dotnet/framework/wpf/app-development/pack-uris-in-wpf) usando a autoridade Application:///<br /><br /> -Uma referência de recurso de componente absoluto<br /><br /> -Um caminho para um arquivo que contém um recurso nativo|
|Segundo plano|Adicional Indica em que tipo de plano de fundo a origem deve ser usada.<br /><br /> Pode ser um dos seguintes:<br /><br /> - *Light*: a origem pode ser usada em um plano de fundo claro.<br /><br /> - *Escuro*: a origem pode ser usada em um plano de fundo escuro.<br /><br /> - *HighContrast*: a origem pode ser usada em qualquer plano de fundo no modo de alto contraste.<br /><br /> - *HighContrastLight*: a origem pode ser usada em um plano de fundo claro no modo de alto contraste.<br /><br /> -*HighContrastDark*: a origem pode ser usada em um plano de fundo escuro no modo de alto contraste.<br /><br /> Se o atributo de **plano de fundo** for omitido, a origem poderá ser usada em qualquer plano de fundo.<br /><br /> Se **o plano de fundo** for *claro*, *escuro*, *HighContrastLight*ou *HighContrastDark*, as cores da fonte nunca serão invertidas. Se o **plano de fundo** for omitido ou definido como *HighContrast*, a inversão das cores da origem será controlada pelo atributo **AllowColorInversion** da imagem.|

 Um \<Source> elemento pode ter exatamente um dos seguintes subelementos opcionais:

|**Elemento**|**Atributos (todos obrigatórios)**|**Definição**|
|-|-|-|
|\<Size>|Valor|A fonte será usada para imagens do tamanho determinado (em unidades do dispositivo). A imagem será quadrada.|
|\<SizeRange>|MinSize, MaxSize|A fonte será usada para imagens de MinSize para MaxSize (em unidades de dispositivo) inclusivamente. A imagem será quadrada.|
|\<Dimensions>|Largura, Altura|A fonte será usada para imagens da largura e da altura especificadas (em unidades do dispositivo).|
|\<DimensionRange>|MinWidth, MinHeight,<br /><br /> MaxWidth, MaxHeight|A fonte será usada para imagens da largura/altura mínima até a largura/altura máxima (em unidades do dispositivo), inclusive.|

 Um \<Source> elemento também pode ter um \<NativeResource> subelemento opcional, que define um \<Source> que é carregado de um assembly nativo em vez de um assembly gerenciado.

```xml
<NativeResource Type="type" ID="int" />
```

|**Atributo**|**Definição**|
|-|-|
|Type|Necessária O tipo do recurso nativo, XAML ou PNG|
|ID|Necessária A parte da ID de número inteiro do recurso nativo|

 **ImageList**

 O \<ImageList> elemento define uma coleção de imagens que podem ser retornadas em uma única faixa. A faixa é criada sob demanda, conforme necessário.

```xml
<ImageList>
      <ContainedImage Guid="guid" ID="int" External="true/false" />
      <!-- optional additional ContainedImage elements -->
 </ImageList>
```

|**Atributo**|**Definição**|
|-|-|
|Guid|Necessária A parte GUID do moniker da imagem|
|ID|Necessária A parte de ID do moniker da imagem|
|Externo|[Opcional, padrão false] Indica se o moniker da imagem faz referência a uma imagem no manifesto atual.|

 O moniker para a imagem contida não precisa fazer referência a uma imagem definida no manifesto atual. Se a imagem contida não puder ser encontrada na biblioteca de imagens, uma imagem de espaço reservado em branco será usada em seu lugar.

## <a name="how-to-use-the-tool"></a>Como usar a ferramenta
 **Validando um manifesto de imagem personalizada**

 Para criar um manifesto personalizado, recomendamos que você use a ferramenta ManifestFromResources para gerar o manifesto novamente. Para validar o manifesto personalizado, inicie o Visualizador de biblioteca de imagens e selecione Arquivo > definir caminhos... para abrir a caixa de diálogo Pesquisar diretórios. A ferramenta usará os diretórios de pesquisa para carregar os manifestos de imagem, mas também o usará para localizar os arquivos. dll que contêm as imagens em um manifesto, portanto, certifique-se de incluir os diretórios de manifesto e DLL nesta caixa de diálogo.

 ![Pesquisa do Visualizador de biblioteca de imagens](../../extensibility/internals/media/image-library-viewer-search.png "Pesquisa do Visualizador de biblioteca de imagens")

 Clique em **Adicionar...** para selecionar novos diretórios de pesquisa para pesquisar manifestos e suas DLLs correspondentes. A ferramenta se lembrará desses diretórios de pesquisa e eles poderão ser ativados ou desativados marcando ou desmarcando um diretório.

 Por padrão, a ferramenta tentará localizar o diretório de instalação do Visual Studio e adicionar esses diretórios à lista de diretórios de pesquisa. Você pode adicionar manualmente os diretórios que a ferramenta não encontra.

 Depois que todos os manifestos são carregados, a ferramenta pode ser usada para alternar as cores do **plano de fundo** , **dpi**, **alto contraste**ou **grayscaling** para as imagens para que um usuário possa inspecionar visualmente os ativos de imagem para verificar se eles estão sendo renderizados corretamente para várias configurações.

 ![Tela de fundo do Visualizador da biblioteca de imagens](../../extensibility/internals/media/image-library-viewer-background.png "Tela de fundo do Visualizador da biblioteca de imagens")

 A cor do plano de fundo pode ser definida como claro, escuro ou um valor personalizado. A seleção de "cor personalizada" abrirá uma caixa de diálogo de seleção de cores e adicionará essa cor personalizada à parte inferior da caixa de combinação de plano de fundo para facilitar a recuperação mais tarde.

 ![Cor personalizada do Visualizador da biblioteca de imagens](../../extensibility/internals/media/image-library-viewer-custom-color.png "Cor personalizada do Visualizador da biblioteca de imagens")

 A seleção de um moniker de imagem exibe as informações de cada imagem real por trás desse moniker no painel de detalhes da imagem à direita. O painel também permite que os usuários copiem um moniker pelo nome ou pelo valor de ID de GUID bruto:.

 ![Detalhes da imagem do Visualizador da biblioteca de imagens](../../extensibility/internals/media/image-library-viewer-image-details.png "Detalhes da imagem do Visualizador da biblioteca de imagens")

 As informações exibidas para cada fonte de imagem incluem o tipo de plano de fundo para exibi-lo, se ele pode ser ou dá suporte a Alto Contraste, para quais tamanhos eles são válidos ou se são de tamanho neutro, e se a imagem é proveniente de um assembly nativo.

 ![O Visualizador de biblioteca de imagens pode aplicar temas](../../extensibility/internals/media/image-library-viewer-can-theme.png "O Visualizador de biblioteca de imagens pode aplicar temas")

 Ao validar um manifesto de imagem, é recomendável que você implante o manifesto e a DLL de imagem em seus locais do mundo real. Isso verificará se todos os caminhos relativos estão funcionando corretamente e se a biblioteca de imagens pode localizar e carregar o manifesto e a DLL de imagem.

 **Pesquisando KnownMonikers de catálogo de imagens**

 Para corresponder melhor ao estilo do Visual Studio, uma extensão do Visual Studio pode usar imagens no catálogo de imagens do Visual Studio, em vez de criar e usar a sua própria. Isso tem a vantagem de não precisar manter essas imagens e garante que a imagem terá uma imagem de backup de alto DPI, portanto, deve parecer correta em todas as configurações de DPI às quais o Visual Studio dá suporte.

 O Visualizador de biblioteca de imagens permite que um manifesto seja pesquisado para que um usuário possa encontrar o moniker que representa um ativo de imagem e usar esse moniker no código. Para procurar imagens, insira o termo de pesquisa desejado na caixa de pesquisa e pressione Enter. A barra de status na parte inferior exibirá quantas correspondências foram encontradas fora do total de imagens em todos os manifestos.

 ![Filtro do Visualizador da biblioteca de imagens](../../extensibility/internals/media/image-library-viewer-filter.png "Filtro do Visualizador da biblioteca de imagens")

 Ao pesquisar monikers de imagem em manifestos existentes, recomendamos que você pesquise e use somente os monikers do catálogo de imagens do Visual Studio, outros monikers publicamente acessíveis intencionalmente ou seus próprios monikers personalizados. Se você usar monikers não públicos, a interface do usuário personalizada poderá ser quebrada ou ter suas imagens alteradas de maneiras inesperadas se ou quando essas imagens e monikers não públicos forem alteradas ou atualizadas.

 Além disso, é possível pesquisar por GUID. Esse tipo de pesquisa é útil para filtrar a lista para um único manifesto, ou uma subseção única de um manifesto, se esse manifesto contiver vários GUIDs.

 ![GUID do filtro do Visualizador de biblioteca de imagens](../../extensibility/internals/media/image-library-viewer-filter-guid.png "GUID do filtro do Visualizador de biblioteca de imagens")

 Por fim, também é possível pesquisar por ID.

 ![ID do filtro do Visualizador de biblioteca de imagens](../../extensibility/internals/media/image-library-viewer-filter-id.png "ID do filtro do Visualizador de biblioteca de imagens")

## <a name="notes"></a>Observações

- Por padrão, a ferramenta receberá vários manifestos de imagem presentes no diretório de instalação do Visual Studio. A única que tem monikers publicamente consumíveis é o manifesto **Microsoft. VisualStudio. ImageCatalog** . GUID: ae27a6b0-e345-4288-96df-5eaf394ee369 (não **substitua este** GUID em um manifesto personalizado) tipo: KnownMonikers

- A ferramenta tenta iniciar para carregar todos os manifestos de imagem encontrados e, portanto, pode levar vários segundos para que o aplicativo seja realmente exibido. Ele também pode ser lento ou não responsivo durante o carregamento dos manifestos.

## <a name="sample-output"></a>Saída de exemplo
 Essa ferramenta não gera nenhuma saída.
