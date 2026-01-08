---
mcp_servers:
  devmate_default:
    enabled: true
  www:
    enabled: false

  # Import shared tools configuration using merge syntax
  <<: !include tools_shared.yaml
---
