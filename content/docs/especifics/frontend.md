---
title: 2.2 - Frontend
type: docs
prev: docs/folder/
---

- **Aqui você vai encontrar o básico para entender como a aplicação funciona, e por quê funciona, caso queira se aprofundar mais procure as documentações oficiais pois elas são o melhor material de aprendizado.**

- **Atualmente o projeto frontend usa o framework [Svelte Kit](https://svelte.dev/docs/kit/introduction)**. 

Depois de algumas análises de mercado, vimos que essa era a melhor escolha para pessoas que nunca tinham tido contato com nenhum tipo de framework web na prática, e precisavam entregar um produto minimamente utilizável em um curto período de tempo.

O **Svelte Kit** simplifica diversos processos na construção de páginas, e costuma ser muito direto ao ponto; é uma ótima porta de entrada para o universo dos frameworks, pois ele usa muitos conceitos que já são utilizados em outras ferramentas mais populares dentro do mercado.

## O que é o Svelte?

Svelte é uma forma de escrever a UI de páginas web que é posteriormente compilada pelo `Svelte Compiler`, e convertida em HTML, CSS, JS.
> [!NOTE]
> Caso queira aprender um pouco sobre o funcionamento do framework utilize os tutoriais, disponibilizados pelo próprio time do Svelte: [Svelte Tutorial](https://svelte.dev/tutorial/svelte/welcome-to-svelte)

## Diferença entre Svelte Kit e Svelte

Enquanto o Svelte serve para construção de componentes dentro da UI, o Svelte Kit se propõe a fornecer todas as ferramentas necessárias para a construção de uma aplicação web funcional; com funcionalidades básicas como o [routing](https://svelte.dev/docs/kit/glossary#Routing), que atualiza em tempo real as alterações feitas dentro da página. 

## Como nossa aplicação é estruturada
```
iris/
├ src/
│ ├ lib/
│ │ ├ server/
│ │ │ └ [your server-only lib files]
│ │ └ [your lib files]
│ ├ params/
│ │ └ [your param matchers]
│ ├ routes/
│ │ └ [your routes]
│ │ └ +error.svelte
│ ├ app.html
│ ├ hooks.client.ts
│ ├ hooks.server.ts
│ └ service-worker.ts
├ static/
│ └ [your static assets]
├ tests/
│ └ [your tests]
├ package.json
├ svelte.config.ts
├ tsconfig.json
└ vite.config.js
```

### src
- É onde 99% do código do projeto vai estar contido.
#### lib
- Contém todo os arquivos que vão ser utilizados uma, ou mais vezes, dentro do projeto. Geralmente padronizamos componentes e colocamos dentro da pasta `lib`, a partir disso você pode importar esses componentes usando o `$lib` alias nos seus imports.
```svelte
<script type="ts">
 import { foo } from "$lib/bar.ts"
</script>
```
##### server
- Contém os arquivos da **lib** que só devem existir na parte `server side` da aplicação, coloque os arquivos que devem ser reaproveitados pelos servidores de rotas aqui.
#### +error.svelte
- É a página que o usuário vai ser direcionado quando algum erro que impeça a aplicação de funcionar corretamente for detectado; na nossa aplicação estamos usando o `+error.svelte` para usufuir de funções do próprio Svelte.
#### hooks.server.ts
- Os hooks são funções declaradas que o Svelte Kit vai chamar toda vez em eventos específicos da aplicação. 
- O `hooks.server.ts` tem uma função chamada `handle` que é chamada toda vez em que uma requisição é feita, geralmente antes da renderização da página, á partir disso a resposta de todos os outros servidores da aplicação vão ser determinadas.

**Trecho de código da própria aplicação:**
```ts
import { BACKEND_URL } from "$env/static/private";
import { type Handle } from "@sveltejs/kit";
import type { Token } from "$lib/types/Token";
import { jwtDecode } from "jwt-decode";

/**
 * @classdesc - hooks.server.ts
 * Classe que executa a cada refresh de página
 * é ideal colocar chamadas de autenticação de usuário
 * aqui dentro, pois assim teremos noção em 100% do tempo
 * se o usuário deve ou não estar tendo acesso á aplicação.
 * 
 * Basicamente um middleware, recomendo pesquisar mais
 * a fundo caso ainda existam dúvidas.
 * 
 * @type { event } representa o contexto do server-side da aplicação
 */
export const handle = (async ({ event, resolve }) => {
    const { cookies } = event
    const token = cookies.get("token")
    if (!token || typeof token !== "string"){
        console.error("Token inválido ou não identificado")
        return resolve(event);
    }
    event.locals.token = token;

    const tokenData: Token = jwtDecode(token);
    const response = await fetch(
        `${BACKEND_URL}/professores/${tokenData.sub}`,
        {
          method: "GET",
          headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${token}`,
          },
        }
      );

    if(!response.ok){
        console.error(`Erro ao puxar dados do usuário: ${response.status}`)
        return resolve(event);
    }
    event.locals.user = await response.json();
    
    return resolve(event);
}) satisfies Handle;
```
##### locals
- Geralmente usamos o locals quando queremos mandar dados customizados para outros servidores — á partir do `hooks.server.ts` — toda vez que a aplicação for carregada, populamos o objeto `event.locals`, assim como é mostrado no trecho acima, onde estamos passando os dados do usuário para as páginas de `server.ts` da aplicação.
#### app.d.ts
- Aqui devem ser colocados os tipos nativos da aplicação, tipos que você quer usar sem necessariamente precisar importar.
**Exemplo da própria aplicação:**
```ts
// See https://kit.svelte.dev/docs/types#app
// for information about these interfaces
import type { User } from "$lib/types/User";

declare global {
	namespace App {
		interface Error {}
		interface Locals {
			token?: string; 
			user?: User;
		}
		interface PageData {
			flash?: { type: 'success' | 'error' | 'warning'; message: string };
		}

		interface PageState {}
		interface Platform {}
		namespace SuperForms {
			type Message = {
				type: 'error' | 'success' | 'warning', text:string
			}
		}
	}
}

export {};
```
#### static
- Todos os arquivos estáticos, imagens por exemplo, devem ser colocados aqui.