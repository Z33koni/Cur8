# Active inter-agent comms protocol

Roster: `root`, `acquisition`, `engineer`, `librarian`, `researcher`,
`visual-interpreter`.

There are 15 active append-only `.v2` channels, one for each unordered pair.

This protocol was validated in the 2026-09-01 collection test. Pairwise
channels, terse TSV-KV frames, explicit request/response states, stable
artifact references, and compact checkpoints are retained as successful
defaults.

## Frame format

```text
@KIND key=value<TAB>key=value...
```

Values are URI-encoded. One frame occupies one line. Common keys:

```text
id ts from to state ref
```

`state` is one of `OPEN`, `WIP`, `DONE`, `BLOCKED`, or `ACK`.
Put substantial context in the referenced artifact or the sender's
`.context/` checkpoint.

Normal handoff:

```text
@REQ  ... state=OPEN
@RESP ... state=DONE|WIP|BLOCKED
@ACK  ... state=ACK
```

Use the narrowest pair channel. ACK means receipt only; active work should
produce visible request/response traffic.

## Pair-specific fields

| Channel | Fields after the common keys |
|---|---|
| `root-acquisition.v2` | `cmd,scope,cell,ask,due` |
| `engineer-root.v2` | `task,files,test,result,risk` |
| `librarian-root.v2` | `item,decision,reason,cell,next` |
| `researcher-root.v2` | `q,cell,claim,conf,gap,next` |
| `root-visual-interpreter.v2` | `item,view,obs,flag,confidence` |
| `acquisition-engineer.v2` | `need,in,out,schema,rate` |
| `acquisition-librarian.v2` | `item,source,period,geo,family,rights,uncertainty` |
| `acquisition-researcher.v2` | `item,claim,query,evidence,conf,followup` |
| `acquisition-visual-interpreter.v2` | `item,image,view,task,quality,flag` |
| `engineer-librarian.v2` | `tool,contract,version,test,blocker` |
| `engineer-researcher.v2` | `tool,question,input,output,test` |
| `engineer-visual-interpreter.v2` | `item,asset,annotation,schema,flag` |
| `librarian-researcher.v2` | `item,term,definition,period,geo,decision` |
| `librarian-visual-interpreter.v2` | `item,visual_gate,obs,uncertainty,decision` |
| `researcher-visual-interpreter.v2` | `item,claim,visual_obs,conflict,next` |

## Operating rules

- Keep messages terse and factual.
- Do not route every observation through root.
- Preserve uncertainty; do not silently upgrade claims.
- Never write `library/` except as librarian.
- Qwen-routed work must record actual provider/model evidence; configuration
  alone is not proof of execution.
- Acquisition may multiplex unrelated domains, but must pace and cache per
  domain and honor site rules.
- Rotate or compact active channels only after unresolved requests are
  indexed in a checkpoint.
- Do not turn a tool request into implementation work automatically; record
  the specification and defer code unless the owner identifies an operational
  blocker or the user requests it.
