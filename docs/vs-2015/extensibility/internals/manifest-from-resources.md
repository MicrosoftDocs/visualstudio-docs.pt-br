---
title: Manifest from Resources | Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 0234109b-5dcb-4d9d-acb9-a63f8bd5699c
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4827402b63eadf517f031b04b7c7cf2fe8a4f56b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537092"
---
# <a name="manifest-from-resources"></a>Manifest from Resources
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A ferramenta de Manifest from Resources é um aplicativo de console que usa uma lista de recursos de imagem (arquivos. png ou. XAML) e gera um arquivo. imagemanifest que permite que essas imagens sejam usadas com o serviço de imagem do Visual Studio. Além disso, essa ferramenta pode ser usada para adicionar imagens a um. imagemanifest existente. Essa ferramenta é útil para adicionar suporte de alto DPI e temas para imagens a uma extensão do Visual Studio. O arquivo. imagemanifest gerado deve ser incluído no e implantado como parte de uma extensão do Visual Studio (. VSIX).  
  
## <a name="how-to-use-the-tool"></a>Como usar a ferramenta  
 **Sintaxe**  
  
 ManifestFromResources/Resources: \<Dir1> ; \<Img1> /assembly: \<AssemblyName>\<Optional Args>  
  
 **Argumentos**  
  
|**Nome do comutador**|**Observações**|**Obrigatório ou opcional**|  
|-|-|-|  
|/resources|Uma lista delimitada por ponto-e-vírgula de imagens ou diretórios. Essa lista deve sempre conter a lista completa de imagens que estarão no manifesto. Se apenas uma lista parcial for fornecida, as entradas não incluídas serão perdidas.<br /><br /> Se um determinado arquivo de recursos for uma faixa de imagens, a ferramenta irá dividi-lo em imagens separadas antes de adicionar cada subimagem ao manifesto.<br /><br /> Se a imagem for um arquivo. png, recomendamos que você formate o nome como este para que a ferramenta possa preencher os atributos corretos para a imagem: \<Name> . \<Width> . \<Height> . png.|Obrigatório|  
|/assembly|O nome do assembly gerenciado (não incluindo a extensão) ou o caminho de tempo de execução do assembly nativo que hospeda os recursos (em relação ao local do tempo de execução do manifesto).|Obrigatório|  
|/Manifest|O nome a ser dado ao arquivo. imagemanifest gerado. Isso também pode incluir um caminho absoluto ou relativo para criar o arquivo em um local diferente. O nome padrão corresponde ao nome do assembly.<br /><br /> Padrão: \<Current Directory> \\<assembly \> . imagemanifest|Opcional|  
|/guidName|O nome a ser dado ao símbolo de GUID de todas as imagens no manifesto gerado.<br /><br /> Padrão: AssetsGuid|Opcional|  
|/rootPath|O caminho raiz que precisa ser removido antes da criação de URIs de recurso gerenciado. (Esse sinalizador é para ajudar com casos em que a ferramenta Obtém o caminho de URI relativo errado, fazendo com que os recursos não sejam carregados.)<br /><br /> Padrão: \<Current Directory>|Opcional|  
|/recursive|A definição desse sinalizador informa à ferramenta para pesquisar recursivamente todos os diretórios no argumento/Resources. Omitir esse sinalizador resultará em uma pesquisa somente de nível superior de diretórios.|Opcional|  
|/isNative|Defina esse sinalizador quando o argumento do assembly for um caminho para um assembly nativo. Omita esse sinalizador quando o argumento do assembly for o nome de um assembly gerenciado. (Consulte a seção observações para obter informações adicionais sobre esse sinalizador.)|Opcional|  
|/newGuids|Definir esse sinalizador informa à ferramenta para criar um novo valor para o símbolo de GUID de imagens em vez de mesclar o do manifesto existente.|Opcional|  
|/newIds|A definição desse sinalizador informa à ferramenta para criar novos valores de símbolo de ID para cada imagem em vez de Mesclar valores do manifesto existente.|Opcional|  
|/noLogo|A definição desse sinalizador impede que as informações de produtos e direitos autorais sejam impressas.|Opcional|  
|/?|Imprimir informações de ajuda.|Opcional|  
|/help|Imprimir informações de ajuda.|Opcional|  
  
 **Exemplos**  
  
- ManifestFromResources/Resources: D:\Images/assembly: My. assembly. Name/isNative  
  
- ManifestFromResources/resources:D:\Images\Image1.png;D: \Images\Image1.xaml/assembly: My. assembly. Name/manifest: MyImageManifest. imagemanifest  
  
- ManifestFromResources/resources:D:\Images\Image1.png;D: \Images\Image1.xaml/assembly: My. assembly. Name/guidName: myImages/newGuids/newIds  
  
## <a name="notes"></a>Observações  
  
- A ferramenta só dá suporte a arquivos. png e. XAML. Qualquer outra imagem ou tipo de arquivo será ignorado. Um aviso é gerado para todos os tipos sem suporte encontrados durante a análise dos recursos. Se nenhuma imagem com suporte for encontrada quando a ferramenta for concluída com a análise dos recursos, um erro será gerado  
  
