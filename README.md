# Netflix_PBI
Criação de Dash só para passar o tempo e treinar um pouco o design. O foco do material NÃO é a linguagem nem análise de dados, apenas o layout mesmo. 
## Entendimento do Negócio
A Netflix é uma plataforma global de streaming que oferece filmes, séries e documentários com conteúdo original. Fundada em 1997, começou como um serviço de aluguel de DVDs pelo correio e, em 2007, lançou seu serviço de streaming. A empresa continua a inovar no mercado de entretenimento, investindo em produções internacionais e tecnologias avançadas.

### Problema do Negócio 
Como é o perfil dos assinantes ativos em junho de 2023?

## Entendimento dos Dados
Base em planilha de Excel bem simples, pois foi disponibilizada apenas para responder duas questões de estatística usando Excel, mas aproveitei para criar um Dash em Power BI. A base contém 9 colunas e 2057 linhas e está disponível no GitHub. 
### Metadados

![image](https://github.com/samvalentim/Netflix_PBI/assets/106708930/2188d237-5291-47ca-91d8-201709f7c534)


## Preparação dos Dados
### Power Query em M
Criação de coluna para identificar quanto tempo de assinatura o cliente possui. 
    #"Idade Inserida" = Table.AddColumn(#"Tipo Alterado", "Idade.1", each Date.From(DateTime.LocalNow()) - [inicio], type duration),
    #"Total de Anos Calculado" = Table.TransformColumns(#"Idade Inserida",{{"Idade.1", each Duration.TotalDays(_) / 365, type number}}),
    #"Colunas Renomeadas" = Table.RenameColumns(#"Total de Anos Calculado",{{"Idade.1", "tempo_casa"}}),
    #"Tipo Alterado2" = Table.TransformColumnTypes(#"Colunas Renomeadas",{{"tempo_casa", type text}})

### Medidas em DAX
n_assinantes: contar quantos assinantes existem na base
n_assinantes = DISTINCTCOUNT('Dados Netflix'[id])

total_receita: soma do total das receitas contidas na base
total_receita = sum('Dados Netflix'[receita])

## Modelagem 
### Data Viz. 

![image](https://github.com/samvalentim/Netflix_PBI/assets/106708930/c2b894dc-42f8-40ee-a249-102d6335c5d1)
