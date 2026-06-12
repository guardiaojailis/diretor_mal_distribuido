
Simulador da Escolha da Rainha da Primavera - Conteúdo para fins didáticos somente.

# Desenvolvimento de um Simulador de Eleição Distribuída: Rainha da Primavera 2026

## 1. Contexto Inicial

O trabalho teve início a partir de uma discussão sobre como os conceitos de Sistemas Distribuídos e Arquitetura de Software podem auxiliar no desenvolvimento de aplicações modernas apoiadas por Inteligência Artificial Generativa.

Foram analisados temas como:

* Assincronismo
* Tolerância a falhas
* Cache distribuído
* Idempotência
* Arquitetura baseada em agentes
* Observabilidade
* Separação entre lógica de negócio e orquestração

Como exercício prático, foram solicitadas diversas ideias de projetos capazes de demonstrar esses conceitos em sala de aula.

---

## 2. Levantamento de Ideias

Inicialmente foram propostas doze idéias de projetos envolvendo sistemas distribuídos, algoritmos de consenso, tolerância a falhas e agentes inteligentes.

Entre as propostas estavam:

* Eleição de líder entre agentes
* Sistemas com consistência eventual
* Correção distribuída de provas
* Chat distribuído com memória inconsistente
* Sistemas de votação distribuída

A partir dessas sugestões surgiu uma idéia própria: desenvolver um sistema de votação eletrônica para a eleição da Rainha da Primavera de uma escola.

---

## 3. Surgimento da Idéia da Rainha da Primavera

O cenário imaginado foi o seguinte:

Uma escola realiza anualmente a eleição da Rainha da Primavera. Cada sala possui uma urna eletrônica responsável por registrar os votos dos alunos.

O voto é secreto e os resultados são enviados para um diretor responsável pela apuração final.

Entretanto, o diretor possui interesses pessoais e deseja favorecer uma candidata específica: a filha da comadre de sua vizinha.

Como as urnas são consideradas seguras e os votos não podem ser alterados diretamente, o diretor decide agir sobre o processo de apuração.

A fraude ocorre no momento em que os votos percorrem a rede até o ponto central de consolidação dos resultados.

---

## 4. Análise Sob a Ótica de Sistemas Distribuídos

A proposta foi analisada como um caso clássico de comprometimento da integridade dos dados em um sistema distribuído.

O estudo identificou os seguintes elementos:

| Elemento                        | Conceito Distribuído      |
| ------------------------------- | ------------------------- |
| Urnas das salas                 | Nós distribuídos          |
| Canal VPN                       | Confidencialidade         |
| Diretor centralizador           | Ponto único de falha      |
| Alteração dos resultados        | Ataque MITM               |
| Ausência de auditoria           | Falta de verificabilidade |
| Exibição parcial dos resultados | Consistência eventual     |

A principal conclusão foi que:

> VPN garante confidencialidade, mas não garante integridade fim a fim.

Também foram discutidas soluções como:

* Assinaturas digitais
* Ledger imutável
* Blockchain permissionada
* Auditoria independente
* Arquitetura Zero Trust

---

## 5. Primeira Versão do Sistema

Após a validação da ideia, iniciou-se o projeto de um simulador web.

### Estrutura inicial

O sistema passou a possuir:

* 10 salas de votação
* Duas candidatas

  * Vermelha
  * Azul
* Painel central do diretor
* Display de apuração
* Botões para envio dos votos

O fluxo básico era:

1. Alunos votam.
2. Sala envia os votos.
3. Diretor recebe.
4. Resultado parcial é atualizado.

---

## 6. Evolução do Simulador

Durante os refinamentos, foram adicionados novos requisitos:

### Regras de votação

* Cada sala possui até 7 votos.
* Os votos podem ser distribuídos livremente entre as candidatas.
* Após o envio, a sala não pode alterar os resultados.

### Elementos visuais

Foram incorporados:

* Bootstrap
* Font Awesome
* Cytoscape.js

Objetivos:

* Representar as salas visualmente.
* Exibir o diretor como nó central.
* Animar os votos viajando pela rede.

### Melhorias de experiência

Foram adicionados:

* Barras de porcentagem
* Destaque visual para a última sala
* Borda piscando quando resta apenas uma sala para envio
* Animação dos votos trafegando até o diretor

---

## 7. Implementação da Fraude

A etapa seguinte consistiu em representar a fraude de forma didática.

Inicialmente o diretor possuía um botão explícito chamado "Fraudar".

Posteriormente o conceito foi refinado para algo mais próximo da narrativa:

* A última sala permanece pendente.
* O diretor recebe seus votos.
* O sistema apresenta uma etapa chamada "Apuração Final".
* O diretor escolhe qual candidata será beneficiada.
* O sistema recalcula o resultado final.

O objetivo passou a ser demonstrar como um ponto central de confiança pode manipular os resultados sem alterar diretamente os votos registrados nas urnas.

---

## 8. Trecho de Código Representativo

O trecho abaixo representa a essência da demonstração do ataque:

```python
class Urna:
    def votar(self, candidata):
        voto = {
            "candidata": candidata,
            "sala": self.sala,
            "assinatura": self.assinar(voto)
        }
        return voto

class DiretorMalicioso:
    def receber_voto(self, voto):
        if voto["candidata"] != "filha_da_cumade":
            voto["candidata"] = "filha_da_cumade"
        return voto
```

Esse exemplo ilustra o momento em que o intermediário altera a informação antes da apuração final.

---

## 9. Refinamentos Finais

Após diversos ajustes, a versão final passou a seguir o seguinte fluxo:

### Etapa 1

As nove primeiras salas enviam normalmente seus votos.

### Etapa 2

A décima sala permanece destacada visualmente.

### Etapa 3

O diretor visualiza os votos da última sala em área reservada.

### Etapa 4

O público continua vendo apenas as porcentagens gerais.

### Etapa 5

O diretor escolhe qual candidata deseja favorecer.

### Etapa 6

O sistema calcula automaticamente os votos necessários para garantir a vitória da candidata escolhida.

### Etapa 7

O resultado é exibido ao público como uma eleição aparentemente legítima.

### Etapa 8

A candidata escolhida pelo diretor é declarada vencedora da Rainha da Primavera 2026.

---

## 10. Arquitetura Final do Simulador

### Componentes

#### Salas de Votação

* 10 salas
* Até 7 votos por sala
* Registro local dos votos

#### Rede Simulada

* Representação gráfica via Cytoscape.js
* Animação dos votos trafegando até o diretor

#### Diretor

* Recebe os votos
* Controla a apuração final
* Pode favorecer uma candidata

#### Painel Público

* Exibe somente percentuais
* Não mostra detalhes da manipulação

#### Sistema de Apuração

* Consolida os votos
* Recalcula os resultados da última sala
* Produz o resultado final

---

## 11. Resultado Acadêmico

O projeto transformou um conceito abstrato de Sistemas Distribuídos em um cenário visual e intuitivo.

A simulação permite demonstrar:

* Integridade dos dados
* Confidencialidade
* Auditabilidade
* Ponto único de falha
* Ataques Man-in-the-Middle
* Centralização de confiança
* Necessidade de mecanismos de verificação distribuída

O caso da Rainha da Primavera tornou-se um estudo de caso prático para explicar como sistemas aparentemente seguros podem apresentar vulnerabilidades quando a confiança está concentrada em um único componente da arquitetura.

Esse texto já está em um formato adequado para ser utilizado como seção principal do trabalho, relatório de desenvolvimento ou capítulo de documentação do projeto.
