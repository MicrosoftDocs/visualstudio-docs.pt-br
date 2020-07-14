---
title: Atribuir licenças a grupos de usuários para assinaturas do Visual Studio | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: c2853359-18fd-4be4-97a6-02230c862f92
ms.date: 05/10/2020
ms.topic: how-to
description: Saiba como os administradores podem atribuir licenças a vários assinantes usando o recurso Adicionar em massa ou grupos de Microsoft Azure Active Directory
ms.openlocfilehash: 459220c7fb2103da05f15607787390963863e622
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903277"
---
# <a name="assign-subscriptions-to-multiple-users"></a>Atribuir assinaturas a vários usuários
O portal de administração de assinaturas permite que você adicione usuários individualmente ou em grupos grandes.  Para adicionar usuários únicos, confira [Adicionar usuários únicos](assign-license.md).

Para adicionar grandes grupos de usuários, você pode usar o recurso adição em massa ou, se sua organização estiver usando Microsoft Azure Active Directory (Azure AD), você poderá usar grupos do Azure AD. Este artigo explicará o processo para ambas as opções. 

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4vxNq]

## <a name="use-bulk-add-to-assign-subscriptions"></a>Usar adição em massa para atribuir assinaturas
1. Entre no portal de administração das assinaturas do Visual Studio em <https://manage.visualstudio.com> .

1. Para adicionar vários assinantes ao mesmo tempo, navegue até a guia **gerenciar assinantes** . escolha a guia **Adicionar** e, em seguida, escolha **Adicionar em massa** na lista suspensa.  

1. A adição em massa usa um modelo do Microsoft Excel para carregar informações do Assinante. Na caixa de diálogo Carregar Vários Assinantes, clique em **Baixar** para baixar o modelo.
   > [!div class="mx-imgBorder"]
   > ![Baixar o modelo do Excel para carregar vários assinantes](media/download-template-upload-subscribers.png)
   >
   > [!NOTE]
   > Sempre baixe a versão mais recente deste modelo. Se você usar uma versão mais antiga, o upload em massa poderá falhar.

1. Na planilha do Excel, preencha os campos com as informações dos indivíduos aos quais deseja atribuir assinaturas. (A*referência* é um campo opcional.) Salve o arquivo localmente depois de terminar.

    > [!NOTE]
    > Um dos campos no modelo permite que os administradores habilitem ou desabilitem a capacidade dos assinantes de baixar o software.  A desabilitação dos downloads também desabilita o acesso às chaves do produto.

   Para que não haja problemas com o upload, observe as seguintes melhores práticas:

    - Verifique se nenhum dos campos do formulário contém vírgulas.
    - Remova os espaços antes e depois de campos de formulário.
    - Verifique se os nomes do usuário não contêm espaços extras entre nomes ou sobrenomes de duas partes (por exemplo, se uma pessoa tiver um nome de duas partes, como "Maria Eduarda", ele deverá ser digitado como "MariaEduarda", porque o sistema não cortará o espaço extra).
    - Verifique se todos os campos obrigatórios foram concluídos. 
    - Verifique a coluna **mensagem de erro** .  Se houver erros listados, resolva-os antes de tentar carregar o arquivo. 

1. Retorne ao portal de Administração de Assinaturas do Visual Studio. Na caixa de diálogo **Carregar Vários Assinantes**, clique em **Procurar**.
   > [!div class="mx-imgBorder"]
   > ![Navegar para o modelo salvo para carregar vários assinantes](media/bulk-add-browse-saved-template.png)

1. Navegue para o arquivo do Excel que você salvou e, em seguida, clique em **OK**.
   > [!div class="mx-imgBorder"]
   > ![Carregar o modelo do Excel para carregar vários assinantes](media/bulk-upload-subscribers.png)

    Uma caixa de diálogo de progresso do upload será exibida.

    Se o modelo contiver erros, o upload falhará e os erros serão mostrados para que você possa corrigir o modelo e tentar o upload em massa novamente.
   > [!div class="mx-imgBorder"]
   > ![Mensagem de erro em caso de falha no upload de vários assinantes](_img/assign-license-bulk/bulk-add-upload-failure.png)

   Se você encontrar uma falha, siga estas etapas:
   1. Abra o arquivo do Excel que você criou, corrija os problemas e salve o arquivo.
   0. Retorne ao portal de administração e escolha **Adicionar**.
   0. Selecione **Adicionar em massa**.
   0. Como você já tem o arquivo do Excel salvo, não é necessário baixar o modelo.  Clique em **procurar**, localize o arquivo que você acabou de salvar e clique em **abrir**.
   0. Clique em **OK**.


    Quando o upload for bem-sucedido, você verá a lista de assinantes e uma mensagem de confirmação.
   > [!div class="mx-imgBorder"]
   > ![Mensagem de confirmação em caso de êxito no upload de vários assinantes](_img/assign-license-bulk/bulk-add-upload-success.png)

## <a name="use-azure-active-directory-groups-to-assign-subscriptions"></a>Usar grupos de Azure Active Directory para atribuir assinaturas 
O uso desse recurso facilita a permanência de suas atribuições de assinatura. Você pode adicionar Azure Active Directory grupos de segurança no portal de administração de assinaturas, o que garantirá que todos os indivíduos do grupo sejam atribuídos a uma assinatura. E para facilitar, quando as pessoas deixam sua organização e são removidas da Azure Active Directory, o acesso às assinaturas também é removido. 


