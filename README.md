# Pretext Typography Benchmark & Stress Test

This project is a high-performance typography playground and interactive benchmark designed to showcase the power of the `@chenglou/pretext` engine compared to native browser DOM layout.

## 🚀 Overview

Pretext is a predictive text layout engine that bypasses the browser's expensive DOM reflow pipeline. This demo provides a live comparison and a rigorous automated benchmark to visualize the performance delta.

## 📊 Benchmark Methodology

Our benchmark is designed to be as fair and rigorous as possible, following the spirit of the official Pretext benchmarks:

1.  **Warmup Phase**: Before measurement, we run 10 layout cycles to allow the JavaScript engine (V8) to perform JIT (Just-In-Time) optimizations.
2.  **Iterative Sampling**: 
    *   **Pretext**: We run 10 iterations per width and take the average to stabilize sub-millisecond timings.
    *   **Native DOM**: We run 5 iterations per width.
3.  **Forced Reflow**: To measure the *real* cost of DOM layout, we dirty the layout state by toggling the container width and reading `offsetHeight` to force a synchronous reflow.
4.  **Width Sweeping**: We test across a range of widths (300px to 1000px) in 25px increments to observe how layout complexity scales.

## 📈 Data Scale (Stress Test)

We use a "Novel-Scale" data approach to push both engines to their limits. Our base text block is ~1,500 characters.

| Setting | Characters (Chars) | Words | Real-world Equivalent |
| :--- | :--- | :--- | :--- |
| **10 Paragraphs** | ~15,000 | ~2,200 | A medium-length blog post |
| **50 Paragraphs** | ~75,000 | ~11,000 | A detailed whitepaper / deep-dive |
| **100 Paragraphs** | ~150,000 | ~22,000 | ~60 pages of document content |
| **200 Paragraphs** | **~300,000** | **~44,000** | **A mid-sized novel (e.g., *The Great Gatsby*)** |

In a full 200-paragraph benchmark, Pretext processes approximately **8.7 million characters** across 29 different layout widths.

## 🔍 Comparison with Official Benchmarks

While our demo and the official Pretext benchmarks share the same core findings, there are interesting nuances:

| Metric | Official Benchmark (Batch) | Our Demo (Stress) |
| :--- | :--- | :--- |
| **Performance Boost** | **20x - 50x** | **10x - 30x** |
| **Data Structure** | 500 independent short snippets | 1 massive continuous string |
| **Focus** | Throughput (many small tasks) | Latency (one massive task) |
| **DOM Behavior** | Many nodes, simple layout | Few nodes, **extreme layout complexity** |

### Why the difference?
Official benchmarks focus on "Batching" (e.g., rendering a list of 500 comments). Our demo focuses on "Long-form Stress" (e.g., a high-performance document editor). In long-form scenarios, Pretext's advantage is even more critical because it prevents the "Layout Thrashing" that makes large documents feel sluggish.

## 💡 Key Findings

1.  **Linear vs. Exponential**: Pretext's layout time is nearly constant regardless of container width. DOM layout time spikes unpredictably as text wraps into more lines.
2.  **The 16.6ms Barrier**: At the 200-paragraph scale, DOM layout often exceeds 16.6ms, causing visible frame drops (stutter). Pretext consistently stays under 3ms, enabling smooth 60FPS interactions.
3.  **Predictive Power**: Because Pretext is pure JavaScript, we can calculate layout *before* anything is painted, enabling features like custom scrollbars, mini-maps, and complex text-wrap effects that are impossible with standard CSS.

## 🛠️ Tech Stack

- **Framework**: React 18 (Vite)
- **Engine**: `@chenglou/pretext`
- **Animations**: `motion/react`
- **Charts**: `recharts`
- **Icons**: `lucide-react`
- **Styling**: Tailwind CSS

---

*Note: This project was built to demonstrate the practical application of predictive typography in modern web development.*
