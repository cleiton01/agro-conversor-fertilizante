# agro-conversor-fertilizante

Calculadora web que converte a dose de um fertilizante líquido (por exemplo, Sensi Grow A+B) em gramas por litro de um ou mais fertilizantes em pó, mantendo a mesma entrega de nutrientes.

## Como usar

Abra o `index.html` no navegador. Não há build nem dependências.

1. **Líquido:** cadastre cada parte (A, B…), com dose em ml/L, base do percentual (p/p ou p/v) e densidade. Depois adicione os nutrientes do rótulo, um por linha.
2. **Pós:** adicione um ou mais pós, informando os nutrientes à mão ou carregando um modelo (nitrato de cálcio, sulfato de magnésio, mix de micros etc.).
3. **Critério:** use "Melhor ajuste" ou priorize um nutriente específico ("Igualar N", por exemplo). Na coluna **Ajustar**, marque quais nutrientes entram no cálculo.
4. **Volume e receita:** no painel de resultado, digite o volume que você vai preparar, em litros. Sem volume, a página mostra só a dose em g/L. Copie a receita pronta.

As entradas ficam salvas no `localStorage` do navegador.

## Cálculo

```
mg/L (líquido) = dose (ml/L) × densidade (g/ml) × % × 10    (p/p)
mg/L (líquido) = dose (ml/L) × % × 10                        (p/v)
mg/L (pó)      = g/L × % × 10
```

**Conversões para a base do resultado:**

| De | Para | Fator |
|---|---|---|
| P | P₂O₅ | × 2,291 |
| K | K₂O | × 1,205 |
| CaO | Ca | × 0,715 |
| MgO | Mg | × 0,603 |

Com mais de um pó, as doses saem de mínimos quadrados não negativos sobre o erro relativo de cada nutriente marcado (descida por coordenadas). No modo "Igualar X", o nutriente X recebe peso 40× maior.

## Limitações

- O resultado é uma estimativa a partir das garantias do rótulo. Confirme sempre com medidor de EC e ajuste o pH depois de dissolver tudo.
- Use apenas pós 100% solúveis para fertirrigação ou hidroponia.
- Dissolva fontes de cálcio separadas de fosfatos e sulfatos.
