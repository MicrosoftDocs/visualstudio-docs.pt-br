---
title: Visualizador da biblioteca de imagem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9d9c7fbb-ebae-4b20-9dd8-3c9070c0d0d1
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6c0e277a123fe24da9824fae94b13eee686f5663
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51778008"
---
# <a name="image-library-viewer"></a>Visualizador da biblioteca de imagens
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A ferramenta Visualizador de biblioteca de imagens do Visual Studio pode carregar e pesquisar os manifestos de imagem, permitindo que o usuário para manipulá-los da mesma maneira que faria do Visual Studio. O usuário pode alterar o plano de fundo, tamanhos, DPI, alto contraste e outras configurações. A ferramenta também exibe informações de carregamento para cada manifesto de imagem e exibe informações de origem para cada imagem no manifesto de imagem. Essa ferramenta é útil para:  
  
1. Diagnosticando erros  
  
2. Atributos de garantir que estão definidos corretamente nos manifestos de imagem personalizada  
  
3. Procurando por imagens no catálogo de imagem do Visual Studio para que uma extensão do Visual Studio pode usar as imagens que se ajustam o estilo do Visual Studio  
  
   ![Imagem Hero de Visualizador de biblioteca](../../extensibility/internals/media/image-library-viewer-hero.png "biblioteca herói de Visualizador de imagem")  
  
   **Moniker de imagem**  
  
   Um moniker de imagem (ou moniker de forma abreviada) é um par de GUID:ID que identifica exclusivamente um ativo de imagem ou um ativo de lista de imagem da biblioteca de imagens.  
  
   **Arquivos de manifesto de imagem**  
  
   Arquivos de manifesto (.imagemanifest) da imagem são arquivos XML que definem um conjunto de ativos de imagem, os identificadores que representam os ativos e a imagem real ou imagens que representam cada ativo. Manifestos de imagem podem definir imagens independentes ou listas de imagens para dar suporte de interface do usuário. Além disso, há atributos que podem ser definidos no ativo ou nas imagens individuais por trás de cada ativo para alterar quando e como esses ativos são exibidos.  
  
   **Esquema de manifesto de imagem**  
  
   Um manifesto de conclusão de imagem tem esta aparência:  
  
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
  
 Como ajudam a um legibilidade e a manutenção, o manifesto de imagem pode usar símbolos para valores de atributo. Símbolos são definidos como este:  
  
```xml  
<Symbols>  
      <Import Manifest="manifest" />  
      <Guid Name="ShellCommandGuid" Value="8ee4f65d-bab4-4cde-b8e7-ac412abbda8a" />  
      <ID Name="cmdidSaveAll" Value="1000" />  
      <String Name="AssemblyName" Value="Microsoft.VisualStudio.Shell.UI.Internal" />  
</Symbols>  
```  
  
|||  
|-|-|  
|**Subelemento**|**Definição**|  
|Importar|Importa os símbolos do arquivo de manifesto fornecido para uso no manifesto do atual.|  
|Guid|O símbolo representa um GUID e deve corresponder ao GUID de formatação.|  
|ID|O símbolo representa uma ID e deve ser um inteiro não negativo.|  
|Cadeia de Caracteres|O símbolo representa um valor de cadeia de caracteres arbitrária.|  
  
 Símbolos são referenciados usando a sintaxe $(symbol-name) e diferencia maiusculas de minúsculas:  
  
```xml  
<Image Guid="$(ShellCommandGuid)" ID="$(cmdidSaveAll)" >  
      <Source Uri="/$(AssemblyName);Component/Resources/image.xaml" />  
</Image>  
```  
  
 Alguns símbolos são predefinidos para todos os manifestos. Eles podem ser usados no atributo de Uri do \<fonte > ou \<Import > elemento aos caminhos de referência no computador local.  
  
