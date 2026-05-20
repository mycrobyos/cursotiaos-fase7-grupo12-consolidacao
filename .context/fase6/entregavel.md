PROJETO FASE 6 – O COMEÇO DA REDE NEURAL
  

   
1) DESCRIÇÃO RÁPIDA DO PROJETO:
Para a Fase 6, vamos botar a mão na massa no desenvolvimento de uma rede neural. Além dessa, vamos ter outras duas entregas definidas como “Ir Além”, que não valem nota.
Assim como aconteceu na fase anterior, esperamos que os grupos se desafiem em aprender ainda mais com essas duas entregas extras. Como recompensa das entregas dos “Ir Além”, os grupos ganharão gratificações (não notas) que serão explicadas ao longo das Lives e nesse documento.
 
2) DESCRIÇÃO DETALHADA DO PROJETO:
Entrega 1: a FarmTech Solutions está expandindo os serviços de IA e indo para além do agronegócio. Sua carteira de clientes aumentou e agora está prestando serviços de IA na área da saúde animal, segurança patrimonial de fazendas e de casas de seus clientes, controle de acessos de funcionários, análise de documentos de qualquer natureza. E ainda, começou a atuar na área da visão computacional.
Nessa entrega, você faz parte do time de desenvolvedores da FarmTech, e está visitando um cliente que gostaria de entender como funciona um sistema de visão computacional na prática.
Seu objetivo é criar um sistema de visão computacional usando o YOLO que demonstre seu potencial e acurácia. É importante ressaltar que você é livre para escolher o cenário de imagens que servirá para a etapa de treinamento, validação e testes.
 
Metas da entrega 1:
Organizar um dataset com no mínimo 40 imagens de um objeto A que você escolher e +40 imagens de um outro objeto B bem diferente do A, totalizando 80 imagens;
Dessas 40 imagens do objeto A, reserve 32 para a etapa do treino, 4 para validação e 4 para testes. Faça o mesmo para o banco de imagens do objeto B;
Organizar suas imagens no seu Google Drive pessoal ou do grupo, separando em pastas de treino, validação e teste;
Fazer a rotulação das imagens de treinamento usando o site Make Sense IA;
Salvar as rotulações no seu Google Drive;
Montar um Colab, conectado ao seu Google Drive, que seja capaz de fazer o treinamento, validação e teste, e que descreva em Markdown, o passo a passo dessas três etapas;
Fazer ao menos duas simulações com a quantidade diferente de épocas, e comparar os resultados de acurácia, erro e desempenho quando alteramos tais parâmetros. Escolha por exemplo, 30 e 60 épocas, isto é, bem diferentes entre si;
Apresente suas conclusões sobre os resultados encontrados na validação e nos testes. Os resultados estarão disponíveis em “Results saved to yolov5/runs/detect/expX” onde X vai incrementando a cada treino que você realizar.
Traga prints das imagens de testes processadas pelo seu modelo para convencer o seu cliente fictício da FarmTech Solutions.
 
Entregáveis do enunciado 1:
Insira a sua solução em um novo repositório do GitHub com o nome do seu grupo (de 1 a 5 pessoas ou solo) e nos envie o link do GitHub via portal da FIAP. Pode usar um arquivo PDF para nos enviar o link. Pedimos que não realize nenhum novo commit após a data da entrega, para não classificar como entrega após o prazo. Além disso, nesse repositório, faça o upload do link do notebook Jupyter, pois vamos executar seu notebook na correção. O Jupyter precisa ter:
Células de códigos executadas, com o código Python otimizado e com comentários das linhas;
Células de markdown organizando seu relatório e discorrendo textualmente sobre os achados a partir dos dados, e conclusões a respeito dos pontos fortes e limitações do trabalho;
O nome do arquivo deve conter seu nome completo, RM e pbl_fase6.ipynb, por exemplo: “JoaoSantos_rm76332_pbl_fase6.ipynb”. 
Vídeo: grave um vídeo de até 5 minutos demonstrando o funcionamento desse entregável, poste no YouTube de forma “não listado”, e coloque o link no seu GitHub, dentro do README.
Desenvolva o seu README com uma documentação introdutória, conduzindo o leitor para o seu Colab/Jupiter, onde lá, estará todo o passo a passo da sua solução e a sua descrição completa. Não precisa repetir a descrição do Jupiter no README do GitHub e sim, fazer uma integração documental da solução. Deixe sempre os seus repositórios públicos para que eles sejam acessíveis pela equipe interna da FIAP, mas cuidado com seus links para não vazarem e serem plagiados.
 
Dica: assista esse vídeo para saber mais detalhes de como subir o Colab Notebook para o seu Git: <https://www.youtube.com/watch?v=5ZYRqca7OVc>.
   
Entrega 2: agora que você já experimentou a customização da YOLO para reconhecer objetos da sua base montada, chegou a hora de comparar o resultado com outras abordagens “concorrentes”.
Como quase tudo na computação, na Visão Computacional não existe uma solução 100% “melhor” ou “pior” que as demais: tudo é uma questão de cenários de aplicabilidade, bem como critérios de desempate, que você adquire fazendo. Assim, ainda que a YOLO tenha performado bem (ou não!) é sempre bom experimentar outras soluções.
 
Metas da entrega 2:
A partir da base de dados que você montou para a Entrega 1:
Aplique a YOLO tradicional, vista no capítulo 3 de Redes Neurais, e avalie a performance desta rede em relação à proposta na Entrega 1;
Treine uma CNN do zero para classificar a qual classe a imagem pertence.
 

 
Entregáveis do enunciado 2:
Para cada abordagem realizada (YOLO adaptável feito na Entrega 1, YOLO padrão e CNN treinada do zero, esses últimos disponíveis nos capítulos de Redes Neurais), avalie criticamente os resultados comparando-os em termos de:
Facilidade de uso/integração;
Precisão do modelo;
Tempo de treinamento/customização da rede (se aplicável);
Tempo de inferência (predição).
Jupyter notebook ou Colab integrado ao seu GitHub com a implementação e avaliação da sua solução. Seu notebook deve conter:
Código executado;
Saídas;
Avaliações;
Células markdown avaliando criticamente seus resultados e comparando as soluções implementadas.

BAREMA DAS ENTREGAS OBRIGATÓRIAS
 
Critérios de avaliação das Entregas 1 e 2:
Critério
Descrição
Peso
Repositório no GitHub
O repositório foi criado no prazo, possui o notebook Jupyter/Colab correto e atende às exigências de nomeação do arquivo. Não deve haver commits após a data de entrega.
1.5
Notebook Jupyter / Colab
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
 - Notebook bem-organizado e de fácil leitura.
1.5


FEEDBACK:

