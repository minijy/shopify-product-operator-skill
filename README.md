# Shopify Product Operator Skill

A reusable Codex skill for safely orchestrating Shopify product operations through MCP tools.

It provides workflow and policy—not Shopify API code. Pair it with a server that exposes the following tools:

- `shopify_connection_status`
- `shopify_search_products`
- `shopify_get_product`
- `shopify_create_product_draft`
- `shopify_update_product`
- `shopify_set_product_status`
- `shopify_list_publications`
- `shopify_publish_product`
- `shopify_unpublish_product`

The companion implementation is published separately as `shopify-commerce-mcp-server`.

## Install locally

Copy or clone this repository into your Codex skills directory, then start a new task so Codex can discover it:

```bash
git clone https://github.com/minijy/shopify-product-operator-skill.git ~/.codex/skills/shopify-product-operator-skill
```

Invoke explicitly with `$shopify-product-operator-skill`, or describe a Shopify product task and allow automatic skill selection.

## Example

```text
$shopify-product-operator-skill 找出所有草稿商品，生成发布计划；未经我确认不要修改店铺。
```
