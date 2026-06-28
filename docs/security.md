# Security Notes

## Token Handling

- Never commit real AI gateway consumer tokens.
- Never paste real tokens into public issues, screenshots, docs, or chat logs.
- Rotate a token immediately if it has been exposed.
- Use one token per consumer when possible.

## Service Boundary

The MCP service is read-only and only exposes published strategy assets.

It must not expose:

- raw production databases
- private model files
- factor libraries
- internal strategy parameters
- account holdings
- order routing details
- secret keys or connection strings

## User-Facing Risk Notice

All outputs are strategy asset information, not investment advice. Historical performance does not represent future returns.
