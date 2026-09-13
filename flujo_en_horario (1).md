# Flujo de Llamadas — En Horario

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'fontFamily': 'Arial', 'background': '#FFFFFF', 'primaryColor': '#FFFFFF', 'primaryBorderColor': '#000000', 'primaryTextColor': '#000000', 'lineColor': '#000000', 'secondaryColor': '#FFFFFF', 'tertiaryColor': '#FFFFFF'}}}%%
flowchart LR
    A1("📞 Llamada Cliente<br/>(680...)") --> A2("🤖 Agente IA<br/>Identifica Lead / ATC")

    A2 -->|Lead| L1("Identifica ciudad<br/>en la que quiere el trastero")
    L1 --> L2("Agente IA transfiere<br/>a equipo correspondiente")
    L1 -.-> CRM1("CRM: Se crea el Lead en TT")
    L2 --> L3("Entra con número IA (93...)<br/>No aparece número cliente")
    L2 --> L4("Equipo MAD<br/>"Equipo BCN")
    L2 --> L5("Notificación WhatsApp<br/>al Agente que recibe la llamada")
    CRM1 -.-> LA("Llamada Atendida:<br/>Agente, Nombre Cliente,<br/>Centro, Resumen")
    CRM1 -.-> LNA("Llamada No Atendida:<br/>Agente, Ciudad,<br/>Indicado en CRM")

    A2 -->|ATC| T1("Agente IA intenta<br/>resolver la solicitud/consulta")
    T1 -.->|Resuelta| CRM2("CRM: Inserta resumen<br/>de resolución")
    T1 -->|No Resuelta| T2("Agente IA transfiere<br/>a equipo correspondiente")
    T2 --> T3("Equipo BCN")
    T2 --> T4("Equipo MAD")
    T2 -.-> CRM3("CRM: Inserta resumen<br/>de resolución")
    T2 -.->|Si es Deuda/Pago| WA1("Notificación WhatsApp<br/>al equipo correspondiente")

    N0("ℹ️ Lead único por Agente:<br/>cada Lead lo gestiona<br/>siempre el mismo agente")

    L3 -.-> L3C("Comments")
    T3 -.-> T3C("Comments")

    classDef todos fill:#FFFFFF,stroke:#000000,color:#000000
    classDef nota fill:#FFFFFF,stroke:#000000,color:#000000,stroke-dasharray: 3 3
    classDef bcn fill:#FFFFFF,stroke:#FF0000,color:#000000,stroke-dasharray: 3 3
    classDef comment fill:#FFFFFF,stroke:#808080,color:#808080,stroke-dasharray: 3 3
    class A1,A2,L1,L2,L4,L5,LA,LNA,CRM1,CRM2,CRM3,T1,T2,T4,WA1 todos
    class N0 nota
    class L3,T3 bcn
    class L3C,T3C comment
    linkStyle 16 stroke:#808080,stroke-width:1px
    linkStyle 17 stroke:#808080,stroke-width:1px
```

---

### Notas
- **Lead único por agente**: todas las comunicaciones de un Lead siempre las gestiona el mismo agente asignado.
- Diagrama generado a partir de `Flujo_Agentes_IA_PONGO.xlsx`.
