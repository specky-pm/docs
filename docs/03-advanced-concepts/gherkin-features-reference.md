---
sidebar_position: 4
---

# Gherkin Features Reference

The `features/*.feature` files in your Specky component specification define tests and acceptance criteria using the Gherkin language (version 6). This reference guide explains how to write effective Gherkin feature files for your component specifications.

## Purpose of Gherkin Feature Files

Gherkin feature files serve several important purposes in your component specifications:

1. **Define acceptance criteria**: Specify when a component implementation is considered complete
2. **Document behavior**: Describe how the component should behave in various scenarios
3. **Enable testing**: Provide a basis for automated testing of implementations
4. **Facilitate communication**: Create a common language between stakeholders
5. **Validate implementations**: Verify that implementations meet the requirements

## References and Best Practices

### Recommended Reading

- **"The BDD Books - Formulation Document Examples with Given/When/Then"** by Gáspár Nagy and Seb Rose (2021) - A comprehensive guide to writing effective Gherkin specifications
- **"User Story Mapping: Discover the Whole Story, Build the Right Product"** by Jeff Patton - Essential reading for understanding how to organize requirements effectively

### User Story Mapping

User Story Mapping is a powerful technique that pairs exceptionally well with Gherkin specifications. In this approach:

- Each **Feature file** represents a single **use case** or user story
- Each **Rule** within a feature represents a specific **business rule** for that use case
- **Examples** (scenarios) demonstrate how the business rules apply in concrete situations

This organization creates a natural mapping between:
1. The user's journey through your system (represented by features)
2. The business rules that govern that journey (represented by rules)
3. Concrete examples that illustrate those rules (represented by examples/scenarios)

By structuring your Gherkin files according to User Story Mapping principles, you create specifications that are more intuitive, easier to navigate, and better aligned with how users actually experience your system.

## Gherkin v6 Structure

A Gherkin feature file (version 6) has this structure:

```gherkin
Feature: Shopping Cart

  Rule: Items can be added to the cart
    
    Example: Add one item to empty cart
      Given the cart is empty
      When a customer adds an item to the cart
      Then the cart should contain 1 item
      And the cart total should be updated

    Example: Add multiple items to the cart
      Given the cart has 2 items
      When a customer adds another item
      Then the cart should contain 3 items
      And the cart total should be updated

  Rule: Items can be removed from the cart
    
    Example: Remove an item from the cart
      Given the cart has 3 items
      When a customer removes an item
      Then the cart should contain 2 items
      And the cart total should be updated
```

Let's explore each section in detail.

## Feature Declaration

Every Gherkin file starts with a `Feature:` declaration that describes a specific functionality:

```gherkin
Feature: Shopping Cart
  In order to purchase multiple items at once
  As a customer
  I want to add items to a cart before checkout
```

The feature declaration includes:
- A title that clearly identifies the feature
- An optional description that provides context (often in the form of a user story)

**Best practices**:
- Use a clear, concise title
- Focus on one cohesive feature per file
- Include a description that explains the business value
- Keep the description focused on the "why" rather than the "how"

## Rule Keyword (Gherkin v6)

The `Rule:` keyword was introduced in Gherkin v6 to represent one business rule that should be implemented. It provides additional structure and context for a feature by grouping related scenarios.

```gherkin
Feature: Manage Inventory Levels
  As a store manager
  I want inventory to be automatically managed
  So that we maintain optimal stock levels

  Rule: Items with stock level below threshold should be reordered
    
    Example: Item reaches reorder threshold
      Given an item with stock level 11
      And the reorder threshold is 10
      When a customer purchases 2 of the item
      Then the stock level should be 9
      And a reorder should be triggered

    Example: Item remains above reorder threshold
      Given an item with stock level 15
      And the reorder threshold is 10
      When a customer purchases 2 of the item
      Then the stock level should be 13
      And no reorder should be triggered
```

**Best practices for Rules**:
- Each rule should represent one specific business rule
- The rule description should be clear and testable
- Group related scenarios under the appropriate rule
- Use multiple rules to organize complex features

## Background

The `Background:` section defines steps that are common to all scenarios in a feature or rule:

```gherkin
Feature: Product Catalog

  Background:
    Given the catalog contains the following products:
      | Product    | Price | Category   |
      | Apple      | 0.99  | Fruit      |
      | Bread      | 2.49  | Bakery     |
      | Milk       | 1.99  | Dairy      |

  Scenario: Filter products by category
    When a customer filters by "Fruit"
    Then they should see 1 product
    And "Apple" should be in the results
```

Background steps run before each scenario in the feature or rule.

**Best practices**:
- Use for common setup steps
- Keep it simple and focused
- Don't overuse—if it's getting complex, consider splitting the feature

## Examples (Scenarios)

In Gherkin v6, the terms "Example" and "Scenario" are synonymous. "Example" is preferred as it better conveys that these are concrete examples of the rules in action.

Examples describe specific instances of how the feature should behave:

```gherkin
Example: Calculate total for multiple items
  Given the cart contains:
    | Product | Price | Quantity |
    | Apple   | 0.99  | 3        |
    | Bread   | 2.49  | 1        |
  When the total is calculated
  Then the subtotal should be 5.46
  And the tax should be 0.55
  And the final total should be 6.01
```

Each example includes:
- A descriptive title
- One or more steps using the Given/When/Then format

**Best practices**:
- Use clear, descriptive titles
- Focus on one specific behavior per example
- Keep examples independent of each other
- Use a consistent level of detail across examples

## Example Outlines (Scenario Outlines)

Example outlines allow you to run the same example with different data:

```gherkin
Example Outline: Calculate shipping cost based on weight
  Given a package weighing <weight> kg
  When shipping cost is calculated
  Then the cost should be <cost>

  Examples:
    | weight | cost  |
    | 0.5    | 5.00  |
    | 1.0    | 7.50  |
    | 2.5    | 12.75 |
    | 5.0    | 22.50 |
```

Example outlines include:
- A template example with placeholders in angle brackets
- An Examples table with concrete values for each placeholder

**Best practices**:
- Use for testing multiple variations of the same behavior
- Keep the examples table readable with clear column names
- Include both boundary values and typical values
- Limit to a reasonable number of examples (3-7 is often sufficient)

## Steps

Steps are the building blocks of examples and use the Given/When/Then format:

### Given Steps

`Given` steps set up the initial context:

```gherkin
Given the inventory has 20 units of product "A"
Given the customer has an empty shopping cart
Given today is "2025-04-22"
```

**Purpose**: Establish the preconditions for the example.

### When Steps

`When` steps describe the action being taken:

```gherkin
When the customer adds 5 units of product "A" to the cart
When the inventory is counted
When the monthly report is generated
```

**Purpose**: Describe the event or action that triggers the behavior being tested.

### Then Steps

`Then` steps describe the expected outcome:

```gherkin
Then the cart should contain 5 units of product "A"
Then the inventory count should be 15 units
Then the report should show total sales of 10,000
```

**Purpose**: Verify the expected results of the action.

### And/But Steps

`And` and `But` steps provide additional context, actions, or expectations:

```gherkin
Given the inventory has 20 units of product "A"
And the inventory has 15 units of product "B"
When the customer adds 5 units of product "A" to the cart
And the customer adds 3 units of product "B" to the cart
Then the cart should contain 5 units of product "A"
And the cart should contain 3 units of product "B"
But the cart should not contain any units of product "C"
```

**Purpose**: Chain multiple related steps of the same type.

## Step Parameters

Steps can include parameters to make them more reusable:

### String Parameters

Quoted strings for text values:

```gherkin
Given the product "Organic Apples" is in the catalog
When the customer searches for "Apple"
```

### Numeric Parameters

Numbers without quotes:

```gherkin
Given the product has a price of 10.99
When the customer orders 5 units
```

### Table Parameters

Tables for structured data:

```gherkin
Given the catalog contains the following products:
  | Product    | Price | Category   |
  | Apple      | 0.99  | Fruit      |
  | Bread      | 2.49  | Bakery     |
  | Milk       | 1.99  | Dairy      |
```

### Doc String Parameters

Doc strings for multi-line text:

```gherkin
Given the product description is:
  """
  Organic, locally-grown apples.
  Available in Red Delicious, Gala, and Granny Smith varieties.
  Perfect for baking or eating fresh.
  """
```

## Tags

Tags help categorize and filter examples:

```gherkin
@inventory @critical
Feature: Inventory Management

  @happy-path
  Example: Update inventory after sale
    # ...

  @error-handling
  Example: Handle insufficient inventory
    # ...
```

Common tag uses:
- Feature categories: `@inventory`, `@shipping`, `@reporting`
- Importance: `@critical`, `@high`, `@low`
- Status: `@wip` (work in progress), `@blocked`, `@deprecated`
- Behavior type: `@happy-path`, `@error-handling`, `@edge-case`

**Best practices**:
- Use consistent naming conventions
- Don't overuse—keep tags meaningful
- Apply tags at both feature and example levels as appropriate

## Complete Example with User Story Mapping

Here's a comprehensive example of a Gherkin feature file following Gherkin v6 conventions and User Story Mapping principles. Note how the feature represents a single use case, and each rule represents a specific business rule within that use case:

