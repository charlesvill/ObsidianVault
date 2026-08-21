#### layout.tsx
- say you have some ui to be shared between two or more components (for example a nav) you use layout to define what that looks like. place it in the same level as your page.tsx. you can pass children aswell and treat it like a react outlet component.
#### page.tsx
- page is special in that when placed in a folder under app, it gets picked up by Next.js as app route and publicly available

#### partial rendering
- a result of flow between layout and its pages. after initial render, the layout components wont re-render, only the new pages will.
- partial rendering allows state preservation in the layout during different page navigation

### rendering methods
#### static rendering
- datafetching and rendering happens at build time (and when revalidating data)
	- the result is cached and that is what is served
- this leads to : 
	- much faster load times
	- less compute costs because it doesnt have to dynamically recompute on each request
	- improved SEO: cached results are easier for search engine crawlers to index. leads to higher search engine rankings
#### dynamic rendering
- don'r really need to go into this right

### streaming data
- data fetches are done in parallel as opposed to sequentially
- data fetches come in chunks and you can stream chunks while others arrive, allowing end user to interact with the site as the rest comes, the traditional model might wait for everything to load first
- you can do this with the loading.tsx or the `<Suspense>` component in an individual file

#### loading.tsx
- a special next js file that offers fallback ui
- since nextjs default rendering is static, whatever static elements you have like sideNav (from example dashboard) it will load that immediately and dynamic content will stream in

#### routing groups
- sometimes you'll have components that are children of a main dashboard component and you have a skeleton component for the dashbaord, but you wont want that skeleton to apply to the children. you can create routing groups with a folder (overview)/ that will allow rendering compoents with certain groups whlie not affecting the url. 

#### Suspense component
- you can stream a whole page but you can also be more granular and stream a component with React Suspense

#### streaming content options: 
- You could stream the **whole page** like we did with `loading.tsx`... but that may lead to a longer loading time if one of the components has a slow data fetch.
- You could stream **every component** individually... but that may lead to UI _popping_ into the screen as it becomes ready.
- You could also create a _staggered_ effect by streaming **page sections**. But you'll need to create wrapper components.

### Search and Pagination patterns
