Projeto Detran
=================
Plano de Gerenciamento de Configuração
======================================
Versão 1.0
------------------


Histórico de Versões
--------------------

|Data                |Versão       |Descrição               |Autor          |
|--------------------|-------------|------------------------|---------------|
|25/11/2013|1.0|Versão inicial|Luis Renné|
|26/11/2013|1.1|Seção 1 finalizada|Luis Renné|
|07/12/2013|1.1|Seção 3 finalizada|Elias de Oliveira|
|08/12/2013|1.0|Seção 4 finalizada|Elias de Oliveira|
|07/12/2013|1.3|Seção 5 finalizada|Marcos Portela|
|08/12/2013|1.4|Seção 6 finalizada|Marcos Portela|  



1. Introdução
==============

1.1 Finalidade
---------------	
Este documento tem como finalidade definir padrões, procedimentos, atividades e seus responsáveis, bem como os itens de configuração a serem controlados e as ferramentas a serem utilizadas no gerenciamento de configuração. 



1.2 Escopo
----------
Este documento se aplica ao projeto Detran e afeta os itens de configuração gerados
pela equipe do projeto, tais como os requisitos, casos de uso, diagramas, arquivos de código-fonte, modelos de dados, casos de teste e manuais.



1.3 Definições, Acrônimos e Abreviações
---------------------------------------
|Termo               |Descrição    |
|--------------------|-------------|
|Baseline|Conjunto de itens de configuração em um determinado momento do processo de  desenvolvimento|
|GC|Gerente de configuração|
|BD|Banco de dados|
|CM|Controle de mudanças|
|GCS|Gestão de configuração de software|
|SCM|Sistema de controle de mudanças|
|CM|Gerenciamento de Configuração|
|Release| Uma versão distribuída ao cliente|
|Repositório|Local onde serão armazenados os itens de configuração|
|SM|Solicitação de mudanças|
|CCB|Comitê de Controle da Configuração|



1.4 Referências
---------------
Não se aplica.



1.5 Visão Geral
---------------
Este documento está organizado em seções. A seção 1 oferece uma visão geral de todo o documento. Ela inclui a finalidade, o escopo, as definições, os acrônimos, as abreviações, as referências e uma visão geral deste Plano de Gerenciamento de Configuração.<p>

A seção 2 descreve quem será o responsável pela execução das diversas atividades de CM, as ferramentas e os procedimentos necessários para o controle de versão dos itens de configuração gerados no ciclo de vida do projeto.

A seção 3  descreve como os itens de configuração devem ser identificados, as Baselines do projeto,a estrutura do repositório e a organização dos itens dentro do repositório.

A seção 4 define os padrões e procedimentos que devem ser seguidos no projeto.

A seção 5 descreve as ferramentas de software, o pessoal e o treinamento necessários para implementar as atividades de CM especificadas.

A seção 6 descreve o cronograma das auditorias de configuração e o que será verificado. Também informa como serão reportados os problemas encontrados e como será feito o acompanhamento das correções.



2. Gerenciamento de Configuração de Software
============================================

2.1 Organização, Responsabilidades e Interfaces
------------------------------------------------

|Papéis              |Equipe       |Responsabilidade        |
|------ |----------------------------|-----------------------------|
|Gerente de Configuração|- Marcos Portela|Escrever o plano de Gerencia de Configuração<br>Configurar ambiente de gerência de configuração<br>Criar Baselines|
|CCB| - Luís Renné<br> - Elias de Oliveira|Definir os processos de controle de mudanças<br>Aprovar ou rejeitar solicitações de mudanças|
|Desenvolvedor|- Marcos Portela<br>- Luís Renné<br>- Elias de Oliveira|Seguir os padrões e procedimentos definidos no plano de gerência de configuração|





2.2 Ferramentas, Ambiente e Infra-estrutura
-------------------------------------------
 
### 2.2.1 Ferramentas
|Nome|Descrição|Versão|Licença|
|----|---------|------|-------|
|Git|Controle de versão distribuído|1.8.5.1|Free|
|EGit|Plugin para integrar o Eclipse ao Git|3.1.0|Free|
|GitHub|Serviço de hospedagem de repositório Git (privado)|...|$ 7,00 / mês|
|Jira|Ferramenta de controle de mudanças|6.1.4|$ 10,00 / mês|
|PostgreSQL|Servidor de Banco de Dados|9.3|Free|
|pgAdmin|Client PostgreSQL|1.18.1|Free|
|Eclipse|IDE para desenvolvimento Java|4.3.0|Free|
|Java JDK| Kit de desenvolvimento Java|1.7|Free|
|Linux Debian| Sistema Operacional|7.0 |Free|
|Ubuntu|Sistema Operacional|13.10|Free|
|JBoss AS|Servidor de aplicações JEE|7.1.1|Free|
|Libre Office|Suite de escritório|4.1.3|Free|


