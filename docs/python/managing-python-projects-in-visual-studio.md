---
title: Gerenciando projetos de aplicativo do Python
description: A finalidade de projetos no Visual Studio, como criar e gerenciar projetos para código Python e os modelos de projeto diferentes disponíveis para Python.
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 9f5612aa166f81bf1f42983989db5bdf5422a7ef
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220463"
---
# <a name="python-projects-in-visual-studio"></a>Projetos do Python no Visual Studio

Normalmente, os aplicativos do Python são definidos com o uso somente de arquivos e pastas, mas essa estrutura pode se tornar complexa conforme os aplicativos ficam maiores e talvez envolvam arquivos gerados automaticamente, JavaScript para aplicativos Web e assim por diante. Um projeto do Visual Studio ajuda a gerenciar essa complexidade. O projeto (um arquivo *.pyproj*) identifica todos os arquivos de origem e de conteúdo associados ao projeto, contém informações de build de cada arquivo, mantém as informações para a integração com sistemas de controle de código-fonte e ajuda a organizar o aplicativo em componentes lógicos.

![Projeto do Python no Gerenciador de Soluções](media/projects-solution-explorer.png)

Além disso, os projetos são sempre gerenciados em uma *solução* do Visual Studio, que pode conter vários projetos que podem se referenciar mutuamente. Por exemplo, um projeto em Python pode fazer referência a um projeto em C++ que implementa um módulo de extensão. Com essa relação, o Visual Studio compila automaticamente o projeto em C++ (se for necessário) ao iniciar a depuração do projeto em Python. (Para obter uma discussão geral, confira [Soluções e projetos no Visual Studio](../ide/solutions-and-projects-in-visual-studio.md).)

