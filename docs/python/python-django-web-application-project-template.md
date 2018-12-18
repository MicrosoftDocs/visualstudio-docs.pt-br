---
title: Modelo de projeto Web do Django para Python
description: Uma visão geral dos modelos do Visual Studio para aplicativos Web escritos em Python usando a estrutura Django.
ms.date: 11/12/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 1e00fd7df429b219589e1e49ddbc5ccadca5e032
ms.sourcegitcommit: 6a955a2d179cd0e137942389f940d9fcbbe125de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607426"
---
# <a name="django-web-project-template"></a>Modelo de projeto Web Django

O [Django](https://www.djangoproject.com/) é uma estrutura do Python de alto nível projetada para um desenvolvimento da Web rápido, seguro e escalonável. O suporte do Python no Visual Studio fornece vários modelos de projeto para configurar a estrutura de um aplicativo Web baseado em Django. Para usar um modelo no Visual Studio, selecione **Arquivo** > **Novo** > **Projeto**, pesquise "Django" e selecione um dentre os modelos **Projeto Web em Branco do Django**, **Projeto Web do Django** e **Projeto Web de Votações do Django**. Confira o [Tutorial – Conheça o Django](learn-django-in-visual-studio-step-01-project-and-solution.md) para obter um passo a passo de todos os modelos.

O Visual Studio fornece o IntelliSense completo para projetos do Django:

- Variáveis de contexto passadas para o modelo:

    ![IntelliSense para variáveis de contexto](media/template-django-intellisense.png)

- Marcação e filtragem para elementos internos e definidos pelo usuário:

    ![IntelliSense para marcas e filtros](media/template-django-intellisense-filter.png)

- Realce de sintaxe para CSS e JavaScript inserido:

    ![CSS IntelliSense](media/template-django-intellisense-css.png)

    ![JavaScript IntelliSense](media/template-django-intellisense-js.png)

O Visual Studio também fornece [suporte de depuração](debugging-python-in-visual-studio.md) completo para projetos do Django: 

![Pontos de interrupção](media/template-django-debugging.png)

É comum que projetos do Django sejam gerenciados por meio do arquivo *manage.py*, que é um pressuposto adotado pelo Visual Studio. Se você parar de usar esse arquivo como o ponto de entrada, basicamente divide o arquivo de projeto. Nesse caso você precisa [recriar o projeto de arquivos existentes](managing-python-projects-in-visual-studio.md#create-a-project-from-existing-files) sem marcá-lo como um projeto do Django.

## <a name="django-management-console"></a>Console de gerenciamento do Django

O console de gerenciamento do Django é acessado por meio de vários comandos no menu **Projeto** ou, no **Gerenciador de Soluções**, clicando com o botão direito do mouse no projeto.

- **Abrir o Shell do Django**: abre um shell no contexto do aplicativo que permite manipular os modelos:

    ![Console](media/template-django-console-shell.png)

- **Banco de Dados de Sincronização do Django**: executa `manage.py syncdb`em uma janela **interativa**:

    ![Console](media/template-django-console-sync-db.png)

- **Coletar Estáticos**: executa `manage.py collectstatic --noinput` para copiar todos os arquivos estáticos para o caminho especificado por `STATIC_ROOT` em *settings.py*.

    ![Console](media/template-django-console-collect-static.png)

- **Validar**: executa `manage.py validate`, que relata os erros de validação nos modelos instalados especificados por `INSTALLED_APPS` em *settings.py*:

    ![Console](media/template-django-console-validate.png)

## <a name="see-also"></a>Consulte também

- [Tutorial – Conheça o Django](learn-django-in-visual-studio-step-01-project-and-solution.md)
- [Publicar no Serviço de Aplicativo do Azure](publishing-python-web-applications-to-azure-from-visual-studio.md)
