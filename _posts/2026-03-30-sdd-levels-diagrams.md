---
layout: post
title: "The Three Levels of Spec-Driven Development"
date: 2026-03-30
lang: en
tags: [sdd, lang-en, research-session]
featured: false
excerpt: "Spec-first, spec-anchored, spec-as-source — three ways AI agents and specifications can relate to each other. Three diagram options to visualize the difference."
problem: "The term 'spec-driven development' is used loosely across tools and articles, making it hard to compare approaches. Without a shared vocabulary for the levels of SDD, evaluating tools like Kiro or spec-kit becomes guesswork."
---

Birgitta Böckeler's [October 2025 article](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) on SDD tools identifies three distinct levels at which spec-driven development can operate. The difference between them is not about *having* a spec — it's about **what role the spec plays after the code exists**.

Below are three diagram options visualizing the same concept. I'm exploring which representation makes the distinction clearest.

---

## Option A — Vertical Stack

Three rows, one per level. Each shows the creation flow and what happens to the spec after code is generated.

<div style="font-family: var(--font-mono); font-size: 0.82rem; margin: 2rem 0;">

  <!-- Header -->
  <div style="display: grid; grid-template-columns: 140px 1fr 1fr; gap: 1px; background: var(--border); border: 1px solid var(--border); border-radius: 6px 6px 0 0; overflow: hidden;">
    <div style="background: var(--surface); padding: 0.6rem 0.8rem; color: var(--text-secondary); font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.08em;">Level</div>
    <div style="background: var(--surface); padding: 0.6rem 0.8rem; color: var(--text-secondary); font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.08em;">Creation</div>
    <div style="background: var(--surface); padding: 0.6rem 0.8rem; color: var(--text-secondary); font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.08em;">After code exists</div>
  </div>

  <!-- Row 1: Spec-first -->
  <div style="display: grid; grid-template-columns: 140px 1fr 1fr; gap: 1px; background: var(--border); border-left: 1px solid var(--border); border-right: 1px solid var(--border);">
    <div style="background: var(--bg); padding: 0.8rem; display: flex; align-items: center;">
      <span style="background: var(--accent); color: #fff; padding: 0.25rem 0.5rem; border-radius: 4px; font-size: 0.75rem; white-space: nowrap;">spec-first</span>
    </div>
    <div style="background: var(--bg); padding: 0.8rem; color: var(--text-primary);">
      spec → <span style="color: var(--accent);">agent</span> → code
    </div>
    <div style="background: var(--bg); padding: 0.8rem; color: var(--text-secondary);">
      spec is discarded or ignored
    </div>
  </div>

  <!-- Row 2: Spec-anchored -->
  <div style="display: grid; grid-template-columns: 140px 1fr 1fr; gap: 1px; background: var(--border); border-left: 1px solid var(--border); border-right: 1px solid var(--border);">
    <div style="background: var(--bg); padding: 0.8rem; display: flex; align-items: center;">
      <span style="background: #5a8f5a; color: #fff; padding: 0.25rem 0.5rem; border-radius: 4px; font-size: 0.75rem; white-space: nowrap;">spec-anchored</span>
    </div>
    <div style="background: var(--bg); padding: 0.8rem; color: var(--text-primary);">
      spec → <span style="color: var(--accent);">agent</span> → code
    </div>
    <div style="background: var(--bg); padding: 0.8rem; color: var(--text-primary);">
      spec <span style="color: #5a8f5a;">evolves</span> alongside code
    </div>
  </div>

  <!-- Row 3: Spec-as-source -->
  <div style="display: grid; grid-template-columns: 140px 1fr 1fr; gap: 1px; background: var(--border); border-left: 1px solid var(--border); border-right: 1px solid var(--border); border-bottom: 1px solid var(--border); border-radius: 0 0 6px 6px; overflow: hidden;">
    <div style="background: var(--bg); padding: 0.8rem; display: flex; align-items: center;">
      <span style="background: #8f5a5a; color: #fff; padding: 0.25rem 0.5rem; border-radius: 4px; font-size: 0.75rem; white-space: nowrap;">spec-as-source</span>
    </div>
    <div style="background: var(--bg); padding: 0.8rem; color: var(--text-primary);">
      spec → <span style="color: var(--accent);">agent</span> → code
    </div>
    <div style="background: var(--bg); padding: 0.8rem; color: var(--text-primary);">
      human edits <span style="color: #8f5a5a;">spec only</span> — never code
    </div>
  </div>

</div>

---

## Option B — Swimlane / Parallel Tracks

Two parallel tracks: **Spec** (top) and **Code** (bottom). The arrows and connections between them differ per level.

