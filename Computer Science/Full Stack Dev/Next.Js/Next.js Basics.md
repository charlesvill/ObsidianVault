#### layout.tsx
- say you have some ui to be shared between two or more components (for example a nav) you use layout to define what that looks like. place it in the same level as your page.tsx. you can pass children aswell and treat it like a react outlet component.
#### page.tsx
- page is special in that when placed in a folder under app, it gets picked up by Next.js as app route and publicly available

#### partial rendering
- a result of flow between layout and its pages. after initial render, the layout components wont re-render, only the new pages will.
- partial rendering allows state preservation in the layout during different page navigation