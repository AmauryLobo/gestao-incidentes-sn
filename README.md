# 🔔 Gestão de Incidentes — ServiceNow

Solução desenvolvida no ServiceNow para registrar, priorizar automaticamente e acompanhar incidentes de TI, aplicando conceitos reais de ITSM — com SLA configurado por prioridade, automação de fluxo e notificações dinâmicas.

Projeto desenvolvido como parte do portfólio prático de ServiceNow, em escopo customizado com versionamento via Source Control.

---

## 🛠️ Tecnologias utilizadas

- **ServiceNow App Engine Studio**
- **Flow Designer**
- **Service Catalog (Record Producer)**
- **Business Rules**
- **Catalog UI Policies**
- **SLA Definitions**
- **Source Control (GitHub)**

---

## 📋 O que foi construído

### INC0001 — Tabela e Formulário
Criação da tabela customizada `x_1319177_gest_o_0_incidentes_ocorridos` com todos os campos necessários: número, solicitante, e-mail, categoria, sub-categoria, impacto, urgência, prioridade, status, descrição, resolução, data de abertura, data de resolução e atribuído a.

O campo **Atribuído a** foi configurado como Reference para `sys_user`, conectando diretamente ao usuário do sistema — seguindo a boa prática de ambientes reais.

### INC0002 — Item de Catálogo no Portal
Publicação de um **Record Producer** no Service Catalog para abertura de incidentes pelo portal. O formulário foi organizado em containers por seção (dados do usuário e dados do incidente) com campos obrigatórios configurados via Catalog UI Policy.

### INC0003 — Cálculo Automático de Prioridade
**Business Rule Before** que calcula a prioridade automaticamente com base na combinação de impacto e urgência, seguindo a matriz ITSM:

| Impacto \ Urgência | Alta | Média | Baixa |
|---|---|---|---|
| **Alto** | Crítica | Alta | Média |
| **Médio** | Alta | Média | Baixa |
| **Baixo** | Baixa | Baixa | Baixa |

A mesma Business Rule define o status inicial como **Aberto** e preenche o número do protocolo automaticamente.

### INC0004 — SLA por Prioridade
Quatro SLA Definitions configuradas com prazo de resolução por prioridade, com schedule em horário comercial (8-5 weekdays):

| Prioridade | Prazo |
|---|---|
| Crítica | 1 hora |
| Alta | 4 horas |
| Média | 8 horas |
| Baixa | 24 horas |

### INC0005 — Fluxo de Notificações
Fluxo criado no **Flow Designer** disparado na criação de cada incidente. Envia e-mail de confirmação em HTML dinâmico para o solicitante com número de protocolo, status, prioridade, categoria e descrição preenchidos automaticamente.

### INC0006 — Lista de Acompanhamento
Lista customizada para o time de TI acompanhar todos os incidentes com os campos mais relevantes visíveis: número, solicitante, categoria, prioridade, status e data de abertura.

---

## 💡 Decisões técnicas

**Matriz de prioridade via Business Rule**
A prioridade não é preenchida pelo usuário — é calculada automaticamente cruzando impacto e urgência. Isso garante consistência nos dados e elimina subjetividade no preenchimento.

**Record Producer em vez de Standard Catalog Item**
O Record Producer gera registros diretamente na tabela customizada de incidentes, mantendo a solução organizada em escopo próprio e separada das tabelas nativas do ServiceNow.

**Catalog UI Policy para obrigatoriedade**
A obrigatoriedade dos campos foi configurada via Catalog UI Policy em vez do Dictionary Entry — mais flexível e não afeta outros contextos da tabela fora do portal.

**Campo condicional para subcategoria**
UI Policy condicional que exibe um campo adicional quando o usuário seleciona "Outro" — melhorando a experiência sem poluir o formulário com campos desnecessários.

**Atribuído a como Reference**
O campo foi configurado como Reference para `sys_user` em vez de String simples — permite vincular o incidente a um usuário real do sistema, habilitando notificações e filtros por atribuído.

**Escopo customizado com Source Control**
A aplicação foi desenvolvida em escopo próprio e versionada via Source Control, seguindo a boa prática de isolamento de customizações em ambientes reais de produção.

---

## 📸 Demonstração

### Portal — Abertura de Incidente
<img width="1365" height="688" alt="image" src="https://github.com/user-attachments/assets/a279abec-d81c-493b-9b8b-97904837be5a" />


### Lista de Acompanhamento
<img width="1365" height="216" alt="image" src="https://github.com/user-attachments/assets/36c04e9a-03ae-4e86-b8e8-8cf032a84257" />

### E-mail de Confirmação
<img width="370" height="390" alt="image" src="https://github.com/user-attachments/assets/50207f4c-7fbe-4742-8678-48d21a1a75ac" />


---

## 🔗 Links

- [Projeto anterior — Solicitação de Materiais](https://github.com/AmauryLobo/sn-solicitacao-materiais)
- [LinkedIn](https://www.linkedin.com/in/amaury-lobo-4b8988304/)

---

## 👨‍💻 Autor

**Amaury Lobo**
Estudante de Engenharia de Software | ServiceNow Developer
[LinkedIn](https://www.linkedin.com/in/amaury-lobo-4b8988304/) · [GitHub](https://github.com/AmauryLobo)