|||  
|-|-|  
|**Símbolo**|**Descrição**|  
|CommonProgramFiles|O valor da variável de ambiente % CommonProgramFiles %|  
|LocalAppData|O valor da variável de ambiente % LocalAppData %|  
|ManifestFolder|A pasta que contém o arquivo de manifesto|  
|Meus documentos|O caminho completo da pasta Meus documentos do usuário atual|  
|ProgramFiles|O valor da variável de ambiente % ProgramFiles %|  
|Sistema|A pasta Windows\System32|  
|WinDir|O valor da variável de ambiente % WinDir %|  
  
 **Image**  
  
 O \<imagem > elemento define uma imagem que pode ser referenciada por um moniker. O GUID e ID juntas formam o moniker de imagem. O identificador de origem para a imagem deve ser exclusivo entre a biblioteca de imagem inteira. Se mais de uma imagem tem um identificador de origem determinado, o primeiro encontrado ao compilar a biblioteca é aquele que é mantido.  
  
 Ele deve conter pelo menos uma fonte. Embora fontes de tamanho neutro dará os melhores resultados em uma ampla gama de tamanhos, eles não são necessários. Se o serviço é solicitado para uma imagem de um tamanho não definido no \<imagem > elemento e não há neutros em relação ao tamanho da fonte, o serviço será escolher a melhor fonte de tamanho específico e dimensioná-lo para o tamanho solicitado.  
  
