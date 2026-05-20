PROJETO FASE 5 – MACHINE LEARNING NA CABEÇA
 

1) DESCRIÇÃO RÁPIDA DO PROJETO:
Para a Fase 5, vamos colocar a mão na massa no desenvolvimento de duas entregas obrigatórias: Machine Learning e Computação em Nuvem. Além dessas, vamos ter outras duas entregas definidas como “Ir Além”, que não valem nota. Contudo, esperamos que os grupos se desafiem em aprender ainda mais com essas duas entregas extras. Como recompensa das entregas dos “Ir Além”, os grupos ganharão gratificações (não notas) que serão explicadas ainda nesse documento.
2) DESCRIÇÃO DETALHADA DO PROJETO:
2.1) Entrega 1:
Você e o seu grupo estão na FarmTech Solutions prestando serviços de IA para uma fazenda de médio porte (200 hectares ou aproximadamente 210 campos de futebol oficiais) que produz várias culturas. Seu time precisa analisar uma base de dados com informações de condições de solo e temperatura, relacionadas com o tipo de produto agrícola dessa fazenda. Você deverá prever o rendimento de safra (conforme visto no capítulo 13 - Modelagem de Dados com Regressão Supervisionada, da Fase 4) e explorar a tendência de produtividade (visto no capítulo 10 - Machine Learning Sem Supervisão: Uma Jornada pela Descoberta de Dados, da Fase 5).
Base de dados: a base está anexada no portal, disponível no arquivo “crop_yield.csv”. As variáveis são:
Cultura: o nome da safra para a qual o rendimento está sendo medido.
Precipitação (mm dia 1): a quantidade de chuva em milímetros por dia.
Umidade específica a 2 metros (g/kg): a quantidade de vapor de água no ar por quilograma de ar seco a uma altura de 2 metros acima do solo.
Umidade relativa a 2 metros (%): a quantidade de vapor de água no ar como uma porcentagem da quantidade máxima de vapor de água que pode ser mantida a uma determinada temperatura e pressão.
Temperatura a 2 metros (ºC): a temperatura em graus Celsius a uma altura de 2 metros acima do solo.
Rendimento: a quantidade de rendimento em toneladas por hectare.
 
Metas da Entrega 1:
Baseado no dataset apresentado, sua atividade consiste em:
Fazer uma análise exploratória na base para se familiarizar com os dados;
Encontrar tendências para os rendimentos das plantações, por meio de clusterizações, e identificar se existem cenários discrepantes (outliers);
Fazer cinco modelos preditivos (cada um com um algoritmo diferente, conforme visto no capítulo “Modelagem de Dados com Regressão Supervisionada”) que, dadas as condições, prevejam qual será o rendimento da safra. Esta parte da tarefa inclui seguir as boas práticas dos projetos de Machine Learning, assim como avaliar o modelo com métricas pertinentes ao problema.
 
Entregáveis do Enunciado 1:
Entregue o link de um novo repositório do GitHub em nome do seu grupo (de 1 a 5 pessoas). Pedimos que não realize nenhum novo commit após a data da entrega, para não classificar como entrega após o prazo. Nesse repositório, faça o upload do link do notebook Jupyter, pois vamos executar seu notebook na correção. O Jupyter precisa ter:
Células de códigos executadas, com o código Python otimizado e com comentários das linhas;
Células de markdown organizando seu relatório e discorrendo textualmente sobre os achados a partir dos dados, e conclusões a respeito dos pontos fortes e limitações do trabalho;
O nome do arquivo deve conter seu nome completo, RM e pbl_fase4.ipynb, exemplo: “JoaoSantos_rm76332_pbl_fase4.ipynb”.
Vídeo: grave um vídeo de até 5 minutos demonstrando o funcionamento desse entregável, poste no YouTube de forma “não listado”, e coloque o link no seu GitHub, dentro do README.
Desenvolva o seu README com uma documentação introdutória, conduzindo o leitor para o seu Jupiter, onde lá, estará todo o passo a passo da sua solução e a sua descrição completa. Não precisa repetir a descrição do Jupiter no README do GitHub. Deixe sempre os seus repositórios públicos para que eles sejam acessíveis pela equipe interna da FIAP, mas cuidado com seus links para que não vazem e sejam compartilhados e plagiados.
Dica: assista esse vídeo para saber mais detalhes de como subir o Jupyter Notebook para o seu Git: <https://www.youtube.com/watch?v=5ZYRqca7OVc>.
2.2) Entrega 2:
Considere que sua Machine Learning precisa ser hospedada em uma estrutura de computação em nuvem.
 
Metas da Entrega 2:
1. Usando a calculadora da AWS, sua missão nessa entrega é realizar uma estimativa de custos (On-Demand – 100%) para usar uma máquina Linux simples, comparando os valores cotados para a região de São Paulo (BR) e para a região da Virgínia do Norte (EUA). A máquina será utilizada para hospedar uma API que receberá dados dos sensores que coletam as variáveis da Entrega 1 e onde rodará a Machine Learning. Qual a solução mais barata com as seguintes configurações?
2 CPUs.
1 GIB de memória.
Até 5 Gigabit de rede.
50 GB de armazenamento (HD).
 