### 2.2.2 Ambiente e Infra-estrutura

#### Banco de Dados
O banco de dados utilizado no  projeto é PostgresSQL. Serão definidos três bancos de dados: Desenvolvimento, Homologação e Produção. Banco de Desenvolvimento é o banco utilizado pelos desenvovledores nas atividades de desenvolvimento ou testes. Banco de Homologação é o banco utilizado pelas versões do sistema a serem homologadas pelo cliente. Banco de Produção
é o banco utilizado pelas versões definitivas disponibilizadas ao cliente. Os bancos de dados estarão configurados da seguinte maneira:


|Banco de desenvolvimento|                   |
|------------------------|-------------------|
|IP|192.168.1.5|
|Porta|5432|
|Nome do banco| detran_desen |
|Sistema Operacional|Linux Debian|
|Hardware| Processador Intel® Core i5 2.8 GHz, 4GB RAM, 500 HD|
 
|Banco de Homologação|              |
|--------------------|--------------|
|IP|192.168.1.6|
|Porta|5432|
|Nome do banco|detran_homolog|
|Sistema Operacional|Linux Debian|
|Hardware| Processador Intel® Core i5 2.8 GHz, 4GB RAM, 500 HD|

|Banco de Produção|              |
|-----------------|--------------|
|IP|192.168.1.7|
|Porta|5432|
|Nome do banco|detran_prod |
|Sistema Operacional|Linux Debian|
|Hardware| Processador Intel® Xeon® Quad-Core 3.10GHz, 8GB RAM, 500 HD.|



#### Controle de Versão
A ferramenta de controle de versão utilizada no projeto será o GIT, uma ferramenta de controle de versão distribuído. Também será usado o serviço GitHub para hospedar o repositório remoto do projeto. Este repositório deverá ser privado. O custo com o serviço de hospedagem do repositório é de $7.00 por mês. Os desenvolvedores da equipe deverão criar um repositório local que deverá ser um "_clone_" do repositório remoto em sua estação de desenvolvimento.


|Repositorio Remoto |                                        |      
|-------------------|----------------------------------------|
|Endereço           | https://github.com/detran/projetodetran|



####Controle de Mudanças
Para controle de mudanças, será utilizado no projeto a ferramenta Jira. Todos os membros da equipe do projeto deverão ter um usuário para acesso, assim como os clientes que irão solicitar as mudanças. 


|Servidor Jira      ||
|----------|--------------|
|IP|192.168.1.8|
|Porta|8080|
|Endereço|http://102.168.1.8:8080/secure/Dashboard.jspa|
|Sistema Operacional|Linux Debian|
|Hardware| Processador Intel® Core i5 2.8 GHz, 4GB RAM, 500 HD|

#### Servidores de Aplicação 
O servidor de aplicação utilizado pelo projeto será o JBoss. Serão disponiblizados dois servidores de aplicação, Homologação, no qual serão implantadas as versões a serem homologadas pelo cliente, e Produção, onde serão implantadas as versões finais a serem disponibilizadas ao  cliente. Os desenvolvedores também terão um servidor JBoss rodando localmente em suas estações de desenvolvimento. 

|Servidor JBoss de Homologação|              |
|-----------------------------|--------------|
|IP|192.168.1.9|
|Porta|8080|
|Sistema Operacional|Linux Debian|
|Hardware| Processador Intel® Core i5 2.8 GHz, 4GB RAM, 500 HD|

|Servidor JBoss de Produção|              |
|--------------------------|--------------|
|IP|192.168.1.10|
|Porta|8080|
|Sistema Operacional|Linux Debian|
|Hardware| Processador Intel® Xeon® Quad-Core 3.10GHz, 8GB RAM, 500 HD.|




#### Configuração da Área de Trabalho
A edição de código-fonte será feita através da IDE Eclipse. A documentação do projeto deverá ser feita utilizando a ferramenta LibreOffice salvando no formato ODF (Open Document Format). As estações de trabalho de desenvolvimento deverão ter as seguintes configurações:

|Área de Trabalho||
|--------------------|-----------|
|Sistema Operacional|Linux Ubuntu|
|Hardware | Processador Intel® Core i7 3.4GHz, 8GB RAM, 500 HD|
|Softwares| Git, Eclipse + EGit, pgAdmin, Java JDK, JBoss, Libre Office     | 

3. O Programa de Gerenciamento de Configuração
==============================================

3.1 Identificação da Configuração
---------------------------------
### 3.1.1 Métodos de Identificação
----------------------------------

