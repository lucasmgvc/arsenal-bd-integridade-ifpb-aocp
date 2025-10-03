# 📊 ARSENAL RESUMIDO 80/20 - INTEGRIDADE DE DADOS EM BD

**Versão:** Condensada 80/20 (20% do conteúdo, 80% dos resultados)
**Tópico:** Integridade de Dados em Banco de Dados
**Banca:** AOCP | **Concurso:** IFPB 2025
**Tempo de estudo:** 30 minutos | **Revisão:** 10 minutos

---

## 🎯 PRIORIDADE: MÁXIMA (Estude PRIMEIRO em BD)

**Por quê:** Base de 80% dos outros tópicos de BD (SQL, ER, Normalização). Alta frequência (20% direto + 60% indireto). ROI excelente (90 min → domina fundação de BD).

---

## 🧠 OS 7 CONCEITOS ESSENCIAIS (80% das questões)

### 1️⃣ PRIMARY KEY (PK)
- **O que é:** Identifica UNIQUAMENTE cada linha (identidade da entidade)
- **Regras:** 
  - ✅ Única (não duplica)
  - ✅ NOT NULL (implícito, automático)
  - ✅ 1 por tabela (pode ser composta: PK(col1, col2))
  - ✅ Cria índice único automático
- **Pegadinha AOCP:** PK permite NULL? **NÃO, NUNCA**
- **SQL:** `id INT PRIMARY KEY` ou `PRIMARY KEY (id)`

### 2️⃣ FOREIGN KEY (FK)
- **O que é:** Referencia PK de outra tabela (implementa relacionamento)
- **Regras:**
  - ✅ Permite NULL se sem NOT NULL (relacionamento opcional)
  - ✅ Valor deve existir na tabela pai OU ser NULL
  - ✅ N por tabela
- **Ações referenciais:** (DECORAR!)
  - **CASCADE:** Deleta pai → deleta filhos automaticamente
  - **RESTRICT:** Deleta pai → ERRO se houver filhos
  - **SET NULL:** Deleta pai → FK dos filhos vira NULL
- **Pegadinha AOCP:** FK NULL viola integridade? **NÃO** (é válido)
- **SQL:** `FOREIGN KEY (id_cliente) REFERENCES Cliente(id) ON DELETE CASCADE`

### 3️⃣ UNIQUE
- **O que é:** Garante unicidade (não duplica)
- **Diferenças de PK:**
  - ⚠️ Permite NULL (pode ter vários NULLs - depende do SGBD)
  - ⚠️ N por tabela (PK é só 1)
  - ⚠️ Não é "identidade" (é só restrição)
- **Pegadinha AOCP:** UNIQUE = PK? **NÃO** (PK é UNIQUE + NOT NULL + identidade)
- **SQL:** `email VARCHAR(100) UNIQUE`

### 4️⃣ CHECK
- **O que é:** Valida expressão booleana (regras simples)
- **Exemplos:** `CHECK (idade >= 18)`, `CHECK (preco > 0)`
- **Limitações CRÍTICAS:**
  - ❌ NÃO pode subquery
  - ❌ NÃO pode referenciar outras tabelas
  - ❌ Só valida linha atual
- **Para regras complexas:** Use TRIGGER
- **Pegadinha AOCP:** CHECK com subquery funciona? **NÃO**
- **Pegadinha versão:** MySQL < 8.0.16 aceita sintaxe mas **IGNORA** (não valida)
- **SQL:** `CHECK (data_fim > data_inicio)`

### 5️⃣ NOT NULL
- **O que é:** Proíbe valores nulos
- **Diferença de PK:** NOT NULL é constraint isolada; PK já inclui NOT NULL
- **Diferença de NULL:** NULL ≠ string vazia (''), NULL ≠ zero (0)
- **SQL:** `nome VARCHAR(100) NOT NULL`

### 6️⃣ DEFAULT
- **O que é:** Preenche valor automático se omitido no INSERT
- **NÃO É CONSTRAINT:** Não valida dados (só preenche)
- **Pegadinha AOCP:** DEFAULT valida valores? **NÃO** (só preenche)
- **SQL:** `status VARCHAR(20) DEFAULT 'ATIVO'`

### 7️⃣ Os 4 Tipos de Integridade
- **Entidade:** PK única e não-nula (identidade)
- **Referencial:** FK consistente (relacionamentos válidos)
- **Domínio:** Valores válidos (tipos, CHECK, NOT NULL)
- **Semântica:** Regras de negócio (TRIGGER)

---

## 🎵 MNEMÔNICOS ESSENCIAIS (DECORAR!)

### "ERED" - 4 Tipos de Integridade
- **E**ntidade (PK)
- **R**eferencial (FK)
- **E** = "e também"
- **D**omínio (CHECK/NOT NULL/tipos)

### "CaRe SeN De" - 5 Ações Referenciais
- **Ca**scade (propaga deleção)
- **Re**strict (rejeita se houver filhos)
- **Se**t **N**ull (FK vira NULL)
- **De**fault (FK vira DEFAULT)

**Frase:** "Carla Reclamou: Sempre Nulo ou Default!"

### "PC FUN" - 5 Constraints SQL
- **P**rimary, **C**heck, **F**oreign, **U**nique, **N**ot null

---

## ⚠️ TOP 10 ARMADILHAS AOCP

1. PK permite NULL? ❌ NÃO, NUNCA!
2. FK NULL viola integridade? ❌ NÃO (é válido)
3. CHECK pode subquery? ❌ NÃO
4. UNIQUE = PK? ❌ NÃO
5. DEFAULT valida? ❌ NÃO (só preenche)
6. MySQL CHECK sempre funciona? ❌ Depende (< 8.0.16 ignora)
7. CASCADE sempre deleta? ✅ SIM (mas pode falhar)
8. FK sem NOT NULL = obrigatório? ❌ NÃO (é opcional)
9. Integridade referencial = PK única? ❌ NÃO (é FK consistente)
10. RESTRICT = SET NULL? ❌ NÃO (rejeita vs atribui NULL)

---

## 📊 TABELA COMPARATIVA

```
╔═══════════╦════════╦════════╦══════════╗
║           ║   PK   ║ UNIQUE ║    FK    ║
╠═══════════╬════════╬════════╬══════════╣
║ NULL?     ║  NUNCA ║  SIM*  ║  SIM*    ║
║ Quantidade║   1    ║   N    ║    N     ║
║ Índice?   ║  AUTO  ║  AUTO  ║ Manual** ║
╚═══════════╩════════╩════════╩══════════╝
*se não tiver NOT NULL
**MySQL auto, PostgreSQL manual
```

---

## 📅 CRONOGRAMA 80/20

**DIA 0 (HOJE):** 30 min
- Ler resumo: 15 min
- Decorar mnemônicos: 5 min
- Fazer 10 questões: 10 min

**DIA 1:** 10 min - Revisar mnemônicos + tabela

**DIA 3-4:** 10 min - Testar recall

**1 SEMANA ANTES:** 5 min - Revisar mnemônicos + armadilhas

---

## 🎯 CHECKLIST PRÉ-PROVA

- [ ] PK vs UNIQUE vs FK (diferenças)
- [ ] CASCADE vs RESTRICT
- [ ] CHECK não faz subquery
- [ ] FK NULL é válido
- [ ] MySQL < 8.0.16 ignora CHECK
- [ ] Mnemônico "CaRe SeN De"
- [ ] Mnemônico "ERED"

**7/7 = Pronto!** 🚀