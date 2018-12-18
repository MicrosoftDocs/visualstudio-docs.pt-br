---
ms.technology: vs-ai-tools
ms.openlocfilehash: 5e4623715133f6203e4e967eb29eca20cb2f181e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49821351"
---
# <a name="create-an-ai-project-from-a-template-in-visual-studio"></a>Criar um projeto do IA com base em um modelo no Visual Studio

Depois de [instalar as Ferramentas do Visual Studio para IA](installation.md), será fácil criar um novo projeto de IA usando uma variedade de modelos.

1. Inicie o Visual Studio.

2. Selecione **Arquivo > Novo > Projeto** (CTRL + SHIFT + N). Na caixa de diálogo **Novo Projeto**, pesquise "**Ferramentas do AI**" e selecione o modelo desejado. Observe que a seleção de um modelo exibe uma breve descrição do que o modelo fornece.

    ![Caixa de diálogo de Novo Projeto com modelo do Python do VS2017](media/create-project/new-ai-project.png)

3. Para este Guia de início rápido, selecione o modelo "**Aplicativo do TensorFlow**", defina um local e um nome para o projeto (por exemplo, "MNIST") e selecione **OK**.

4. O Visual Studio cria o arquivo de projeto (um arquivo `.pyproj` no disco) juntamente com outros arquivos, conforme descrito pelo modelo. Com o modelo "Aplicativo do TensorFlow", o projeto contém um arquivo com o mesmo nome que o seu projeto. O arquivo é aberto no editor do Visual Studio, por padrão.

    ![Projeto resultante ao usar o modelo de aplicativo do Python](media/create-project/new-tensorflowapp.png)

5. Observe que o código já importa várias bibliotecas, incluindo TensorFlow, numpy, sys e os. Além disso, ele inicia seu aplicativo pronto com alguns argumentos de entrada para permitir facilmente a comutação do local dos dados de treinamento de entrada, dos modelos de saída e dos arquivos de log. Esses parâmetros serão úteis quando você enviar seus trabalhos para vários contextos de computação (por exemplo, um diretório diferente em sua caixa de desenvolvimento local de um Compartilhamento de Arquivos do Azure).

6. Seu projeto também tem algumas propriedades criadas para facilitar a depuração do seu aplicativo passando automaticamente argumentos de linha de comando para esses parâmetros de entrada. **Clique com botão direito do mouse** em seu projeto e selecione **Propriedades**

    ![Propriedades](media/create-project/project-properties.png)

7. Clique na guia **Depurar** para ver os Argumentos de script adicionados automaticamente. você poderá alterá-los conforme necessário para o local em que seus dados de entrada estão localizados e para o local em que você gostaria que a saída fosse armazenada.

    ![Propriedades](media/create-project//project-properties_1.png)

8. Execute o programa pressionando CTRL + F5 ou selecionando **Depurar > Iniciar Sem Depuração** no menu. Os resultados são exibidos em uma janela do console.