```xml  
<Image Guid="guid" ID="int" AllowColorInversion="true/false">  
      <Source ... />  
      <!-- optional additional Source elements -->  
</Image>  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|Guid|[Obrigatório] A parte GUID do moniker de imagem|  
|ID|[Obrigatório] A parte de identificação do moniker de imagem|  
|AllowColorInversion|[Opcional, padrão Verdadeiro] Indica se a imagem pode ter suas cores invertidas programaticamente quando usado em um plano de fundo escuro.|  
  
 **Source**  
  
 O \<origem > elemento define um ativo de origem única imagem (XAML e PNG).  
  
```xml  
<Source Uri="uri" Background="background">  
      <!-- optional NativeResource element -->  
 </Source>  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|URI|[Obrigatório] Um URI que define onde a imagem pode ser carregada de. Ele pode ser um dos seguintes:<br /><br /> -A [Pack URI](http://msdn.microsoft.com/library/aa970069\(v=vs.100\).aspx) usando o aplicativo: autoridade<br /><br /> -Referência de recurso um componente absoluto<br /><br /> -Um caminho para um arquivo que contém um recurso nativo|  
|Informações preliminares|[Opcional] Indica qual tipo de plano de fundo que a fonte se destina a ser usado.<br /><br /> Ele pode ser um dos seguintes:<br /><br /> - *Luz*: A fonte pode ser usada no plano de fundo claro.<br /><br /> - *Escuro*: A origem pode ser usada em um plano de fundo escuro.<br /><br /> - *HighContrast*: A fonte pode ser usada em qualquer tela de fundo no modo de alto contraste.<br /><br /> - *HighContrastLight*: A fonte pode ser usada no plano de fundo claro no modo de alto contraste.<br /><br /> -*HighContrastDark*: A origem pode ser usada em um plano de fundo escuro no modo de alto contraste.<br /><br /> Se o **plano de fundo** atributo for omitido, a origem pode ser usada em qualquer tela de fundo.<br /><br /> Se **plano de fundo** é *luz*, *escuro*, *HighContrastLight*, ou *HighContrastDark*, o cores da fonte nunca são invertidas. Se **plano de fundo** é omitido ou definido como *HighContrast*, a inversão de cores da fonte é controlada pela imagem **AllowColorInversion** atributo.|  
  
 Um \<origem > elemento pode ter exatamente um dos seguintes subelementos opcionais:  
  
||||  
|-|-|-|  
|**Elemento**|**Atributos (todos necessária)**|**Definição**|  
|\<Tamanho >|Valor|A origem será usada para imagens de determinado tamanho (em unidades de dispositivo). A imagem será quadrada.|  
|\<SizeRange >|MinSize, MaxSize|A origem será usada para imagens de MinSize para tamanho máximo (em unidades de dispositivo), inclusive. A imagem será quadrada.|  
|\<Dimensões >|Largura, altura|A origem será usada para imagens de determinada largura e altura (em unidades de dispositivo).|  
|\<DimensionRange >|MinWidth, MinHeight,<br /><br /> MaxWidth, MaxHeight|A origem será usada para imagens de largura/altura mínimo para a largura/altura máxima (em unidades de dispositivo), inclusive.|  
  
 Um \<origem > elemento também pode ter um recurso opcional \<NativeResource > subelemento, que define um \<fonte > que é carregada a partir de um assembly nativo em vez de um assembly gerenciado.  
  
```xml  
<NativeResource Type="type" ID="int" />  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|Tipo|[Obrigatório] O tipo do recurso nativo, XAML ou PNG|  
|ID|[Obrigatório] A parte de ID inteiro do recurso nativo|  
  
 **ImageList**  
  
 O \<ImageList > elemento define uma coleção de imagens que podem ser retornadas em uma única faixa. A faixa é criada sob demanda, conforme necessário.  
  
```xml  
<ImageList>  
      <ContainedImage Guid="guid" ID="int" External="true/false" />  
      <!-- optional additional ContainedImage elements -->  
 </ImageList>  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|Guid|[Obrigatório] A parte GUID do moniker de imagem|  
|ID|[Obrigatório] A parte de identificação do moniker de imagem|  
|Externo|[Opcional, padrão é false] Indica se o moniker de imagem faz referência a uma imagem no manifesto do atual.|  
  
 O identificador de origem para a imagem independente não tem que fazer referência a uma imagem definida no manifesto do atual. Se a imagem independente não for encontrada na biblioteca de imagem, uma imagem de espaço reservado em branco será usada em seu lugar.  
  
## <a name="how-to-use-the-tool"></a>Como usar a ferramenta  
 **Validando um manifesto de imagem personalizada**  
  
 Para criar um manifesto personalizado, é recomendável que você use a ferramenta ManifestFromResources para gerar automaticamente o manifesto. Para validar o manifesto personalizado, inicie o Visualizador da biblioteca de imagens e selecione Arquivo > Definir caminhos... Para abrir a caixa de diálogo de pesquisa de diretórios. A ferramenta usará os diretórios de pesquisa para carregar os manifestos de imagem, mas ele também usá-lo para localizar os arquivos. dll que contêm as imagens em um manifesto, certifique-se de incluir o manifesto e os diretórios DLL nesta caixa de diálogo.  
  
 ![Pesquisa do Visualizador de biblioteca de imagem](../../extensibility/internals/media/image-library-viewer-search.png "pesquisa do Visualizador de biblioteca de imagem")  
  
 Clique em **adicionar...** para selecionar novos diretórios de pesquisa para procurar manifestos e suas DLLs correspondentes. A ferramenta irão se lembrar desses diretórios de pesquisa, e pode ser ativados ou desativado, marcando ou desmarcando um diretório.  
  
 Por padrão, a ferramenta tentará localizar o diretório de instalação do Visual Studio e adicionar esses diretórios à lista de diretórios de pesquisa. Você pode adicionar manualmente os diretórios para que a ferramenta não encontra.  
  
 Depois que todos os manifestos são carregados, a ferramenta pode ser usada para ativar/desativar **plano de fundo** cores **DPI**, **alto contraste**, ou **escala de cinza** para as imagens para que um usuário possa inspecionar visualmente os ativos de imagem para verificar se estão sendo processados corretamente para várias configurações.  
  
 ![Imagem de plano de fundo de Visualizador de biblioteca](../../extensibility/internals/media/image-library-viewer-background.png "imagem de plano de fundo de Visualizador de biblioteca")  
  
 A cor do plano de fundo pode ser definida como claro, escuro ou um valor personalizado. Selecionar "Cor personalizada" abrirá uma caixa de diálogo de seleção de cor e adicione essa cor personalizada na parte inferior da caixa de combinação de plano de fundo fácil de lembrar mais tarde.  
  
 ![Cor personalizada do Visualizador de biblioteca de imagem](../../extensibility/internals/media/image-library-viewer-custom-color.png "cor personalizada do Visualizador de biblioteca de imagem")  
  
 Selecionar um moniker de imagem exibe as informações para cada imagem real por trás desse moniker no painel de detalhes da imagem à direita. O painel também permite que os usuários copiem um moniker por nome ou valor bruto GUID:ID.  
  
 ![Detalhes da biblioteca de imagem Visualizador de imagem](../../extensibility/internals/media/image-library-viewer-image-details.png "detalhes da biblioteca de imagem Visualizador de imagem")  
  
 As informações exibidas para cada fonte de imagem incluem o tipo de plano de fundo para exibi-lo, se ele pode ser com tema ou dá suporte a alto contraste, quais são os tamanhos é válido para ou é neutro de tamanho e se a imagem é proveniente de um assembly nativo.  
  
 ![Visualizador da biblioteca de imagem pode tema](../../extensibility/internals/media/image-library-viewer-can-theme.png "Visualizador da biblioteca de imagem pode tema")  
  
 Ao validar um manifesto de imagem, é recomendável que você implante a imagem DLL em seus locais do mundo real e o manifesto. Isso vai verificar se todos os caminhos relativos estão funcionando corretamente e que a biblioteca de imagens pode localizar e carregar a DLL de imagem e o manifesto.  
  
 **Pesquisando o catálogo de imagens KnownMonikers**  
  
 Para melhor corresponder ao estilo do Visual Studio, uma extensão do Visual Studio pode usar imagens no catálogo de imagens do Visual Studio em vez de criar e usar seu próprio. Isso tem a vantagem de não precisar manter essas imagens e garante que a imagem terá uma imagem de backup com alto DPI para que pareça correto no Visual Studio dá suporte a todas as configurações de DPI.  
  
 O Visualizador da biblioteca de imagem permite que um manifesto a ser pesquisado para que um usuário possa localizar o identificador de origem que representa um ativo de imagem e usar esse moniker no código. Para procurar imagens, insira o termo de pesquisa desejada na caixa de pesquisa e pressione Enter. A barra de status na parte inferior exibirá quantas correspondências foram encontradas fora do total de imagens em todos os manifestos.  
  
 ![Filtro do Visualizador de biblioteca de imagem](../../extensibility/internals/media/image-library-viewer-filter.png "filtro do Visualizador de biblioteca de imagem")  
  
 Ao procurar identificadores de origem de imagem nos manifestos existentes, é recomendável que você procure e use somente os monikers do catálogo Visual Studio imagem, outros monikers intencionalmente publicamente acessíveis ou suas própria monikers personalizados. Se você usar monikers não públicos, interface do usuário personalizada pode ser interrompida ou suas imagens mudaram de maneiras inesperadas se ou quando os monikers não públicos e imagens são alteradas ou atualizadas.  
  
 Além disso, é possível pesquisar pelo GUID. Esse tipo de pesquisa é útil para filtrar a lista para um único manifesto ou única subseção de um manifesto se esse manifesto contém vários GUIDs.  
  
 ![Filtro do Visualizador de biblioteca GUID da imagem](../../extensibility/internals/media/image-library-viewer-filter-guid.png "biblioteca visualizador filtro GUID de imagem")  
  
 Por fim, pesquisar por ID é possível também.  
  
 ![ID de filtro do Visualizador de biblioteca de imagem](../../extensibility/internals/media/image-library-viewer-filter-id.png "ID de filtro do Visualizador de biblioteca de imagem")  
  
## <a name="notes"></a>Observações  
  
-   Por padrão, a ferramenta vai receber vários manifestos de imagem presentes no diretório de instalação do Visual Studio. É o único que tem monikers publicamente consumíveis a **Microsoft.VisualStudio.ImageCatalog** de manifesto. GUID: ae27a6b0-e345-4288-96df-5eaf394ee369 (fazer **não** substituir esse GUID em um manifesto personalizado) tipo: KnownMonikers  
  
-   A ferramenta na inicialização para carregar todos os manifestos de imagem que ele encontrar, portanto, pode levar vários segundos para que o aplicativo seja exibido, na verdade, as tentativas. Ele também pode ser lenta ou que não responde ao carregar os manifestos.  
  
## <a name="sample-output"></a>Saída de Exemplo  
 Essa ferramenta não gera nenhuma saída.

