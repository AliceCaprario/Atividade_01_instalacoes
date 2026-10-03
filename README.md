# Preparando o ambiente para Análise de Dados no Windows

Este material apresenta um passo a passo para preparar um computador Windows para projetos de análise de dados com **VS Code**, **Python**, **SQL**, **Git** e **GitHub**.

Ao finalizar, você terá:

- VS Code instalado e configurado;
- Python funcionando no terminal;
- extensões de Python, Jupyter e SQL instaladas;
- ambiente virtual `.venv` criado;
- bibliotecas de análise de dados instaladas;
- Git configurado;
- repositório criado e conectado ao GitHub;
- arquivo Python testado e publicado com commit e push.

> Apresentação completa: [Preparando o ambiente para Análise de Dados](./Preparando_ambiente_analise_dados_v9.pptx)

## Roteiro

1. [Instalar o VS Code](#1-instalar-o-vs-code)
2. [Instalar o Python](#2-instalar-o-python)
3. [Instalar as extensões](#3-instalar-as-extensões)
4. [Criar o ambiente virtual](#4-criar-o-ambiente-virtual)
5. [Instalar as bibliotecas](#5-instalar-as-bibliotecas)
6. [Instalar e configurar o Git](#6-instalar-e-configurar-o-git)
7. [Criar um repositório no GitHub](#7-criar-um-repositório-no-github)
8. [Conectar o computador ao GitHub](#8-conectar-o-computador-ao-github)
9. [Testar o ambiente](#9-testar-o-ambiente)
10. [Fazer commit e push](#10-fazer-commit-e-push)
11. [Resolver problemas comuns](#11-problemas-comuns)

## 1. Instalar o VS Code

1. Acesse [code.visualstudio.com](https://code.visualstudio.com/).
2. Baixe a versão para Windows.
3. Execute o instalador e aceite o contrato de licença.
4. Mantenha a pasta de instalação sugerida.
5. Nas tarefas adicionais, recomenda-se marcar:
   - **Criar um atalho na área de trabalho**;
   - **Abrir com Code** no menu de contexto de arquivos;
   - **Abrir com Code** no menu de contexto de diretórios;
   - **Registrar Code como editor**;
   - **Adicionar ao PATH**.
6. Clique em **Instalar** e aguarde a conclusão.

Para abrir o terminal integrado do VS Code, use:

```text
Ctrl + `
```

Também é possível acessar **Terminal → New Terminal**.

## 2. Instalar o Python

No terminal do VS Code, execute:

```powershell
winget install Python.Python.3.14
```

Se o terminal solicitar a aceitação dos termos, digite `Y` e pressione **Enter**.

Depois da instalação, feche e abra novamente o VS Code. Confira a versão:

```powershell
python --version
```

Se o comando `python` não funcionar, tente:

```powershell
py --version
```

## 3. Instalar as extensões

1. Abra o VS Code.
2. Clique no ícone **Extensions** na barra lateral ou use `Ctrl+Shift+X`.
3. Pesquise e instale as extensões publicadas pela Microsoft:
   - **Python**;
   - **Pylance**, caso não seja instalada automaticamente;
   - **Jupyter**, se o curso utilizar notebooks `.ipynb`.
4. Para trabalhar com bancos de dados, pesquise uma extensão SQL adequada ao banco utilizado no curso, como **SQLTools**, e instale também o driver correspondente.

### Selecionar o interpretador Python

1. Pressione `Ctrl+Shift+P`.
2. Digite `Python: Select Interpreter`.
3. Selecione o Python instalado ou, depois de criar o ambiente virtual, o interpretador da pasta `.venv`.

## 4. Criar o ambiente virtual

Crie ou escolha a pasta do projeto e abra-a pelo menu **File → Open Folder**.

No terminal integrado, execute:

```powershell
python -m venv .venv
```

Ative o ambiente virtual no PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

No Prompt de Comando, use:

```bat
.venv\Scripts\activate.bat
```

Quando o ambiente estiver ativo, o terminal normalmente exibirá `(.venv)` antes do caminho atual.

Depois, pressione `Ctrl+Shift+P`, execute **Python: Select Interpreter** e escolha o Python localizado na pasta `.venv`.

## 5. Instalar as bibliotecas

Com a `.venv` ativa, atualize o `pip`:

```powershell
python -m pip install --upgrade pip
```

Instale as bibliotecas utilizadas em análise de dados:

```powershell
python -m pip install pandas numpy matplotlib seaborn openpyxl
```

Confira os pacotes instalados:

```powershell
python -m pip list
```

### Evitar publicar a `.venv`

Crie um arquivo chamado `.gitignore` na raiz do projeto e adicione:

```gitignore
.venv/
__pycache__/
*.pyc
.ipynb_checkpoints/
```

## 6. Instalar e configurar o Git

No terminal do VS Code, execute:

```powershell
winget install Git.Git
```

Depois da instalação, feche e abra novamente o VS Code. Verifique:

```powershell
git --version
```

Configure o nome e o e-mail utilizados nos commits:

```powershell
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
```

Confira a configuração:

```powershell
git config --global --list
```

> Use, de preferência, o mesmo e-mail cadastrado na sua conta do GitHub.

## 7. Criar um repositório no GitHub

1. Acesse [github.com](https://github.com/) e entre na sua conta.
2. Abra o menu do perfil.
3. Clique em **Repositories**.
4. Clique no botão verde **New**.
5. Preencha o formulário:
   - informe um nome curto e claro, como `analise-de-dados`;
   - adicione uma descrição, se desejar;
   - escolha entre **Public** e **Private**;
   - ative **Add README**;
   - selecione um `.gitignore` para Python, se essa opção estiver disponível.
6. Clique em **Create repository**.

## 8. Conectar o computador ao GitHub

Na página do repositório, clique em **Code** e copie a URL HTTPS.

No terminal, navegue até a pasta em que deseja guardar o projeto e execute:

```powershell
git clone <url-do-repositorio>
```

Exemplo:

```powershell
git clone https://github.com/seu-usuario/analise-de-dados.git
```

Entre na pasta clonada:

```powershell
cd analise-de-dados
```

Abra a pasta atual no VS Code:

```powershell
code .
```

Na primeira operação de rede, o Git pode abrir o navegador para autenticar sua conta. Siga as instruções exibidas na tela. O curso também pode utilizar token pessoal ou chave SSH.

## 9. Testar o ambiente

Crie um arquivo chamado `teste.py` com o conteúdo:

```python
import pandas as pd

print("Ambiente OK! pandas versão:", pd.__version__)
```

Execute o arquivo:

```powershell
python teste.py
```

A saída esperada será semelhante a:

```text
Ambiente OK! pandas versão: 2.x.x
```

O número exato depende da versão instalada.

## 10. Fazer commit e push

Confira os arquivos alterados:

```powershell
git status
```

Adicione o arquivo de teste à área de preparação:

```powershell
git add teste.py
```

Crie o commit:

```powershell
git commit -m "Adiciona arquivo de teste"
```

Envie o commit para o GitHub:

```powershell
git push
```

Abra o repositório no GitHub e atualize a página. O arquivo `teste.py` e a mensagem do commit deverão aparecer.

## 11. Problemas comuns

| Sintoma | Causa provável | Solução |
|---|---|---|
| `python` ou `git` não reconhecido | O VS Code estava aberto durante a instalação | Feche e abra novamente o VS Code |
| Biblioteca não encontrada | Interpretador incorreto | Use **Python: Select Interpreter** e escolha a `.venv` |
| Ativação da `.venv` bloqueada | Política de execução do PowerShell | Use o Prompt de Comando ou, se permitido pela instituição, ajuste a política do usuário atual |
| Erro ao criar o commit | Nome ou e-mail do Git não configurado | Configure `user.name` e `user.email` |
| Erro no `git push` | Falha de autenticação | Refazer o login ou utilizar o método indicado pelo curso |
| `code` não reconhecido | VS Code não foi adicionado ao PATH | Abra a pasta pelo menu **File → Open Folder** |

Se a instituição permitir alterar a política do PowerShell para o usuário atual, o comando é:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

> Antes de alterar a política de execução, confirme as regras de segurança da instituição.

## Checklist final

- [ ] VS Code instalado
- [ ] Python instalado e reconhecido
- [ ] Extensões de Python, Jupyter e SQL instaladas
- [ ] Interpretador da `.venv` selecionado
- [ ] Bibliotecas instaladas
- [ ] Git instalado e configurado
- [ ] Repositório criado no GitHub
- [ ] Projeto clonado no computador
- [ ] `teste.py` executado com sucesso
- [ ] Commit visível no GitHub

## Próximos passos

- Atualizar este README com a descrição do projeto;
- organizar os scripts, notebooks e arquivos de dados;
- criar commits pequenos e com mensagens claras;
- nunca publicar senhas, tokens ou dados confidenciais;
- incluir um arquivo `requirements.txt` com as dependências do projeto:

```powershell
python -m pip freeze > requirements.txt
```

Em outro computador, as dependências podem ser instaladas com:

```powershell
python -m pip install -r requirements.txt
```

---

Material preparado para apoio à aula de configuração do ambiente de análise de dados no Windows.
