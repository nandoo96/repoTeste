# repoTeste



# Gerenciamento de Usuários, Grupos e Permissões no Linux

## Visão Geral

Este documento tem como objetivo explicar o processo de criação de **usuários**, **grupos** e **permissões** no sistema Linux, conforme os padrões adotados pela empresa **Tecnologia 2025**.

Todas as atividades relacionadas à criação e gerenciamento de acessos são de responsabilidade da equipe **SRE**, sendo **Joaquim da Silva** o colaborador designado para a execução dessas tarefas.

---

## 1. Criação de Grupos

Antes de adicionar usuários, é comum criar os grupos que irão representar funções, departamentos ou permissões específicas no sistema.

```bash
sudo groupadd nome_do_grupo
```

**Exemplo:**
```bash
sudo groupadd desenvolvedores
```

---

## 2. Criação de Usuários

Para criar um novo usuário e já vinculá-lo a um grupo:

```bash
sudo useradd -m -s /bin/bash -g nome_do_grupo nome_do_usuario
```

**Explicação:**
- `-m` cria o diretório home.
- `-s /bin/bash` define o shell padrão.
- `-g` associa o usuário ao grupo primário.

**Exemplo:**
```bash
sudo useradd -m -s /bin/bash -g desenvolvedores joao.souza
```

### 2.1 Definir Senha do Usuário

Após criar o usuário, defina a senha com:

```bash
sudo passwd joao.souza
```

---

## 3. Adicionar o Usuário a Grupos Secundários

Caso o usuário deva pertencer a mais de um grupo (além do primário):

```bash
sudo usermod -aG nome_do_grupo nome_do_usuario
```

**Exemplo:**
```bash
sudo usermod -aG docker joao.souza
```

---

## 4. Permissões de Arquivos e Diretórios

### 4.1 Ver permissões

Use o comando `ls -l` para listar permissões:

```bash
ls -l /caminho/do/diretorio
```

### 4.2 Alterar dono e grupo de um arquivo/diretório

```bash
sudo chown usuario:grupo arquivo_ou_diretorio
```

**Exemplo:**
```bash
sudo chown joao.souza:desenvolvedores /projetos/app1
```

### 4.3 Alterar permissões de leitura, escrita e execução

```bash
sudo chmod modo arquivo_ou_diretorio
```

**Exemplo:**
```bash
sudo chmod 750 /projetos/app1
```

**Explicação de `750`:**
- **7** (usuário): leitura, escrita e execução
- **5** (grupo): leitura e execução
- **0** (outros): sem permissão

---

## 5. Boas Práticas

- Sempre utilize nomes de usuários e grupos padronizados (ex: `nome.sobrenome` para usuários).
- Crie um grupo novo apenas se não houver um existente com a finalidade desejada.
- Documente cada criação de usuário/grupo e permissões concedidas.
- Nunca forneça permissões desnecessárias aos usuários.
- Para acesso administrativo (sudo), adicione o usuário ao grupo `sudo` com cautela:

```bash
sudo usermod -aG sudo nome_do_usuario
```

---

## 6. Responsável

Todas as solicitações de criação de usuários, grupos ou permissões devem ser direcionadas à equipe **SRE**.  
**Responsável direto:** **Joaquim da Silva**.

---
