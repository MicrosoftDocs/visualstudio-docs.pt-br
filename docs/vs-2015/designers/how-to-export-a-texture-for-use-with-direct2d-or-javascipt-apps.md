---
title: Como exportar uma textura para uso com aplicativos Direct2D ou Javascipt | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 241c25fe-764e-4e1b-ad32-b1377dcbb605
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: e2b08760e567f6e000e191703695ee0703da7215
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812134"
---
# <a name="how-to-export-a-texture-for-use-with-direct2d-or-javascipt-apps"></a>Como exportar uma textura para uso com aplicativos Direct2D ou Javascipt
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Pipeline de conteúdo de imagem pode gerar texturas que são compatíveis com as convenções de renderização interna do Direct2D. Texturas desse tipo são adequadas para uso em aplicativos que usam Direct2D e em aplicativos da Windows Store criados usando JavaScript.  
  
 Este documento demonstra essas atividades:  
  
-   Configurando a imagem de origem a ser processada pelo Pipeline de conteúdo da imagem.  
  
-   Configurando o Pipeline de conteúdo de imagem para gerar uma textura que possa ser usada em um aplicativo Direct2D ou JavaScript.  
  
    -   Gere um arquivo .dds compactado em blocos.  
  
    -   Gerar alfa pré-multiplicado.  
  
    -   Desabilite a geração de mipmap.  
  
## <a name="rendering-conventions-in-direct2d"></a>Convenções de renderização do Direct2D  
 Texturas que são usadas no contexto do Direct2D devem estar em conformidade com as seguintes convenções de renderização internas do Direct2D:  
  
-   O Direct2D implementa a transparência e a translucência usando alfa pré-multiplicado. Texturas usadas com Direct2D devem conter alfa pré-multiplicado, mesmo se a textura não usar transparência ou translucência. Para obter mais informações sobre alfa pré-multiplicado, consulte [Como exportar uma textura que contém alfa pré-multiplicado](../designers/how-to-export-a-texture-that-has-premultiplied-alpha.md).  
  
-   A textura deve ser fornecida no formato .dds, usando um desses formatos de compactação de bloco:  
  
    -   Compactação BC1_UNORM  
  
    -   Compactação BC2_UNORM  
  
    -   Compactação BC3_UNORM  
  
-   Não há suporte para mipmaps.  
  
#### <a name="to-create-a-texture-thats-compatible-with-direct2d-rendering-conventions"></a>Para criar uma textura compatível com as convenções de renderização do Direct2D  
  
1. Comece com uma textura básica. Carregue uma imagem existente ou crie uma conforme descrito em [Como criar uma textura básica](../designers/how-to-create-a-basic-texture.md). Para dar suporte à compactação de blocos no formato .dds, especifique uma textura que tenha uma largura e altura que são múltiplos de quatro em tamanho, por exemplo, 100x100, 128x128 ou 256x192. Como não há suporte para mipmap, a textura não precisa ser quadrada nem ser uma potência de dois de tamanho.  
  
2. Configure o arquivo de textura para que ele seja processado pelo Pipeline de conteúdo de imagem. No **Gerenciador de Soluções**, abra o menu de atalho do arquivo de textura que acabou de criar e selecione **Propriedades**. Na página **Propriedades de Configuração**, **Geral**, defina a propriedade **Tipo de Item** como **Pipeline de Conteúdo de Imagem**. Verifique se a propriedade **Conteúdo** está definida como **Sim** e se **Excluir do Build** está definido como **Não** e, em seguida, escolha o botão **Aplicar**. A página de propriedades de configuração **Pipeline de Conteúdo de Imagem** é exibida.  
  
3. Defina o formato de saída para um dos formatos de compactação em bloco. Na página **Propriedades de configuração**, **Pipeline de conteúdo de imagem**, **Geral**, defina a propriedade **Compactar** para **Compactação BC3_UNORM (/compress:BC3_UNORM)**. Você pode escolher qualquer um dos outros formatos BC1, BC2 ou BC3, dependendo dos seus requisitos. O Direct2D não dá suporte a texturas BC4, BC5, BC6 ou BC7 no momento. Para obter mais informações sobre os diferentes formatos de BC, consulte [Compactação em bloco (Direct3D 10)](http://msdn.microsoft.com/library/windows/desktop/bb694531.aspx).  
  
   > [!NOTE]
   >  O formato de compactação especificado determina o formato do arquivo que é produzido pelo Pipeline de conteúdo de imagem. Isso é diferente da propriedade **Format** da imagem de origem no Editor de imagens, que determina o formato do arquivo de imagens de origem quando armazenados em disco, ou seja, o *formato de trabalho*. Normalmente, não é recomendável usar um formato de trabalho compactado.  
  
4. Configure o Pipeline de conteúdo de imagem para gerar uma saída que usa alfa pré-multiplicado. Na página **Propriedades de Configuração**, **Pipeline de Conteúdo de Imagem**, **geral**, defina a propriedade **Converter para formato alfa pré-multiplicado** como **Sim (/ generatepremultipliedalpha)**.  
  
5. Configure o pipeline de conteúdo de imagem para não gerar mipmaps. Na página **Propriedades de configuração**, **Pipeline de conteúdo de imagem**, **Geral**, defina a propriedade **Gerar Mips** como **Não**.  
  
6. Escolha o botão **OK**.  
  
   Quando você compila o projeto, o Pipeline de conteúdo de imagem converte a imagem de origem do formato de trabalho para o formato de saída que você especificou, a conversão inclui o formato alfa pré-multiplicado e o resultado é copiado para o diretório de saída do projeto.