Todos os produtos gerados durante o ciclo de vida do projeto são _Itens de Configuração \(ICs\). Os Itens de Configuração do projeto deverão ser identificados por rótulos contendo sufixos que identificam o projeto, a data de entrega do mesmo, a fase do ciclo de vida do projeto e o número da versão do IC. Com a finalidade de facilitar a identificação e localização dos Itens de Configurações utiliza-se o código único de identificação no formato **[SIGLA DO PROJETO]-[NOME DO DOCUMENTO]-[DATA]-VERSÃO**.

Exemplo: **DETRAN-SCM-PLANO-20131201-1.00**, representando a versão 1.00 do Documento de Visão do projeto DETRAN entregue ao _CCB_ em 01/12/2013 na fase de Elicitação de Requisitos. A versão 2 deste artefato seria armazenado com o identificador **DETRAN-SCM-PLANO-20131215-2.00-R1**.

_Aplicar os Padrões e Procedimentos especificados na Seção 4._

### 3.1.2 Itens de Configuração

No processo serão controlados os seguintes _Itens de Configurações_.

#### Artefatos Técnicos

* Documentação técnica \(Requisitos Funcionais e Especificações\).
* Banco de Dados e arquivos de dados.
* Configuração de hardware \(Servidores\).
* Componentes de Redes.
* Itens de Configurações de Software.
* Itens de Rede.

#### Artefatos Gerenciais

* Plano do Projeto de Software.
* Estrutura Analítica do Trabalho.
* Documentos de Orçamentos e Cronograma.
* Requisitos de relatórios.
* Relatório de Acompanhamento de Projeto.

#### Artefatos do gerencimanto de mudanças

* Planilha de Acompanhamento de Mudanças.
* Formulário de Solicitação de Mudança.
* Relatório de Controle de Mudança.

_Um item de configuração é um conjunto de itens de hardware e/ou software vistos como uma entidade única para fins de gerência de configuração. Um item de configuração está sujeito a mudanças e essas devem obedecer às políticas estabelecidas. Normalmente, um item de configuração é estabelecido para cada pedaço de software que pode ser projetado, implementado e testado de forma independente. Documentos e massas de dados, entretanto, também são passíveis de configuração e também podem ser considerados itens de configuração._

### 3.1.3 Baselines do Projeto

A _Baseline_ pode ser vista como uma _foto da versão_ de todos os itens de configuração utilizados em uma aplicação, desde os aspectos de _harware_ como os de _software_, devendo ser alterado pelo processo de gerenciamento de mudanças.

#### Promoção de Baseline

É o evento pelo qual uma baseline muda de estado, como resultado de sua aprovação em um determinado ponto de controle. _Baselines intermediárias_ podem ou não ser submetidas a teste. _Baselines em final de iteração e final de fase devem ser submetidas a teste_. As que forem candidatas a entrar em produção deverão ser submetidas a teste e homologação. _Os estados sugeridos:_ **inicial, desenvolvida, testada, homologada e implantada**.

#### Criação de Baselines de Documentação

As baselines deverão ser geradas de acordo com a definição abaixo:

| Baseline | Composição | Em que momento é gerada |
|----------|------------|-------------------------|
| Baseline de Planejamento | Cronograma, Data Planejada de Início do Projeto, Data Planejada de Término do Projeto, Percentual Concluído, Duração Planejada, Duração Real, Esforço Planejado, Esforço Real, Custo Planejado e Custo Real. | Após aprovação do Plano de Projeto ou Após planejamento de iteração. |
| Baseline de Artefatos | Documento de Visão, Declaração de Escopo e Especificação Casos de Uso. | A cada Homologação de artefato pelo Cliente. Desta forma, pode ser criada uma baseline para cada artefato homologado ou para um conjunto de artefatos homologados. |
| Baseline de Mudança | Quaisquer itens que componham baseline e que precisem ser alterados.Os itens de configuração que compõem Baseline somente poderão ser alterados mediante uma _Solicitação de Mudança Aprovada_ na _Ferramenta de Gestão de Projetos_. | A cada alteração de itens de baseline. |
| Build Externo | Códigos Fonte | Nas entregas de pacotes para o cliente. |

### 3.1.4 Estrutura do Repositório de Versões

Os projetos deverão seguir a seguinte estrutura de pastas no repositório:

_Exemplo:_ **SIGLA DO CLIENTE\>SIGLA DO PROJETO\>DIRETÓRIO\>SUBDIRETÓRIO\(ARTEFATOS\)**