<div style="font-family: var(--font-mono); font-size: 0.8rem; margin: 2rem 0; display: flex; flex-direction: column; gap: 1.5rem;">

  <!-- Spec-first -->
  <div style="border: 1px solid var(--border); border-radius: 6px; overflow: hidden;">
    <div style="background: var(--surface); padding: 0.5rem 1rem; color: var(--accent); font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.08em; border-bottom: 1px solid var(--border);">spec-first</div>
    <div style="padding: 1rem; background: var(--bg);">

      <!-- Spec track -->
      <div style="display: flex; align-items: center; margin-bottom: 0.5rem;">
        <span style="width: 40px; color: var(--text-secondary); font-size: 0.7rem;">SPEC</span>
        <div style="background: var(--accent); color: #fff; padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem;">write spec</div>
        <div style="width: 32px; height: 2px; background: var(--accent);"></div>
        <div style="width: 0; height: 0; border-top: 5px solid transparent; border-bottom: 5px solid transparent; border-left: 8px solid var(--accent); margin-left: -1px;"></div>
        <span style="margin-left: 8px; color: var(--text-secondary); font-size: 0.75rem; font-style: italic;">— — — archived — — —</span>
      </div>

      <!-- Connector arrow down -->
      <div style="margin-left: 103px; width: 2px; height: 20px; background: var(--accent); position: relative;">
        <div style="position: absolute; bottom: -6px; left: -4px; width: 0; height: 0; border-left: 5px solid transparent; border-right: 5px solid transparent; border-top: 8px solid var(--accent);"></div>
      </div>

      <!-- Code track -->
      <div style="display: flex; align-items: center; margin-top: 0.3rem;">
        <span style="width: 40px; color: var(--text-secondary); font-size: 0.7rem;">CODE</span>
        <div style="background: var(--surface); border: 1px solid var(--border); color: var(--text-secondary); padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem;">(none)</div>
        <div style="width: 16px; height: 2px; background: var(--border);"></div>
        <div style="width: 0; height: 0; border-top: 5px solid transparent; border-bottom: 5px solid transparent; border-left: 8px solid var(--border); margin-left: -1px;"></div>
        <div style="background: var(--surface); border: 1px solid var(--accent); color: var(--text-primary); padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem; margin-left: 8px;">agent generates code</div>
        <div style="width: 16px; height: 2px; background: var(--border);"></div>
        <div style="width: 0; height: 0; border-top: 5px solid transparent; border-bottom: 5px solid transparent; border-left: 8px solid var(--border); margin-left: -1px;"></div>
        <div style="background: var(--surface); border: 1px solid var(--border); color: var(--text-primary); padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem; margin-left: 8px;">human edits code</div>
      </div>

    </div>
  </div>

  <!-- Spec-anchored -->
  <div style="border: 1px solid var(--border); border-radius: 6px; overflow: hidden;">
    <div style="background: var(--surface); padding: 0.5rem 1rem; color: #5a8f5a; font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.08em; border-bottom: 1px solid var(--border);">spec-anchored</div>
    <div style="padding: 1rem; background: var(--bg);">

      <div style="display: flex; align-items: center; margin-bottom: 0.5rem;">
        <span style="width: 40px; color: var(--text-secondary); font-size: 0.7rem;">SPEC</span>
        <div style="background: #5a8f5a; color: #fff; padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem;">write spec</div>
        <div style="width: 16px; height: 2px; background: #5a8f5a;"></div>
        <div style="width: 0; height: 0; border-top: 5px solid transparent; border-bottom: 5px solid transparent; border-left: 8px solid #5a8f5a; margin-left: -1px;"></div>
        <div style="background: #5a8f5a; color: #fff; padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem; margin-left: 8px;">spec evolves</div>
        <div style="width: 16px; height: 2px; background: #5a8f5a;"></div>
        <div style="width: 0; height: 0; border-top: 5px solid transparent; border-bottom: 5px solid transparent; border-left: 8px solid #5a8f5a; margin-left: -1px;"></div>
        <div style="background: #5a8f5a; color: #fff; padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem; margin-left: 8px;">spec evolves</div>
      </div>

      <div style="margin-left: 103px; width: 2px; height: 20px; background: #5a8f5a; position: relative;">
        <div style="position: absolute; bottom: -6px; left: -4px; width: 0; height: 0; border-left: 5px solid transparent; border-right: 5px solid transparent; border-top: 8px solid #5a8f5a;"></div>
      </div>

      <div style="display: flex; align-items: center; margin-top: 0.3rem;">
        <span style="width: 40px; color: var(--text-secondary); font-size: 0.7rem;">CODE</span>
        <div style="background: var(--surface); border: 1px solid var(--border); color: var(--text-secondary); padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem;">(none)</div>
        <div style="width: 16px; height: 2px; background: var(--border);"></div>
        <div style="width: 0; height: 0; border-top: 5px solid transparent; border-bottom: 5px solid transparent; border-left: 8px solid var(--border); margin-left: -1px;"></div>
        <div style="background: var(--surface); border: 1px solid #5a8f5a; color: var(--text-primary); padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem; margin-left: 8px;">agent generates code</div>
        <div style="width: 16px; height: 2px; background: var(--border);"></div>
        <div style="width: 0; height: 0; border-top: 5px solid transparent; border-bottom: 5px solid transparent; border-left: 8px solid var(--border); margin-left: -1px;"></div>
        <div style="background: var(--surface); border: 1px solid var(--border); color: var(--text-primary); padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem; margin-left: 8px;">human edits code</div>
      </div>

    </div>
  </div>

  <!-- Spec-as-source -->
  <div style="border: 1px solid var(--border); border-radius: 6px; overflow: hidden;">
    <div style="background: var(--surface); padding: 0.5rem 1rem; color: #8f5a5a; font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.08em; border-bottom: 1px solid var(--border);">spec-as-source</div>
    <div style="padding: 1rem; background: var(--bg);">

      <div style="display: flex; align-items: center; margin-bottom: 0.5rem;">
        <span style="width: 40px; color: var(--text-secondary); font-size: 0.7rem;">SPEC</span>
        <div style="background: #8f5a5a; color: #fff; padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem;">write spec</div>
        <div style="width: 16px; height: 2px; background: #8f5a5a;"></div>
        <div style="width: 0; height: 0; border-top: 5px solid transparent; border-bottom: 5px solid transparent; border-left: 8px solid #8f5a5a; margin-left: -1px;"></div>
        <div style="background: #8f5a5a; color: #fff; padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem; margin-left: 8px;">human edits spec only</div>
        <div style="width: 16px; height: 2px; background: #8f5a5a;"></div>
        <div style="width: 0; height: 0; border-top: 5px solid transparent; border-bottom: 5px solid transparent; border-left: 8px solid #8f5a5a; margin-left: -1px;"></div>
        <div style="background: #8f5a5a; color: #fff; padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem; margin-left: 8px;">human edits spec only</div>
      </div>

      <div style="margin-left: 103px; width: 2px; height: 20px; background: #8f5a5a; position: relative;">
        <div style="position: absolute; bottom: -6px; left: -4px; width: 0; height: 0; border-left: 5px solid transparent; border-right: 5px solid transparent; border-top: 8px solid #8f5a5a;"></div>
      </div>

      <div style="display: flex; align-items: center; margin-top: 0.3rem;">
        <span style="width: 40px; color: var(--text-secondary); font-size: 0.7rem;">CODE</span>
        <div style="background: var(--surface); border: 1px solid var(--border); color: var(--text-secondary); padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem;">(none)</div>
        <div style="width: 16px; height: 2px; background: var(--border);"></div>
        <div style="width: 0; height: 0; border-top: 5px solid transparent; border-bottom: 5px solid transparent; border-left: 8px solid var(--border); margin-left: -1px;"></div>
        <div style="background: var(--surface); border: 1px solid #8f5a5a; color: var(--text-primary); padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem; margin-left: 8px;">agent generates code</div>
        <div style="width: 16px; height: 2px; background: var(--border);"></div>
        <div style="width: 0; height: 0; border-top: 5px solid transparent; border-bottom: 5px solid transparent; border-left: 8px solid var(--border); margin-left: -1px;"></div>
        <div style="background: var(--surface); border: 1px solid var(--border); color: var(--text-secondary); padding: 0.3rem 0.7rem; border-radius: 4px; font-size: 0.75rem; margin-left: 8px; opacity: 0.4; text-decoration: line-through;">human edits code</div>
        <span style="margin-left: 8px; color: #8f5a5a; font-size: 0.72rem;">← forbidden</span>
      </div>

    </div>
  </div>

