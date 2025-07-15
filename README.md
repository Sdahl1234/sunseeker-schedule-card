# Sunseeker Lovelace Cards

Custom Lovelace cards for Sunseeker integrations.

## Installation (via HACS)

1. Add this repository to HACS as a custom frontend (plugin) repository.
2. Install the cards via HACS → Frontend.
3. Add the resources to your dashboard:
   - `/hacsfiles/Sunseeker-lawn-mower-cards/sunseeker-schedule-card.js`
   - `/hacsfiles/Sunseeker-lawn-mower-cards/sunseeker-mower-control-card.js`
4. Use in your dashboard:

```yaml
type: 'custom:sunseeker-schedule-card'
# or
type: 'custom:sunseeker-mower-control-card'
```
