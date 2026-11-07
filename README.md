# 🎮 Quais os sucessos da Ice? Análise de vendas de videogames para a campanha de 2017

Projeto integrado do Sprint 6 do curso de Data Science. Estudo de caso analítico sobre vendas de videogames da loja online fictícia **Ice**, com o objetivo de identificar os padrões que determinam o sucesso de um jogo e apoiar o planejamento da campanha publicitária de 2017.

> Cenário: estamos em dezembro de 2016. Os dados de 2016 podem estar incompletos.

## 📌 Objetivo

Identificar quais fatores (plataforma, gênero, avaliações de críticos e usuários, região e classificação etária) estão associados ao sucesso comercial de um jogo, e transformar os achados em recomendações concretas para a campanha de 2017.

## 📂 Dados

Arquivo `games.csv` (16.715 registros, 11 colunas), com dados históricos de vendas e avaliações obtidos de fontes abertas.

| Coluna | Descrição |
|---|---|
| `Name` | Nome do jogo |
| `Platform` | Plataforma (ex.: Xbox, PlayStation) |
| `Year_of_Release` | Ano de lançamento |
| `Genre` | Gênero |
| `NA_sales` | Vendas na América do Norte (milhões de USD) |
| `EU_sales` | Vendas na Europa (milhões de USD) |
| `JP_sales` | Vendas no Japão (milhões de USD) |
| `Other_sales` | Vendas em outros países (milhões de USD) |
| `Critic_Score` | Pontuação da crítica (máx. 100) |
| `User_Score` | Pontuação dos usuários (máx. 10) |
| `Rating` | Classificação etária ESRB |

## 🔎 Etapas da análise

1. **Exploração inicial**: importação, inspeção de tipos, valores ausentes e duplicados.
2. **Preparação dos dados**
   - Padronização dos nomes das colunas para minúsculas.
   - Conversão de `year_of_release` para `Int64` e de `user_score` para `float` (valores `tbd` tratados como ausentes).
   - Validação do ano de lançamento contra o ano oficial de lançamento de cada plataforma, o que permitiu corrigir um registro de DS com ano 1985 (correto: 2007).
   - Remoção de uma duplicata (*Madden NFL 13*, PS3) e de linhas sem nome ou gênero.
   - Valores ausentes de `rating` preenchidos com `Unknown`; ausências em ano e pontuações mantidas e excluídas apenas nas análises que dependem delas.
   - Criação da coluna `total_sales` (soma das vendas de todas as regiões).
3. **Análise exploratória**
   - Lançamentos por ano e ciclo de vida das plataformas.
   - Definição do **período relevante (2013–2016)** para prever 2017.
   - Plataformas potencialmente lucrativas e distribuição de vendas (boxplots).
   - Correlação entre avaliações (críticos e usuários) e vendas, para PS4 e X360.
   - Jogos multiplataforma e distribuição de vendas por gênero.
4. **Perfil dos usuários por região** (América do Norte, União Europeia e Japão): top 5 plataformas, top 5 gêneros e efeito da classificação ESRB.
5. **Testes de hipótese** (teste t para amostras independentes, α = 0,05, com teste de Levene para escolher entre t padrão e Welch):
   - H₀: as notas médias dos usuários de **Xbox One** e **PC** são iguais.
   - H₀: as notas médias dos usuários dos gêneros **Action** e **Sports** são iguais.
6. **Conclusão geral e recomendações.**

## 💡 Principais resultados

- **Período relevante:** o ciclo de vida típico de uma plataforma é curto (mediana de cerca de 6 anos) e a nova geração (PS4, XOne, WiiU) começa a substituir a anterior (PS3, X360, Wii) a partir de 2013. Por isso, os dados de 2013 em diante foram usados para o modelo de 2017.
- **Plataformas:** PS4 é a líder e a mais segura para 2017. XOne mantém posição estável e secundária. PS3, X360 e Wii estão em declínio.
- **Avaliações:** a nota da crítica tem correlação positiva moderada com as vendas (PS4: 0,41; X360: 0,35). A nota dos usuários praticamente não se correlaciona com as vendas.
- **Gêneros:** Action lidera em vendas totais, mas por volume de lançamentos. Shooter é o gênero com maior retorno por título, com forte dependência de *blockbusters*. Adventure tem desempenho consistentemente baixo.
- **Regiões:** América do Norte e Europa têm perfil parecido (consoles de mesa, Action e Shooter, classificação M). O Japão é diferente: lidera o 3DS (portáteis) e o gênero Role-Playing. Cerca de 60% das vendas japonesas vêm de jogos sem classificação ESRB, uma limitação importante da análise.
- **Testes de hipótese:** não há diferença significativa nas notas dos usuários entre Xbox One e PC (p ≈ 0,146). Há diferença significativa entre Action e Sports (p ≈ 1,45e-20).

## ✅ Recomendações para 2017

1. Priorizar o **PS4** como foco principal de investimento.
2. Apostar em **Shooter** pelo maior retorno por título e em **Action** pelo volume.
3. Usar a **avaliação da crítica**, e não a dos usuários, como indicador de potencial comercial ao escolher jogos para promover.
4. **Segmentar por região:** NA e UE com linha semelhante (PS4/XOne, Action/Shooter); Japão com foco em portáteis (3DS) e Role-Playing.

## 🛠️ Tecnologias

- Python 3
- pandas e NumPy (manipulação de dados)
- Matplotlib e Seaborn (visualização)
- SciPy (`stats.levene`, `stats.ttest_ind`)
- Jupyter Notebook

## ▶️ Como executar

```bash
# 1. Clone o repositório
git clone https://github.com/LarissaBotany/Videogame-sales-analysis.git
cd Videogame-sales-analysis.git

# 2. Instale as dependências
pip install pandas numpy matplotlib seaborn scipy jupyter

# 3. Coloque o arquivo games.csv na pasta de dados
#    (o notebook lê de /datasets/games.csv; ajuste o caminho em pd.read_csv, se necessário)

# 4. Abra o notebook
jupyter notebook
```

## 📁 Estrutura do repositório

```
├── notebook_s6.ipynb   # Análise completa
├── games.csv           # Base de dados (se permitido incluir no repositório)
└── README.md
```

## 👩‍💻 Autoria
Larissa Areal

Projeto desenvolvido como parte do curso de Data Science. 
