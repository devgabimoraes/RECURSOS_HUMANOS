# **RECURSOS_HUMANOS**
Repositório para desenvolvimento de projeto como trabalho em grupo do curso TDS.

## Criação de Tabelas
Alimentando as tabelas com as informações que cada uma carregará 

## Resumo
Este trabalho consiste na construção de uma base de dados em SQL e sua implementação, capaz de armazenar informações de uma determinada empresa e/ou organização. Nesse caso, nosso grupo optou por construir uma base de dados para uma empresa fictícia de Recursos Humanos. Foram desenvolvidas tabelas para sustentar essa base de dados, inseridos dados fictícios e realizado consultas, conforme exercício simulado para gerar um modelo relacional como resultado deste projeto.


## Autores

* Bruna Leite
* Tatiane Medeiros
* Gabriela de Moraes



# **Diagrama Entidade-Relacionamento — Next People**

```mermaid
graph TD

    %% =========================
    %% EMPRESA
    %% =========================

    EMPRESA["EMPRESA<br/><br/>
    🔑 id_empresa INT<br/>
    nome_empresa VARCHAR(50)<br/>
    nif INT<br/>
    email VARCHAR(50)<br/>
    telefone VARCHAR(50)<br/>
    morada VARCHAR(100)<br/>
    website VARCHAR(100)
    "]

    %% =========================
    %% RECRUTADOR
    %% =========================

    RECRUTADOR["RECRUTADOR<br/><br/>
    🔑 id_recrutador INT<br/>
    nome_recrutador VARCHAR(50)<br/>
    email VARCHAR(50)<br/>
    telefone VARCHAR(50)<br/>
    🔗 id_empresa INT
    "]

    %% =========================
    %% LOCALIZAÇÃO
    %% =========================

    LOCALIZACAO["LOCALIZACAO<br/><br/>
    🔑 id_localizacao INT<br/>
    cidade VARCHAR(50)<br/>
    distrito VARCHAR(50)<br/>
    pais VARCHAR(50)
    "]

    %% =========================
    %% VAGA
    %% =========================

    VAGA["VAGA<br/><br/>
    🔑 id_vaga INT<br/>
    titulo VARCHAR(50)<br/>
    descricao VARCHAR(200)<br/>
    data_publicacao DATE<br/>
    data_limite DATE<br/>
    salario_min DECIMAL(10,2)<br/>
    salario_max DECIMAL(10,2)<br/>
    tipo_contrato VARCHAR(50)<br/>
    🔗 id_empresa INT<br/>
    🔗 id_recrutador INT<br/>
    🔗 id_localizacao INT
    "]

    %% =========================
    %% CANDIDATO
    %% =========================

    CANDIDATO["CANDIDATO<br/><br/>
    🔑 id_candidato INT<br/>
    nome_candidato VARCHAR(50)<br/>
    email VARCHAR(50)<br/>
    telefone VARCHAR(50)<br/>
    data_nascimento DATE<br/>
    data_registro DATE<br/>
    morada VARCHAR(100)
    "]

    %% =========================
    %% ESTADO CANDIDATURA
    %% =========================

    ESTADO["ESTADO_CANDIDATURA<br/><br/>
    🔑 id_estado INT<br/>
    descricao VARCHAR(50)
    "]

    %% =========================
    %% CANDIDATURA
    %% =========================

    CANDIDATURA["CANDIDATURA<br/><br/>
    🔑 id_candidatura INT<br/>
    data_candidatura DATE<br/>
    salario_pretendido DECIMAL(10,2)<br/>
    carta_apresentacao VARCHAR(500)<br/>
    🔗 id_candidato INT<br/>
    🔗 id_vaga INT<br/>
    🔗 id_estado INT
    "]

    %% =========================
    %% ENTREVISTA
    %% =========================

    ENTREVISTA["ENTREVISTA<br/><br/>
    🔑 id_entrevista INT<br/>
    data_entrevista DATE<br/>
    tipo VARCHAR(50)<br/>
    observacoes VARCHAR(50)<br/>
    avaliacao INT<br/>
    🔗 id_candidatura INT
    "]

    %% =========================
    %% QUALIFICAÇÃO
    %% =========================

    QUALIFICACAO["QUALIFICACAO<br/><br/>
    🔑 id_qualificacao INT<br/>
    nome_qualificacao VARCHAR(50)<br/>
    descricao VARCHAR(500)
    "]

    %% =========================
    %% CANDIDATO QUALIFICAÇÃO
    %% =========================

    CAND_QUAL["CANDIDATO_QUALIFICACAO<br/><br/>
    🔑 id_candidato_qualificacao INT<br/>
    🔗 id_candidato INT<br/>
    🔗 id_qualificacao INT<br/>
    nivel VARCHAR(50)
    "]

    %% =========================
    %% VAGA QUALIFICAÇÃO
    %% =========================

    VAGA_QUAL["VAGA_QUALIFICACAO<br/><br/>
    🔑 id_vaga_qualificacao INT<br/>
    🔗 id_vaga INT<br/>
    🔗 id_qualificacao INT<br/>
    nivel_minimo VARCHAR(50)
    "]

    %% =========================
    %% EXPERIÊNCIA
    %% =========================

    EXPERIENCIA["EXPERIENCIA_PROFISSIONAL<br/><br/>
    🔑 id_experiencia INT<br/>
    🔗 id_candidato INT<br/>
    empresa VARCHAR(50)<br/>
    data_inicio DATE<br/>
    data_fim DATE<br/>
    descricao VARCHAR(500)
    "]

    %% =========================
    %% FORMAÇÃO
    %% =========================

    FORMACAO["FORMACAO<br/><br/>
    🔑 id_formacao INT<br/>
    🔗 id_candidato INT<br/>
    instituicao VARCHAR(50)<br/>
    curso VARCHAR(50)<br/>
    grau INT<br/>
    data_inicio DATE<br/>
    data_fim DATE
    "]

    %% =========================
    %% HISTÓRICO
    %% =========================

    HISTORICO["HISTORICO_CANDIDATURA<br/><br/>
    🔑 id_historico INT<br/>
    🔗 id_candidatura INT<br/>
    🔗 id_estado INT<br/>
    data_alteracao DATE<br/>
    observacao VARCHAR(100)
    "]

    %% =========================
    %% RELACIONAMENTOS
    %% =========================

    EMPRESA -->|"1 : N"| RECRUTADOR
    EMPRESA -->|"1 : N"| VAGA

    RECRUTADOR -->|"1 : N"| VAGA
    LOCALIZACAO -->|"1 : N"| VAGA

    CANDIDATO -->|"1 : N"| CANDIDATURA
    VAGA -->|"1 : N"| CANDIDATURA
    ESTADO -->|"1 : N"| CANDIDATURA

    CANDIDATURA -->|"1 : N"| ENTREVISTA

    CANDIDATO -->|"1 : N"| CAND_QUAL
    QUALIFICACAO -->|"1 : N"| CAND_QUAL

    VAGA -->|"1 : N"| VAGA_QUAL
    QUALIFICACAO -->|"1 : N"| VAGA_QUAL

    CANDIDATO -->|"1 : N"| EXPERIENCIA
    CANDIDATO -->|"1 : N"| FORMACAO

    CANDIDATURA -->|"1 : N"| HISTORICO
    ESTADO -->|"1 : N"| HISTORICO

    %% =========================
    %% CORES
    %% =========================

    classDef principal fill:#2563EB,color:#FFFFFF,stroke:#1E3A8A,stroke-width:2px;
    classDef apoio fill:#16A34A,color:#FFFFFF,stroke:#166534,stroke-width:2px;
    classDef associativa fill:#F59E0B,color:#FFFFFF,stroke:#92400E,stroke-width:2px;
    classDef processo fill:#9333EA,color:#FFFFFF,stroke:#581C87,stroke-width:2px;

    class EMPRESA,CANDIDATO,VAGA principal;
    class RECRUTADOR,LOCALIZACAO,ESTADO,QUALIFICACAO apoio;
    class CAND_QUAL,VAGA_QUAL associativa;
    class CANDIDATURA,ENTREVISTA,EXPERIENCIA,FORMACAO,HISTORICO processo;
```
