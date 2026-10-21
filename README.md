# Linux Process Collector

**Coleta e organização de dados de processos Linux com Python e pandas.**

Protótipo de estudo que transforma a saída de `ps aux` em um conjunto de dados estruturado. A aplicação registra informações dos processos a cada **cinco segundos** e mantém os resultados em **CSV e pickle**.

O projeto exercita fundamentos de Linux, execução de comandos, tratamento de texto e persistência de dados, úteis para aprofundar estudos em monitoramento de sistemas e segurança.

## Funcionalidades implementadas

- Executa `ps aux` com `subprocess` e lê sua saída.
- Extrai usuário, PID, CPU, memória, VSZ, RSS, TTY, estado, início, tempo e comando.
- Organiza as observações em um DataFrame do pandas.
- Acrescenta registros a um CSV e atualiza um arquivo pickle com as coletas acumuladas.
- Repete a coleta em um laço com intervalo de cinco segundos entre ciclos.

**Código principal:** [`backend/main.py`](backend/main.py).

## Tecnologias

Python 3, Linux, pandas e módulos da biblioteca padrão (`os`, `time` e `subprocess`).

## Executar o coletor

Requisitos: Linux com `ps aux` disponível e Python 3 com suporte a ambientes virtuais.

Na raiz do repositório, crie seu próprio ambiente:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install pandas
python backend/main.py
```

Para encerrar a coleta, pressione **Ctrl+C**. O programa cria os arquivos abaixo relativamente à pasta em que foi iniciado:

```text
datasets/
├── processos.csv
└── processos.pkl
```

O CSV pode ser aberto em uma planilha ou analisado com pandas. Os campos vêm da saída do comando `ps aux`; o conteúdo e a quantidade de registros dependem do sistema observado.

## Organização do código

| Função | Responsabilidade |
| --- | --- |
| `listagem` | Executar o comando e obter a saída textual |
| `rotulaProcesso` | Interpretar os campos de uma linha de processo |
| `salvaCSV` | Criar o CSV ou acrescentar linhas |
| `salvaBinario` | Criar ou atualizar o DataFrame em pickle |
| `main` | Organizar a coleta periódica e a persistência |

O repositório também conserva outros experimentos e dados de estudo. O fluxo descrito neste README corresponde ao coletor em `backend/main.py`.

## Escopo atual

Este protótipo coleta e organiza observações do sistema. A versão documentada não implementa classificação de processos, alertas de segurança ou treinamento de modelos de inteligência artificial.

O intervalo inclui o tempo necessário para executar a coleta e salvar os arquivos. O laço não tem duração máxima e o armazenamento cresce com as observações. A interpretação do texto pressupõe o formato de saída de `ps aux` usado no estudo.

## Próximos passos

- [ ] Permitir configurar intervalo, duração e diretório de saída.
- [ ] Adicionar horário de coleta e identificação de cada observação.
- [ ] Melhorar o tratamento de falhas de comando e de interpretação de linhas.
- [ ] Limitar o crescimento dos arquivos e evitar regravar todo o histórico em pickle.
- [ ] Publicar dados de exemplo controlados e testes de interpretação e persistência.
- [ ] Registrar as versões das dependências e organizar os artefatos de estudo.

## Autor

**Gustavo Henrique Xavier de Brito**  
[LinkedIn](https://www.linkedin.com/in/gustavohenriquexdebrito/) · [Portfólio no GitHub](https://github.com/GustavoHenrique-png)

## Licença

[MIT](LICENSE).