> [!IMPORTANT]
>
> As seguintes limitações se aplicam ao uso de grupos do Azure AD para adicionar assinantes:
> - O administrador deve ser membro do locatário do AAD ao adicionar inicialmente um grupo ao portal de administração.  Depois que o grupo tiver sido adicionado, as alterações na associação dos grupos não exigirão o envolvimento do administrador. 
> - Os grupos devem conter pelo menos um membro.  Não há suporte para grupos vazios.
> - Os grupos devem ter menos de 1.000 usuários. 
> - Todos os usuários devem estar no nível superior do grupo.  Não há suporte para grupos aninhados.
> - Somente contratos confiáveis têm suporte.
> - Todos os membros do grupo devem ter um endereço de email associado à sua conta do Azure AD.
> - Endereços de email separados para notificações não têm suporte para assinaturas adicionadas usando grupos do Azure AD.  

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4rvvW]

1. Entre no portal de administração das assinaturas do Visual Studio em [https://manage.visualstudio.com](https://manage.visualstudio.com) .

2. Para adicionar vários assinantes ao mesmo tempo, navegue até a guia **gerenciar assinantes** .

3. Escolha a guia **Adicionar** e, em seguida, selecione **Azure Active Directory grupo** na lista suspensa.  

   > [!div class="mx-imgBorder"]
   > ![Escolher adição em massa usando o Azure AD](_img/assign-license-bulk/bulk-add-aad.png)

4. Comece a inserir o nome do grupo do Azure AD que você deseja adicionar ao campo de formulário. Isso pesquisará os grupos do Azure AD disponíveis em sua organização. 

5. Ao selecionar o grupo, o campo será preenchido automaticamente com o nome do grupo. Você terá a opção de exibir os usuários nesse grupo antes de adicioná-los. Em seguida, você pode escolher o nível da assinatura, os direitos de download e as preferências de comunicação para o grupo. Você pode adicionar detalhes ao campo de referência, se desejar. 

   > [!div class="mx-imgBorder"]
   > ![Escolher adição em massa usando o Azure AD](_img/assign-license-bulk/bulk-add-aad-details.png)

6. Clique em **Adicionar** e em **confirmar**. 

7. Para ver o grupo adicionado, role até a parte inferior da lista de usuários.  

8. Selecione **Exibir assinantes** para exibir os membros do grupo. Você pode exibir detalhes sobre os assinantes no grupo, mas não pode fazer nenhuma edição nos assinantes ou nas assinaturas que eles estão atribuídos.    

> [!NOTE]
> Se você já tiver atribuído assinaturas individualmente a usuários que são adicionados subsequentemente como parte de um grupo do Azure AD, eles serão adicionados como parte do grupo e não serão mais listados individualmente. No entanto, se a assinatura individual for para um nível de assinatura diferente, ela terá duas assinaturas.  Exemplo: se um usuário tiver uma assinatura de Visual Studio Professional individual e for um membro de um grupo ao qual você atribui Visual Studio Enterprise assinaturas, eles terão ambos.  


## <a name="frequently-asked-questions"></a>Perguntas frequentes
### <a name="q-can-i-choose-multiple-subscription-levels-to-be-assigned-within-an-azure-ad-group"></a>P: posso escolher vários níveis de assinatura a serem atribuídos dentro de um grupo do Azure AD? 
R: não--todos no grupo recebem a mesma assinatura. 

### <a name="q-can-i-edit-subscriber-details-of-individuals-added-in-an-azure-ad-group"></a>P: posso editar os detalhes do assinante de indivíduos adicionados em um grupo do Azure AD?  
R: não--para modificar as informações de um assinante individual, você precisará removê-los do grupo de segurança do Azure AD e atribuir a eles uma assinatura individualmente.  

### <a name="q-i-added-someone-to-my-azure-ad-security-group-but-i-dont-see-them-added-in-the-subscriptions-administration-portal-and-they-dont-have-a-subscription-why-not"></a>P: adicionei alguém ao meu grupo de segurança do Azure AD, mas não os vejo adicionados no portal de administração de assinaturas e eles não têm uma assinatura. Por que não?  
R: dependendo de como sua organização tiver configurado o Azure AD, você poderá ver atrasos de até 24 horas antes que o usuário seja adicionado. Se tiver sido mais de 24 horas, [entre em contato com o suporte](https://visualstudio.microsoft.com/support/support-overview-vs).  

## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](https://docs.microsoft.com/visualstudio/)
- [Documentação do Azure DevOps](https://docs.microsoft.com/azure/devops/)
- [Documentação do Azure](https://docs.microsoft.com/azure/)
- [Documentação do Microsoft 365](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
- Há apenas um ou dois assinantes para adicionar?  Confira [Adicionar usuários únicos](assign-license.md)
- Precisa de ajuda? Contate o [Suporte à administração e às assinaturas do Visual Studio](https://visualstudio.microsoft.com/support/support-overview-vs).
