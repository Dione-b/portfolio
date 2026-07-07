# Refatoração Horizontal Scroll — 10 Sprints

> **Problema:** Transição entre seções horizontalmente não é suave — scroll com jank, sem easing, sem snap, sem paralaxe real entre camadas.

**Objetivo:** Transições butter-smooth, snap preciso, paralaxe com profundidade, navegação intuitiva.

**Stack:** Lenis (smooth scroll) + CSS custom properties + GPU-accelerated transforms

---

### Sprint 1: Substituir scroll manual por Lenis

**Problema:** `scroll` event + `translate3d` manual causa jank em frames baixos. Lenis oferece requestAnimationFrame nativo com easing interpolado.

- Remover `window.addEventListener('scroll', ...)` do HorizontalScroll.astro
- Instalar Lenis: `pnpm add lenis`
- Inicializar Lenis no lugar do scroll handler raw
- Lenis gerencia o scroll virtual e emite `progress` por frame

```astro
<script>
  import Lenis from 'lenis';

  const lenis = new Lenis({
    duration: 1.2,
    easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
    orientation: 'vertical',
    gestureOrientation: 'vertical',
    smoothWheel: true,
  });

  function onProgress(time) {
    const maxScroll = document.body.scrollHeight - window.innerHeight;
    const progress = lenis.progress;
    const translateX = -progress * (totalSections - 1) * 100;
    track.style.transform = `translate3d(${translateX}vw, 0, 0)`;
    updateDots(progress);
    lenis.raf(time);
  }

  lenis.on('scroll', onProgress);
  requestAnimationFrame(function raf(time) {
    lenis.raf(time);
    requestAnimationFrame(raf);
  });
</script>
```

---

### Sprint 2: Snap sections com scroll progressivo

**Problema:** Scroll contínuo permite parar entre duas seções — visualmente quebrado.

- Calcular section-alvo baseado na velocidade/direção do scroll Lenis
- Aplicar `lenis.scrollTo(destination, { immediate: false })` ao soltar o scroll
- Usar `lerp` para interpolar entre seções

```
scrollDirection = down → next section
scrollDirection = up → previous section
scrollVelocity > threshold → skip section
```

---

### Sprint 3: Camadas de paralaxe (profundidade)

**Problema:** Tudo se move junto — sem sensação de profundidade.

- Dividir cada seção em 2-3 camadas: foreground, content, background
- Cada camada com `translateX` em velocidade diferente:
  - Background: moves at 0.3x section speed
  - Content: moves at 1.0x section speed (padrão)
  - Foreground: moves at 1.5x section speed
- CSS `will-change: transform` na camada content

```css
.bg-layer   { transform: translateX(calc(var(--progress) * -30vw)); }
.content    { transform: translateX(calc(var(--progress) * -100vw)); }
.fg-layer   { transform: translateX(calc(var(--progress) * -150vw)); }
```

---

### Sprint 4: Easing customizado por seção

**Problema:** Mesma curva de easing para todas as seções — monótono.

- Definir curvas cubic-bezier diferentes por tipo de seção
- Hero → ease-out (suave na chegada)
- Projetos → ease-in-out (neutro)
- Timeline → ease-out-quart (natural)
- Skills → ease-out-expo (rápido)
- Passar easing como prop do HorizontalScroll

---

### Sprint 5: Navegação com teclado + touch

**Problema:** Só funciona com scroll do mouse.

- Arrow keys (← →) para navegar entre seções
- Touch swipe horizontal detectado via touch events
- Prevenir conflito entre scroll vertical Lenis e swipe horizontal

---

### Sprint 6: Indicadores de progresso animados

**Problema:** Dots estáticos, sem feedback de transição.

- Animação de preenchimento contínuo nos dots
- Progress bar horizontal no topo (como YouTube chapters)
- Mini-map das seções no canto (nomes + progresso)
- Transição suave de cor nos dots (gradiente entre seções)

---

### Sprint 7: Responsivo + mobile

**Problema:** Viewport height em mobile com UI bars.

- Usar `100dvh` (dynamic viewport height) em vez de `100vh`
- Ajustar altura do body dinamicamente com `window.innerHeight`
- Touch events com zona morta para evitar scrolls acidentais
- Reduzir número de dots em mobile (agrupar)

---

### Sprint 8: Reduced motion + a11y

**Problema:** Sem suporte para `prefers-reduced-motion`.

- Detectar `prefers-reduced-motion: reduce`
- Desabilitar Lenis, voltar para scroll nativo vertical
- Fallback: scroll vertical sem animação, seções empilhadas
- Adicionar `aria-label` nos dots
- Skip to content link

---

### Sprint 9: Performance profiling

**Problema:** Sem métricas de performance.

- Medir FPS com `requestAnimationFrame` delta
- Log de long tasks (>50ms)
- Verificar composite layers no DevTools
- Garantir que `transform` e `opacity` são as únicas propriedades animadas
- Verificar `will-change` não exagerado (memory leak)

---

### Sprint 10: Deferred loading + code splitting

**Problema:** Todas as seções carregam junto.

- Carregar seções abaixo da dobra com `loading="lazy"`
- Section components como `client:visible`
- Lenis import dinâmico (`await import('lenis')`)
- Fallback para scroll vertical nativo se Lenis falhar carregar
