# 📊 Tutorial: Configuração e Uso do R no Jupyter Notebook

Bem-vindo! Este repositório contém um guia passo a passo, desenvolvido para auxiliar os membros do grupo de pesquisa e demais interessados na instalação e configuração da linguagem **R** dentro do ambiente do **Jupyter Notebook**. 

Além da configuração, este tutorial aborda conceitos básicos da linguagem R e demonstra um caso prático de análise estatística utilizando ANOVA (Análise de Variância).

---

## 1. Instalando o R

Antes de integrar o R ao Jupyter, você precisa ter a linguagem instalada no seu computador.

### Windows
1. Acesse o site oficial do CRAN: [Download R for Windows](https://cran.r-project.org/bin/windows/base/)
2. Clique em **"Download R [versão] for Windows"**.
3. Execute o arquivo `.exe` baixado e siga as instruções do instalador (pode deixar todas as opções padrão selecionadas).

### macOS
1. Acesse o site do CRAN: [Download R for macOS](https://cran.r-project.org/bin/macosx/)
2. Baixe o arquivo `.pkg` correspondente à versão do seu processador (Apple Silicon M1/M2/M3 ou Intel).
3. Execute o arquivo e siga as instruções de instalação.
*(Alternativamente, via Homebrew: `brew install r`)*

### Linux (Ubuntu/Debian)
Abra o terminal e execute os seguintes comandos:
```bash
sudo apt update
sudo apt install r-base
```
## 2. Integrando o R ao Jupyter Notebook
Para que o Jupyter Notebook reconheça a linguagem R, precisamos instalar o kernel do R, chamado IRkernel.

Abra o console do R.

No Windows/macOS: Procure por "R" nos seus aplicativos e abra o programa.

No Linux: Digite R no terminal e aperte Enter.

Dentro do console do R (onde você verá o símbolo >), digite o comando abaixo para instalar o pacote do kernel:

```R
   install.packages("IRkernel")
(Se perguntar sobre qual "CRAN mirror" utilizar, selecione o mais próximo de você, como o do Brasil).
```
Após a instalação terminar, registre o kernel para que o Jupyter o encontre executando este comando:

```R
   IRkernel::installspec(user = FALSE)
(Nota: user = FALSE instala para todos os usuários do sistema. Se der erro de permissão, tente IRkernel::installspec(user = TRUE)).
```

Pronto! Na próxima vez que você abrir o Jupyter Notebook, verá a opção de criar um novo notebook usando a linguagem R.

## 3. O Básico de Programação em R
Se você já programa em Python, a transição para o R será bem tranquila. O R foi construído especificamente com a manipulação de dados em mente.

Variáveis e Atribuições
No R, a convenção para atribuir valores a uma variável é usar a "setinha" <-, embora o = também funcione.

```R
# Atribuindo um valor
idade <- 22
nome <- "Pesquisador"

# Imprimindo na tela
print(idade)
```
**Vetores**
A estrutura de dados mais básica no R é o vetor. Usamos a função c() (de combine) para criá-los.

```R
temperaturas <- c(25.5, 26.0, 24.8, 27.1)
```

**Data Frames**
O Data Frame é o equivalente ao pandas.DataFrame do Python. É uma tabela onde cada coluna pode ser de um tipo diferente.

```R
dados_experimento <- data.frame(
  amostra = c(1, 2, 3),
  resultado = c(10.5, 11.2, 9.8),
  sucesso = c(TRUE, TRUE, FALSE)
)
```
## 4. Exemplo Prático: ANOVA em R
O R brilha de verdade nas análises estatísticas. A ANOVA (Análise de Variância) é usada para comparar as médias de três ou mais grupos para ver se eles são estatisticamente diferentes entre si.

Vamos usar um dataset nativo do R chamado PlantGrowth, que contém os resultados de um experimento para comparar o peso de plantas cultivadas sob três condições diferentes: um grupo controle (ctrl) e dois tratamentos diferentes (trt1, trt2).

No seu Jupyter Notebook (com kernel R), você pode rodar o seguinte código:

```R
# 1. Carregando e visualizando os dados nativos
data("PlantGrowth")
head(PlantGrowth)
Saída esperada:
```

```Plaintext
  weight group
1   4.17  ctrl
2   5.58  ctrl
3   5.18  ctrl
```


# Executando a ANOVA
```R
# A sintaxe "weight ~ group" significa: queremos analisar o Peso em função do Grupo.
modelo_anova <- aov(weight ~ group, data = PlantGrowth)

# Visualizando o resumo estatístico
summary(modelo_anova)
```

## Interpretando o resultado:
Você verá uma tabela na saída do summary. O valor mais importante é o Pr(>F), que é o nosso p-valor (p-value).

Se o p-valor for menor que 0.05 (nível de significância padrão), rejeitamos a hipótese nula e concluímos que existe diferença estatística significativa entre o peso das plantas dependendo do tratamento aplicado.

## 📚 Recursos Adicionais
[Documentação do IRkernel](https://irkernel.github.io/)

[R for Data Science](https://r4ds.had.co.nz/) (Livro Gratuito)

[Cheat Sheets do RStudio](https://opensource.posit.co/resources/cheatsheets/)
