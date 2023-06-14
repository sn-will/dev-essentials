# Competências Essencias

O que a gente espera de um dev é que ele tenha a consciência de que para todo código que escrevemos, não estamos resolvendo um problema singular, mas sim criando uma solução, solução essa que faz parte de um todo, precisa ter um código limpo, ser fácil de ser mantida e não causar bugs. Para isso, existem algumas perguntas que precisamos nos fazer durante o processo de desenvolvimento que nos ajudam a chegar a um resultado consistente:

- Repetição: estou repetindo código demais? A repetição pode se dar tanto no arquivo em que estamos trabalhando quanto o padrão que estamos desenvolvendo já ter sido utilizado em outros locais. É indispensável identificarmos padrões durante o desenvolvimento e criarmos funções que previnam a repetição.

    Exemplo:

    **O que não fazer:**
    ```javascript
    const resultadoA = (10 * 12) - 120;
    const resultadoB = (10 * 4) - 100;
    const resultadoC = (10 * 8) - 80;

    console.log(resultadoA, resultadoB, resultadoC);
    ```

    **O que fazer:**
    ```javascript
    const construirResultado = (multiplier: number, subtractor: number) => (10 * multiplier) -subtractor;
    
    const resultadoA = construirResultado(12, 120);
    const resultadoB = construirResultado(4, 100);
    const resultadoC = construirResultado(8, 80);

    console.log(resultadoA, resultadoB, resultadoC);
    ```

- Tão importante quanto não se repetir é prever uma possível repetição, é preciso enxergar que o código que estamos escrevendo pode ser utilizado em outros locais e tomar uma ação de antemão. Nestes casos, tudo com potencial de utilização futura deve ser criado em uma função, útil ou em um arquivo separado.

- Manutenção: o código que estou escrevendo esta modular o suficiente? Se algum dos valores mudar ele vai continuar funcionando? Quais locais serão preciso alterar caso os dados de entrada mudem? O quão simples será a manutenção dele?

    Um bom exemplo para isso é evitar passar valores diretamente nos arquivos e criar constantes e enums para valores que são utilizados em mais de um local:

    **O que não fazer:**
    ```javascript
    // ArquivoA
    const construirString => (product: IProduct) => `valor-padrao-x-${product.id}`;

    // ArquivoB
    const construirString => (category: ICategory) => `valor-padrao-x-${categori.id}`;
    ```

    **O que fazer:**
    ```javascript
    // ArquivoC com constants ou utils
    const valorPadraoX = 'valor-padrao-x';

    // ArquivoA
    import { valorPadraoX } from 'constants';
    const construirString => (product: IProduct) => `${valorPadraoX}-${product.id}`;

    // ArquivoB
    import { valorPadraoX } from 'constants';
    const construirString => (category: ICategory) => `${valorPadraoX}-${categori.id}`;
    ```

    Isso facilita a manutenção porque o `valorPadraoX` será alterado em um só local.

- Evitar bugs: existe a possibilidade deste código quebrar? O que acontece se os valores que estou esperando não chegarem? Apesar do `Typescript` nos ajudar com possíveis valores indefinidos é extremamente necessário fazermos uma análise dos possíveis efeitos colaterais do que estamos criando/alterado.
    
    Não esquecer de criar `try {} catches {}` para as requisições (caso a API fique fora do ar) e não consultar propriedades em objetos que possam ser indefinidos, são bons exemplos de práticas para evitar erros:

    **O que não fazer:**
    ```javascript
    const objetoA => {
        propA: { value: 'valueA' },
        propB: { value: 'valueB' },
        propC: { value: 'valueC' }
    };

    // Valores diferentes de propA, propB ou propC serão undefined
    const usarObjeto = (key) => objetoA[key].value
    ```

    **O que fazer:**
    ```javascript
    const objetoA => {
        propA: { value: 'valueA' },
        propB: { value: 'valueB' },
        propC: { value: 'valueC' }
    };

    // Verificar se a propriedade existe no objeto, caso não retornar um default
    const usarObjeto = (key) => objetoA[key]?.value || objetoA.propA.value
    ```

- Insistir na melhor solução, não se dar por satisfeito em apenas resolver o problema.
