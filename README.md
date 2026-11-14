# Acervo — Arsenal dos Criativos Validados

964 criativos estáticos e 197 formatos de vídeo prontos pra importar na plataforma. São cards no mesmo formato do modal atual (título, formato, nicho, etapa, por que funciona, quando usar, estrutura do texto, legenda, prompt para IA e atenção), com dois campos novos: tipo de solução e oferta.

## Estrutura

```
catalogo-estaticos.json   array com os 964 cards estáticos
catalogo-videos.json      array com os 197 cards de vídeo
taxonomia.json            listas fechadas: nichos, tipo_solucao, oferta, etapa_funil, formatos
formatos-novos.md         formatos estáticos que não cabiam nos 19 atuais (valor "novo:<nome>")
estaticos/<nicho>/<id>.jpg + <id>.json   arte + card (o JSON é igual ao item do catálogo)
videos/<id>.json                         card de vídeo
videos/<id>/frames/f1..f6.jpg            frames da referência
videos/<id>/transcricao.txt              transcrição da referência (quando houver)
videos/RESULTADO.md                      totais e ressalvas dos vídeos
```

## Card estático

| campo | o que é |
|---|---|
| `id` | `est-<nicho>-<library_id>` |
| `titulo`, `descricao`, `quando_usar` | texto do modal |
| `formato` | um dos 19 formatos atuais, ou `novo:<nome>` |
| `nicho` | chave de `taxonomia.json > nichos` (filtro) |
| `tipo_solucao` | produto-fisico, infoproduto, mentoria-consultoria, servico-local, servico-online, saas-app, financeiro, imovel, evento |
| `oferta` | desconto-cupom, garantia, gratis-isca, quiz-diagnostico, lancamento, escassez-prazo… (ver taxonomia) |
| `etapa_funil` | topo, meio, fundo |
| `proporcao` | 1:1, 4:5, 9:16, 1.91:1 |
| `por_que_funciona` | array de 3 a 4 frases |
| `estrutura_texto`, `legenda` | modelos com [colchetes] |
| `prompt_ia` | prompt com variáveis `{{nome}}` `{{o_que_e}}` `{{para_quem}}` `{{problema}}` `{{beneficios}}` `{{oferta}}` `{{marca}}`, que correspondem aos campos da aba Meu produto. Campo vazio vira "não informado", como já é hoje |
| `alerta_politica` | texto da caixa Atenção, ou `null` |
| `validacao` | `forte` (30+ dias no ar ou 5+ variações) · `media` (14 a 29 dias) · `fraca` |
| `arquivo` | caminho da arte, relativo à raiz do repo |
| `fonte` | **dado interno, não exibir**: anunciante, library_id, início, dias no ar, texto original do anúncio. `dias_no_ar` pode virar selo no card ("rodando há 87 dias") |

## Card de vídeo

Mesmos campos de classificação, com `nichos` (array) no lugar de `nicho`, e mais estes:

| campo | o que é |
|---|---|
| `formato_video` | tipo do vídeo (ugc-talking-head, demonstracao, split-screen…); são 88 valores |
| `duracao`, `proporcao` | duração sugerida e proporção |
| `hook` | `{falado, texto_tela, visual}`: os primeiros segundos |
| `estrutura` | array de cenas `{tempo, cena, fala, texto_tela}` |
| `roteiro_modelo` | roteiro completo com [colchetes] |
| `tomadas_celular` | lista do que gravar |
| `caminho_ia` | como fazer sem gravar (Veo/Sora, avatar, slideshow) |
| `prompt_ia` | mesmas variáveis do estático; devolve roteiro, legenda e prompts de cena |
| `referencias` | origem e frames da referência. **Interno**: os frames podem ilustrar o card, mas o `url_ou_id` não deve aparecer |

## Contagem por nicho

| nicho | estáticos | vídeos (um vídeo pode estar em vários nichos) |
|---|---|---|
| `infoproduto-cursos` | 199 | 39 |
| `educacao-concursos` | 110 | 33 |
| `renda-extra` | 87 | 14 |
| `saas-b2b` | 45 | 53 |
| `mentoria-high-ticket` | 43 | 27 |
| `saude` | 42 | 28 |
| `consorcio-credito` | 41 | 9 |
| `marketing-trafego` | 37 | 54 |
| `seguros` | 35 | 10 |
| `produtos-fisicos-marketplace` | 33 | 22 |
| `suplementos` | 32 | 6 |
| `imoveis` | 32 | 18 |
| `servicos-locais` | 30 | 40 |
| `investimentos` | 25 | 30 |
| `automotivo` | 24 | 18 |
| `pet` | 20 | 11 |
| `beleza-cosmeticos` | 20 | 15 |
| `eventos-lives` | 17 | 11 |
| `infantil-maternidade` | 17 | 8 |
| `ia-ferramentas` | 14 | 48 |
| `estetica-clinicas` | 14 | 14 |
| `moveis-decoracao` | 14 | 12 |
| `emagrecimento-fitness` | 12 | 17 |
| `relacionamento-desenvolvimento` | 12 | 8 |
| `moda-acessorios` | 9 | 11 |

## Ressalvas

- As artes são anúncios reais de terceiros e trazem a marca visível. Avaliar se o botão "Baixar original" continua ou se a arte vira só referência na tela.
- Nos vídeos, 172 de 197 estão com validação `media`. Nos que vieram de anúncios, o card se baseia na arte e no texto do anúncio; o vídeo inteiro não foi assistido.
- Os formatos estáticos estão concentrados: "Oferta e promoção" e "Produto em destaque" somam 62% dos estáticos.
