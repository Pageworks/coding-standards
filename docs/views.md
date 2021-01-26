# Views

Views are allowed to do the following:

- Call service functions.

Views are **not allowed** to do the following:

- Perform business logic.

## Example

```twig
{# Incorrect #}
{% if not cart.isEmpty %}
    {% set subtotal = 0 %}
    {% for lineItem in lineItems %}
        {% set discount = cart.getSubscriptionDiscount(lineItem) %}
        {% if discount %}
            {% set subtotal = subtotal + ((lineItem.price - (lineItem.price * discount)) * lineItem.qty) %}
        {% elseif lineItem.onSale %}
            {% set subtotal = subtotal + (lineItem.salePrice * lineItem.qty) %}
        {% else %}
            {% set subtotal = subtotal + (lineItem.price * lineItem.qty) %}
        {% endif %}
    {% endfor %}
    {% set subtotal = subtotal|round(2) %}
    {% set doConvert = false %}
    {% if cart.paymentCurrency != 'USD' %}
        {% set doConvert = true %}
    {% endif %}
    <span>{{ subtotal }}</span>
{% endif %}

{# Correct #}
{% if not cart.isEmpty %}
    {% set subtotal = cart.getSubtotal() %}
    <span>{{ subtotal }}</span>
{% endif %}
```
