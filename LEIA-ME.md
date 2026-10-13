# Quattuor

## Como rodar

1. Instale o Python e, na pasta do projeto, as bibliotecas:

   ```
   pip install -r requirements.txt
   ```

2. Entre na pasta `BackEnd` e ligue o servidor:

   ```
   cd BackEnd
   python app.py
   ```

3. Abra no navegador: **http://localhost:5000**

O servidor precisa ficar ligado (a janela do terminal aberta) enquanto você usa o site.

### Se aparecer "Failed to fetch"

Esse erro quer dizer que o navegador não conseguiu falar com o servidor. Confira:

- o `python app.py` está rodando? (a janela não pode ter fechado nem mostrar erro);
- você abriu o site por `http://localhost:5000`? Abrir o HTML dando dois cliques nele
  (endereço `file:///...`) pode falhar, principalmente no Firefox.

## Como as pastas se organizam (igual ao projeto do Gabriel)

```
BackEnd/
  app.py          rotas do Flask (o que cada endereço faz)
  banco.py        tudo do banco de dados: conectar, criar_tabelas, inserir_..., buscar_...
  perguntas.json  as 20 perguntas do quiz
  database.db     o banco (SQLite)
FrontEnd/
  tela_*.html     as telas
  app.js          funções comuns (falar com o servidor, login, alertas)
  quiz.js         a lógica da tela do quiz
  style.css
```

## O banco (database.db)

| Tabela | Para que serve |
|---|---|
| `usuario` | cadastro de aluno e professor (a senha é guardada embaralhada, nunca em texto) |
| `sessao` | quem está logado (o token que o navegador guarda) |
| `quiz`, `pergunta`, `alternativa` | as perguntas e as alternativas do quiz |
| `tentativa`, `resposta` | o que cada aluno respondeu |
| `perfil` | o resultado do aluno: pontos de cada papel e o papel final |
| `solicitacao` | pedidos de troca, reclamações e elogios |

Os quatro papéis são Líder, Relator(a), Monitor(a) de Foco e Guardião do Tempo.

## Como o quiz vira perfil

Cada pergunta tem 4 opções, e **a posição da opção define o papel**:
1ª = Líder, 2ª = Relator, 3ª = Monitor de Foco, 4ª = Guardião do Tempo.
No fim, o papel com mais pontos é o perfil do aluno (empate: vale a ordem acima).

## Trocar as perguntas

Edite `BackEnd/perguntas.json` (sempre 4 opções por pergunta) e rode, dentro de `BackEnd`:

```
python banco.py --recarregar-quiz
```

Atenção: isso apaga o quiz atual e as respostas e perfis dos alunos.

## Contas

- **Aluno**: cadastro com "Aluno" marcado.
- **Professor**: cadastro com "Instituição" marcado (abre o painel do professor).
- Não existe nenhuma conta pronta: crie as suas na tela de cadastro.
