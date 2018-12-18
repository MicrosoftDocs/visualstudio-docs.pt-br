---
title: Manifesto de recursos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0234109b-5dcb-4d9d-acb9-a63f8bd5699c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 514135e5c6ba932d7b3b4319dd39c1df4e8cb212
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31134270"
---
# <a name="manifest-from-resources"></a>Manifesto de recursos
O manifesto da ferramenta de recursos é um aplicativo de console que usa uma lista de recursos de imagem (arquivos. png ou. XAML) e gera um arquivo de .imagemanifest que permite que as imagens a serem usadas com o serviço de imagem do Visual Studio. Além disso, essa ferramenta pode ser usada para adicionar imagens a um .imagemanifest existente. Essa ferramenta é útil para adicionar suporte a alto DPI e temas para imagens a uma extensão do Visual Studio. O arquivo gerado .imagemanifest deve ser incluído no e implantado como parte de uma extensão do Visual Studio (.vsix).  
  
## <a name="how-to-use-the-tool"></a>Como usar a ferramenta  
 **Sintaxe**  
  
 ManifestFromResources /recursos:\<Dir1 >;\< Img1 > /assembly:\<AssemblyName > \<Args opcional >  
  
 **Argumentos**  
  
||||  
|-|-|-|  
|**Nome do comutador**|**Observações**|**Obrigatório ou opcional**|  
|/recursos|Uma lista separada por ponto-e-vírgula de imagens ou diretórios. Essa lista deve sempre conter a lista completa de imagens que estarão no manifesto. Se apenas uma lista parcial for especificada, as entradas não incluídas serão perdidas.<br /><br /> Se um arquivo de recurso fornecido é uma faixa de imagem, a ferramenta será dividi-lo em imagens separadas antes de adicionar cada subimage no manifesto.<br /><br /> Se a imagem for um arquivo. png, é recomendável formatar o nome desta forma que a ferramenta pode preencher os atributos à direita para a imagem: \<Name >.\< Largura >. \<Altura >. PNG.|Necessária|  
|/assembly|O nome do assembly gerenciado (não incluindo a extensão) ou o caminho de tempo de execução do assembly nativo que hospeda os recursos (relativo ao local de tempo de execução do manifesto).|Necessária|  
|/ manifesto|O nome a ser atribuído ao arquivo .imagemanifest gerado. Isso também pode incluir um caminho absoluto ou relativo para criar o arquivo em um local diferente. O nome padrão corresponde ao nome do assembly.<br /><br /> Padrão: \<diretório atual >\\< Assembly\>.imagemanifest|Opcional|  
|/guidName|O nome a ser atribuído para o símbolo GUID para todas as imagens no manifesto gerado.<br /><br /> Padrão: AssetsGuid|Opcional|  
|/rootPath|O caminho raiz que precisa ser removidos antes de criar URIs de recursos gerenciados. (Esse sinalizador é ajudar com casos em que a ferramenta obtém o caminho URI relativo errado, fazendo com que os recursos para a falha ao carregar.)<br /><br /> Padrão: \<diretório atual >|Opcional|  
|/Recursive|Defina esse sinalizador informa a ferramenta recursivamente todos os diretórios de pesquisa no argumento /recursos. Omitir esse sinalizador resultará em uma pesquisa somente superior nível de diretórios.|Opcional|  
|/isNative|Defina esse sinalizador quando o argumento de assembly é um caminho para um assembly nativo. Omita esse sinalizador quando o argumento de assembly é o nome de um assembly gerenciado. (Consulte a seção Observações para obter informações adicionais sobre este sinalizador).|Opcional|  
|/newGuids|Definir esse sinalizador indica que a ferramenta para criar um novo valor para o símbolo GUID as imagens em vez de mesclagem do manifesto existente.|Opcional|  
|/newIds|Defina esse sinalizador informa a ferramenta para criar novos valores de símbolo de ID para cada imagem em vez de valores do manifesto de existentes de mesclagem.|Opcional|  
|/noLogo|Defina esse sinalizador para de informações de produto e os direitos autorais da impressão.|Opcional|  
|/?|Imprima informações de Ajuda.|Opcional|  
|/help|Imprima informações de Ajuda.|Opcional|  
  
 **Exemplos**  
  
-   ManifestFromResources /resources:D:\Images /assembly:My.Assembly.Name /isNative  
  
-   ManifestFromResources /resources:D:\Images\Image1.png;D:\Images\Image1.xaml /assembly:My.Assembly.Name /manifest:MyImageManifest.imagemanifest  
  
-   ManifestFromResources /resources:D:\Images\Image1.png;D:\Images\Image1.xaml /assembly:My.Assembly.Name /guidName:MyImages /newGuids /newIds  
  
## <a name="notes"></a>Observações  
  
-   A ferramenta só oferece suporte a arquivos. PNG e. XAML. Quaisquer outros tipos de arquivo de imagem ou serão ignorados. Um aviso será gerado para todos os tipos sem suporte encontrados ao analisar os recursos. Se nenhum suporte para imagens são encontradas quando a ferramenta for concluída os recursos de análise, um erro será gerado  
  
-   Seguindo o formato sugerido para imagens PNG, a ferramenta definirá o valor de tamanho/dimensão para o PNG para o tamanho do formato especificado, mesmo se for diferente do tamanho real da imagem.  
  
-   O formato de largura/altura pode ser omitido para imagens PNG, mas a ferramenta lerá largura/altura da imagem real e usá-las para o valor de dimensão/tamanho da imagem.  
  
-   Executar essa ferramenta na faixa de imagens várias vezes para o mesmo .imagemanifest resultará em entradas duplicadas de manifesto, porque a ferramenta tenta dividir a faixa de imagem em imagens autônomas e adicioná-las ao manifesto existente.  
  
-   Mesclando (omitindo /newGuids ou /newIds) deve ser feito somente para gerados por ferramenta manifestos. Manifestos que foram personalizados ou gerados por outros meios não podem ser mesclados corretamente.  
  
-   Manifestos que são gerados para assemblies nativo talvez precise ser editados manualmente após a geração para tornar os símbolos de ID corresponde ao recurso IDs de arquivo. RC do assembly nativo.  
  
## <a name="sample-output"></a>Saída de Exemplo  
 **Manifesto de imagem simples**  
  
 Um manifesto de imagem será semelhante a este arquivo. XML:  
  
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
  
 Um manifesto de imagem para uma faixa de imagem será semelhante a este arquivo. XML:  
  
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
  
 **Manifesto de imagem para recursos de imagem de assembly nativo**  
  
 Um manifesto de imagem para imagens nativas será semelhante a este arquivo. XML:  
  
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