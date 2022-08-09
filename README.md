<h1 align="center">Gestão de Projetos</h1>

<p align="center">
  <img src="https://user-images.githubusercontent.com/102304054/183707646-e281a382-f080-43f4-967f-83e61d83839d.png">
</p>

## 1. Dashboard

Esse dashboard foi desenvolvido através da **"Semana do Power BI"**, realizado em Agosto de 2021 pela [DATAB](https://www.datab.com.br/). Ele pode ser visualizado de forma online e interativa, clicando na imagem abaixo:

 <p align="center">
<a href="https://app.powerbi.com/view?r=eyJrIjoiN2VmZjM2NTItM2E1MC00NGU2LWE1MjUtM2NlMzJiOTQxMjdkIiwidCI6IjhlNDJlNTBlLTNkMWEtNDAzYy04ZWZmLTU4OGJkOGQxMjk5ZiJ9"><img src="https://user-images.githubusercontent.com/102304054/183717989-6a813637-a430-48a5-934d-a49abdfecc7f.png"></a>
</p>

## 2. Estudo de Caso

Você acabou de ganhar uma tarefa em sua empresa: coordenar novos projetos da sua área. Sua primeira missão é garantir que todos da equipe que coordena estão fazendo um bom trabalho: atingindo prazos, executando tarefas e não gastando mais do que deveriam nas execuções.

A boa notícia é que tudo isso já é armazenado em um software que exporta dados organizados. A notícia melhor ainda é que não tem nenhum relatório ou dashboard estruturado e você vai poder mostrar tudo o que sabe de Power BI e impressionar seus gestores, para quem sabe, realizar um ótimo trabalho e garantir uma promoção.

O projeto deve possibilitar uma análise dos indicadores abaixo. Você pode aplicar o gráfico que desejar, desde que favoreça a simplicidade e sua leitura pelos tomadores de decisão.

1. Qual é a quantidade total de atividades?
2. Qual é o percentual de gastos versus orçamento?
3. Qual é o percentual de conclusão total e por projeto quando é realizado algum filtro?
4. Qual é a quantidade de atividades por status?
5. Qual é a quantidade de atividades atrasadas em relação ao dia de hoje versus não atrasadas?
6. Resumo por projeto com os indicadores de Conclusão, Custo e Peso;
7. Tabela geral de carga de trabalho por responsável com suas respectivas fotos para gerar mais engajamento e responsabilidade.
8. No mesmo visual da tabela anterior, informar a quantidade de atividades cada responsável possui.
9. Ainda no mesmo visual da tabela anterior, calcular o *"Workload"* de cada responsável. Acima de 10 atividades no período selecionado é considerado uma carga pesada de trabalho. Representar esse fator de forma visual (dentro da tabela).
10. Criar um *gráfico Gantt* por projeto e atividade com os respectivos responsáveis.
11. Filtros necessários: Data, Responsável e Projeto.

## 3. Indicadores

Com o carregamento e a compreensão dos dados, foi possível dar início no desenvolvimento das visualizações, conforme as informações solicitadas pelo Estudo de Caso.

**1. Qual é a quantidade total de atividades?**

<img src="https://user-images.githubusercontent.com/102304054/183707827-00f093f4-8536-489a-bfa8-ae439ea38ad9.png"/><a>
</p>

Para responder a essa pergunta, foi criada uma medida chamada de *"Total de Atividades"*, utilizando a tabela *"Relatórios por Projeto"*, coluna **"Atividade"** e a função *COUNT*. A medida *"Total de Atividades"*, foi adicionada a um *cartão*.

**2. Qual é o percentual de gastos versus orçamento?**

<img src="https://user-images.githubusercontent.com/102304054/183707924-8e275ab4-f2bb-4d34-aa33-62cef7a696f1.png"/><a>
</p>

Para responder a essa pergunta, foram criadas três medidas, são elas: *"Realizado"*, *"Orçamento"* e *"Custo"*.

Realizado = SUM('Relatorios por Projeto'[Valor Usado])
Orçamento = SUM('Relatorios por Projeto'[Valor Orçamento])
Custo = [Realizado] / [Orçamento]

Por último,  a medida *"Custo"*, foi adicionada a um *cartão*.

**3. Qual é o percentual de conclusão total e por projeto quando é realizado algum filtro?**

<img src="https://user-images.githubusercontent.com/102304054/183707982-fa2e3a01-29f8-4388-9119-8c5b97e39a39.png"/><a>
</p>

Para responder a essa pergunta, foram criadas três medidas, são elas: *"Dias Finalizados"*, *"Dias Previstos"* e *"Conclusão"*.

Dias Finalizados = SUM('Relatorios por Projeto'[Dias Executados])
Dias Previstos = SUM('Relatorios por Projeto'[Dias Duração])
Conclusão = Medidas[Dias Finalizados] / Medidas[Dias Previstos]

Por último,  a medida *"Conclusão"*, foi adicionada a um *cartão*.

**4. Qual é a quantidade de atividades por status?**

<img src="https://user-images.githubusercontent.com/102304054/183708058-af3620fb-8314-473a-bbb8-f981255f9e45.png"/><a>
</p>

Para responder a essa pergunta, foi utilizado um *gráfico de barras*, em eixo  X, a coluna **"Status"** e no eixo Y, a medida *"Total de Atividades"*. A medida chamada de *"Total de Atividades"*, foi criada utilizando a tabela *"Relatórios por Projeto"*, coluna **"Atividade"** e a função *COUNT*.

**5. Qual é a quantidade de atividades atrasadas em relação ao dia de hoje versus não atrasadas?**

<img src="https://user-images.githubusercontent.com/102304054/183708074-d3fb4288-fa17-44c5-9630-a2b809a839d1.png"/><a>
</p>

Para responder a essa pergunta, foi utilizado um *gráfico de rosca*, trazendo a coluna **"devicecategory"**, trazendo a medida *"Total de Atividades"* para valores e a coluna calculada **"Atrasado?"** para a legenda. A medida chamada de *"Total de Atividades"*, foi criada utilizando a tabela *"Relatórios por Projeto"*, coluna **"Atividade"** e a função *COUNT*. Já a coluna calculada **"Atrasado?"**, foi criada, utilizando a fórmula abaixo:

Atrasado? = IF('Relatorios por Projeto'[Data Final] < TODAY() && 'Relatorios por Projeto'[Status] <> "Finalizada", "Sim","Não")

O **&&** é igual a **AND**.

**6. Resumo por projeto com os indicadores de Conclusão, Custo e Peso.**

<img src="https://user-images.githubusercontent.com/102304054/183708084-76e31774-e61c-437e-9225-63e9982a21e6.png"/><a>
</p>

Para responder a essa pergunta, foi utilizado uma *tabela*, trazendo a coluna **"Projeto"** e as medidas *"Conclusão"*, *"Custo"* e *"Peso"*.

Conclusão = [Dias Finalizados] dividido por [Dias Previstos]
Custo = Soma do realizado dividido pela soma do orçamento
Peso = Total de atividades dividido pela quantidade de responsáveis

Por último, foi aplicado uma formatação condicional nas colunas **"Custo"** (Background) e **"Peso"** (Ícone).

**7. Tabela geral de carga de trabalho por responsável com suas respectivas fotos para gerar mais engajamento e responsabilidade.**

**8. No mesmo visual da tabela anterior, informar a quantidade de atividades cada responsável possui.**

**9. Ainda no mesmo visual da tabela anterior, calcular o "Workload" de cada responsável. Acima de 10 atividades no período selecionado é considerado uma carga pesada de trabalho. Representar esse fator de forma visual (dentro da tabela).**

<img src="https://user-images.githubusercontent.com/102304054/183708094-63d0eb50-3d8e-4bc3-8db2-8a5ae3fa5cc1.png"/><a>
</p>

Para responder as perguntas 7, 8 e 9, foi utilizado uma *tabela*, trazendo a tabela *Gerente* e as colunas **"Foto"** e  **"Responsáveis"**, assim como, a as medidas *"Total de Atividades"*, *"Workload"*. A medida chamada de *"Total de Atividades"*, foi criada utilizando a tabela *"Relatórios por Projeto"*, coluna **"Atividade"** e a função *COUNT*. E a medida *"Workload"* foi criada utilizando a fórmula abaixo:

Workload = IF([Total de Atividades] >= 10, "😡","😀")

**10. Criar um gráfico Gantt por projeto e atividade com os respectivos responsáveis.**

<img src="https://user-images.githubusercontent.com/102304054/183708114-7f5b3894-f884-4d86-b018-6ed7bf5e0982.png"/><a>
</p>

Para responder a essa pergunta, foi utilizado o *gráfico de Gantt by MAQ Software*. Na opção Categoria, foi adicionado as colunas **"Projeto"** e **"Atividade"**, já nas opções de Início e Fim, foram adicionadas as colunas **"Data Inicial"** e **"Data Final"** e por último, na opção Rótulo de Dados, foi adicionado a coluna **"Responsável"**.

**11. Filtros necessários: Data, Responsável e Projeto.**

<img src="https://user-images.githubusercontent.com/102304054/183708128-85f84f87-7e18-4a70-86e2-edbc281b6856.png"/><a>
</p>

Para criação dos filtros a cima, foi utilizado a opção de *Segmentação de Dados* e as colunas **"Data Inicial"**, **"Projeto"** e **"Responsável"**.