| Diretório | Subdiretório | Artefatos |
|-----------|--------------|-----------|
| Documentos | Gerência de Configuração | Modelo do Plano de Gerenciamento de configuração, Relatório de Acompanhamento de Projeto, Notas de Releases e Arquivos de aprovação dos documentos. |
| Documentos | Gerência de Projetos | Documento de Visão, Termo de Abertura, Plano de Projeto, Cronograma, Relatório de Status, Atas de Reuniões e Arquivos de aprovação dos documentos. |
| Documentos | Requisitos | Especificação de Caso de Uso, Modelo de Caso de Uso, Glossário e Arquivos de aprovação dos documentos. |
| Documentos | Analise e Projeto | Manual de Implantação, Documento de Arquitetura, Modelo de Banco de Dados, Modelo de Análise e Projetos e Arquivos de aprovação dos documentos. |
| Documentos | Gerência de Mudança | Planilha de Acompanhamento de Mudanças, Formulário de Solicitação de Mudança, Relatório de Controle de Mudança e Arquivos de aprovação dos documentos |
| Aplicação | ... | Códigos Fonte |

Caso exista algum projeto onde a estrutura de pastas não atenda, será gerada uma adaptação e esta deverá ser descrita no _Plano de Projeto_.

A responsabilidade de operacionalizar esses procedimentos ficará a cargo do _Analista de Gestão de Configuração_.

3.2 Controle de Configuração e Mudança
--------------------------------------

### 3.2.1 Processamento e Aprovação de Solicitações de Mudança

Para o projeto deverá ser selecionado o _Gerente de Projeto_ para facilitar e acompanhar a execução do _Processo e Aprovação de Solicitação de Mudança_.

A detecção de necessidades de mudanças e formalização das solicitações das mudanças da _Baseline_ serão realizadas pelos membros da equipe do projeto autorizado a solicitar através da ferramenta _Issue_ disponibilizada pelo GitHub através do endereço do repositório do _projeto_ e submete o mesmo ao _Comitê de Controle de Mudanças_ na qual terá o seguinte fluxo.

