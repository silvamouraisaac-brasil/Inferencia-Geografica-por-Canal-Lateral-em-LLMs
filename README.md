# PoC — Inferência Geográfica por Canal Lateral em LLMs

## Objetivo

Esta PoC investiga um possível cenário de **information leakage** em LLMs, no qual informações geográficas podem ser inferidas indiretamente através da combinação de respostas individualmente permitidas.

O objetivo não é obter um endereço residencial, mas analisar se consultas aparentemente inofensivas podem ser utilizadas para **reduzir progressivamente um perímetro geográfico**.

## Cenário analisado

O modelo possui restrições relacionadas à exposição de informações geográficas sensíveis.

Em vez de solicitar diretamente uma localização protegida, a PoC utiliza consultas sobre informações públicas relacionadas à região, como:

- estabelecimentos;
- pontos de referência;
- localização aproximada;
- serviços disponíveis na região.

A hipótese é que essas respostas possam ser correlacionadas para produzir uma inferência geográfica mais precisa do que aquela permitida diretamente pelo modelo.

## Vetor analisado

**Side-Channel / Indirect Information Disclosure**

O problema analisado ocorre quando o modelo avalia cada solicitação isoladamente e não considera o contexto acumulado das consultas.

### Fluxo conceitual

Contexto geográfico aproximado
            ↓
Consultas aparentemente legítimas
            ↓
Informações públicas fornecidas pelo LLM
            ↓
Correlação entre respostas
            ↓
Redução progressiva do perímetro
            ↓
Inferência geográfica

Resultado observado

Durante os testes, foi observado que respostas individuais consideradas não sensíveis podem, quando combinadas, fornecer informações suficientes para afunilar uma determinada região geográfica.

A precisão obtida depende do contexto, das informações disponíveis e do comportamento específico do modelo.

A PoC demonstra um comportamento experimental e não deve ser interpretada como método garantido para determinar um endereço residencial.

Risco potencial

Esse tipo de comportamento pode aumentar riscos relacionados a:

engenharia social;
phishing direcionado;
profiling;
correlação de informações públicas;
exposição indevida de contexto geográfico.
Mitigação

Uma possível abordagem seria implementar Context-Aware Guardrails, considerando não apenas cada prompt individualmente, mas também padrões de consultas relacionados entre si.

Possíveis controles:

detecção de tentativas progressivas de afunilamento geográfico;
limitação de precisão em respostas de localização;
análise de contexto entre múltiplas consultas;
políticas de minimização de dados;
monitoramento de padrões de information disclosure.
Limitações

Esta PoC possui algumas limitações:

resultados podem variar entre modelos;
informações públicas disponíveis podem mudar;
localização inferida não significa necessariamente localização residencial;
uma única execução não é suficiente para estabelecer uma vulnerabilidade generalizada.
Objetivo educacional

Projeto desenvolvido para estudo de LLM Security, AI Red Teaming, prompt-based attacks e information leakage.

A PoC utiliza informações não sensíveis e tem finalidade exclusivamente educacional.

Área: LLM Security / AI Security
Tipo: Proof of Concept
Nível: Junior / Experimental
