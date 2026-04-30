# Design System Master File — Tamsui Kindergarten Picker

> **LOGIC:** When building a specific page, first check `design-system/pages/[page-name].md`.
> If that file exists, its rules **override** this Master file.
> If not, strictly follow the rules below.

---

**Project:** Tamsui Kindergarten Picker
**Generated:** 2026-04-30 (refined from ui-ux-pro-max output)
**Category:** Public Service / Decision-Aid Tool

## Audience & Tone

- 受眾：忙碌新手爸媽（30-40 歲，可能孕期或新生兒爸媽）
- 心理狀態：焦慮、時間少、想快速比較
- 期待：政府工具的可信度 + 親子應用的溫暖
- 不要：兒童玩具感（Comic Neue / Baloo）、企業 dashboard 感（Fira Code）、極簡奢華感（Bodoni）

---

## Color Palette (preserved from existing CSS, expanded with semantic aliases)

| Role | Hex | CSS Variable |
|------|-----|--------------|
| Background base (cream paper) | `#fffaf1` | `--color-bg-base` / `--cream` |
| Surface (cards, paper) | `#fffefa` | `--color-surface` / `--paper` |
| Ink (high-contrast text) | `#3b352f` | `--color-text` / `--ink` |
| Muted text | `#796f63` | `--color-text-muted` / `--muted` |
| Accent green (positive/有缺額) | `#83b47a` | `--color-success` / `--green` |
| Accent blue (info/distance) | `#83b8d9` | `--color-info` / `--blue` |
| Accent yellow (highlight/brand) | `#ffd66b` | `--color-accent` / `--yellow` |
| Coral (warning/裁罰) | `#f18f79` | `--color-warning` / `--coral` |
| Rose (negative state) | `#f6b8b8` | `--color-error-soft` / `--rose` |
| Line/border | `#eadfcf` | `--color-line` / `--line` |

**Notes:** 保留原 repo 的「暖米紙感 + soft pastel accent」定位。Soft yellow + warm browns 對台灣讀者有「公立機關公告」+「童書封面」的雙重熟悉感。

## Typography

- **Heading & Body:** Noto Sans TC（中文為主，英文用相同字體）
  - 退路：`"PingFang TC"` (macOS) → `"Microsoft JhengHei"` (Windows) → `system-ui`
- **Display accent (optional):** Inter（Latin only）— 用於數字/英文字母獨立場景
- **Weights used:** 400 (regular), 500 (medium), 600 (semibold), 700 (bold)
- **Line-height:** body 1.6 / heading 1.25
- **Mood:** humanist, neutral, public service, no novelty

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;600;700&family=Inter:wght@400;500;600;700&display=swap');

:root {
  --font-sans: "Noto Sans TC", "Inter", "PingFang TC", "Microsoft JhengHei", system-ui, sans-serif;
  --font-mono: "JetBrains Mono", "Menlo", monospace;
}
```

## Spacing Scale (8px base)

| Token | Value | Usage |
|-------|-------|-------|
| `--space-1` | `4px` | Hairline gaps |
| `--space-2` | `8px` | Inline icon gaps |
| `--space-3` | `12px` | Tight padding |
| `--space-4` | `16px` | Default card padding |
| `--space-6` | `24px` | Section padding |
| `--space-8` | `32px` | Block separator |
| `--space-12` | `48px` | Hero / section margin |
| `--space-16` | `64px` | Page-level margin |

## Radius

| Token | Value | Usage |
|-------|-------|-------|
| `--radius-sm` | `6px` | Inputs, chips |
| `--radius-md` | `10px` | Buttons |
| `--radius-lg` | `14px` | Cards |
| `--radius-xl` | `20px` | Hero blocks |
| `--radius-full` | `9999px` | Pills |

## Shadow

| Token | Value | Usage |
|-------|-------|-------|
| `--shadow-sm` | `0 1px 2px rgba(98, 76, 44, 0.06)` | Subtle lift |
| `--shadow-md` | `0 4px 12px rgba(98, 76, 44, 0.10)` | Cards |
| `--shadow-lg` | `0 16px 38px rgba(98, 76, 44, 0.13)` | Hero, drawer |
| `--shadow-brutal` | `5px 5px 0 var(--ink)` | Brand mark, kids vibe |

Note: shadow tint follows `rgba(98, 76, 44)`（warm brown）not `rgba(0, 0, 0)` to keep paper feel.

## Transitions

| Token | Value | Usage |
|-------|-------|-------|
| `--ease-fast` | `150ms ease` | Hover color/opacity |
| `--ease-base` | `200ms ease` | Card lift, drawer |
| `--ease-slow` | `300ms ease` | Page entrance |
| `--ease-spring` | `350ms cubic-bezier(0.34, 1.56, 0.64, 1)` | Modal pop |

All transitions must respect `prefers-reduced-motion: reduce`.

## Accessibility (NON-NEGOTIABLE)

- 文字對比度：body text ≥ 4.5:1（淡水分區範圍內爸媽常常邊抱小孩邊滑手機，光線條件變動大）
- Body 字級：mobile ≥ 16px、desktop ≥ 15px
- Touch target：所有可點擊元素 min 44x44px
- Focus ring：3px 高對比、用 `--color-accent`
- 全站尊重 `prefers-reduced-motion`
- ARIA：所有 icon button 必須有 aria-label

## Pre-Delivery Checklist

- [ ] 沒用 emoji 當 icon（必要時用 SVG）
- [ ] 所有可點 element 有 `cursor: pointer`
- [ ] Hover 過渡 150-300ms
- [ ] 文字對比 ≥ 4.5:1
- [ ] Focus state 可見（鍵盤瀏覽）
- [ ] `prefers-reduced-motion: reduce` 時關閉動畫
- [ ] 375px / 768px / 1024px / 1440px 都不破版
- [ ] mobile 沒有 horizontal scroll

## Anti-Patterns (Do NOT Use)

- ❌ AI 紫粉漸層
- ❌ Comic Neue / Baloo / Pacifico 等「童書字體」
- ❌ 純 navy 政府風（會抹掉「親子」面）
- ❌ Glassmorphism（光線下看不清楚）
- ❌ 大量 box-shadow 黑色（會破壞紙質感，要用 brown tint）
- ❌ Layout-shifting hover（card 不要 scale 變大）
