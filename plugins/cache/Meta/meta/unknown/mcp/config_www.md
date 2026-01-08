---
mcp_servers:
  devmate_default:
    enabled: false
  www:
    enabled: true

  # Import shared tools configuration using merge syntax
  <<: !include tools_shared.yaml
---
