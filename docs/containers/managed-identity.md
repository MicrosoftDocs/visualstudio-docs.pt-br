---
title: Como usar a identidade gerenciada com o Bridge para kubernetes
ms.technology: vs-azure
ms.date: 04/28/2021
ms.topic: conceptual
description: Saiba como usar a identidade gerenciada do Azure Active Directory (AD do Azure) em um cluster AKS com ponte para kubernetes
monikerRange: '>=vs-2019'
manager: jmartens
author: ghogen
ms.author: ghogen
ms.openlocfilehash: e4847b25531b48c8200a2620ca3e975f9677c881
ms.sourcegitcommit: 60b7a6159045a44293043a519c8ea6d915bf2c31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2021
ms.locfileid: "108335084"
---
# <a name="use-managed-identity-with-bridge-to-kubernetes"></a>Usar identidade gerenciada com a ponte para kubernetes

Se o seu cluster AKS usa recursos [gerenciados](/azure/active-directory/managed-identities-azure-resources/overview) de segurança de identidade para proteger o acesso a segredos e recursos, o Bridge para o kubernetes precisa de alguma configuração especial para garantir que ele possa funcionar com esses recursos. Um token Azure Active Directory (AD) precisa ser baixado para o computador local para garantir que a execução e a depuração locais sejam protegidas corretamente, e isso exige uma configuração especial no Bridge para o kubernetes. Este artigo mostra como configurar a ponte para o kubernetes para trabalhar com serviços que usam identidade gerenciada.

## <a name="how-to-configure-your-service-to-use-managed-identity"></a>Como configurar seu serviço para usar identidade gerenciada

Para habilitar um computador local com suporte para identidade gerenciada, no arquivo *KubernetesLocalConfig. YAML* , na `enableFeatures` seção, adicione `ManagedIdentity` . Adicione a `enableFeatures` seção se ela ainda não estiver lá.

```yaml
enableFeatures:
    ManagedIdentity
```

> [!WARNING]
> Certifique-se de usar apenas a identidade gerenciada para a ponte para kubernetes ao trabalhar com clusters de desenvolvimento, não clusters de produção, porque o token do Azure AD é buscado no computador local, o que apresenta um risco de segurança potencial.

Se você não tiver um arquivo *KubernetesLocalConfig. YAML* , poderá criar um; consulte [como: configurar a ponte para o kubernetes](configure-bridge-to-kubernetes.md).

## <a name="how-to-fetch-the-azure-active-directory-tokens"></a>Como buscar os tokens de Azure Active Directory

Você deve garantir que você esteja confiando em um <xref:Azure.Identity.DefaultAzureCredential> ou <xref:Azure.Identity.ManagedIdentityCredential> no código ao buscar o token.

O código C# a seguir mostra como buscar as credenciais da conta de armazenamento quando você usa `ManagedIdentityCredential` :

```csharp
var credential = new ManagedIdentityCredential(miClientId);
Console.WriteLine("Created credential");
var containerClient = new BlobContainerClient(new Uri($"https://{accountName}.blob.windows.net/{containerName}"), credential);
Console.WriteLine("Created blob client");
```

O código a seguir mostra como buscar as credenciais da conta de armazenamento ao usar o DefaultAzureCredential:

```csharp
var credential = new DefaultAzureCredential();
Console.WriteLine("Created credential");
var containerClient = new BlobContainerClient(new Uri($"https://{accountName}.blob.windows.net/{containerName}"), credential);
Console.WriteLine("Created blob client");
```

Para saber como acessar outros recursos do Azure usando a identidade gerenciada, consulte a seção [próximas etapas](#next-steps) .

## <a name="receive-azure-alerts-when-tokens-are-downloaded"></a>Receber alertas do Azure quando os tokens forem baixados

Sempre que você usa a ponte para kubernetes em um serviço, o token do Azure AD é baixado para o computador local. Você pode habilitar alertas do Azure para serem notificados quando isso ocorrer. Para obter informações, consulte [habilitar o Azure defender](/azure/security-center/enable-azure-defender). Lembre-se de que há um encargo (após um período de avaliação de 30 dias).

## <a name="next-steps"></a>Próximas etapas

Agora que você configurou o Bridge para kubernetes para trabalhar com seu cluster AKS que usa identidade gerenciada, você pode depurar normalmente. Consulte [ponte para kubernetes. MD # Connect-to-your-cluster-and-debug-a-Service].

Saiba mais sobre como usar a identificação gerenciada para acessar recursos do Azure seguindo estes tutoriais:

- [Tutorial: Usar uma identidade gerenciada atribuída pelo sistema da VM do Linux para acessar o Armazenamento do Azure](/azure/active-directory/managed-identities-azure-resources/tutorial-linux-vm-access-storage)
- [Tutorial: Usar uma identidade gerenciada atribuída pelo sistema da VM do Linux para acessar o Azure Data Lake Storage](/azure/active-directory/managed-identities-azure-resources/tutorial-linux-vm-access-datalake)
- [Tutorial: Usar uma identidade gerenciada atribuída pelo sistema da VM do Linux para acessar o Azure Key Vault](/azure/active-directory/managed-identities-azure-resources/tutorial-linux-vm-access-nonaad)

Há outros tutoriais nessa seção também para usar identidade gerenciada para acessar outros recursos do Azure.

## <a name="see-also"></a>Confira também

[Azure Active Directory](/azure/active-directory/managed-identities-azure-resources/)
