# Flujo de Llamadas — Agentes IA PONGO

```mermaid
flowchart TD
    subgraph EH["🕐 EN HORARIO"]
        direction TB
        A1["📞 Llamada Cliente<br/>(680...)"] --> A2["🤖 Agente IA<br/>Identifica Lead / ATC"]

        A2 -->|Lead| L1["Identifica ciudad<br/>en la que quiere el trastero"]
        L1 --> L2["Agente IA transfiere<br/>a equipo correspondiente"]
        L1 --> CRM1["CRM: Se crea el Lead en TT"]
        L2 --> L3["Equipo BCN<br/><small>Entra con número IA (93...)<br/>No aparece número cliente</small>"]
        L2 --> L4["Equipo MAD"]
        L2 --> L5["Notificación WhatsApp<br/>al Agente que recibe la llamada"]
        CRM1 --> LA["Llamada Atendida:<br/>Agente, Nombre Cliente,<br/>Centro, Resumen"]
        CRM1 --> LNA["Llamada No Atendida:<br/>Agente, Ciudad,<br/>Indicado en CRM"]

        A2 -->|ATC| T1["Agente IA intenta<br/>resolver la solicitud/consulta"]
        T1 -->|Resuelta| CRM2["CRM: Inserta resumen<br/>de resolución"]
        T1 -->|No Resuelta| T2["Agente IA transfiere<br/>a equipo correspondiente"]
        T2 --> T3["Equipo BCN"]
        T2 --> T4["Equipo MAD"]
        T2 --> CRM3["CRM: Inserta resumen<br/>de resolución"]
        T2 -.->|Si es Deuda/Pago| WA1["Notificación WhatsApp<br/>al equipo correspondiente"]

        N0["ℹ️ Lead único por Agente:<br/>cada Lead lo gestiona<br/>siempre el mismo agente"]
    end

    subgraph FH["🌙 FUERA DE HORARIO"]
        direction TB
        B1["📞 Llamada Cliente<br/>(680...)"] --> B2["🤖 Agente IA<br/>Identifica Lead / ATC"]

        B2 -->|Lead| M1["Agente IA recoge necesidades<br/>enfocando el cierre de la visita"]
        M1 --> M2["Identifica ciudad<br/>en la que quiere el trastero"]
        M2 --> M3["Envía solicitud de visita<br/>a Agente PONGO asignado<br/>(pdte. confirmación)"]
        M2 --> CRM4["CRM: Se crea el Lead en TT"]
        CRM4 --> M4["Resumen: asigna a Agente PONGO<br/>según ciudad —<br/>Nombre, Centro, Tamaño"]
        M4 --> M5["Cambio de estado del Lead<br/>si se solicitó visita"]
        M4 --> M6["Envía petición de visita<br/>a Agente PONGO"]

        B2 -->|ATC| P1["Agente IA intenta<br/>resolver la solicitud/consulta"]
        P1 -->|Resuelta| CRM5["CRM: Inserta resumen<br/>de resolución"]
        P1 -->|No Resuelta| WA2["Aviso WhatsApp"]
        WA2 --> P2["Equipo BCN"]
        WA2 --> P3["Equipo MAD"]
        WA2 --> CRM6["CRM: Inserta resumen<br/>de resolución"]
        P1 -->|Incidencia| WA3["Aviso WhatsApp<br/>Equipo PONGO"]

        N1["ℹ️ Lead único por Agente:<br/>cada Lead lo gestiona<br/>siempre el mismo agente"]
    end
```

---

### Notas
- **Lead único por agente**: todas las comunicaciones de un Lead siempre las gestiona el mismo agente asignado.
- Diagrama generado a partir de `Flujo_Agentes_IA_PONGO.xlsx`. Si el flujo cambia, edita el bloque `mermaid` de arriba y vuelve a subir el archivo — GitHub lo re-renderiza automáticamente.
