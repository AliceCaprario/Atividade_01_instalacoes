# Roteiro: Preparando o ambiente para Análise de Dados (Windows)

**Duração estimada:** 25 a 35 min
**Fluxo:** VS Code → Python → Extensões → Bibliotecas → Git → GitHub → Arquivo de verificação

> **Regra de ouro da apresentação:** depois de instalar qualquer programa pelo terminal, **feche e reabra o VS Code** antes de testar. Foi o erro que apareceu com o Python e com o Git.

---

## Slide 1: Abertura

- **Título:** Preparando o ambiente para Análise de Dados
- **Conteúdo:** objetivo da aula e o caminho em 6 etapas.
- **Visual:** `VS Code → Python → Extensões → Bibliotecas → Git → GitHub`
- **Fala:** "Ao final, vocês terão o ambiente funcionando e um arquivo de vocês publicado no GitHub."

---

## Slide 2: Instalar o VS Code

- Baixar em https://code.visualstudio.com e fazer a instalação padrão.
- Dica: marcar "Adicionar ao PATH" e "Abrir com Code" no menu do botão direito.
- **Demo / print:** tela inicial. Apresentar Explorer, editor, extensões e terminal.
- Abrir o terminal: ``Ctrl+` ``
- Abrir a pasta da aula: *File → Open Folder*.

---

## Slide 3: Instalar o Python pelo terminal do VS Code

Ver as versões disponíveis e instalar a mais recente:

```powershell
winget search Python.Python
winget install Python.Python.3.14
```

- Aceitar os termos com `Y`, se perguntar.
- Rodar em terminal **normal** (o do VS Code), sem administrador.
- **Fechar o VS Code por completo e reabrir.**
- Conferir:

```powershell
python --version
```

> Versão usada nos testes: **3.14.7**. Confira no https://www.python.org/downloads/ antes da aula, porque a versão muda.

### Slide de reserva: "Python não foi encontrado"

| Sintoma | Causa | Solução |
|---|---|---|
| "Python não foi encontrado… Microsoft Store" | Atalho da Store interceptando | *Configurações → Aplicativos → Configurações avançadas do aplicativo → Aliases de execução do aplicativo*, desligar `python.exe` e `python3.exe` |
| `python` não reconhecido | VS Code não foi reaberto | Fechar por completo e reabrir |
| `py --version` funciona, `python` não | Alias da Store | Mesma solução da primeira linha |

- Plano B: baixar o instalador em python.org e marcar **"Add python.exe to PATH"**.

---

## Slide 4: Extensões do Python

- **Python** (Microsoft), que já inclui o Pylance.
- **Jupyter**, se o curso usar notebooks.
- Selecionar o interpretador: `Ctrl+Shift+P` → *Python: Select Interpreter*.
- **Demo:** instalar a extensão e mostrar o interpretador na barra inferior.

### Dica visual (opcional)

- Ícones coloridos por tipo de arquivo: **vscode-icons** ou **Material Icon Theme**.
- Ativar em `Ctrl+Shift+P` → *Preferences: File Icon Theme*.
- Ajuda na leitura do Explorer, principalmente no projetor.

---

## Slide 5: Ambiente virtual e bibliotecas

Explicar em uma frase: o ambiente virtual isola as bibliotecas de cada projeto.

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

- Quando ativo, o terminal mostra `(.venv)` no início da linha.
- No Prompt de Comando (cmd), o ativador é `.venv\Scripts\activate`.

Instalar e conferir:

```powershell
pip install pandas numpy matplotlib seaborn openpyxl
pip list
```

> Ajuste a lista de bibliotecas ao que o curso pedir.

**Erro comum no PowerShell:** "a execução de scripts foi desabilitada neste sistema". Solução (uma vez):

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

---

## Slide 6: Instalar e configurar o Git

```powershell
winget install Git.Git
```

- **Fechar e reabrir o VS Code.**
- Conferir:

```powershell
git --version
```

- Se não reconhecer, atualizar o PATH da sessão sem reabrir:

```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
```

Configurar a identidade (uma única vez no computador):

```powershell
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
git config --global --list
```

- Usar o **mesmo e-mail da conta do GitHub**.
- **Fala:** Git é a ferramenta local que registra o histórico das alterações.

---

## Slide 7: Conta e repositório no GitHub

- Criar conta em https://github.com.
- *New repository*: nome claro, README marcado, público ou privado.
- **Fala:** o GitHub é o serviço online que guarda o repositório. Git e GitHub são coisas diferentes.
- **Print:** tela de criação do repositório.

---

## Slide 8: Conectar o computador ao GitHub

```powershell
git clone <url-do-repositorio>
```

- Na primeira vez, o login é feito pelo navegador (ou por token/SSH, conforme o curso).
- Abrir a **pasta clonada** no VS Code (*File → Open Folder*).

---

## Slide 9: Arquivo de verificação e commit (demonstração principal)

**1. Criar `teste.py`:**

```python
import pandas as pd
print("Ambiente OK! pandas versão:", pd.__version__)
```

**2. Executar:**

```powershell
python teste.py
```

**3. Versionar:**

```powershell
git status
git add teste.py
git commit -m "Adiciona arquivo de teste"
git push
```

**4. Conferir:** abrir o repositório no GitHub e **atualizar a página**. O arquivo e a mensagem do commit devem aparecer.

- **Fala:** "Se vocês veem o arquivo no GitHub, tudo está funcionando."
- Dica: use `git add teste.py` (arquivo específico) em vez de `git add .`, para não enviar a pasta `.venv`. Num projeto real, crie um `.gitignore` com a linha `.venv/`.

---

## Slide 10: Problemas comuns

| Sintoma | Causa provável | Solução |
|---|---|---|
| `python` ou `git` não reconhecido | VS Code não foi reaberto | Fechar por completo e reabrir |
| "Python não foi encontrado… Store" | Alias da Store | Desativar `python.exe` / `python3.exe` |
| Biblioteca não encontrada | Interpretador errado | *Select Interpreter* → `.venv` |
| Script bloqueado ao ativar o venv | Política do PowerShell | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| Erro no commit | Git sem identidade | `git config --global user.name` / `user.email` |
| Erro no `push` | Autenticação | Refazer login ou usar token |

---

## Slide 11: Checklist final e próximos passos

- [ ] VS Code instalado
- [ ] Python instalado e reconhecido (`python --version`)
- [ ] Extensões ativas
- [ ] Ambiente virtual criado e bibliotecas instaladas
- [ ] Git instalado e configurado
- [ ] Repositório criado no GitHub e clonado
- [ ] Commit visível no GitHub

**Próximos passos:** conteúdo da próxima aula.

---

## Sugestões de produção

- **Prints no lugar de demo ao vivo** nas instalações (slides 2, 3 e 6), porque demoram.
- **Demo ao vivo** nos slides 4, 5 e 9.
- Ensaie o fluxo completo em uma pasta limpa antes, para validar prints e tempos.
- Se for projetar ou gravar, aumente o zoom do VS Code (`Ctrl +`) para o terminal ficar legível.

## Pendências para fechar

1. O curso usa notebooks (Jupyter) ou apenas scripts `.py`?
2. A autenticação no GitHub será por navegador, token ou SSH?
3. A lista de bibliotecas está completa?
4. Qual versão do Python o curso pede, se houver uma específica?