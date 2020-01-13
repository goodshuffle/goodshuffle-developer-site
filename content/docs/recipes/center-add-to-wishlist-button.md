---
title: Center Add to Wishlist Button (no icon)
bookHidden: true
---

# Center Add to Wishlist Button (no icon)

Use this snippet to create a centered "Add to Wishlist" button. This is useful for layouts using cards without a visible border.

```

gspro-item-card.gspro-o-card button.gspro-o-button::after {
  content: "Add to Wishlist";
}

gspro-item-card.gspro-o-card button.gspro-o-button {
  display: initial;
  line-height: 1rem;
  padding: 0.5rem 1rem;
  font-size: 0.8rem;
  min-height: unset;
}

gspro-item-card.gspro-o-card button.gspro-o-button gspro-icon {
  display: none;
}

gspro-item-card.gspro-o-card .gspro-o-card__add {
  position: static;
}
```
