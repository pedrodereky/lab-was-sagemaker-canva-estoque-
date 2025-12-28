Projeto de Previsão de Inventário com AWS SageMaker Canvas
Este repositório contém conjuntos de dados estruturados para o desenvolvimento de modelos de Machine Learning focados em previsão de séries temporais. O objetivo é prever os níveis de stock com base em variáveis como preço, promoções e datas.

Conteúdo dos Datasets
Os ficheiros apresentam três níveis de complexidade para o treino de modelos de previsão:

dataset-500-curso-sagemaker-canvas-dio.csv

Tamanho: 500 registos.

Atributos: ID_PRODUTO, DIA, FLAG_PROMOCAO, QUANTIDADE_ESTOQUE.

Contexto: Histórico base focado na relação entre promoções e saída de stock.

dataset-1000-com-preco-promocional-e-renovacao-estoque.csv

Tamanho: 1000 registos.

Atributos: ID_PRODUTO, DATA_EVENTO, PRECO, FLAG_PROMOCAO, QUANTIDADE_ESTOQUE.

Contexto: Introduz a variável de preço e simula o comportamento de reposição automática (renovação) quando o stock atinge níveis baixos.

dataset-1000-com-preco-variavel-e-renovacao-estoque.csv

Tamanho: 1000 registos.

Atributos: ID_PRODUTO, DATA_EVENTO, PRECO, QUANTIDADE_ESTOQUE.

Contexto: Cenário onde o preço é dinâmico, permitindo analisar como a flutuação de valores impacta a velocidade de esgotamento do inventário.

Dicionário de Variáveis
ID_PRODUTO: Código identificador único do item (25 produtos representados).

DIA / DATA_EVENTO: Timestamp diário dos registos (formato AAAA-MM-DD).

PRECO: Valor unitário de venda do produto no dia específico.

FLAG_PROMOCAO: Indicador binário (1 para ativo, 0 para inativo) de campanhas promocionais.

QUANTIDADE_ESTOQUE (Target): Volume disponível em armazém no final do período diário.

Passo a Passo para Descrever os Dados
Para descrever estes dados de forma eficaz em apresentações ou documentação técnica, siga estes cinco passos:

1. Análise da Janela Temporal

Identifique o intervalo de tempo coberto. Os dados iniciam-se em 31/12/2023. Verifique a última data disponível para definir o horizonte de previsão (por exemplo, prever os próximos 5 dias com base nos últimos 40 dias).

2. Identificação da Granularidade

Explique que os dados estão no nível de produto por dia. Note que existem múltiplos produtos no mesmo ficheiro, o que exige que o modelo de ML aprenda padrões individuais para cada ID_PRODUTO.

3. Análise da Variável Alvo (Target)

Observe a coluna QUANTIDADE_ESTOQUE. Descreva se o stock diminui gradualmente (vendas orgânicas) ou se apresenta quedas bruscas em dias de promoção. Identifique os pontos de reposição, onde o valor salta repentinamente para um patamar superior (ex: 100 unidades).

4. Correlação entre Variáveis

Relacione a FLAG_PROMOCAO ou o PRECO com a velocidade de saída do stock. Dados com preços variáveis permitem identificar a elasticidade-preço da procura: quanto maior o desconto, mais rápida é a necessidade de reposição.

5. Preparação para o Modelo

No SageMaker Canvas, descreva a configuração:

Item ID: ID_PRODUTO.

Time Column: DIA ou DATA_EVENTO.

Target Column: QUANTIDADE_ESTOQUE.

Horizonte de Previsão: Definir quantos dias à frente o negócio precisa de prever para evitar rutura de stock.