</div>

---

## Option C — Before / After Columns

Two columns: **Creation** (what you do to produce code) and **Evolution** (what you do when requirements change). The key difference between levels lives in the Evolution column.

<div style="font-family: var(--font-mono); font-size: 0.8rem; margin: 2rem 0;">

  <!-- Header row -->
  <div style="display: grid; grid-template-columns: 150px 1fr 1fr; gap: 1px; background: var(--border); border: 1px solid var(--border); border-radius: 6px 6px 0 0; overflow: hidden;">
    <div style="background: var(--surface); padding: 0.6rem 0.8rem;"></div>
    <div style="background: var(--surface); padding: 0.6rem 0.8rem; text-align: center; color: var(--text-secondary); font-size: 0.72rem; text-transform: uppercase; letter-spacing: 0.08em; border-left: 1px solid var(--border);">Creation</div>
    <div style="background: var(--surface); padding: 0.6rem 0.8rem; text-align: center; color: var(--text-secondary); font-size: 0.72rem; text-transform: uppercase; letter-spacing: 0.08em; border-left: 1px solid var(--border);">Evolution</div>
  </div>

  <!-- spec-first row -->
  <div style="display: grid; grid-template-columns: 150px 1fr 1fr; gap: 1px; background: var(--border); border-left: 1px solid var(--border); border-right: 1px solid var(--border);">
    <div style="background: var(--bg); padding: 1rem 0.8rem; display: flex; align-items: flex-start; padding-top: 1rem;">
      <span style="background: var(--accent); color: #fff; padding: 0.25rem 0.5rem; border-radius: 4px; font-size: 0.72rem;">spec-first</span>
    </div>
    <div style="background: var(--bg); padding: 1rem; border-left: 1px solid var(--border);">
      <div style="color: var(--text-secondary); font-size: 0.75rem; margin-bottom: 0.5rem;">write spec → agent → code</div>
      <div style="color: var(--text-primary); font-size: 0.78rem;">Spec guides initial generation. Human reviews output.</div>
    </div>
    <div style="background: var(--bg); padding: 1rem; border-left: 1px solid var(--border);">
      <div style="color: var(--text-secondary); font-size: 0.75rem; margin-bottom: 0.5rem;">spec is abandoned</div>
      <div style="color: var(--text-primary); font-size: 0.78rem;">Requirements change → edit code directly. Spec becomes stale.</div>
    </div>
  </div>

  <!-- spec-anchored row -->
  <div style="display: grid; grid-template-columns: 150px 1fr 1fr; gap: 1px; background: var(--border); border-left: 1px solid var(--border); border-right: 1px solid var(--border);">
    <div style="background: var(--bg); padding: 1rem 0.8rem; display: flex; align-items: flex-start; padding-top: 1rem;">
      <span style="background: #5a8f5a; color: #fff; padding: 0.25rem 0.5rem; border-radius: 4px; font-size: 0.72rem;">spec-anchored</span>
    </div>
    <div style="background: var(--bg); padding: 1rem; border-left: 1px solid var(--border);">
      <div style="color: var(--text-secondary); font-size: 0.75rem; margin-bottom: 0.5rem;">write spec → agent → code</div>
      <div style="color: var(--text-primary); font-size: 0.78rem;">Same as spec-first. Spec is the authoritative starting point.</div>
    </div>
    <div style="background: var(--bg); padding: 1rem; border-left: 1px solid var(--border);">
      <div style="color: #5a8f5a; font-size: 0.75rem; margin-bottom: 0.5rem;">spec stays current</div>
      <div style="color: var(--text-primary); font-size: 0.78rem;">Requirements change → <strong style="color: #5a8f5a;">update spec first</strong>, re-run agent. Spec and code stay in sync.</div>
    </div>
  </div>

  <!-- spec-as-source row -->
  <div style="display: grid; grid-template-columns: 150px 1fr 1fr; gap: 1px; background: var(--border); border-left: 1px solid var(--border); border-right: 1px solid var(--border); border-bottom: 1px solid var(--border); border-radius: 0 0 6px 6px; overflow: hidden;">
    <div style="background: var(--bg); padding: 1rem 0.8rem; display: flex; align-items: flex-start; padding-top: 1rem;">
      <span style="background: #8f5a5a; color: #fff; padding: 0.25rem 0.5rem; border-radius: 4px; font-size: 0.72rem;">spec-as-source</span>
    </div>
    <div style="background: var(--bg); padding: 1rem; border-left: 1px solid var(--border);">
      <div style="color: var(--text-secondary); font-size: 0.75rem; margin-bottom: 0.5rem;">write spec → agent → code</div>
      <div style="color: var(--text-primary); font-size: 0.78rem;">Same pipeline. Code is fully agent-generated from spec.</div>
    </div>
    <div style="background: var(--bg); padding: 1rem; border-left: 1px solid var(--border);">
      <div style="color: #8f5a5a; font-size: 0.75rem; margin-bottom: 0.5rem;">spec is the only source</div>
      <div style="color: var(--text-primary); font-size: 0.78rem;">Requirements change → <strong style="color: #8f5a5a;">only the spec is edited</strong>. Code is regenerated entirely. Human never touches generated code.</div>
    </div>
  </div>

</div>

---

*Source: Böckeler, B. (Oct 2025). [Exploring Generative AI — SDD 3 Tools](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html). Martin Fowler's blog.*
