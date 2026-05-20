# Introducao

## Projeto Fase 7 - A Consolidacao de um Sistema

A Fase 7 tem como objetivo consolidar, em um unico projeto Python, tudo o que foi desenvolvido nas Fases 1 a 6 da FarmTech Solutions. A proposta e transformar entregas isoladas em um sistema integrado de gestao para o agronegocio, com potencial de adaptacao para outros setores mediante troca de dados.

---

## 1. Descricao Rapida do Projeto

Integrar todos os servicos das fases anteriores em uma unica pasta de projeto e disponibilizar sua execucao por meio de:
- dashboard com botoes;
- comandos no terminal do VS Code.

---

## 2. Resgate das Fases 1 a 6

### Fase 1 - Base de Dados Inicial
- Calculo de area de plantio e manejo de insumos.
- Organizacao de dados como base do ecossistema digital.
- Integracao com API meteorologica publica.
- Analise estatistica em R com base nos dados meteorologicos.

### Fase 2 - Banco de Dados Estruturado
- Estruturacao de banco relacional completo (MER e DER).
- Integracao dos dados de manejo e producao da Fase 1.
- Organizacao dos dados em tempo real para futuras analises.

### Fase 3 - IoT e Automacao Inteligente
- Sistema IoT com ESP32 e sensores para irrigacao automatizada.
- Operacoes CRUD conectadas ao banco estruturado da Fase 2.
- Logica de acionamento de bomba baseada em nutrientes, pH (LDR) e umidade (DHT22), com dados simulados e reais.

### Fase 4 - Dashboard Interativo com Data Science
- Integracao de Machine Learning com Scikit-Learn e Streamlit.
- Dashboard interativo para visualizacao e apoio a decisao.
- Monitoramento fisico com LCD e Serial Plotter no ESP32.
- Algoritmos preditivos para sugerir acoes de irrigacao e manejo.

### Fase 5 - Cloud Computing e Seguranca
- Hospedagem da infraestrutura em AWS.
- Foco em seguranca, disponibilidade e escalabilidade.
- Aplicacao de boas praticas alinhadas a ISO 27001 e ISO 27002 para protecao de dados sensiveis.

### Fase 6 - Visao Computacional com Redes Neurais
- Sistema com YOLO para monitoramento visual da plantacao.
- Deteccao de pragas, doencas e crescimento irregular.
- Coleta por ESP32-CAM (opcional) ou processamento por imagens estaticas em pasta.

---

## 3. O Que a Fase 7 Exige

### 3.1 Integracao Tecnica em Projeto Unico
- Reunir em uma unica pasta de projeto os programas das fases anteriores.
- Integrar principalmente os servicos das Fases 1, 2, 3 e 6 na dashboard da Fase 4.
- Permitir acionamento por botoes na dashboard e/ou comandos no terminal.

### 3.2 Servico de Alertas na AWS
- Implementar mensageria AWS integrada ao sistema consolidado.
- Monitorar dados de sensores (Fase 1 ou 3) ou resultados de visao computacional (Fase 6).
- Disparar alertas para funcionarios por e-mail ou SMS com acoes corretivas definidas pelo grupo.

### 3.3 Consolidacao de Entregas Pendentes
- Caso alguma etapa entre Fases 1 e 6 nao tenha sido entregue anteriormente, ela pode ser implementada agora para composicao da nota.

---

## 4. Entregaveis Obrigatorios

### Entregavel 1 - Dashboard Final Integrada
- Dashboard final baseada na Fase 4.
- Inclusao dos programas das Fases 1, 2, 3 e 6.
- Projeto organizado em unico ambiente de desenvolvimento (VS Code ou IDE equivalente).

### Entregavel 2 - Mensageria AWS
- Servico simples de alerta na AWS para sensores ou visao computacional.
- Inclusao no README de:
  - explicacao da solucao;
  - prints da AWS;
  - comentarios claros e objetivos.

### Entregavel 3 - Documentacao e Repositorio
- Novo repositorio GitHub com nome do grupo (ou solo).
- Documentacao das melhorias e integracoes das Fases 1, 2, 3, 4, 5 e 6.
- Estrutura de pastas do GitHub coerente com a estrutura local no VS Code.
- Envio do link via portal FIAP (podendo usar PDF).
- Nao realizar commits apos o prazo.
- Compartilhamento privado opcional com tutor no GitHub: leoruiz197.

### Entregavel 4 - Video Demonstrativo
- Video de ate 10 minutos.
- Demonstracao das funcionalidades das Fases 1 a 6 consolidadas.
- Publicacao no YouTube como nao listado.
- Link do video no README.

---

## 5. Projeto Ir Alem (Opcional, sem impacto na nota oficial)

A Fase 7 apresenta duas opcoes extras para desafio tecnico. Embora nao valham nota oficial, geram pontuacao interna e reconhecimento.

### Opcao 1 - Integracao de IA na AWS (Rekognition)
- Tentar implementar o reconhecedor de imagens na AWS (Rekognition).
- Caso haja bloqueio no ambiente estudantil, documentar com prints as etapas de configuracao ate o limite permitido.
- Entregar documentacao no GitHub com arquitetura, justificativa e video de ate 5 minutos.

### Opcao 2 - Otimizacao com Algoritmos Geneticos
- Adaptar algoritmo genetico para problema de otimizacao agricola.
- Garantir reprodutibilidade via leitura/escrita de dados em arquivo.
- Alterar funcoes estruturantes (selection, crossover, mutation) e comparar desempenho.
- Entregar notebook/Colab documentado, justificativas e video de ate 5 minutos.

---

## 6. BAREMA das Entregas Obrigatorias

### Criterios e Pesos

1. Repositorio no GitHub (3.0)
- Criado no prazo.
- Estrutura coerente com VS Code local.
- Sem commits apos a data de entrega.

2. VS Code (3.0)
- Codigos Python otimizados e funcionais.
- Arquivos organizados por servicos/fases.
- Desconto de -0,5 para cada item das Fases 1 a 6 nao entregue na consolidacao.

3. Estrutura do README (2.0)
- Documentacao clara e objetiva.
- Link do video demonstrativo no YouTube.

4. Video Demonstrativo (2.0)
- Ate 10 minutos.
- Demonstracao clara do funcionamento.
- Publicado como nao listado e linkado no README.

---

## 7. Detalhes Adicionais Reforcados no Enunciado

### VS Code
- Codigos Python devem executar corretamente.
- Organizacao do projeto deve facilitar manutencao e avaliacao.

### README
- Deve conduzir o leitor ao entendimento completo do sistema consolidado da fazenda.

---

## 8. Sintese Final da Fase 7

A entrega da Fase 7 nao e apenas adicionar funcionalidades novas. O foco principal e consolidar tudo o que foi construido anteriormente em um sistema unico, coerente e demonstravel, com:
- integracao tecnica real entre modulos;
- operacao centralizada via dashboard/terminal;
- alertas automatizados na AWS;
- documentacao completa e verificavel;
- apresentacao final objetiva em video.