- Seguindo o formato sugerido para imagens. png, a ferramenta definirá o valor de tamanho/dimensão para o. png para o tamanho especificado pelo formato, mesmo se ele for diferente do tamanho real da imagem.  
  
- O formato de largura/altura pode ser omitido para imagens. png, mas a ferramenta lerá a largura/altura real da imagem e as usará para o valor de tamanho/dimensão da imagem.  
  
- Executar essa ferramenta na mesma faixa de imagens várias vezes para o mesmo. imagemanifest resultará em entradas de manifesto duplicadas, pois a ferramenta tenta dividir a faixa de imagens em imagens autônomas e adicioná-las ao manifesto existente.  
  
- A mesclagem (omitir/newGuids ou/newIds) só deve ser feita para manifestos gerados por ferramentas. Os manifestos que foram personalizados ou gerados por meio de outros meios podem não ser mesclados corretamente.  
  
- Os manifestos gerados para assemblies nativos podem precisar ser editados manualmente após a geração para fazer com que os símbolos de ID correspondam às IDs de recurso do arquivo. rc do assembly nativo.  
  
## <a name="sample-output"></a>Saída de exemplo  
 **Manifesto de imagem simples**  
  
 Um manifesto de imagem será semelhante a este arquivo. xml:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<!-- This file was generated by the ManifestFromResources tool.-->  
<!-- Version: 14.0.15197 -->  
<ImageManifest xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/ImageManifestSchema/2014">  
  <Symbols>  
    <String Name="Resources" Value="/My.Assembly.Name;Component/Resources/Images" />  
    <Guid Name="AssetsGuid" Value="{fb41b7ef-6587-480c-aa27-5b559d42cfc9}" />  
    <ID Name="MyImage" Value="0" />  
  </Symbols>  
  <Images>  
    <Image Guid="$(AssetsGuid)" ID="$(MyImage)">  
      <Source Uri="$(Resources)/Xaml/MyImage.xaml" />  
      <Source Uri="$(Resources)/Png/MyImage.16.16.png">  
        <Size Value="16" />  
      </Source>  
    </Image>  
  </Images>  
  <ImageLists />  
</ImageManifest>  
```  
  
 **Manifesto de imagem para uma faixa de imagem**  
  
 Um manifesto de imagem para uma faixa de imagem será semelhante a este arquivo. xml:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<!-- This file was generated by the ManifestFromResources tool.-->  
<!-- Version: 14.0.15197 -->  
<ImageManifest xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/ImageManifestSchema/2014">  
  <Symbols>  
    <String Name="Resources" Value="/My.Assembly.Name;Component/Resources/ImageStrip" />  
    <Guid Name="AssetsGuid" Value="{fb41b7ef-6587-480c-aa27-5b559d42cfc9}" />  
    <ID Name="MyImageStrip_0" Value="1" />  
    <ID Name="MyImageStrip_1" Value="2" />  
    <ID Name="MyImageStrip" Value="3" />  
  </Symbols>  
  <Images>  
    <Image Guid="$(AssetsGuid)" ID="$(MyImageStrip_0)">  
      <Source Uri="$(Resources)/MyImageStrip_0.png">  
        <Size Value="16" />  
      </Source>  
    </Image>  
    <Image Guid="$(AssetsGuid)" ID="$(MyImageStrip_1)">  
      <Source Uri="$(Resources)/MyImageStrip_1.png">  
        <Size Value="16" />  
      </Source>  
    </Image>  
  </Images>  
  <ImageLists>  
    <ImageList Guid="$(AssetsGuid)" ID="$(MyImageStrip)">  
      <ContainedImage Guid="$(AssetsGuid)" ID="$(MyImageStrip_0)" />  
      <ContainedImage Guid="$(AssetsGuid)" ID="$(MyImageStrip_1)" />  
    </ImageList>  
  </ImageLists>  
</ImageManifest>  
```  
  
 **Manifesto de imagem para recursos de imagem de assembly nativa**  
  
 Um manifesto de imagem para imagens nativas será semelhante a este arquivo. xml:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<!-- This file was generated by the ManifestFromResources tool.-->  
<!-- Version: 14.0.15198 -->  
<ImageManifest xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/ImageManifestSchema/2014">  
  <Symbols>  
    <String Name="Resources" Value="..\Assembly\Folder\My.Assembly.Name" />  
    <Guid Name="AssetsGuid" Value="{442d8739-efde-46a4-8f29-e3a1e5e7f8b4}" />  
    <ID Name="MyImage1" Value="0" />  
    <ID Name="MyImage2" Value="1" />  
  </Symbols>  
  <Images>  
    <Image Guid="$(AssetsGuid)" ID="$(MyImage1)">  
      <Source Uri="$(Resources)">  
        <Size Value="16" />  
        <NativeResource ID="$(MyImage1)" Type="PNG" />  
      </Source>  
    </Image>  
    <Image Guid="$(AssetsGuid)" ID="$(MyImage2)">  
      <Source Uri="$(Resources)">  
        <Size Value="16" />  
        <NativeResource ID="$(MyImage2)" Type="PNG" />  
      </Source>  
    </Image>  
  </Images>  
  <ImageLists />  
</ImageManifest>  
```
