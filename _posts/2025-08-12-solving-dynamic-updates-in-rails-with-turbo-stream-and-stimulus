---
layout: post
title:  "Solving Dynamic Updates in Rails with Turbo Stream and Stimulus"
date:   2025-08-12 18:59:44 +0545
categories: turbo stream
tags: rails turbo stimilus
share: true
---

## Solving Dynamic Updates in Rails with Turbo Stream and Stimulus

Recently, I ran into a situation in a Rails project where I needed to update part of a page dynamically when a user selected a new shipping address. The requirement was simple on paper:

> When the user changes the address, instantly update the shipping cost in the order summary — without reloading the page.

That’s exactly the kind of thing Turbo Stream is great for… but it didn’t work at first.

---

### The Problem (Before)

My initial setup relied on a simple form submission and Turbo Streams’ automatic magic. I had a `select` dropdown for addresses and expected Turbo to pick up the POST request and render the new shipping cost.

But here’s what happened:

* The page wasn’t updating automatically.
* Turbo Stream requests weren’t being triggered the way I expected.
* I needed to send **multiple pieces of data** (address ID and multiple order IDs) together, which was tricky with just a standard form.

It became clear I needed more control over the request — both the data being sent and how the Turbo Stream response was rendered.

---

### The Fix (After)

I rewrote the interaction using a **Stimulus controller** to:

1. Capture the dropdown change event.
2. Gather all the required data.
3. Send a `POST` request via `fetch` with the correct headers.
4. Render the Turbo Stream response manually.

Here’s the final code:

```javascript
import { Controller } from "@hotwired/stimulus"

export default class extends Controller {
  select(event) {
    const addressId = event.target.value
    const orderIds = event.target.dataset.shippingAddressOrderIds.split(',')

    const token = document.querySelector('meta[name="csrf-token"]').content

    fetch("/orders/shipping_cost", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "X-CSRF-Token": token,
        "Accept": "text/vnd.turbo-stream.html"
      },
      body: JSON.stringify({
        address_id: addressId,
        order_ids: orderIds
      })
    })
    .then(response => response.text())
    .then(turboStreamHTML => {
      Turbo.renderStreamMessage(turboStreamHTML)
    })
  }
}
```

---

### How It Works

1. **Listening for Changes**
   The `select` method runs whenever the address dropdown changes.

2. **Gathering Data**

   * `addressId`: From the selected value.
   * `orderIds`: Pulled from a `data-shipping-address-order-ids` attribute.

3. **Making the Turbo Stream Request**
   We send JSON to the server with the right CSRF token and an `Accept` header requesting a Turbo Stream response.

4. **Applying the Update**
   We manually call `Turbo.renderStreamMessage()` to immediately apply the Turbo Stream changes without a page reload.

---

### Why This Works Better

This approach gives:

* **Control** over the request and response cycle.
* **Flexibility** to send exactly the data the server needs.
* **Instant UI updates** without relying on form submissions or page reloads.

Turbo and Stimulus together are powerful, but sometimes you need to step in and handle the request manually — and that’s exactly what solved this problem.
