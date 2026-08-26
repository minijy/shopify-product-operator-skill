---
name: shopify-product-operator-skill
description: Orchestrate safe Shopify product searches, draft creation, updates, status changes, publication, and unpublication through shopify_ MCP tools. Use for Shopify product operations; do not use for orders, fulfillment, refunds, or inventory unless matching tools are available.
---

# Shopify Product Operator Skill

Use the available tools whose names begin with `shopify_`. The MCP server owns authentication, Shopify API details, and input validation; this skill owns workflow, confirmation, and result verification.

## Preconditions

- If connection state is unknown, call `shopify_connection_status` before other Shopify operations.
- Resolve product and publication IDs with read tools. Never invent or transform Shopify GIDs.
- Never request, print, or pass access tokens, client secrets, or client IDs through tool arguments or chat.
- If the required `shopify_` tools are unavailable, stop and tell the user to enable the Shopify Commerce MCP Server.

## Read operations

Run connection checks, searches, product reads, and publication listing without confirmation. Return compact results with product IDs so later mutations target unambiguous resources.

## Mutations

Before creating or changing data, summarize the exact target and fields. A clear user request authorizes an ordinary single-item draft creation or content update. Ask for confirmation immediately before:

- publishing or unpublishing any product;
- changing a product to `ACTIVE`, `ARCHIVED`, or `UNLISTED`;
- modifying more than one product;
- retrying a partially failed mutation when the final state is uncertain.

Create new products with `shopify_create_product_draft`; do not combine creation with publication. After every mutation, read the affected product again when a read tool can verify the requested state. Report Shopify user errors without hiding partial success.

## Status and publication

Treat product status and sales-channel publication as separate state. `ACTIVE` does not mean published. For any publish, unpublish, or scheduled-publish request, read [references/publication-workflows.md](references/publication-workflows.md) before acting.

## Batch boundaries

- Default to at most 20 products per batch unless the user chooses another limit.
- Preview the resolved products, intended changes, and sales channels before confirmation.
- Execute item by item so failures are attributable and resumable.
- Stop after three consecutive authorization, schema, or validation failures and report the common blocker.

Do not imply support for variants, prices, inventory, orders, refunds, or fulfillment merely because Shopify supports them. Use only capabilities represented by currently available tools.
