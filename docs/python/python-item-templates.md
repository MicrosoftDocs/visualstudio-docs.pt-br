---
title: Modelos de item para projetos do Python
description: Uma lista de referência de modelos de item para o projeto do Python que estão disponíveis na caixa de diálogo Adicionar > Novo Item no Visual Studio.
ms.date: 12/06/2018
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 528606356c2d976de71ab2c0317a1a0236d2e63f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533387"
---
# <a name="python-item-templates"></a>Modelos de item do Python

Os modelos de item estão disponíveis em projetos do Python **Project**por meio do  >  comando de menu**Adicionar novo item** do projeto ou do comando **Adicionar**  >  **novo item** no menu de contexto no **Gerenciador de soluções**.

![Caixa de diálogo Adicionar Novo Item](media/project-item-templates.png)

Se você usar o nome fornecido para o item, o modelo geralmente criará um ou mais arquivos e pastas dentro da pasta que está atualmente marcada no projeto (ao clicar duas vezes com o botão direito do mouse em uma pasta para exibir o menu de contexto, essa pasta será automaticamente marcada). Se você adicionar um item, ele será incluído no projeto do Visual Studio e será exibido no **Gerenciador de Soluções**.

A tabela a seguir explica brevemente o efeito de cada modelo de item em um projeto do Python:

| Modelo | O que o modelo cria |
| --- | --- |
| **Arquivo vazio do Python** | Um arquivo vazio com a extensão *.py*. |
| **Classe Python** | Um arquivo *.py* que contém uma única definição de classe vazia do Python. |
| **Pacote do Python** | Uma pasta que contém um arquivo * \_ \_ init \_ \_ . py* . |
| **Teste de Unidade do Python** | Um arquivo *.py* com um único teste de unidade baseado na estrutura `unittest`, juntamente com uma chamada a `unittest.main()` para executar os testes no arquivo. |
| **Página HTML** | Um arquivo *.html* com uma estrutura de página simples que consiste em um `<head>` e um elemento `<body>`. |
| **JavaScript** | Um arquivo *.js* vazio. |
| **Folha de estilos** | Um arquivo *.css* que contém um estilo vazio para `body`. |
| **Arquivo de texto** | Um arquivo *.txt* vazio. |
| **Aplicativo Django 1.9**<br/>**Aplicativo Django 1.4** | Uma pasta com o nome do aplicativo que contém os arquivos principais de um aplicativo do Django conforme explicado em [Aprender Django no Visual Studio, Etapa 2 de 2](learn-django-in-visual-studio-step-02-create-an-app.md#step-2-1-create-an-app-with-a-default-structure) para o Django 1.9. No caso do Django 1.4, a pasta *migrations*, o arquivo *admin.py* e o arquivo *apps.py* não estão incluídos. |
| **Janela WPF do IronPython** | Uma janela WPF consiste em dois arquivos lado a lado: um arquivo *.xaml* que define um `<Window>` com um elemento `<Grid>` vazio e um arquivo *.py* associado que carrega o arquivo XAML usando a biblioteca do `wpf`. Normalmente usado em um projeto criado usando um dos modelos de projeto do IronPython. Confira [Gerenciar projetos Python – Modelos de projetos](managing-python-projects-in-visual-studio.md#project-templates). |
| **Arquivos de Suporte de Função da Web** | Uma pasta *bin* na raiz do projeto (independentemente da pasta escolhida no projeto). A pasta contém um script de implantação padrão e um arquivo *web.config* para funções da web do Serviço de Nuvem do Azure. O modelo também inclui um arquivo *readme.html* que explica os detalhes. |
| **Arquivos de suporte à função de trabalho** | Uma pasta *bin* na raiz do projeto (independentemente da pasta escolhida no projeto). A pasta contém o script de implantação e lançamento padrão, além de um arquivo *web.config*, para funções de trabalho do Serviço de Nuvem do Azure. O modelo também inclui um arquivo *readme.html* que explica os detalhes. |
| **web.config do Azure (FastCGI)** | Um arquivo *web.config* que contém entradas para aplicativos que usam um objeto [WSGI](https://wsgi.readthedocs.io/en/latest/) para tratar das conexões de entrada. Normalmente, esse arquivo é implantado na raiz de um servidor Web que executa o IIS. Para saber mais, confira [Configurar um aplicativo para IIS](configure-web-apps-for-iis-windows.md). |
| **web.config do Azure (HttpPlatformHandler)** | Um arquivo *web.config* que contém entradas para aplicativos que escutam conexões de entrada com um soquete. Normalmente, esse arquivo é implantado na raiz de um servidor Web que executa o IIS, como o Serviço de Aplicativo do Azure. Para saber mais, confira [Configurar um aplicativo para IIS](configure-web-apps-for-iis-windows.md). |
| **Arquivos estáticos web.config do Azure** | Um arquivo *web.config* normalmente adicionado a uma pasta *static* (ou outra pasta que contém itens estáticos) para desabilitar o processamento do Python para essa pasta. Esse arquivo de configuração funciona em conjunto com um dos arquivos de configuração FastCGI ou HttpPlatformHandler acima. Para saber mais, confira [Configurar um aplicativo para IIS](configure-web-apps-for-iis-windows.md). |
| **Depuração remota de web.config do Azure** | Preterido (foi usado para depuração remota no Serviço de Aplicativo do Azure para Windows, que não é mais suportado). |

## <a name="see-also"></a>Confira também

- [Gerenciar projetos Python – Modelos de projetos](managing-python-projects-in-visual-studio.md#project-templates)
- [Modelos de projeto Web do Python](python-web-application-project-templates.md)
- [Publicar no Serviço de Aplicativo do Azure](publishing-python-web-applications-to-azure-from-visual-studio.md)