![Fluxo de Solicitações de Mudanças](https://raw.github.com/marcosnasp/trab-gcs-fa7-turma7/branch-elias/trabalho/FluxoStatusMudanca.png)

**_Tabela de Status do Issues_**

Os possíveis status das mudanças estão especificado na tabela abaixo.

| Atividade | Descrição |
|-----------|-----------|
| Aberto | Solicitação de mudança aberto mas ainda não foi aprovado. |
| Em análise | Solicitação de mudança aguardando aprovação do _Comitê de Controle de Mudança_. |
| Analisado | Aguardando desenvolvimento. |
| Em desenvolvmento  Requisição de mudança aprovada e trabalho em andamento. |
| Desenvolvido | Mudança solicitada implementada e em revisão para entrar na fase de testes. |
| Em teste | Mudança solicitada em fase de testes. |
| Teste com erro | Solicitação aguardando finalização. |
| Finalizado | Mudança solicitada implementada, testada com atualizações realizadas. |
| Rejeitada | Requisição de mudança rejeitada pelo Comitê de Controle de Mudanças. |

#### Avaliação da requisição de mudança

O processo de avaliação de solicitações de mudanças devem seguir os seguintes passos:

* Avaliar se a mudança solicitada encontra-se dentro dos objetivos do projeto determinado no _Documento de Visão do Projeto_.
* Avaliar se a mudança necessita de _Estudo de Viabilidade_.
* Avaliar e quantificar o impacto da mudança em termos de escopo, cronograma, custos e qualidade.
* Avaliar os riscos associados à mudança.
* Avaliar se a mudança afeta outros projetos da empresa ou sistemas integrados.
* Avaliar impactos relacionados a empresa terceirizadas ou terceiras partes e en outros contratos existentes.
* Solicitar avaliação da mudança ao _time do projeto_.
* Avaliar junto ao Gerente de Projeto, impactos das mudanças relacionados a prazos, custos e recursos.

#### Aprovação ou rejeição da solicitação de mudança

Após a avaliação da solicitação de mudanças, o Comitê de Controle de Mudanças poderá aprovar, rejeitar ou requisitar maiores informações. A decisão normalmente se baseia nos riscos do projeto com ou sem implementação da mudança e no impacto desta implementação em termos de prazo, custos, riscos, recursos e qualidade. No caso de mudança ser _aprovada_, o Plano do Projeto deve ser atualizado e nova _Baseline_ deverá ser registrada relacionada a custo, cronograma e escopo. No caso da _rejeição_ a solicitação, deve ser enviada mensagem para o solicitante informando os motivos do não atendimento e o _status_ da solicitação sendo armazenado como _rejeitada_. Independente da decisão, a _Planilha de Acompanhamento de Mudanças_ deve ser atualizada.

### 3.2.2 Comitê de Controle de Mudança (CCB)

O Comitê de Controle de Mudança do projeto terá as seguintes responsabilidades:

* Manter o Plano de Gerenciamento de Configuração.
* Gerenciar Repositórios de Itens de Configuração do projeto.
* Identificar Itens de Configurações do projeto documentando suas características.
* Controlar e facilitar mudanças nas características dos Itens de Configuração.
* Receber e rever todos os Formulários de Manutenção de ICs \(inclusão, alteração e exclusão de IC\), verificando se informações adicionais são necessárias e enviando para o administrador técnico realizar pré-análise.
* Garantir que as ações sejam tomadas dentro dos prazos previstos, fornecendo sugestões relacionados e versionamento quando couber.
* Criar pacotes e versões de aplicações, realizando promoções quando solicitado.
* Reportar ao Gerente de Projeto _status_ de aprovações de todas as mudanças propostas e todas as mudanças aprovadas.
* Realizar auditorias para verificar ou inspeções por amostragem para verificar se o projeto está efetivamente seguindo o previsto no Plano de Gerenciamento de Configuração.

Além destas responsabilidades, o Comitê de Controle de Mudança é responsável pelo gerenciamento de todos os _Itens de Configuração das Baselines_ do projeto, incluindo software, hardware e documentação.

A tabela abaixo relaciona os papéis, responsabilidades e responsáveis definidos para o projeto.

| Papel | Responsabilidade | Responsável | E-mail |
|-------|------------------|-------------|--------|
| Responsável pelos documentos do projeto | Manter e atualizar os artefatos \( _Requisição de alteração na Baseline e Intens de Configuração, Plano de Projeto de Software, Plano de Gerenciamento de Configuração, Plano de Gerencimanto de Qualidade, Plano de Gerenciamento de Requisitos, Plano de Gerenciamento de Riscos, Glosário do Projeto, Especificação de Caso de Uso, Plano de testes, Planilha de Acompanhamento de Mudanças, Formulário de solicitação de mudança e Relatório de Controle de Mudança._\), mantidos no repositório de documentos do projeto. | Marcos Portela | marcos.portela@detran.com |
| Responsável pelos requisitos | Manter e atualizar o repositório de requisitos do projeto. | Elias de Oliveira | elias.oliveira@detran.com |
| Responsável pela configuração do software | Promover versões de software e fornecer componentes solicitados pela equipe de desenvolvimento. | ELias de Oliveira | elias.oliveira@detran.com |
| Administrador técnico do sistema | Manter e rastrear componentes do sistema \- Monitorar o desenvolvimento, garantindo integridade técnica e consistênca com os requisitos e arquitetura do sistema \- Rever solicitações de mudanças e auxiliar na avaliação para o CCB \- Verificar relatórios de problemas para resolver questões de prioridades. | Luis Renné | luis.renne@detran.com |

4. Padrões e Procedimentos
==========================

Nesta seção, serão apresentados os _padrões utilizados no projeto_ tais como, identificadores, nomes de arquivos, nomes de tags, nomes de branches, versionamento \(sistema, documentos e baselines\) e composição dos vários CCBs.

4.1 Identificadores
--------------------

São descritos nessa seção os identificadore a serem utilizados nos padrões de _nomeclatura_ do projeto.

### 4.1.1 Identificadores do Projeto

_Identificador\(es\) relacionado\(s\) ao projeto e seus produtos._

#### Fábrica de Software:

|Identificador |Descrição |
|--------------|----------|
|DETRAN|Identificador da Fábrica de Software|

#### Projeto\(s\):

|Identificador |Descrição |
|--------------|----------|
|APPANDROID|Identificador do Projeto|
|SITEINSTITUCIONAL|Identificador do Projeto|

### 4.1.2 Identificadores das Áreas de Processos

_Identificadores a serem usados nos nomes de artefatos de projeto._

|Identificador |Descrição |
|--------------|----------|
|SCM|Gerência de Configuração|
|SQA|Garantia da Qualidade|
|SPM|Gerência de Projeto|

### 4.1.3 Identificadores de Tipos de Artefatos

_Identificador\(es\) relacionado\(s\) aos tipos de artefatos._

#### Identificadores de artefatos de Desenvolvimento

|Identificador|Descrição |
|-------------|----------|
|ARQ|Documento de Arquitetura do Sistema|
|DOC|Documento não classificado|
|I18N|Tabela de Internacionalização|
|MAD|Modelo de Análise e Projeto|
|MAN|Manual|
|MBD|Esquema do Banco de Dados|
|MRT|Matriz de Ratreabilidade de Requisitos|
|REQ|Especificação de Requisitos de Software|
|TSTD|Projeto de Testes|
|TSTP|Plano de Testes|
|TSTR|Resultado de Testes|
|UCS|Especificação de Casos de Uso|

#### Identificadores de artefatos de Projeto

|Versão |Descrição |
|-------|----------|
|ATA|Atas|
|CHK|Checklist|
|CRO|Cronograma|
|EST|Documentos de Estimativas|
|FIN|Financeiro|
|PLAN|Planos|
|REL|Relatórios|

4.2 Nomenclatura de Labels/Tags
--------------------------------

As seções seguintes descrevem o padrão de nomenclatura de **TAGS**. Para todos eles, todos os caracteres devem utilizar **CAIXA ALTA**.

### 4.2.1 Aprovação de Documentos

_Regra:_

* **DETRAN-[NOME DO DOCUMENTO]-[DATA \(ANO MÊS DIA\)]-[VERSÃO]**

_Descrição:_

* **[NOME DO DOCUMENTO]:** É o nome do documento _sem_ sua extensão.
* **[DATA]:** Data da entrega do documento especificado pelo _ANO_, _MÊS_ e _DIA_.
* **[VERSÃO]:** Versão do documento.

<pre>
    Exemplo 01: DETRAN-SCM-PLANO-20131201-1.00
    Exemplo 02: DETRAN-SCM-PLANO-20131225-1.00
    Exemplo 02: DETRAN-SCM-PLANO-20131230-1.01
</pre>

_Uso:_ Aplicado somente em documentos em _versão estável_ a partir do momento da aprovação.

### 4.2.2 Baseline de Desenvolvimento

_Regra:_

* **DETRAN-[PROJETO]-DEV-[VERSÃO]**

_Descrição:_

* **DETRAN:** Identificador da Fábrica de Software.
* **[PROJETO]:** Identificador da área do projeto.
* **[VERSÃO]:** É a versão da baseline de desenvolvimento.

<pre>
    Exemplo 01: DETRAN-APPANDROID-DEV-001
    Exemplo 02: DETRAN-APPANDROID-DEV-017
</pre>

_Uso:_ Aplicado em todas as versões dos artefatos da baseline.

### 4.2.3 Release

_Regra:_

* **DETRAN-[PROJETO]-REL-[VERSÃO]**

_Descrição:_

* **[VERSÃO]:** é a versão do sistema, aplicação ou módulo que está sendo entregue.

<pre>
    Exemplo 01: DETRAN-APPANDROID-REL-1.00.00
    Exemplo 02: DETRAN-APPANDROID-REL-2.03.00
</pre>

_Uso:_ Aplicado em todos os artefatos entregues na baseline de desenvolvimento testada;

4.3 Nomenclatura de Branches
-----------------------------

As seções seguintes descrevem o padrão de nomenclatura de _branches_. Para todos eles, todos os caracteres devem utilizar **caixa baixa**.

### 4.3.1 Branches de Desenvolvimento

_Regra:_

* **dev\_[ID]\_[LOGIN]\_[PROJETO]\_[EXTRA]**

_Descrição:_

* **[ID]:** Ldentificador da atividade.
* **[LOGIN]:** Login do usuário responsável pela correção do release\(opcional\).
* **[PROJETO]:** Identificador do projeto.
* **[EXTRA]:** Campo adicional para alguma informação extra que ajude a identificar o branch \(opcional\). Se o branch for para correções de release, usar **_rel[VERSION]**. Se não, utilizar alguma informação relativa à correção sendo feita;

<pre>
    Exemplo 01: dev_123_faeliaso_appandroid_issue;
</pre>

### 4.3.2 Branches de Integração

_Regra:_

* **int\_[PROJETO]\_[EXTRA]**

_Descrição:_

* **[PROJETO]:** Identificador do projeto.
* **[EXTRA]:** Campo adicional para alguma informação extra que ajude a identificar o branch \(opcional\).

<pre>
    Exemplo 01: int_appandroid_integracaoxyz-001;
</pre>

4.4 Nomenclatura de Documento
------------------------------

Nesta seção serão apresentados os padrões de nomenclatura para os documentos.

### 4.4.1 Documentação do Projeto

_Regra:_

* **DETRAN-[PROJETO]-[AP]-[TIPO]-[EXTRA].[EXT]**

_Descrição:_

* **[PROJETO]:** Identificador do projeto.
* **[AP]:** Identificador da área do processo.
* **[TIPO]:** Identificador do tipo de documento.
* **[EXTRA]:** Campo para informações extra (opcional).
* **[EXT]:** Extensão do documento.

<pre>
    Exemplo 01: DETRAN-SCM-PLAN.doc;
</pre>

### 4.4.2 Documentação de Desenvolvimento

_Regra:_

* **DETRAN-[PROJETO]-[TIPO]-[EXTRA].[EXT]**

_Descrição:_

* **[PROJETO]:** Identificador do projeto.
* **[TIPO]:** Identificador do tipo de documento.
* **[EXTRA]:** Campo para informações extra (opcional).
* **[EXT]:** Extensão do documento.

<pre>
    Exemplo 01: DETRAN-APPANDROID-MAN-USER.doc;
</pre>

### 4.4.3 Aprovações Formais de Documentos

Esta seção mostra como nomear os arquivos de aprovação de documentos e o pacote
contendo todas as aprovações.

#### Aprovações Individuais

_Regra:_

* **DETRAN-[NOME DO DOC]-[VERSÃO]-[APROVADOR].txt**

_Descrição:_

* **[NOME DO DOC]:** Nome do documento.
* **[VERSÃO]:** Versão do documento.
* **[APROVADOR]:** Nome ou Login do aprovador do documento.

<pre>
    Exemplo 01: DETRAN-APPANDROID-REQ-01.00-MARCOS.txt;
    Exemplo 02: DETRAN-SCM-PLAN-01.00-FAELIASO.txt;
</pre>

#### Pacote de Aprovações Formais

_Regra:_

* **DETRAN-[NOME DO DOC].zip**

_Descrição:_

* **[NOME DO DOC]:** Nome do documento.

<pre>
    Exemplo 01: DETRAN-APPANDROID-REQ-aprovacoes.zip;
    Exemplo 02: DETRAN-SCM-PLAN.aprovacoes.zip;
</pre>

_Observações:_ Pacotes de aprovações devem conter todas as aprovações individuais.

4.5 Versionamento
------------------

As seções seguintes descrevem o padrão de versionamento dos artefatos.

### 4.5.1 Código – Versionamento dos Releases

_Esquema:_

* **[XX]-[YY]-[ZZ]-\(\[TIPO\]\[SEQ\]\)**

_Descrição:_

* **[XX]:** Versão do software a ser entregue ao cliente com modificações substanciais nos requisitos e/ou funcionalidades do sistema. Ele representa o número da iteração do release. Inicia-se este campo com o valor **"1"**.

* **[YY]:** Número a ser incrementado quando um release for produzido com uma nova funcionalidade incluída no sistema. Inicia-se este campo com o valor **"00"** e volta a este valor quando **[XX]** é alterado. Este campo só deve ser incrementado depois do primeiro release final.

* **[ZZ]:** Número a ser incrementado quando um novo release for produzido para correção de um release **[XX].[YY]**. Inicia-se este campo com o valor **"00"** e volta a este valor quando **[XX]** ou **[YY]** é alterado. Este campo só deve ser incrementado depois do primeiro release final.

* **[TIPO]:** Campo opcional que indica o tipo do release:

    <ul>
        <li>"d": para builds internos com o sistema em desenvolvimento. Pode ser utilizado para marcar algum checkpoint periódico ou para congelar o sistema para algum outro fim.</li>
        <li>"a": para releases alpha, um release para testes internos, possivelmente sem todos os requisitos planejados implementados e com erros.</li>
        <li>"b": para releases beta, um release completo, com todas as funcionalidades implementadas, pronto para testes do cliente e possivelmente com problemas. Poderão existir diversos releases beta até que os problemas detectados sejam insignificantes com baixa severidades ou seja, o critério de aceitação tenha sido alcançado.</li>
    </ul>

* **[SEQ]:** Campo opcional que indica a quantidade de releases/builds produzidos para um determinado tipo de release de uma versão **XX.YY.ZZ**.

|Versão|Descrição|
|------|---------|
|1.00.00|Baseline de release para a versão 1.00 do sistema.|
|1.00.00d2|Segunda baseline de release com o sistema ainda em desenvolvimento.|
|1.00.00a1|Primeira baseline de release para testes internos (alpha).|
|1.00.01|Baseline de release para correção de bugs na versão 1.00 do sistema e sem inclusões de novas funcionalidades.|
|2.00.00|Baseline de release com mudanças substanciais de funcionalidades do sistema.|

### 4.5.2 Documentos

_Esquema:_

* **[XX]-[YY]-\(\-R\[SEQ\]\)**

_Descrição:_

* **[XX]:** Indica alterações significativas no artefato ou seja, este campo deve ser incrementado a
cada nova aprovação de documento. Inicia-se em **"1"**.
* **[YY]:** Indica pequenas alterações no artefato. Inicia-se esse campo com "00" e quando [XX]
for incrementado, este número deverá voltar para "00".
* **\(\-R\[SEQ\]\):** Indica uma _versão rascunho_, ou seja, uma versão que ainda está sendo trabalhada e não deve ser considerada, pois sua estabilidade ainda não foi comprovadamente atestada.

_Logo que um item de configuração é criado, possui número de versão "1.00-R1"._

<pre>
    Exemplo 01: DETRAN-SCM-PLANO-20131201-1.00-R1
    Exemplo 02: DETRAN-SCM-PLANO-20131225-1.00
    Exemplo 02: DETRAN-SCM-PLANO-20131230-1.01-R1
</pre>

_Observações:_ As versões rascunho crescem conforme decisão do seu responsável.

### 4.5.3 Baselines

_Esquema:_

* **[SEQ]**

_Descrição:_

* **[SEQ]:** É um número sequencial incrementado a cada vez que uma solicitação de mudança (ou um conjunto delas) impacta em versões estáveis do artefato.

5. Treinamento e Recursos
=========================

5.1 Treinamento
---------------

### 5.1.1 Ferramenta GIT
Deve ser agendado um treinamento com pessoal especializado em controle de versão distruído, mais especificamente,
GIT. A programação do treinamento deve ser dirigida pelos seguintes pontos:
<ol>
<li>Conceitos de Controle de Versão distribuído</li>
<li>Comparações e diferenças relacionadas ao Controle Centralizado.</li>
<li>Visão Geral das Principais Ferramentas Disponíveis no Mercado.</li>
<li>Utilização através de um estudo dirigido para um caso específico abordando as principais funcionalidades do
cliente definido na seção de <b>recursos 5.2</b>.</li>
<li>Avaliação da absorção dos conteúdos apreendidos visando medir a eficácia do treinamento.
</ol> 

### 5.1.2 Ferramenta JIRA
Deve ser agendado um treinamento com pessoal especializado na Ferramenta de tracking (Controle de mudanças) JIRA. A 
programação do treinamento deve ser dirigida pelos seguintes pontos:
<ol>
<li>Conceitos de Controle de Mudanças e Ciclo de Vida</li>
<li>Necessidades de Engenharia.</li>
<li>Visão Geral das Principais Ferramentas concorrentes disponíveis no Mercado.</li>
<li>Utilização através de um estudo dirigido para um caso específico abordando as principais funcionalidades do
cliente definido na seção de <b>recursos 5.2</b>, ferramenta JIRA.</li>
<li>Avaliação da absorção dos conteúdos apreendidos visando medir a eficácia do treinamento.
</ol> 

5.2 Recursos
------------

Para o Gerenciamento de Configuração de Software no projeto DETRAN serão utilizadas as seguintes ferramentas:
<ol>
<li>Para realizar o Controle de versão será utilizado a ferramenta Open Source GIT-SCM, nas suas versões: Bash e GUI. Essa ferramenta possui suporte para diversos tipos de sistemas operacionais: Windows, Mac OS e Linux. E está disponível
em: http://git-scm.com/download. Mais informações sobre instalação em: http://git-scm.com/book/en/Getting-Started-Installing-Git.</li>
<li>EGit - Plugin do Eclipse para o Git.</li>
<li>Para realizar o Controle de Mudanças será utilizada a ferramenta JIRA da Atlassian.</li>
</ol>

6. Auditorias de Configuração
=============================

6.1 Auditorias e o Ciclo de Vida do Projeto
---------------------------------------------

<p>
As auditorias de configuração consistem na avaliação periódica das linhas de base do projeto definidas em pontos especiais do ciclo de vida do projeto:
<ol>
<li>Definição do projeto <i>(design)</i></li>
<li>Revisão do status do projeto <i>(design)</i></li>
<li>Finalização da Etapa de Implementação do Software</li>
<li>Entrega/Implantação do Software</li>
</ol>
</p>
<b>Fonte:</b> <i>MODELO PARA O GERENCIAMENTO DA CONFIGURAÇÃ E GERENCIAMENTO DA INFORMAÇÃO E DOCUMENTAÇÃO DO PROGRAMA ESPACIAL BRASILEIRO.</i> Albuquerque, Inaldo S. São José dos Campos, INPE 2012. Dissertação de Mestrado.

6.2 Cronograma baseado nas Baselines
------------------------------------

| Baseline               | Momento no ciclo de vida	     | Data |
|----------------------------------------|-----------------------------|----------------------|
|Baseline de Planejamento|Definição do projeto - Criação da Baseline|Na data de Fechamento - Aprovação do plano|
|Baseline de Artefatos|Revisão do Status do projeto - Homologação do artefato aprovado pelo cliente|Data definida no cronograma do Projeto|
|Baseline de Mudança|Revisão do status do projeto|Na data da aprovação|
|Build Externo|Finalização da Etapa de Implementação e/ou Entrega/implantação no cliente|Data definida no cronograma do Projeto|

6.3 Descrição do Procedimento de Documentação de Problemas
----------------------------------------------------------

<p>
Os problemas encontrados deverão ser reportados às partes interessadas, tais como: membros da equipe de desenvolvimento, gestores, etc, de acordo com a natureza do problema e gravidade tudo deve ser considerado. Será utilizada uma ferramenta de <i>bug tracking</i> <b>JIRA</b>, para realizar o controle de mudanças e o acompanhamento da resolução do problema encontrado.
</p>
<p>
Os problemas encontrados deverão ter o seu correspondente ciclo de vida definido, conforme a seção 3.2.2 Controle de mudanças. Deve-se fazer a customização do ciclo de vida da ferramenta JIRA visando a adequação a estrutura definida
nesse documento.
</p>
