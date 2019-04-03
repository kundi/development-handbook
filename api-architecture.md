This guide contains the guidelines for coding APIs written in Ruby on Rails.

# Sorting and filtering collections

To implement sorting/ordering, use the following pattern. This is an example for sorting `Purchase` models:

```
module SortPurchases
  extend self

  def sort(scope, key = nil, direction = nil)
    key = key.presence || "description"
    direction = parse_direction(direction)

    case key
    when "items"
      sort_by_item_count(scope, direction)
    when "date"
      sort_by_column(scope, key, direction)
    # when ...
    else
      raise ArgumentError, "very bad"
    end
  end

  private

  def parse_direction(value)
    value.in?(%w(asc desc)) ? value : "asc"
  end

  def sort_by_item_count(scope, direction)
    scope
      .joins(:purchase_items)
      .group('purchases.id')
      .select('purchases.*, count(purchase_items.id) as items_count')
      .order("items_count #{direction}")
      .order('purchases.id') # ensure consistent order
  end
  
  def sort_by_column(scope, column, direction)
    scope
      .order(column => direction)
      .order('purchases.id')
  end

  # ...
end
```

# Command pattern

In progress.

# Controllers

Keep the controller actions lean. Gather request params and send them to a service object to perform necessary operations. 

# Authorization

In progress.

# Models

In progress.

# Routes

# Services 

In progress.
