---
title: SDK do Azure para Python
description: O SDK do Azure para Python facilita o consumo de serviços do Microsoft Azure em aplicativos Python executados em qualquer plataforma.
ms.date: 10/10/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: 9f1eb52e87cf9a411cf453c90f35ebc192616e8c
ms.sourcegitcommit: 12d6398c02e818de4fbcb4371bae9e5db6cf9509
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050216"
---
# <a name="azure-sdk-for-python"></a>SDK do Azure para Python

O SDK do Azure para Python facilita o consumo e o gerenciamento de serviços do Microsoft Azure em aplicativos em execução no Windows, MacOS e Linux.

## <a name="installation"></a>Instalação

O SDK do Azure está instalado no [Índice de Pacote Python](https://pypi.python.org/pypi/azure).

Instale a **última versão estável** (dá suporte ao Python 2.7 e 3.x) da seguinte maneira:

```command
pip install azure
```

Também é possível seguir [Instalar o Python e o SDK](https://docs.microsoft.com/azure/python-how-to-install/) na documentação do Azure.

## <a name="documentation"></a>Documentação

O [SDK do Azure para a Central de desenvolvedores do Python](https://docs.microsoft.com/python/azure/?view=azure-python) também conta com diversos recursos úteis, incluindo vários tutoriais:

- [Criar aplicativos Web no Serviço de Aplicativo do Azure no Linux](/azure/app-service/containers/quickstart-python).
- [Armazenamento de Blobs](/azure/storage/blobs/storage-quickstart-blobs-python)
- [Armazenamento de tabelas](/azure/cosmos-db/table-storage-how-to-use-python)
- [Armazenamento de filas](/azure/storage/storage-python-how-to-use-queue-storage)
- [Azure Cosmos DB](/azure/cosmos-db/sql-api-python-application)
- [Filas do Barramento de Serviço](/azure/service-bus-messaging/service-bus-python-how-to-use-queues)
- [Tópicos/assinaturas do Barramento de Serviço](/azure/service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions)
- [Gerenciamento de serviços](/azure/cloud-services/cloud-services-python-how-to-use-service-management)

Para as APIs públicas sem documentação, os testes de unidade no [repositório GitHub do SDK](https://github.com/Azure/azure-sdk-for-python) são uma boa fonte de informações:

- [Testes de unidade de Armazenamento](https://github.com/Azure/azure-storage-python/tree/master/tests)
- [Testes de unidade do Barramento de Serviço](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus/tests)
- [Testes de unidade de gerenciamento de serviços](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicemanagement-legacy/tests)

## <a name="support"></a>Suporte

O repositório GitHub do SDK está localizado em [https://github.com/Azure/azure-sdk-for-python](https://github.com/Azure/azure-sdk-for-python).

[Registre problemas no repositório](https://github.com/Azure/azure-sdk-for-python/issues) se encontrar problemas ou tiver dúvidas relacionadas ao uso do SDK.
