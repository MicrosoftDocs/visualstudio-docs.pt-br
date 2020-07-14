---
title: Como exportar uma textura que contenha mipmaps
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 3d1ad14b-44fb-4cf0-a995-5e2f60026524
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b46a353606fc90aa89abf68d1e901675b4880b4c
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768930"
---
# <a name="how-to-export-a-texture-that-contains-mipmaps"></a>Como exportar uma textura que contenha mipmaps

O Pipeline de conteúdo de imagem pode gerar mipmaps de uma imagem de origem como parte da fase de build do projeto. Para obter certos efeitos, às vezes, você precisa especificar o conteúdo da imagem de cada nível de MIP manualmente. Quando você não precisa especificar o conteúdo da imagem de cada nível de MIP manualmente, gerar mipmaps no momento da compilação garante que o conteúdo do mipmap nunca fique fora de sincronia. Ele também elimina o custo de desempenho da geração de mipmaps em tempo de execução.

Este artigo cobre:

- Configurando a imagem de origem a ser processada pelo Pipeline de conteúdo da imagem.

- Configurando o Pipeline de conteúdo de imagem para gerar mipmaps.

## <a name="export-mipmaps"></a>Exportar mipmaps

O mapeamento mip fornece o nível de detalhe do espaço de tela automático para superfícies com textura em um aplicativo ou jogo 3D. Ele aumenta o desempenho de renderização de um jogo ou aplicativo computando previamente versões com amostra reduzida de uma textura. Pré-computar versões reduzidas significa que a textura inteira não ter sua amostra reduzida cada vez que é amostrada.

### <a name="to-export-a-texture-that-has-mipmaps"></a>Para exportar uma textura que contenha mipmaps

1. Comece com uma textura básica. Carregue um arquivo de imagem existente ou crie um, conforme descrito em [Como criar uma textura básica](../designers/how-to-create-a-basic-texture.md). Para oferecer suporte a mipmaps, especifique uma textura que tenha uma largura e altura que sejam as mesmas, por exemplo, 64x64, 256x256 ou 512x512.

2. Configure o arquivo de textura que você acabou de criar para que ele seja processado pelo Pipeline de conteúdo de imagem. No **Gerenciador de Soluções**, abra o menu de atalho do arquivo de textura que você criou e selecione **Propriedades**. Na página **Propriedades de configuração**  >  **geral** , defina a propriedade **tipo de item** como pipeline de conteúdo da **imagem**. Verifique se a propriedade **Conteúdo** está definida como **Sim** e se **Excluir do Build** está definido como **Não**. Escolha **Aplicar**.

   A página de propriedades de configuração **Pipeline de Conteúdo de Imagem** é exibida.

3. Configure o Pipeline de conteúdo de imagem para gerar mipmaps. Na página **Propriedades de configuração**do  >  **pipeline de conteúdo**  >  **geral** , defina a propriedade **gerar MIPS** como **Sim (/generatemips)**.

4. Selecione **OK**.

Quando você cria o projeto, o Pipeline de conteúdo de imagem converte a imagem de origem do formato de trabalho para o formato de saída que você especificou, incluindo níveis de MIP. O resultado é copiado para o diretório de saída do projeto.