O Visual Studio fornece uma variedade de modelos de projeto do Python para configurar diversas estruturas de aplicativo rapidamente, incluindo um modelo para criar um projeto com base em uma árvore de pastas existente e um modelo para criar um projeto limpo e vazio. Veja [Modelos de projeto](#project-templates) para obter um índice.

<a name="lightweight-usage-project-free"></a>

> [!Tip]
> Mesmo sem um projeto, o Visual Studio funciona bem com o código Python. Por exemplo, é possível abrir um arquivo Python sozinho e aproveitar o preenchimento automático, o IntelliSense e a depuração (clicando com o botão direito do mouse no editor e selecionando **Iniciar com Depuração**). No entanto, como esse código sempre usa o ambiente global padrão, talvez você veja preenchimentos incorretos ou erros, caso o código se destine a outro ambiente. Além disso, o Visual Studio analisa todos os arquivos e pacotes na pasta da qual o arquivo individual é aberto, o que pode consumir tempo considerável de CPU.
>
> É simples criar um projeto do Visual Studio com base em um código existente, conforme descrito em [Criar um projeto com base em arquivos existentes](#create-project-from-existing-files).

|   |   |
|---|---|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo (Microsoft Virtual Academy)](https://mva.microsoft.com/en-US/training-courses-embed/python-tools-for-visual-studio-2017-18121/Video-Getting-Python-Code-iLAv23LWE_3905918567) para obter uma introdução a projetos do Python (2min17s). |
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | Confira também [Deep Dive: Using source control with Python projects](https://youtu.be/Aq8eqApnugM) (Aprofundamento: Usando o controle do código-fonte com projetos do Python) (youtube.com, 8min55s). |

## <a name="add-files-assign-a-startup-file-and-set-environments"></a>Adicionar arquivos, atribuir um arquivo de inicialização e definir os ambientes

À medida que você desenvolve seu aplicativo, normalmente, você precisa adicionar novos arquivos de diferentes tipos ao projeto. Para adicionar esses arquivos, clique com o botão direito do mouse no projeto e selecione **Adicionar** > **Item existente** com o qual você procura um arquivo para adicionar ou **Adicionar** > **Novo item**, que abre uma caixa de diálogo com uma variedade de modelos de item. Conforme descrito na referência de [modelos de item](python-item-templates.md), as opções incluem arquivos vazios do Python, uma classe do Python, um teste de unidade e vários arquivos relacionados a aplicativos Web. Explore essas opções com um projeto de teste para saber o que está disponível em sua versão do Visual Studio.

Cada projeto do Python tem um arquivo de inicialização atribuído, mostrado em negrito no **Gerenciador de Soluções**. O arquivo de inicialização é o arquivo executado quando você inicia a depuração (**F5** ou **Depurar** > **Iniciar Depuração**) ou quando você executa o projeto na janela **interativa** (**Shift**+**Alt**+**F5** ou **Depurar** > **Executar Projeto na janela Interativa do Python**). Para alterá-lo, clique com o botão direito do mouse no novo arquivo e selecione **Definir como Arquivo de Inicialização**.

> [!Tip]
> Se você remover o arquivo de inicialização selecionado de um projeto e não selecionar um novo, o Visual Studio não saberá com qual arquivo do Python iniciar quando tentar executar o projeto. Nesse caso, o Visual Studio 2017 versão 15.6 e posterior mostra um erro; as versões anteriores abrem uma janela de Saída com o interpretador do Python em execução ou você vê a janela de Saída aparecer, mas, em seguida, desaparecer quase imediatamente. Se você observar algum desses comportamentos, verifique se haverá um arquivo de inicialização atribuído.
>
> Se quiser manter a janela de saída aberta por qualquer motivo, clique com o botão direito do mouse no projeto, selecione **Propriedades**, selecione a guia **Depurar** e, em seguida, adicione `-i` ao campo **Argumentos do Interpretador**. Esse argumento faz com que o interpretador entre no modo interativo após a conclusão de um programa, mantendo a janela aberta até que você pressione **Ctrl**+**Z** > **Enter** para sair.

Um novo projeto sempre é associado ao ambiente global padrão do Python. Para associar o projeto a outro ambiente (incluindo ambientes virtuais), clique com o botão direito do mouse no nó **Ambientes do Python** do projeto, selecione **Adicionar/Remover Ambientes do Python** e selecione os ambientes desejados. Para alterar o ambiente ativo, clique com o botão direito do mouse no ambiente desejado e selecione **Ativar Ambiente**, conforme mostrado abaixo. Para obter mais informações, confira [Selecionar um ambiente para um projeto](selecting-a-python-environment-for-a-project.md).

![Ativando um ambiente para um projeto do Python](media/projects-activate-environment.png)

<a name="project-types"></a>

## <a name="project-templates"></a>Modelos de projeto

O Visual Studio fornece várias maneiras para configurar um projeto do Python, do zero ou com base em um código existente. Para usar um modelo, selecione o comando de menu **Arquivo** > **Novo** > **Projeto** ou, no **Gerenciador de Soluções**, clique com o botão direito do mouse na solução e selecione **Adicionar** > **Novo Projeto**, que abrirá a caixa de diálogo **Novo Projeto** abaixo. Para ver modelos específicos do Python, pesquise "Python" ou selecione o nó **Instalado** > **Python**:

![Nova caixa de diálogo do projeto com modelos do Python](media/projects-new-project-dialog.png)

A seguinte tabela resume os modelos disponíveis no Visual Studio 2017 (nem todos os modelos estão disponíveis em todas as versões anteriores):

| Modelo | Descrição |
| --- | --- |
| [**Com base em um código existente do Python**](#create-project-from-existing-files) | Cria um projeto do Visual Studio com base em um código existente do Python em uma estrutura de pastas.  |
| **Aplicativo do Python** | Uma estrutura de projeto básica para um novo aplicativo do Python com um único arquivo de origem vazio. Por padrão, o projeto é executado no interpretador do console do ambiente global padrão, que pode ser alterado com a [atribuição de outro ambiente](selecting-a-python-environment-for-a-project.md). |
| [**Serviço de Nuvem do Azure**](python-azure-cloud-service-project-template.md) | Um projeto para um serviço de nuvem do Azure escrito em Python. |
| [**Projetos Web**](python-web-application-project-templates.md) | Projetos para aplicativos Web baseados em várias estruturas, incluindo Bottle, Django e Flask. |
| **Aplicativo do IronPython** | Semelhante ao modelo de Aplicativo do Python, mas usa o IronPython, por padrão, habilitando a interoperabilidade do .NET e a depuração de modo misto com as linguagens .NET. |
| **Aplicativo WPF do IronPython** | Uma estrutura de projeto que usa o IronPython com arquivos XAML do Windows Presentation Foundation para a interface do usuário do aplicativo. O Visual Studio fornece um designer de interface do usuário XAML, code-behind pode ser escrito no Python e o aplicativo é executado sem exibir um console. |
| **Página da Web do IronPython Silverlight** | Um projeto do IronPython executado em um navegador usando o Silverlight. O código do aplicativo do Python é incluído na página da Web como um script. Uma marca de script de texto clichê puxa um código JavaScript que inicializa o IronPython em execução dentro do Silverlight, no qual o código do Python pode interagir com o DOM. |
| **Aplicativo do Windows Forms do IronPython** | Uma estrutura de projeto que usa o IronPython com a interface do usuário criada usando o código com o Windows Forms. O aplicativo é executado sem exibir um console. |
| **Aplicativo em segundo plano (IoT)** | Dá suporte à implantação de projetos do Python a serem executados como serviços em segundo plano em dispositivos. Visite a [Central de desenvolvedores do Windows IoT](https://dev.windows.com/en-us/iot) para obter mais informações. |
| **Módulo de Extensão do Python** | Esse modelo é exibido no Visual C++ se você instalou as **ferramentas de desenvolvimento nativo do Python** com a carga de trabalho do Python no Visual Studio 2017 (confira [Instalação](installing-python-support-in-visual-studio.md)). Ele fornece a estrutura principal para uma DLL de extensão do C++, semelhante ao que é descrito em [Criar uma extensão do C++ para o Python](working-with-c-cpp-python-in-visual-studio.md). |

> [!Note]
> Como Python é uma linguagem interpretada, os projetos em Python no Visual Studio não produzem um executável autônomo como outros projetos de linguagem compilada (C#, por exemplo). Para saber mais, confira [Perguntas e respostas](overview-of-python-tools-for-visual-studio.md#questions-and-answers).

<a name="create-project-from-existing-files"></a>

### <a name="create-a-project-from-existing-files"></a>Criar um projeto com base em um código existente

> [!Important]
> O processo descrito aqui não move ou copia os arquivos de origem. Se você quiser trabalhar com uma cópia, basta primeiro duplicar a pasta.

[!INCLUDE[project-from-existing](includes/project-from-existing.md)]

## <a name="linked-files"></a>Arquivos vinculados

Os arquivos vinculados são aqueles que são inseridos em um projeto, mas que geralmente residem fora das pastas do projeto do aplicativo. Eles são exibidos no **Gerenciador de Soluções** como arquivos normais com um ícone de atalho sobreposto: ![Ícone de arquivo vinculado](media/projects-linked-file-icon.png)

Os arquivos vinculados são especificados no arquivo *.pyproj* usando o elemento `<Compile Include="...">`. Os arquivos vinculados serão implícitos se usarem um caminho relativo fora da estrutura de diretórios ou explícitos se usarem caminhos dentro do **Gerenciador de Soluções**:

```xml
<Compile Include="..\test2.py">
    <Link>MyProject\test2.py</Link>
</Compile>
```

Arquivos vinculados são ignorados em uma das seguintes condições:

- O arquivo vinculado contém metadados do Link e o caminho especificado no atributo Include reside no diretório do projeto
- O arquivo vinculado duplica um arquivo que existe na hierarquia do projeto
- O arquivo vinculado contém metadados do Link e o caminho do Link é um caminho relativo fora da hierarquia do projeto
- O caminho do link tem raiz

### <a name="work-with-linked-files"></a>Trabalhar com arquivos vinculados

Para adicionar um item existente como um link, clique com o botão direito do mouse na pasta do projeto em que deseja adicionar o arquivo e, em seguida, selecione **Adicionar** > **Item Existente**. Na caixa de diálogo exibida, selecione um arquivo e escolha **Adicionar como Link** no menu suspenso do botão **Adicionar**. Desde que não existam arquivos conflitantes, esse comando criará um link na pasta selecionada. No entanto, o link não será adicionado se já existir um arquivo com o mesmo nome ou se já existir um link para esse arquivo no projeto.

Se você tentar vincular a um arquivo que já existe nas pastas do projeto, ele será adicionado como um arquivo normal e não como um link. Para converter um arquivo em um link, selecione **Arquivo** > **Salvar Como** para salvar o arquivo em um local fora da hierarquia do projeto. O Visual Studio o converte em um link automaticamente. Da mesma forma, um link pode ser convertido novamente usando a opção **Arquivo** > **Salvar Como** para salvar o arquivo em algum lugar na hierarquia do projeto. 

Se você mover um arquivo vinculado no **Gerenciador de Soluções**, o link será movido, mas o arquivo real não será afetado. Da mesma forma, a exclusão de um link removerá o link sem afetar o arquivo.

Os arquivos vinculados não podem ser renomeados.

## <a name="references"></a>Referências

Os projetos do Visual Studio dão suporte à adição de referências a projetos e extensões, que são exibidas no nó **Referências** do **Gerenciador de Soluções**:

![Referências de extensão em projetos do Python](media/projects-extension-references.png)

Geralmente, referências de extensão indicam dependências entre projetos e são usadas para fornecer o IntelliSense em tempo de design ou a vinculação em tempo de compilação. Os projetos do Python usam referências de forma semelhante, mas devido à natureza dinâmica do Python, elas são usadas principalmente em tempo de design para fornecer um IntelliSense avançado. Elas também podem ser usadas para implantação no Microsoft Azure para instalar dependências adicionais.

### <a name="extension-modules"></a>Módulos de extensão

Uma referência a um arquivo *.pyd* habilita o IntelliSense no módulo gerado. O Visual Studio carrega o arquivo *.pyd* no interpretador do Python e examina seus tipos e suas funções. Ele também tenta analisar as cadeias de caracteres doc em funções para fornecer ajuda da assinatura.

Se, a qualquer momento, o módulo de extensão é atualizado em disco, o Visual Studio analisa o módulo novamente em segundo plano. Essa ação não tem nenhum efeito no comportamento do tempo de execução, mas alguns preenchimentos não estarão disponíveis até que a análise seja concluída.

Talvez você também precise adicionar um [caminho de pesquisa](search-paths.md) à pasta que contém o módulo.

### <a name="net-projects"></a>Projetos do .NET

Ao trabalhar com o IronPython, é possível adicionar referências aos assemblies do .NET para habilitar o IntelliSense. Para projetos do .NET na solução, clique com o botão direito do mouse no nó **Referências** do projeto do Python, selecione **Adicionar Referência**, selecione a guia **Projetos** e procure o projeto desejado. Para as DLLs baixadas separadamente, selecione a guia **Procurar** e procure a DLL desejada.

Como as referências no IronPython não estão disponíveis até uma chamada para `clr.AddReference('<AssemblyName>')` ser feita, você também precisará adicionar uma chamada apropriada para `clr.AddReference` ao assembly, normalmente no início do seu código. Por exemplo, o código criado pelo modelo de projeto **Aplicativo Windows Forms do IronPython** no Visual Studio inclui duas chamadas na parte superior do arquivo:

```python
import clr
clr.AddReference('System.Drawing')
clr.AddReference('System.Windows.Forms')

from System.Drawing import *
from System.Windows.Forms import *

# Other code omitted
```

### <a name="webpi-projects"></a>Projetos do WebPI

É possível adicionar referências a entradas de produto do WebPI para implantação nos Serviços de Nuvem do Microsoft Azure, em que é possível instalar componentes adicionais por meio do feed do WebPI. Por padrão, o feed exibido é específico ao Python e inclui o Django, o CPython e outros componentes básicos. Você também pode selecionar seu próprio feed, conforme mostrado abaixo. Ao publicar no Microsoft Azure, uma tarefa de instalação instala todos os produtos referenciados.

![Referências do WebPI](media/projects-webPI-components.png)