```gherkin
@inventory @product-management
Feature: Manage Store Inventory
  As a store manager
  I want to track product inventory accurately
  So that we maintain optimal stock levels and fulfill customer orders

  Background:
    Given the following products exist in the inventory:
      | Product ID | Name        | Category | Initial Stock |
      | P001       | Red Apple   | Fruit    | 100           |
      | P002       | Whole Bread | Bakery   | 50            |
      | P003       | Milk 1L     | Dairy    | 75            |

  Rule: Inventory decreases when products are sold

    @critical @happy-path
    Example: Selling products reduces inventory
      When 5 units of "Red Apple" are sold
      Then the inventory of "Red Apple" should be 95
      And the system should record the sale timestamp

    @error-handling
    Example: Attempting to sell more than available inventory
      Given the inventory of "Whole Bread" is 50
      When a sale of 60 units of "Whole Bread" is attempted
      Then the sale should be rejected
      And an "Insufficient Inventory" message should be displayed
      And the inventory of "Whole Bread" should remain 50

  Rule: Inventory increases when products are received

    Example: Receiving new products increases inventory
      When 25 units of "Milk 1L" are received
      Then the inventory of "Milk 1L" should be 100
      And the system should record the receipt timestamp

    Example Outline: Inventory updates are logged for auditing
      When <quantity> units of "<product>" are <action>
      Then the inventory log should record:
        | Product    | Quantity | Action   | Previous Level | New Level   |
        | <product>  | <quantity> | <action> | <previous>     | <new>       |

      Examples:
        | product    | quantity | action    | previous | new  |
        | Red Apple  | 10       | sold      | 100      | 90   |
        | Whole Bread| 15       | received  | 50       | 65   |
        | Milk 1L    | 5        | sold      | 75       | 70   |

  Rule: Products below threshold are flagged for reordering

    Example: Product reaching reorder threshold
      Given "Red Apple" has a reorder threshold of 20
      And the inventory of "Red Apple" is 25
      When 10 units of "Red Apple" are sold
      Then the inventory of "Red Apple" should be 15
      And "Red Apple" should be flagged for reordering

    Example: Product above reorder threshold
      Given "Milk 1L" has a reorder threshold of 20
      And the inventory of "Milk 1L" is 75
      When 10 units of "Milk 1L" are sold
      Then the inventory of "Milk 1L" should be 65
      And "Milk 1L" should not be flagged for reordering
```

This example demonstrates User Story Mapping principles by:
1. Focusing on a single use case (Manage Store Inventory)
2. Organizing business rules as Rules within the feature
3. Providing concrete examples for each business rule

## Best Practices for Gherkin Features

### Focus on Business Behavior, Not Implementation

```gherkin
# Good - focuses on business behavior
When the customer adds a product to the cart
Then the cart total should reflect the product price

# Not as good - focuses on implementation
When the addToCart() method is called
Then the cartTotal property should be updated
```

### Use Domain Language

```gherkin
# Good - uses domain language
Given the product is out of stock
When a customer attempts to order the product
Then the order should be rejected with "Out of Stock" reason

# Not as good - uses technical language
Given the product.stockLevel is 0
When orderService.placeOrder() is called
Then an OutOfStockException should be thrown
```

### Be Specific and Testable

```gherkin
# Good - specific and testable
Then the order total should be 25.50

# Not as good - vague and hard to test
Then the order total should be correct
```

### Keep Examples Independent

Each example should be able to run independently without relying on the state from other examples.

### Use Consistent Terminology

Use the same terms consistently across all your feature files.

### Balance Detail Level

Include enough detail to be clear, but not so much that the examples become brittle.

## Organizing Feature Files with User Story Mapping

When organizing feature files according to User Story Mapping principles, structure them by user activities and journeys:

```
features/
  customer_journey/
    browse_products.feature
    add_to_cart.feature
    checkout.feature
    track_order.feature
  store_management/
    manage_inventory.feature
    process_returns.feature
    generate_reports.feature
  admin_activities/
    manage_users.feature
    configure_system.feature
    audit_activities.feature
```

This organization:
1. Groups features by user roles and activities
2. Follows the natural flow of user journeys
3. Makes it easier to understand the system from a user's perspective
4. Helps identify gaps in your specifications

Each feature file should represent a complete user story or use case, with rules representing the business rules that apply to that use case.

## Validating Your Feature Files

Use the Specky validation tools to check your feature files:

```bash
spm validate --focus=features
```

This will check for:
- Valid Gherkin syntax
- Consistent terminology
- Completeness of examples
- Best practices adherence

## Using Features for Testing

While Specky component specifications are language-agnostic, the Gherkin feature files can be used with testing frameworks in various languages to verify that implementations meet the specified behavior.

## Next Steps

Now that you understand how to write effective Gherkin feature files using User Story Mapping principles, you might want to explore:

- [Advanced Testing Patterns](./advanced-testing-patterns.md) - Learn advanced techniques for testing components
- [Component Integration Testing](./component-integration-testing.md) - Understand how to test component interactions
- [Behavior-Driven Development](./behavior-driven-development.md) - Explore the BDD methodology with Specky

## Further Reading

- Nagy, G., & Rose, S. (2021). *The BDD Books - Formulation Document Examples with Given/When/Then*. Leanpub.
- Patton, J. (2014). *User Story Mapping: Discover the Whole Story, Build the Right Product*. O'Reilly Media.
- North, D. (2006). *Introducing BDD*. Better Software Magazine.