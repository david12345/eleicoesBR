# Apuração Eleições BR

Página única (`index.html`) que mostra o resultado das eleições do Brasil em tempo real,
consultando os dados públicos do TSE **a cada 3 segundos**, e projeta o resultado final
com base no **ritmo de crescimento dos votos** de cada candidato.

## Uso

Abra `index.html` no navegador. Sem configuração, roda em **modo simulação** (dados fictícios).

Para dados reais, abra *Fonte de dados e configuração* e informe o ciclo (ex.: `ele2026`),
o código da eleição e o cargo, ou clique em *Detectar eleição de hoje*. Também dá para passar
na URL:

```
index.html?ciclo=ele2026&eleicao=XXX&cargo=0001&abr=br
index.html?modo=sim
```

O arquivo consultado segue o padrão do TSE:
`https://resultados.tse.jus.br/oficial/{ciclo}/{eleicao}/dados-simplificados/{abr}/{abr}-c{cargo}-e{eleicao6}-r.json`

Se o navegador bloquear a requisição (CORS), informe um proxy no campo *Proxy CORS*.

## Projeção

- Entre parciais, calcula a fatia de cada candidato nos votos recém-apurados.
- Fatias recentes pesam mais (média móvel exponencial), antecipando viradas quando
  regiões com outro perfil entram na contagem.
- O total final de válidos é estimado pelo ritmo de votos por ponto de seção totalizada.
- A faixa de incerteza (~90%) e a "chance" de vitória vêm da variação das fatias entre parciais.

É uma estimativa matemática, não oficial.
