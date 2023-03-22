# EC2 Placement Groups

É a configuração feita para organizar como as instâncias EC2 serão organizadas
no hack do data-center da AWS.

Elas podem estar:

- Afastadas: Garante Redundância.
- Juntas: Garante Performance.

## Estratégias

- Cluster: Muito próximas, garante performance.
- Partition: Grupos dentro da Zona. Procura balancear performance e redundância.
- Spread: Todas as instâncias estão separadas. Maior redundância.
