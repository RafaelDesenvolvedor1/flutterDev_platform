```markdown
# � Plataforma de Desenvolvimento - Flutter & PHP Stack

Este projeto fornece um ambiente de desenvolvimento robusto, conteinerizado e totalmente automatizado utilizando **Docker** e **VS Code Dev Containers**. Ele integra um frontend em **Flutter Web**, uma API em **PHP (Apache)** e um banco de dados **MySQL 8.0** com interface gráfica **Adminer**.

O ambiente foi blindado para evitar conflitos de redes órfãs e isolamento de portas, centralizando toda a configuração em um único arquivo de credenciais de ambiente.

---

## �️ O que o Ambiente Fornece?

Ao subir este ecossistema, você terá à disposição:

1. **Frontend (Flutter Web)**: Ambiente isolado com o SDK do Flutter configurado, pronto para compilar e rodar a aplicação Web na porta `8085`.
2. **Backend (PHP API)**: Servidor Apache com PHP 8.2 configurado para rodar na porta `8000`, já com suporte nativo a conexões PDO e headers de CORS liberados.
3. **Banco de Dados (MySQL 8.0)**: Instância do MySQL escutando na porta padrão `3306`, isolada com segurança dentro da rede interna do Docker.
4. **Gerenciador de Banco (Adminer)**: Interface gráfica leve e rápida rodando na porta `8080` para administrar o MySQL diretamente pelo navegador.
5. **Rede Unificada (`flutterdev_platform_network`)**: Uma ponte de rede privada (bridge) que interconecta todos os contêineres automaticamente pelo nome dos serviços.

---

## � Pré-requisitos do Sistema

Antes de iniciar, certifique-se de ter instalado na sua máquina física (Host Linux Debian/Mint ou Windows):

1. **Docker Engine** (Versão 20.10+ ou superior)
2. **Docker Compose V2**
3. **Visual Studio Code**
4. Extensão do VS Code: **Dev Containers** (`ms-vscode-remote.remote-containers`)

---

## ⚙️ Configuração Inicial (.env)

O projeto utiliza um arquivo `.env` na raiz para controlar as portas e credenciais do banco com segurança. Crie um arquivo chamado `.env` na raiz do projeto e defina as variáveis conforme o exemplo abaixo:

```env
# Portas dos Serviços (Acesso Externo)
API_PORT=8000
ADMINER_PORT=8080
DB_PORT=3306
FLUTTER_WEB_PORT=8085

# Dados do Aplicativo Flutter
FLUTTER_APP_NAME=facul_app

# Credenciais do Banco de Dados
DB_ROOT_PASSWORD=suasenharoot
DB_DATABASE=db_plataforma
DB_USER=rafael
DB_PASSWORD=suasenhadesenvolvedor

### � Passo a Passo: Como Executar o Projeto

Siga estritamente a ordem abaixo para garantir que o banco de dados e as tabelas de rotas de rede subam sem conflitos.

#### Passo 1: Subir a Infraestrutura de Backend
Abra o terminal do seu sistema operacional (Debian/Mint) na pasta raiz do projeto e execute o comando para iniciar o banco, a API e o Adminer em segundo plano:

```bash
docker compose up -d


#### Passo 2: Abrir o Frontend no VS Code Dev Container
1. Abra o VS Code na pasta raiz do projeto.
2. Pressione `Ctrl + Shift + P` para abrir a paleta de comandos.
3. Selecione a opção: **Dev Containers: Reopen in Container**.
4. O VS Code vai ler o arquivo `.devcontainer/devcontainer.json`, limpar qualquer contêiner órfão anterior automaticamente usando etiquetas (`labels`) e inicializar o SDK do Flutter de forma limpa.

#### Passo 3: Rodar o Aplicativo Flutter Web
Uma vez dentro do contêiner do VS Code (você verá o indicador `Dev Container: Flutter...` na barra inferior esquerda):
1. Abra o terminal integrado do VS Code com o atalho `Ctrl + '`.
2. Entre na pasta do aplicativo gerada automaticamente com base no seu arquivo `.env`:
   ```bash
   cd $FLUTTER_APP_NAME

#### Execute o comando para iniciar o servidor web do Flutter acoplado à porta mapeada:
    ```bash
    flutter run -d web-server --web-port=8085 --web-hostname=0.0.0.0