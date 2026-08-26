# Publication workflows

Read this reference only for publish, unpublish, scheduled-publish, or product-status requests.

## Publish

1. Read the product and capture its current status.
2. Call `shopify_list_publications`; do not infer a publication ID from a channel name.
3. Present the product, current status, target publications, and any requested publish time.
4. Obtain explicit confirmation immediately before changing state.
5. If needed, call `shopify_set_product_status` with `ACTIVE`.
6. Call `shopify_publish_product` with the confirmed publication IDs.
7. Read the product again and report the mutation result. Do not claim channel visibility unless the tool result supports it.

Scheduled publishing is valid only when the selected publication supports it. If support is unknown or false, do not silently publish immediately.

## Unpublish

1. Read the product and list publications.
2. Present exactly which publications will lose the product.
3. Explain that unpublishing does not delete or archive the product.
4. Obtain explicit confirmation immediately before the mutation.
5. Call `shopify_unpublish_product` with only the confirmed publication IDs.
6. Verify and report the result.

## Status-only changes

Changing a status does not alter publication assignments. Explain this distinction before setting `ACTIVE`, `ARCHIVED`, or `UNLISTED`. A request to “下架” normally means unpublish from specified channels; do not reinterpret it as archive unless the user says so.