2. Suponha também que você precisa acessar rapidamente os dados dos sensores e que há restrições legais para armazenamento no exterior. Qual opção você escolheria? Justifique.
Entregáveis do Enunciado 2:
Acrescente esses dados no mesmo README da Entrega 1 em nome do seu grupo (de 1 a 5 pessoas), desenvolvendo o README com imagens, gráficos e textos suficientes para entender a justificativa em escolher recursos na nuvem AWS. Pedimos que continue não realizando nenhum novo commit após a data da entrega, para não ser classificado como entrega após o prazo.
Vídeo: grave um segundo vídeo de até 5 minutos demonstrando a comparação de recursos usando a calculadora AWS, poste no YouTube de forma “não listado” e coloque o link no seu GitHub, dentro do README.

BAREMA DAS ENTREGAS OBRIGATÓRIAS
Critérios de Avaliação da Entrega 1:
Critério
Descrição
Peso
Repositório no GitHub
O repositório foi criado no prazo, possui o notebook Jupyter correto e atende às exigências de nomeação do arquivo. Não deve haver commits após a data de entrega.
1.5
Notebook Jupyter
O notebook contém:
 - Células de código executadas, com código Python otimizado e funcional.
 - Células de markdown organizadas, explicando os achados, os pontos fortes e as limitações do trabalho.
3.0
Estrutura do README
O README possui:
 - Documentação introdutória clara.
 - Link funcional para o notebook Jupyter.
 - Link para o vídeo demonstrativo no YouTube.
2.0
Vídeo Demonstrativo
O vídeo atende às exigências:
 - Duração de até 5 minutos.
 - Demonstra o funcionamento do entregável de forma clara.
 - Postado no YouTube como “não listado” e incluído no README.
2.0
Organização e Apresentação Geral
Clareza e organização geral do projeto:
 - Estrutura do repositório.
 - Nome correto dos arquivos.
 - Notebook bem organizado e de fácil leitura.
1.5
 
Detalhes Adicionais:
Notebook Jupyter:
Código Python deve ser otimizado, funcional e executado corretamente.
As células markdown devem conter explicações textuais bem estruturadas sobre resultados, achados, conclusões e limitações.

Critérios de Avaliação da Entrega 2:
Critério
Descrição
Peso
Estimativa de Custos na AWS
Apresentação da comparação de custos entre as regiões São Paulo (BR) e Virgínia do Norte (EUA) utilizando a calculadora da AWS.
 - Valores devem ser precisos e alinhados às configurações exigidas: 2 CPUs, 1 GiB RAM, 5 Gbps de rede, e 50 GB de HD.
2.5
Justificativa Técnica
Clareza na escolha da opção mais adequada, levando em consideração:
 - Acesso rápido aos dados dos sensores.
 - Restrições legais para armazenamento no exterior.
 - Análise crítica e bem fundamentada das vantagens da solução escolhida.
2.5
Documentação no README
O README deve conter:
 - Explicação clara da comparação de recursos com textos organizados.
 - Imagens ou gráficos que ilustrem os custos e as opções comparadas.
 - Justificativa final bem estruturada.
 - Link funcional para o vídeo no YouTube.
2.0
Vídeo Demonstrativo
O vídeo atende às exigências:
 - Duração de até 5 minutos.
 - Explica a comparação de custos usando a calculadora AWS.
 - Demonstra os valores cotados e justifica a solução escolhida.
 - Postado no YouTube como “não listado” e incluído no README.
2.0
Organização e Pontualidade
Clareza na entrega:
 - Nenhum commit adicional após o prazo.
 - Estrutura organizada no GitHub (README e vídeo acessíveis).
1.0
Detalhes Adicionais:
Estimativa de Custos:
Os valores cotados devem ser precisos e detalhados.
Mostrar claramente as diferenças de preço entre São Paulo e Virgínia do Norte.
Justificativa Técnica:
Deve demonstrar entendimento das restrições legais e justificar tecnicamente a solução escolhida.
Abordar tempo de acesso aos dados, desempenho e viabilidade econômica.
README:
Organização do texto com imagens e gráficos que facilitem a compreensão.
Evitar duplicação de informações do notebook.


FEEDBACK:

O grupo entregou um trabalho muito sólido e bem pensado, especialmente na Entrega 2, onde a justificativa técnica com dados concretos de latência e a argumentação sobre LGPD demonstraram um nível de maturidade bem acima do esperado. O notebook da Entrega 1 também impressiona pela qualidade da conclusão e pela escolha criteriosa dos modelos, com análise clara de pontos fortes e limitações. Dois pontos merecem atenção para próximas entregas: o nome do arquivo entregue não bate com o referenciado no README, o que gera confusão na navegação do repositório, e a análise exploratória poderia ter começado com uma etapa mais formal de estatística descritiva antes de partir para os gráficos. São ajustes simples que, quando incorporados ao fluxo de trabalho do grupo, vão elevar ainda mais a qualidade de um projeto que já demonstra muito capricho e dedicação real.