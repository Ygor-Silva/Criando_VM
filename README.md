## 🚀 Processo de Criação da VM no Azure (Simulação Detalhada)

A seguir, detalho os passos simulados e as configurações escolhidas para criar a Máquina Virtual neste desafio, utilizando o Portal Azure:

1.  **Login no Portal Azure:** Acesso realizado com as credenciais da conta. ([https://portal.azure.com/](https://portal.azure.com/))

2.  **Criação de um Grupo de Recursos (Resource Group):** Essencial para agrupar os recursos do desafio.
    *   **Nome:** `rg-dio-challenge-vm` *(Convenção: rg-<ambiente>-<projeto/finalidade>)*
    *   **Região:** `East US` *(Escolha de uma região comum, poderia ser Brazil South também)*
    *   *Observação:* Facilita o gerenciamento e a exclusão de todos os recursos juntos ao final.

3.  **Criação da Máquina Virtual:** Iniciado o processo clicando em "Criar um recurso" > "Máquina Virtual".
    *   **Guia Básico:**
        *   **Assinatura:** `[Sua Assinatura - ex: Azure for Students, Free Trial, Pay-as-you-go]`
        *   **Grupo de Recursos:** `rg-dio-challenge-vm` (Selecionado o grupo criado anteriormente)
        *   **Nome da Máquina Virtual:** `vm-dio-challenge-linux` *(Convenção: vm-<ambiente>-<finalidade/OS>)*
        *   **Região:** `East US` (Mantida a mesma do RG para proximidade)
        *   **Opções de Disponibilidade:** `Nenhuma redundância de infraestrutura necessária` (Padrão para labs)
        *   **Tipo de Segurança:** `Standard` (Padrão)
        *   **Imagem (SO):** `Ubuntu Server 20.04 LTS - Gen2` *(Escolha popular e estável para Linux)*
            *   *(Alternativa comum seria: `Windows Server 2019 Datacenter - Gen2`)*
        *   **Tamanho da VM:** `Standard_B1s` *(Escolhido por ser uma opção econômica da série B (Burstable), ideal para cargas de trabalho leves/labs)*
        *   **Autenticação:** `Senha` *(Escolhido para simplicidade neste lab)*
            *   *(Alternativa mais segura: `Chave pública SSH`)*
            *   **Nome de usuário:** `azureuser` *(Nome de administrador padrão)*
            *   **Senha:** `[Definir Senha Segura]` ***(NÃO COLOCAR A SENHA REAL AQUI NO GITHUB!)***
        *   **Regras de Porta de Entrada Pública:** `Permitir portas selecionadas`
            *   **Selecionar portas de entrada:** `SSH (22)` *(Necessário para conectar via SSH ao Linux)*
            *   *(Se fosse Windows, escolheria `RDP (3389)`)*
        *   **Licenciamento (se Windows):** `[Marcar se aplicável para economia com licenças existentes]`
    *   **Guia Discos:**
        *   **Tipo de disco do SO:** `SSD Standard` *(Equilíbrio entre custo e performance para labs. Premium SSD é mais rápido, HDD Standard mais barato)*
        *   **Gerenciamento de Chaves:** `Chave gerenciada pela plataforma` (Padrão)
    *   **Guia Rede:**
        *   **Rede Virtual:** `vnet-dio-challenge` *(Azure sugeriu a criação de uma nova com este nome)*
        *   **Sub-rede:** `default (10.X.0.0/24)` *(Azure sugeriu a criação de uma sub-rede padrão)*
        *   **IP Público:** `pip-vm-dio-challenge-linux` *(Azure sugeriu a criação de um novo IP público)*
        *   **Grupo de Segurança de Rede da NIC (NSG):** `Básico`
        *   **Portas de Entrada Públicas:** Confirmado `Permitir portas selecionadas` e `SSH (22)` estava listado.
        *   **Excluir IP público e NIC quando a VM for excluída:** `Marcado` (Boa prática para labs)
    *   **Guia Gerenciamento:**
        *   **Monitoramento:** Desabilitado o diagnóstico de inicialização para economizar custos de armazenamento (opcional).
        *   **Identidade, Autologin, Desligamento automático:** Mantidas as configurações padrão.
    *   **Guia Avançado, Marcas:** Mantidas as configurações padrão. *(Marcas/Tags poderiam ser usadas para organização, ex: `Environment: Lab`, `Project: DIO-Challenge`)*
    *   **Revisar + Criar:**
        *   Verificação das configurações na tela de resumo.
        *   Validação passou com sucesso.
        *   Clique em **"Criar"**.

4.  **Acompanhamento do Provisionamento:** Aguardei a notificação de conclusão da implantação no portal Azure (geralmente alguns minutos).

5.  **Acesso à VM (Teste):**
    *   Navegação até o recurso da VM criada (`vm-dio-challenge-linux`).
    *   Cópia do **Endereço IP Público** exibido na visão geral.
    *   Utilização de um cliente SSH (como o Terminal no Linux/Mac ou PowerShell/PuTTY no Windows):
        ```bash
        ssh azureuser@[Endereço_IP_Público_Copiado]
        ```
    *   Aceite da chave do host (na primeira conexão) e inserção da senha definida durante a criação.
    *   Conexão estabelecida com sucesso ao terminal da VM Linux. *(Descrever o resultado real)*

6.  **Limpeza (Pós-Desafio):**
    *   **IMPORTANTE:** Após concluir os testes e a documentação, navegar até o Grupo de Recursos (`rg-dio-challenge-vm`) e **excluí-lo** para interromper todas as cobranças associadas aos recursos criados (VM, Disco, IP, NSG, VNet).
