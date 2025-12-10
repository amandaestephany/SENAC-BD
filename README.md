# MedEco - Sistema de Gestão Sustentável de Medicamentos Hospitalares

## Visão Geral

MedEco é uma plataforma desenvolvida para contribuir com a sustentabilidade hospitalar no contexto de ESG (Environmental, Social and Governance). O sistema utiliza inteligência artificial preditiva para analisar o fluxo de reestoque e consumo de medicamentos em hospitais, com o objetivo principal de reduzir o desperdício através da redistribuição inteligente de medicamentos entre instituições participantes.

## Mini-Mundo

### Contexto do Problema

Hospitais frequentemente enfrentam desafios no gerenciamento de estoque de medicamentos. Enquanto algumas unidades possuem medicamentos próximos do vencimento que não serão consumidos a tempo, outras unidades necessitam urgentemente dos mesmos medicamentos. O MedEco atua como uma ponte entre essas instituições, permitindo a transferência coordenada de medicamentos que seriam desperdiçados, promovendo economia de recursos e sustentabilidade ambiental.

### Entidades e Relacionamentos

#### Medicamentos e Composição

O sistema trabalha com **medicamentos** identificados por nome comercial, fabricante e tipo. Cada medicamento pode ser classificado como controlado ou não controlado, o que afeta as regras de transferência e armazenamento.

A composição dos medicamentos é detalhada a nível de **princípios ativos**, permitindo que a IA identifique medicamentos similares ou substituíveis. Um medicamento pode conter múltiplos princípios ativos (como combinações de antibióticos), e cada princípio ativo possui dosagem específica (quantidade e unidade, como "500 mg" ou "10 mL").

Para lidar com nomenclaturas alternativas, cada princípio ativo pode ter múltiplos nomes (sinônimos), como "acetaminofeno" e "paracetamol" para o mesmo composto. Essa funcionalidade permite que a IA faça correspondências precisas mesmo quando hospitais utilizam terminologias diferentes.

#### Embalagens e Lotes

Os medicamentos são comercializados em **embalagens** com quantidades específicas (caixas com 10, 20, 30 unidades, etc.) e podem ter código de barras para rastreamento. Cada embalagem origina diferentes **lotes** de produção, identificados por código único, data de fabricação e data de validade.

#### Estrutura Hospitalar

O sistema organiza a estrutura hospitalar em **unidades de saúde**, que possuem endereço completo (CEP, logradouro, número, complemento, ponto de referência, bairro, cidade e estado). Cada unidade de saúde pode ter uma ou mais **farmácias**, identificadas por nome e localização dentro da instituição (como "Farmácia Central", "Farmácia Ambulatorial", "Farmácia de Emergência").

#### Estoque e Rastreamento

O estoque é gerenciado através de **caixas de medicamento**, que representam unidades físicas de embalagens pertencentes a um lote específico. Cada caixa é armazenada em uma farmácia específica e possui uma situação (disponível, reservada, vencida, em transferência, etc.). Caixas podem ter sua data de validade revalidada quando isso é permitido pelo fabricante.

#### Operadores e Vínculos

**Operadores** são os profissionais responsáveis pelas operações no sistema, identificados por CPF, com informações de cargo, nome e email. Um operador pode estar vinculado a múltiplas farmácias ao longo do tempo através de **vínculos**, que registram data de início e fim do vínculo, permitindo rastreamento completo de quem tinha acesso a cada farmácia em determinado período.

#### Propostas de Transferência

O core do sistema MedEco são as **propostas** de transferência de medicamentos entre farmácias. Cada proposta registra:
- Data e hora da criação
- Tipo (doação, empréstimo, troca)
- Quantidade de caixas
- Situação (pendente, aprovada, rejeitada, concluída)
- Farmácia de origem (enviadora)
- Farmácia de destino (receptora)
- Operador que enviou a proposta
- Operador que avaliou a proposta

Propostas são criadas quando a IA identifica oportunidades de redistribuição ou quando operadores solicitam transferências manualmente.

#### Movimentos de Estoque

Todas as operações que afetam o estoque são registradas como **movimentos**, incluindo:
- Entrada de novos medicamentos
- Saída por dispensação
- Transferências entre farmácias
- Descartes
- Revalidações
- Ajustes de inventário

Cada movimento registra data e hora, tipo de operação, a caixa de medicamento envolvida, o operador autor, a farmácia onde ocorreu e, quando aplicável, a proposta que gerou o movimento (para transferências).

### Fluxo Operacional

1. **Entrada de Estoque**: Quando novos medicamentos chegam, são registrados com todas as informações do lote, embalagem e medicamento, criando caixas de medicamento no sistema.

2. **Monitoramento Preditivo**: A IA analisa continuamente padrões de consumo e datas de validade, identificando medicamentos em risco de vencer.

3. **Geração de Propostas**: O sistema sugere transferências entre farmácias participantes, considerando necessidades de estoque e prazos de validade.

4. **Avaliação e Aprovação**: Operadores responsáveis avaliam as propostas, considerando fatores logísticos e necessidades locais.

5. **Execução de Transferências**: Propostas aprovadas geram movimentos de saída na farmácia origem e entrada na farmácia destino.

6. **Rastreamento Completo**: Todo o histórico de cada caixa de medicamento é preservado, permitindo auditorias e análises de eficiência.

### Benefícios do Sistema

- **Redução de Desperdício**: Medicamentos são redistribuídos antes de vencer
- **Economia de Recursos**: Hospitais evitam compras desnecessárias
- **Sustentabilidade Ambiental**: Menos descarte de medicamentos
- **Otimização de Estoque**: IA sugere transferências baseadas em padrões reais
- **Rastreabilidade Completa**: Histórico detalhado de cada medicamento
- **Conformidade Regulatória**: Controle rigoroso de medicamentos controlados
- **Colaboração Inter-hospitalar**: Rede de compartilhamento entre instituições

### Inteligência Artificial

A IA do MedEco possui capacidades especiais para:
- Identificar medicamentos similares através dos princípios ativos
- Sugerir substituições quando medicamentos específicos não estão disponíveis
- Prever padrões de consumo baseados em histórico
- Otimizar rotas de transferência entre múltiplas farmácias
- Alertar sobre medicamentos próximos do vencimento
- Reconhecer sinônimos de princípios ativos automaticamente

## Estrutura do Banco de Dados

O banco de dados foi projetado seguindo princípios de normalização e suporta todas as operações necessárias para o funcionamento da plataforma. As principais tabelas incluem:

- `Medicamento`, `Embalagem`, `Lote`, `CaixaMedicamento`
- `PrincipioAtivo`, `PrincipioAtivoNome`, `ComposicaoMedicamento`
- `UnidadeSaude`, `Endereco`, `Farmacia`
- `Operador`, `VinculoOperadorFarmacia`
- `Proposta`, `Movimento`

Consulte o arquivo `Schema-MedEco-IA.sql` para a estrutura completa do banco de dados.

## Equipe
- Polyana Fontes
- Half Ukan Soares
- Izabella Regina Norberto Santos
- Amanda Estephany Silva dos Santos
- Vicente de Paula Gomes da Silva
