# Dante

## Dead Message

### State

```mermaid
stateDiagram-v2
    [*] --> CREATED
    CREATED --> UPDATED : edit
    CREATED --> REPLAYED : replay
    CREATED --> SHELVED : shelve

    UPDATED --> UPDATED : edit
    UPDATED --> REPLAYED : replay
    UPDATED --> SHELVED : shelve

    SHELVED --> [*]
    REPLAYED --> [*]
```
