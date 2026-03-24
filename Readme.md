# Laboratório de Máquina Virtual na Azure com Terraform

Este repositório contém a infraestrutura como código (IaC) necessária para criar uma máquina virtual Linux completa e seus recursos de rede associados na nuvem da Microsoft Azure utilizando o Terraform.

## ☁️ Ambiente do Projeto

- **Provedor Cloud:** Microsoft Azure
- **Ferramenta de IaC:** Terraform

## 🏗️ Esboço da Infraestrutura Criada

Ao executar este projeto, os seguintes recursos são gerenciados na Azure, conectando-se através de um Resource Group (Grupo de Recursos) pré-existente especificado:

1. **Virtual Network (Rede Virtual):** `devopsautomation-vnet` com espaço de endereçamento `10.0.0.0/16`.
2. **Subnet (Sub-rede):** `devopsautomation-subnet` com o prefixo `10.0.1.0/24`.
3. **Public IP (IP Público):** `devopsautomation-public-ip` configurado com alocação estática para que a VM tenha um endereço estático na web.
4. **Network Interface (Interface de Rede):** `devopsautomation-nic` conectando a VM à sub-rede local e ao IP público externo.
5. **Linux Virtual Machine (Máquina Virtual Linux):** `devopsautomation-vm` rodando Ubuntu Server 24.04-LTS (tamanho da máquina configurado para `D2ads_v7`), acessível através de usuário e senha.

## ⚙️ Variáveis de Configuração

É **necessário a criação ou edição do arquivo `variables.tf`** para adicionar e customizar os dados da sua cloud. Nele, você pode definir as principais variáveis como:
- `admin_username`: Nome do usuário administrador da VM.
- `admin_password`: Senha para acesso à VM (defina uma senha forte).
- `location`: Região onde os recursos serão criados (ex: `eastus2`).
- `resource_group_name`: O nome do Resource Group na Azure que armazenará os recursos.

*(Dica: Para dados sensíveis, você pode criar também um arquivo `terraform.tfvars` ou passá-los durante a execução dos comandos).*

## 🚀 Passo a Passo: Como Rodar o Projeto

Siga os comandos abaixo no seu terminal para provisionar a infraestrutura:

1. **Autenticação na Azure CLI:**
   Antes de rodar o Terraform, garanta que você está logado na sua conta Azure pelo terminal.
   ```bash
   az login
   ```

2. **Inicializar o Terraform (`init`):**
   Esse comando baixa os plugins/provedores necessários (no caso, o `azurerm` da Microsoft Azure).
   ```bash
   terraform init
   ```

3. **Verificar a Formatação e Validade (Opcional):**
   Garante que o código esteja bem formatado e válido.
   ```bash
   terraform fmt
   terraform validate
   ```

4. **Planejar a Infraestrutura (`plan`):**
   Gera um levantamento e mostra quais recursos serão criados na nuvem. Revise-o cuidadosamente.
   ```bash
   terraform plan
   ```

5. **Aplicar as Mudanças (`apply`):**
   Executa o plano levantado e cria a infraestrutura de fato na Azure. Após conferir, digite `yes` para confirmar a criação.
   ```bash
   terraform apply
   ```

6. **Destruir a Infraestrutura (`destroy`):**
   ⚠️ *Muito Importante:* Quando finalizar os seus estudos, não se esqueça de remover os recursos para evitar cobranças extras na sua Azure.
   ```bash
   terraform destroy
   ```

---
**Bons estudos com Terraform e Azure!** Se precisar ajustar algo, basta modificar os arquivos `.tf` e rodar novamente `terraform plan` e `terraform apply`.
